# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

maevainnocent

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/63#issuecomment-6352856396

> Hi! Following up on my repro above, here’s my plan.
>
> After looking into it, I don’t think the scorer itself is the problem. It marks a README as “comprehensive” once it reaches 500 words, and the `test_word_count_category_*` tests already check those limits. The issue is that the fixture in `test_readme_with_all_quality_signals` is only 51 words, so it doesn’t meet either assertion: `word_count > 100` or `word_count_category == "comprehensive"`. Since this test is meant to cover a README with all the quality signals, I think it makes more sense to fix the fixture instead of changing the assertions.
>
> I’m planning to only edit `tests/unit/test_readme_scorer.py`. I’ll add some filler text to the fixture to get it past 500 words, keep all the quality signals already there, and remove the `xfail(strict=True)` marker for this issue. I won’t change `readme_scorer.py` or any other tests.
>
> To make sure everything works, I’ll rerun the same commands from my repro on my branch. The normal run should go from `22 passed, 1 xfailed` to `23 passed`, and the `--runxfail` run should pass instead of failing at `assert 51 > 100`. I’ll also run the rest of `tests/unit` to check that nothing else breaks.
>
> My branch will be `fix/63-readme-scorer-fixture-length`. If anyone thinks changing the assertions would be a better approach, please let me know before I get started!

---

## Your branch

**Branch**

`fix/63-readme-scorer-fixture-length`

**Evidence**

Environment: macOS 14.4 (arm64), Python 3.14.8 in the repo's `.venv`, repo at commit `99673c7` (before) and `7134d9e` on `fix/63-readme-scorer-fixture-length` (after).

**Before** (on `main`, commit `99673c7`):

```
$ python -m pytest tests/unit/test_readme_scorer.py -q
x......................                                                  [100%]
22 passed, 1 xfailed in 0.06s

$ python -m pytest tests/unit/test_readme_scorer.py -q --runxfail
>       assert data["word_count"] > 100
E       assert 51 > 100

tests/unit/test_readme_scorer.py:60: AssertionError
----------------------------- Captured stdout call -----------------------------
2026-10-23 10:26:53 [info     ] readme_scored                  category=minimal score=0.8717142857142858 word_count=51
=========================== short test summary info ============================
FAILED tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals
1 failed, 22 passed in 0.04s
```

**After** (on `fix/63-readme-scorer-fixture-length`, commit `7134d9e`):

```
$ python -m pytest tests/unit/test_readme_scorer.py -q
.......................                                                  [100%]
23 passed in 0.04s

$ python -m pytest tests/unit/test_readme_scorer.py -q --runxfail
.......................                                                  [100%]
23 passed in 0.02s

$ python -m pytest "tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals" -q -s
2026-10-23 10:27:09 [info     ] readme_scored                  category=comprehensive score=1.0 word_count=533
.
1 passed in 0.01s
```

Rest of the unit tests, same environment:

```
$ python -m pytest tests/unit -q        # on main, before
6 failed, 369 passed, 53 xfailed, 20 warnings in 6.78s

$ python -m pytest tests/unit -q        # on the branch, after
6 failed, 370 passed, 52 xfailed, 20 warnings in 10.95s
```

The 6 failures are all in `tests/unit/test_review_service.py` and fail the same way on `main` without my change, so they aren't caused by it. The only difference is my test moving from xfailed to passed.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run (20 packages), saved as `eval-run.txt`: `agreement: 19/20 scored items  (bar: 18/20: PASS)`

**Package analysis**

`pkg-14` (zellij-org/zellij#5174, color query responses leaking into the pane on SSH reattach, category `clear-accept`)

- My rubric's decision: `reject`. From `eval-run.txt`: `pkg-14  clear-accept       accept  reject   NO     failed: cause-grounded, executable, unknowns-stated`
- Gold label: `accept`. Gold note: "honestly scoped-down: reattach handshake fix with a regression-window repro; defers the untestable Windows variant and says so; arguable on the deferral, ready as scoped"

The plan says zellij's reattach path wires stdin to the session before the OSC color query responses are consumed, and the fix is to drain those responses in the reattach handshake. My rubric failed it on two required checks:

- `executable`: the plan names areas, not a code site: "the client attach/reattach path in `zellij-server` (session connection handling) and `zellij-client`'s terminal query issuance; exact functions to be pinned in the PR after tracing the query issuance with debug logs". My check fails a plan when "the real decisions are deferred to build time", and the grader read "exact functions to be pinned in the PR" as exactly that.
- `cause-grounded`: the repro's cache control says "After `rm -rf ~/.cache/zellij` ... the next attach is clean, the one after leaks again." The grader decided the stdin-ordering cause doesn't explain why the leak depends on the cache, so it counted that control as ruling the cause out.

The gold label reads it differently: the approach is chosen (drain OSC responses in the reattach handshake), the location is narrowed to one path in two named crates, and the plan's own explanation of the cache control ("with an empty cache the color data is refetched along the fresh-attach path once") is consistent with the evidence rather than ruled out by it. My rubric was stricter than the gold on both: it wants a function or specific code site, not a named path, and it treated a control the plan explains as one that contradicts it.

**Check rationale**

From `tools/plan-check/rubric.md`:

> | executable | The plan's change statement: the files, functions, or code sites named, and the approach chosen. | Pass if a stranger could start work without asking the author anything: the plan names where the change goes (file, function, or a specific code site) and commits to one approach. Fail if the location is "somewhere", the approach is left open ("whichever is easier", "gocui? tcell? not sure", "profile and optimize"), or the real decisions are deferred to build time. | required |

It reads this way because the question it answers is whether a stranger could pick the plan up and start. That needs two things: a place to start (a file, function, or specific code site) and one chosen approach. The fail conditions quote the shapes I wanted it to catch, like "whichever is easier" or "gocui? tcell? not sure", where the plan is really a menu, and "profile and optimize", where the plan is really "I'll figure it out later". Naming a file alone isn't enough, because a plan can name a file and still leave every real decision open. "The real decisions are deferred to build time" is the line that catches that.

**Trade-offs**

`executable` gives up pkg-14. That plan picks one approach and narrows the location to the reattach path in two named crates, but says the exact functions will be "pinned in the PR after tracing". A maintainer would probably be fine with that, since the investigation step is concrete and the debug logs are already working. My check can't tell "I know the path and will trace to the exact function" apart from "I don't know where the change goes", so it rejects both. I accepted that miss instead of loosening the check, because the run was already at 19/20 with every category matched, and a looser "named area is enough" rule risks letting through the unbuildable plans this check exists for (unbuildable 3/3 in my run).

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
