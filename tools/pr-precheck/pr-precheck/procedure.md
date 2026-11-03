# Procedure: how this tool grades a PR package

Follow these steps in order for every package. Do not grade any check
until the read order is complete.

## Read order

1. Live mode only: read `scope.md`, confirm the PR targets the scoped
   repo, and note the house rules. Then read `voice-guide.md`. Eval
   mode: skip both files.
2. Read `rubric.md` and `references/evidence-guide.md`. Write down the
   six check names and the verdict rule.
3. Read the Repo facts block (live: the repo's
   `.github/PULL_REQUEST_TEMPLATE.md` and CONTRIBUTING.md). Note, as a
   numbered list: (a) every template section, checklist item,
   issue-link format, and required entry file the "pull requests"
   line asks for, or "none"; (b) the AI policy's exact ask, or "none".
4. Read the Issue and the Thread highlights. Note in one line what
   behavior is wrong and the input that reproduces it, and list every
   maintainer direction or open question, or "none".
5. Read the Plan context (live: `plan.md`, Deviations section
   included) BEFORE the PR. Note: (a) every planned piece of work, one
   per line; (b) every file it names; (c) everything it puts out of
   scope; (d) every deviation or deferral note; (e) every case and
   expected-after its test plan names. Reading the plan first matters:
   the fidelity and evidence checks compare the PR to these notes, and
   reading the description first makes its claims look like the plan.
6. Read the Diff (live: `git diff main...HEAD`) BEFORE the
   description. List every file header and, for each hunk, one line
   saying what it does.
7. Read the Description, the Commits, and the Test evidence (live: the
   draft title and description, the commit log, the captured output).

## Evidence gathering

For each check, pull exactly this and write it down:

- plan-fidelity: put the step-5 planned pieces beside the step-6 hunk
  list. For each hunk, write the planned piece, deviation note, test,
  or required entry it maps to, or "unplanned". For each planned
  piece, write the hunk that delivers it, or the note that defers it,
  or "missing". Then quote every description sentence that claims
  what the change does or how faithful it is, and mark each "true of
  the diff" or "not in the diff".
- decisive-evidence: quote the before and after results. Write the
  input they ran and whether it is the issue's reproducing input
  (step 4) or a control. List each case from step 5(e) and mark it
  "shown", "noted as not run", or "missing". Quote the suite/check
  command and its result, or write "none shown".
- clean-diff: scan every `+` line and every hunk from step 6. Quote
  each debug print, commented-out code line, dead function, new TODO,
  or churn-only hunk (import reorder, re-indent, identical re-print).
  Write "none" if there are none.
- template-asks: for each ask in the step-3(a) list, quote the
  description text or name the diff file that meets it, or write
  "missing".
- ai-disclosure: take the step-3(b) policy ask. Quote the
  description's disclosure sentence, or write "no disclosure".
- thread-engaged: for each step-4 maintainer direction or question,
  quote the description sentence that responds, or write "not
  mentioned".

## Check execution

1. Execute the checks in rubric order: plan-fidelity,
   decisive-evidence, clean-diff, template-asks, ai-disclosure,
   thread-engaged.
2. Grade each check only by its pass condition in `rubric.md`,
   against the evidence gathered for it above. Do not let one check
   decide another: a correct fix does not excuse debris, decisive
   evidence does not excuse a missing template item, and a messy diff
   is not drift unless a hunk does unplanned work.
3. Grade every check, even after a required check has already failed:
   the student needs every result.
4. If the evidence a check needs is genuinely absent from the package
   (not just hard to find), grade it `unclear` and say what is
   missing. Two absences are passes, not `unclear`: no stated template
   or asks (template-asks) and no stated AI policy (ai-disclosure).
5. Write one evidence line per check: the quote or fact that decided
   it. For a fail, quote the offending hunk line, claim, or missing
   item.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every required
   check (plan-fidelity, decisive-evidence, clean-diff,
   template-asks, ai-disclosure) is `pass`. Any required `fail` gives
   reject.
2. `unclear` on a required check counts as `fail`.
3. thread-engaged is preferred: report it, never use it in the
   verdict.
4. In the readable summary, name the deciding check: the first
   required check in rubric order that failed or was unclear, with its
   evidence quote, or "all required checks passed". Live mode: list
   every voice-guide rule the draft title or description breaks,
   quoting the rule.
5. End with the JSON block exactly as SKILL.md specifies, one entry
   per check in rubric order, and nothing after it.
