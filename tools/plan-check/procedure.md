[procedure.md](https://github.com/user-attachments/files/33878271/procedure.md)

# Procedure: how this skill grades a plan package

Follow these steps in order for every package. Do not grade any check
until the read order is complete.

## Read order

1. Live mode only: read `scope.md`, confirm the issue is in the scoped
   repo, and note the house rules. Then read `voice-guide.md`.
2. Read `rubric.md` and `references/evidence-guide.md`. Write down the
   check names and the verdict rule.
3. Read the Issue (title, body, stated version/steps). Note in one
   line: what behavior is wrong.
4. Read the Thread highlights (live: every issue comment). Note:
   (a) every maintainer/OWNER/MEMBER direction (a culprit location, a
   patch or test binary, a request to test, a settled approach), and
   (b) every open or prior PR mentioned. Write "none" if there are none.
5. Read the Repro evidence (live: the student's posted repro comment)
   BEFORE the plan. Note: (a) the step where the bad behavior first
   appears, (b) every control run and what it showed, (c) what the
   repro does not establish. Reading it before the plan matters: the
   cause-grounded check compares the plan to these notes, and reading
   the plan first makes its confident cause look like the evidence.
6. Read the Repo facts block (live: CONTRIBUTING.md and any AI policy
   file). Note the contribution policy's exact AI ask for issue
   comments, or "none".
7. Read the Candidate plan, then the Candidate plan comment (live: the
   draft plan.md and draft comment).

## Evidence gathering

For each check, pull exactly this and quote it:

- cause-grounded: quote the plan's cause sentence. From the step-5
  notes, list each control/step and write whether it is consistent
  with that cause.
- bounded-scope: quote the change statement and the In/Out lines;
  list every distinct piece of work the plan commits to.
- executable: list every file, function, or code site named, and quote
  the sentence that chooses the approach. Quote any hedge ("somewhere",
  "not sure", "whichever").
- decisive-test: quote the test plan. Write the observable outcome it
  names, or "none named".
- thread-engaged: take the step-4 notes. For each direction or PR,
  quote the comment sentence that responds to it, or write "not
  mentioned".
- ai-disclosure: take the step-6 policy note. Quote the comment's
  disclosure sentence, or write "no disclosure".
- unknowns-stated: quote the plan's unknowns/risks lines and any
  certainty claim not backed by the step-5 notes.

## Check execution

1. Execute the checks in rubric order: cause-grounded, bounded-scope,
   executable, decisive-test, thread-engaged, ai-disclosure,
   unknowns-stated.
2. Grade each check only by its pass condition in `rubric.md`,
   against the evidence gathered for it above. Do not let one check's
   result change another's (a wrong cause does not make the test plan
   fail; a great test plan does not rescue a bundled scope).
3. Grade every check, even after a required check has already failed:
   the student needs every result.
4. If the evidence a check needs is genuinely absent from the package
   (not just hard to find), grade it `unclear` and say what is missing.
   For thread-engaged, an empty thread is not absent evidence: it is a
   pass. For ai-disclosure, a repo with no stated policy is a pass.
5. Write one evidence line per check: the quote or fact that decided it.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every required
   check is `pass`. Any required `fail` gives reject.
2. `unclear` on a required check counts as `fail`, except on
   ai-disclosure, where it counts as pass unless the policy explicitly
   names issues, comments, or all/any AI usage.
3. `unknowns-stated` is preferred: report it, never use it in the
   verdict.
4. In the readable summary, name the deciding check (the first
   required check that failed, or "all required checks passed") with
   its evidence quote. Live mode: add any voice-guide rule the draft
   comment breaks.
5. End with the JSON block exactly as SKILL.md specifies, and nothing
   after it.
