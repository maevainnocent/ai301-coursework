# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-howard/pull/95

**Branch**

`fix/63-readme-scorer-fixture-length`

---

## Eval iterations

**Run history**

1. Attempted full run with `python3` (3.8.10 on my PATH). It crashed before grading any package: `TypeError: 'type' object is not subscriptable` at `run_eval.py` line 82, because the harness needs a newer Python. No packages were graded.
2. First full run (20 packages) with Python 3.14: `agreement: 20/20 scored items  (bar: 18/20: PASS)`, `categories: clear-accept 7/7  not-tested 4/4  silent-drift 4/4  standards-wall 2/2  unreviewable 3/3`. The grading finished, but `--save-run` pointed at a directory that didn't exist, so the harness crashed with `FileNotFoundError` while writing the file and saved nothing.
3. Second full run, same tool files with no changes, saved as `eval-run.txt`: `agreement: 20/20 scored items  (bar: 18/20: PASS)`, same category tallies. This is the committed run.

I didn't revise any component between runs 2 and 3, so I didn't need any `--only` re-runs.

**Package analysis**

`pkg-13` (neovim/neovim#41337, `vim.ui.open` on Windows truncating a URL at `&`, category `clear-accept`)

- My rubric's decision: `accept`. From `eval-run.txt`: `pkg-13  clear-accept    accept  accept   yes`
- Gold label: `accept`. Gold note: "honestly disclosed shortfall: caret-escapes cmd metacharacters with before/after evidence; %VAR% expansion explicitly deferred in the plan's note AND restated in the description; arguable on the deferral, ready as scoped"

This package is a trap for a rubric that equates "less than everything" with "hold". The PR deliberately doesn't fix part of the problem: a URL like `?q=%PATH%` still expands. My tool accepted it because of how `plan-fidelity` treats missing work. A planned piece may be missing if "its absence is stated in a plan deviation/deferral note or in the description". The plan says ahead of time: "Known limit, stated in the plan: `%` ... is NOT covered by this change; if it proves messy it will be deferred with a note". The description restates it: "Deviation note, recorded in the plan before this PR: percent-sign environment expansion (`%VAR%`) is NOT handled here". The grader's evidence line was: "Both hunks (ui.lua caret-escape of & | ^ < >, and ui_spec.lua test) map to the plan's Files list; the %VAR% limit is a stated plan deferral restated in the description." The other required checks passed on their own evidence. `decisive-evidence` saw the issue's own input re-run ("before code=1 truncated URL, after code=0 full URL"). `template-asks` found the Problem and Solution sections the repo asks for. So the tool and the gold label agree for the same reason: the shortfall is disclosed in both places a reviewer would look, and everything the PR claims to do is shown working.

**Check rationale**

From `tools/pr-precheck/rubric.md`:

> | plan-fidelity | Every file and every hunk in the diff, read against the plan's scope (its change statement, Files list, In/Out lines, "not in scope" lines) and its deviation or deferral notes; then every claim the description makes about what the PR does ("implements the plan exactly", "no other changes", "docs updated", "CHANGELOG added"), read against the diff. | Pass if every hunk does work the plan names, or work a plan deviation note records, or one of these always-in-scope items: a test for the planned behavior, or an entry/file the repo-facts block requires (CHANGELOG, whatsnew, release note); AND every piece of work the plan commits to appears in the diff, or its absence is stated in a plan deviation/deferral note or in the description; AND every description claim about the change is true of the diff. Fail if any hunk does work the plan does not name (a rewrite of nearby code, a renaming pass, a new option/flag/setting, an edit to a file the plan never mentions, a dependency bump) with no deviation note; or a planned piece is missing with no note anywhere; or the description claims something the diff does not contain, or claims fidelity ("exactly as planned", "no changes beyond the plan") the diff contradicts. A disclosed shortfall passes. | required |

The check reads drift in both directions because silent drift goes both ways: doing more than the plan (pkg-03's new `resolve_symlinks` option, pkg-06's renaming pass) and doing less while claiming more (pkg-17's docs update that the description says exists but the diff doesn't contain). It has three parts joined by AND, so a PR can't pass by satisfying one direction only. A test for the planned behavior and a required CHANGELOG/whatsnew entry are always in scope. Without that, a strict reader would call pkg-02's CHANGELOG line "unplanned" and reject a clear accept. The last sentence, "A disclosed shortfall passes", is there for the honest-outcome rule: missing work only fails when it's disclosed nowhere. That's what separates pkg-13 and pkg-16 (accept) from pkg-17 (reject). Description claims are checked against the diff, not trusted, because calib-03 showed a description saying "no changes beyond the plan" over a hunk the plan never mentions.

**Trade-offs**

`plan-fidelity` is strict about how a description characterizes the diff, and on pkg-01 that strictness fired for a reason the gold label doesn't give. The gold rejects pkg-01 only for the standards wall: the required checklist, `closes #xxxx`, and the whatsnew entry are missing. My tool rejected it on `template-asks` for that, and also on `plan-fidelity`: "Description says it adds a capacity check 'to the bulk-copy path', but the diff adds it once at tokenize_bytes entry ... the planned per-copy check in the bulk-copy paths is missing with no deviation note." The verdict agreed, but a strict reading of where the check lives could make the tool reject a PR that should be accepted when the description summarizes the fix loosely. I kept the check as it is because loosening "every description claim about the change is true of the diff" would weaken the part that catches pkg-17 and calib-03. Those are the silent-drift cases where the description is the only thing hiding the problem. I'd rather risk an occasional extra reject for a sloppy summary than let a PR through whose description misstates the diff.

---

## My pr-precheck verdict on my draft

Live mode, run on the draft title and description, `git diff main...HEAD`, and my `plan.md`, before opening the PR.

**Verdict: `accept`.** All required checks passed:

| Check | Grade | Evidence |
|---|---|---|
| plan-fidelity | pass | Diff touches only `tests/unit/test_readme_scorer.py`: removes the issue #63 xfail marker and adds the `## About` padding, both named in the plan's In line. |
| decisive-evidence | pass | Before `22 passed, 1 xfailed` / `assert 51 > 100`, after `23 passed` (also with `--runxfail`), log shows `category=comprehensive ... word_count=533`; ruff, black, mypy, and pytest outcomes stated. |
| clean-diff | pass | The only non-fix line is an explanatory comment on the padding. |
| template-asks | pass | All template sections filled, `Closes #63` present, xfail marker removed per CONTRIBUTING; CI-green item pending until the PR exists. |
| ai-disclosure | pass | Repo states no AI policy; the description discloses AI use anyway. |
| thread-engaged (preferred) | pass | No maintainer direction on #63. |

The run also flagged three things to handle before or right after opening:
1. The description reported a repo-wide mypy run that my plan's Deviations section didn't mention. I added Deviations lines to `plan.md` for the repo-wide ruff/black/mypy runs and for the commit-scope change.
2. My commit scope `readme-scorer` isn't one of CONTRIBUTING's listed scopes. I changed it to `test(agent)`, which matches CONTRIBUTING's own example for readme_scorer tests. The amend only changed the message: the tree is identical, and the commit went from `7134d9e` to `25694e3`.
3. CI could only go green after opening. After I opened the PR, all five jobs passed ([run 41675557470](https://github.com/codepath/pathreview-ai301-fa26-howard/actions/runs/41675557470)): `lint`, `typecheck`, `test-unit` (`376 passed, 52 xfailed`, including `test_readme_with_all_quality_signals PASSED`), `test-integration`, and `frontend`. I then ticked the CI box in the PR description and added a note that the 6 `test_review_service.py` failures I saw locally only happen on my Python 3.14 setup.

The voice guide flagged the first, AI-drafted description against my "own words" rule. I rewrote the description in my own words and re-ran pr-precheck in live mode on the final text and the reworded commit `25694e3`. Verdict: `accept`, with every required check passing and no voice-guide rule broken. The only reservation was that my fork still had the old commit, so I force-pushed `25694e3` before opening the PR.

---

Related paths: `eval-run.txt` in this directory; your skill's files in `tools/pr-precheck/`.
