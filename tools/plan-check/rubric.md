[rubric.md](https://github.com/user-attachments/files/33878317/rubric.md)
# Rubric: is this plan ready to post and build from?

Every check reads the plan package against the issue and the repro
evidence it builds on. Grade the plan, not the polish: a terse plan
that names its cause, its file, and an observable test is ready; a
long, confident one that contradicts the repro or bundles a redesign
is not. "The repro evidence" means the repro-evidence block in an eval
bundle, or the student's posted repro comment in live mode.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| cause-grounded | The plan's stated cause (and any cause the plan comment adopts from the thread), read against every step, control run, and artifact in the repro evidence. | Pass if the stated cause is consistent with everything the repro evidence shows, including its control runs and the step where the bad behavior first appears. Fail if any part of the repro evidence rules the cause out: a control where the blamed component is present or exercised and the behavior is fine, or a step showing the failure already happened before or without the blamed component. A cause taken from the thread or a maintainer still fails if the package's own evidence contradicts it. Fail if no cause or mechanism is stated at all. | required |
| bounded-scope | The plan's change statement, its in-scope/out-of-scope lines, and the list of files or areas it will touch, read against what the issue asks for. | Pass if the plan is one change aimed at the issue's reported behavior; deferring related work explicitly ("out: ...", "separate effort") and scoping down to a subset with a stated reason both pass. Fail if the plan bundles work the issue did not ask for alongside the fix: refactors or rewrites of surrounding code, migrations or dependency upgrades, new options/settings/UI, new frameworks or abstractions, CI or test-harness overhauls. Bundling fails even when the core fix inside it is right. | required |
| executable | The plan's change statement: the files, functions, or code sites named, and the approach chosen. | Pass if a stranger could start work without asking the author anything: the plan names where the change goes (file, function, or a specific code site) and commits to one approach. Fail if the location is "somewhere", the approach is left open ("whichever is easier", "gocui? tcell? not sure", "profile and optimize"), or the real decisions are deferred to build time. | required |
| decisive-test | The plan's test plan, read against the repro evidence's steps and observed artifacts. | Pass if the test plan names an observable outcome that would differ between the broken and fixed code: re-running the repro steps with a stated expected result, or a regression test with a named case and expected value. Extra checks may be added on top. Fail if the only test is subjective ("should feel fast", "nothing else should feel broken"), or is only "run the full test suite" / "CI passes" without any check that observes the fix itself. | required |
| thread-engaged | The plan comment and plan, read against the thread highlights: maintainer/owner comments (direction, located culprit, posted patch, requested testing, a settled approach) and any open or prior PRs mentioned. | Pass if the thread holds no explicit direction or competing PR, or if the plan comment acknowledges and works with it (follows the direction, or names it and gives a reason to differ; engages open PRs instead of silently racing them). Fail if a maintainer gave explicit direction (a culprit location, a patch to test, a chosen approach) and the comment proposes something else without mentioning it. | required |
| ai-disclosure | The repo-facts block's contribution policy (CONTRIBUTING.md / AI_POLICY.md summary), read against the plan comment's text. Treat every package as AI-assisted work. | Pass if the repo states no AI policy, or a policy with no disclosure ask for issue comments (disclosure only in PRs, "be responsible", "understand what you submit"). If the policy requires disclosing AI usage in issues/comments or "in any form", pass only if the comment explicitly discloses AI assistance (tool and/or extent); fail if it does not. If the policy requires comments in the contributor's own words, pass if the comment is first-person and specific to this issue. | required |
| unknowns-stated | The plan's risks/unknowns lines and confident claims, read against what the repro evidence actually established. | Pass if things the evidence has not established are named as unknowns or things to check, not asserted as fact. | preferred |

## Verdict rule

accept if every required check passes; reject if any required check
fails. preferred checks never change the verdict. unclear on a
required check counts as fail, with one exception: on ai-disclosure,
unclear (the policy text is ambiguous about issue comments) counts as
pass unless the policy explicitly names issues, comments, or "all"/"any"
AI usage.
