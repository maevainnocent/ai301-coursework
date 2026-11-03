# Evidence guide: where evidence lives in a PR package

The plan says what the PR promised, the diff shows what it actually
does, the evidence shows it ran, and the repo facts say what the repo
asks of every PR. In an eval bundle the parts are: Repo facts, Issue,
Thread highlights, Plan context (repro evidence plus the accepted
plan), and Candidate PR (Title, Description, Commits, Diff, Test
evidence). In live mode: the student's `plan.md` (with its Deviations
section), `git diff main...HEAD` from the working copy on the fix
branch, the draft PR title and description, the captured test output,
the issue page and its comments on GitHub, and the repo's
`.github/PULL_REQUEST_TEMPLATE.md` and CONTRIBUTING.md.

## Plan fidelity (harness category: silent-drift)

- Where it lives: the plan's scope lives in the Plan context block
  (live: `plan.md`): its change statement ("Scope, one bounded
  change: ..."), its "Files:" list, its In/Out or "Not in scope"
  lines, and any deviation, deferral, or "recorded in the plan" note.
  What actually changed lives in the Diff: every `--- a/` / `+++ b/`
  file header and every `@@` hunk. The description's claims ("per the
  plan", "exactly as planned", "no functional changes outside X",
  "docs now document ...", "CHANGELOG entry added") live in the
  Description.
- What good looks like: list the diff's files and say for each hunk
  which planned piece it delivers. Every hunk maps to a planned piece,
  a recorded deviation, a test of the planned behavior, or a
  repo-required entry, and every planned piece maps to a hunk or to a
  note saying it was deferred. Drift in the "more" direction: a
  renaming pass, a rewrite of a neighboring function, a new flag or
  config option, help-text rewording, or a file the plan never names,
  with no note. Drift in the "less" direction: a planned piece (a docs
  update, a second failure mode) missing with no note, especially when
  the description says it is there. A shortfall stated in a plan note
  and restated in the description is honest, not drift.

## Test evidence (harness category: not-tested)

- Where it lives: the Test evidence section and any before/after
  blocks inside the Description, read side by side with the plan's
  "Test plan:" (or "Test" section) and the repro evidence's steps and
  input. The repo's own checks show up as a named command with a
  result (`pytest ... passes (2841 passed)`, `cargo test` (214 tests),
  `go test ./...`, `make lint`). Live: the student's captured terminal
  output and the PR's CI run.
- What good looks like: the same input the issue reports, run before
  and after, with outputs that differ in the way the plan's
  "expected-after" says; every case the test plan names is shown (two
  repros named means two re-runs); controls are extra, never the
  whole proof; and the suite result is stated with a number or
  pass/fail. Red flags: "tested locally", "works now", "verified for a
  full day", "tests pass" alone; a before/after that only runs the
  path the bug never touched (the single-file case, a GET when the bug
  is POST); a test plan naming two failure modes with evidence for one.

## Diff quality (harness category: unreviewable)

- Where it lives: the `+` and `-` lines of every hunk in the Diff, and
  the Commits list ("wip", "fix", "fmt + cleanup", "misc cleanups
  while debugging" point at where debris usually sits).
- What good looks like: every changed line belongs to the fix, its
  test, or a required repo entry, and a reviewer sees the fix without
  sifting. Debris tells, any one of which fails: a debug print or
  `DEBUG` log, `// ` or `# ` in front of a code line, a commented-out
  first attempt, a function nobody calls (`_unused_...`,
  `#[allow(dead_code)]`), a new TODO/FIXME, an import reshuffle, a
  re-indent or reformat of untouched code, or the same lines removed
  and re-added unchanged.

## Standards and comms (harness category: standards-wall)

- Where it lives: the Repo facts block. Its "pull requests" line names
  the template's sections, checklist, issue-link format ("closes
  #xxxx", "fixes #<n>"), and required entries (CHANGELOG.md,
  doc/source/whatsnew, release notes). Its "contribution policy" line
  names any AI policy (CONTRIBUTING.md "Use of AI", AI_POLICY.md). The
  PR's answer lives in the Description (sections, checklist content,
  issue-link line, disclosure sentence) and in the Diff (the required
  entry files). The Thread highlights hold maintainer questions the
  description should engage. Live: `.github/PULL_REQUEST_TEMPLATE.md`,
  CONTRIBUTING.md, and the scope's house rule that "the template is
  always used" with the disclosure section where it applies.
- What good looks like: each stated ask has a matching piece of
  content, in any format; an asked changelog/whatsnew entry is visible
  as a file in the diff, not just promised; and when the policy
  demands disclosure of all AI usage or AI usage in PRs, the
  description says which tool helped and how much. Boilerplate with
  the asks unanswered, or a strict AI policy with no disclosure line,
  is a wall. (Whether the description's claims match the diff is plan
  fidelity, above.)
