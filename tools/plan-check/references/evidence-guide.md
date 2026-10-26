# Evidence guide: where evidence lives in a plan package

The issue says what is wrong, the repro evidence pins down where and
when it goes wrong, and the plan has to follow from both. In an eval
bundle the parts are: Repo facts, Issue, Thread highlights, Repro
evidence, Candidate plan, Candidate plan comment. In live mode: the
issue page and its comments on GitHub, the student's posted repro
comment on that issue, the repo's CONTRIBUTING.md / AI policy files,
and the student's draft plan.md and draft plan comment.

## Diagnosis and grounding

- Where it lives: the plan's "Cause:" line (or whatever sentence says
  why the bug happens), plus any cause the plan comment or thread
  highlights put forward. The behavior that cause must explain lives
  in the repro evidence: every numbered step, every control run ("same
  input without the flag", "English-first", "top-level", "unchanged
  bindings"), every timing or debug output, and the step where the bad
  value or behavior first shows up. Live mode: the student's posted
  repro comment on the issue.
- What good looks like: the named cause is consistent with every
  control. Test it directly: if the cause were true, would each
  control run have come out the way the repro says it did? If a
  control shows the blamed component working, or a step shows the
  damage already done before the blamed code runs (data already wrong
  on read, arguments already consumed earlier), the cause is ruled
  out, however confident the plan or the thread is.

## Scope

- Where it lives: the plan's "Change:" statement, its "In:" and
  "Out:" lines, any list of files/areas/phases, and words like "while
  I'm in there", "also", "migrate", "rewrite", "unify", "new option",
  "CI matrix".
- What good looks like: one change to the code site that produces the
  issue's behavior, with related bigger work either absent or
  explicitly deferred. A plan that handles only part of the issue and
  says why (e.g. one platform it can test) is still bounded. A plan
  with several fronts (the fix plus a refactor, upgrade, new setting,
  redesign, or harness migration) is not, even if the fix inside it is
  right.

## Executability

- Where it lives: the plan's change statement: named files
  (`src/...`), functions, callbacks, branches, constants, and the verb
  attached to them (add, clamp, normalize, wire, remove).
- What good looks like: a stranger could open the named file and start.
  There is one chosen approach, not a menu. Red flags: "somewhere",
  "investigate the stack", "not sure which layer", "upstream or
  vendored, whichever is easier", "profile and optimize", "maybe
  also".

## Test plan

- Where it lives: the plan's "Test:" section, read side by side with
  the repro evidence's steps and its "Expected"/"Actual" lines.
- What good looks like: the test would come out differently on broken
  vs. fixed code and says what the observer will see: "re-run the repro
  steps; at step 3 the color must flip", "exit 0 instead of the
  panic", "regression test with the issue's input expects X". A suite
  run is fine as an extra, never as the only test. Subjective outcomes
  ("feels fast", "nothing else broken") observe nothing.

## Honesty

- Where it lives: the plan's risks/unknowns lines, words of certainty
  ("definitely", "the root cause is", "guaranteed"), and (live mode,
  after building) the plan's deviations section.
- What good looks like: what the repro evidence did not establish is
  named as an unknown or something to check ("verify each tool accepts
  `--`"). A deviation discovered during the build is written into the
  plan with what changed and why; a deviation that only shows up in the
  diff is not honest.

## Comms

- Where it lives: the candidate plan comment, read against (1) the
  thread highlights, especially OWNER/MEMBER/maintainer comments:
  "this seems to be the culprit" with a file, a posted patch or test
  binary, "please test", an approach the thread settled on, open or
  prior PRs; and (2) the repo-facts block's contribution policy line
  (CONTRIBUTING.md, AI_POLICY.md). Live mode: the issue's comments on
  GitHub and the repo's CONTRIBUTING.md.
- What good looks like: the comment shows it read the thread: it
  follows the maintainer's direction or names it and explains a
  different choice, and it engages existing PRs (offers tests to them,
  says it will not race them). For AI policy, decide what the repo
  requires of issue comments first: "all AI usage in any form must be
  disclosed" means the comment needs an explicit disclosure line;
  policies that only ask about PRs, or only ask contributors to
  understand their work, or state nothing, need none; "comments in
  your own words" is met by first-person, issue-specific writing.
