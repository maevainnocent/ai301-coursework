# Rubric: is this reproduction package ready to post?

Every check reads the package against the issue it belongs to. Grade
the proof, not the polish: a short report with the right artifact
passes, a long confident one with the wrong artifact fails. Where a
check says "the issue's target", that means the version, platform,
input, and trigger the issue body and thread highlights establish (see
the evidence guide's Environment and Steps sections).

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| env-recorded | The repro report's environment record (version of the tool tested, OS/platform, and any setting the issue or the repo-facts bug-report template names as relevant, e.g. driver, shell, build profile, backend), read against the issue's stated environment and the thread highlights. | Pass if the report states the tool version and platform it ran on, plus any dimension the issue itself says the bug depends on, AND the tested version/platform either matches the issue's target or the report explicitly names the difference. Fail if there is no environment record, if a dimension the issue makes decisive is missing, or if the report silently tested a version the issue/thread has moved past (e.g. an old release when the bug is confirmed on latest/main). | required |
| steps-rerunnable | The repro report's steps or command transcript, read from starting state to trigger, against the issue's trigger (the exact syntax, flag, input, or action the issue says causes the bug). | Pass if a stranger with only public inputs could re-run the attempt: every command, input file, or config needed is shown or quoted (or the issue's own script is named as run verbatim), AND the steps contain the issue's trigger itself, unchanged. Fail if a step depends on something private or unshared (private repo, unshared config), is a vague instruction with no command where the trigger needs one, or if the input was altered so the issue's trigger is not what ran. | required |
| behavior-matches-issue | The artifacts in the repro report (pasted output, logs, console text, exit codes, error messages) read against the specific behavior the issue describes (its error class/message, exit code, crash vs. graceful error, wrong value). | Pass if the shown artifact displays the issue's specific behavior (same failure kind, same symptom; minor version-related wording drift is fine), OR, for a report that says it could not reproduce, the artifact shows what the attempt actually produced. Fail if there is no artifact, if the artifact only shows the tool running normally, or if it shows a different/adjacent failure (a compile error instead of a runtime path error, a graceful validation error instead of a crash/panic, garbled output with the process still alive instead of a crash, an old version's different error). | required |
| honest-outcome | The report's stated conclusion and the claim comment's description of the reproduction, read against what the artifacts actually show. | Pass if the central claim (reproduced, or could not reproduce) is backed by a shown artifact, deviations from the issue are named, and an inability to reproduce is stated as such with what differed. Supporting observations stated in plain words (a control run's result, a version note) do not each need their own pasted output, as long as they do not contradict the artifacts shown. An evidenced cannot-reproduce PASSES. Fail if the words claim more than the artifacts show: "confirmed", "guaranteed reproducible", "verified the root cause", or "matches the issue" over an artifact that does not show it, or a generalization to environments the report never tested (especially ones maintainers said they could not reproduce on). | required |
| claim-specific-modest | The candidate claim comment, read against the issue's title and body. | Pass if the claim names something only true of this issue (its symptom, component, version, or a thread pointer) AND states a concrete next step of investigation, while promising no fix, outcome, or date. Fail if the claim could be pasted onto any issue unchanged ("+1", "assign me", "I can work on this"), states no intent, or promises a fix, a guaranteed outcome, or a deadline. | required |
| ai-disclosure | The repo-facts block's contribution policy (CONTRIBUTING.md / AI_POLICY.md summary), read against the text of both candidate comments. Treat every package as AI-assisted work. | Read the policy first. Pass if the repo states no AI policy, or a policy that asks for no disclosure on issue comments (e.g. disclosure only on PRs, "be responsible", "understand what you submit"). If the policy requires disclosing AI usage in issues/comments or "in any form", pass only if a comment explicitly discloses AI assistance (tool and/or extent); fail if neither comment discloses. If the policy requires comments in the contributor's own words, pass if the comments are first-person and specific to this issue, fail if they read as templated generated text. | required |
| control-run | The repro report's steps and artifacts. | Pass if the report includes a contrasting run (without the trigger, other setting, other version) whose artifact differs, isolating the trigger. | preferred |

## Verdict rule

accept if every required check passes; reject if any required check
fails. preferred checks never change the verdict. unclear on a required
check counts as fail, with one exception: on ai-disclosure, unclear
(the policy text is ambiguous about issue comments) counts as pass
unless the policy explicitly names issues, comments, or "all"/"any"
AI usage. In claim-only live mode, checks marked not-yet-applicable
are left out of the verdict as SKILL.md describes.
