# Evidence guide: where proof lives in a reproduction package

The issue sets the target; the candidate comments are measured against
it. Always read the issue (body plus thread highlights) first, then the
claim comment, then the repro report.

## Environment

- Where it lives: eval bundle: the "Environment:" line or paragraph at
  the top of the candidate repro report; compare it against the
  issue's own "Environment" section, the version numbers in the issue
  body/title, the thread highlights (maintainers often say "confirmed
  on main" or "cannot reproduce on X"), and the repo-facts block's
  "bug reports: template asks for ..." line and "latest release" line.
  Live mode: the draft's environment block, against the issue body,
  its comments, and the repo's issue template (`.github/ISSUE_TEMPLATE`).
- What good looks like: the tool's version and the OS/platform are
  stated, and any dimension the issue says the bug depends on (Windows
  driver, shell, build profile, GUI backend) is named. The version
  tested matches what the issue targets, or the report says how it
  differs ("filed against 13.0.0; still present on 15.2.0"). A record
  of an older version than the one the issue is confirmed on, with no
  mention of that, is a silent deviation, not a record.

## Steps

- Where it lives: eval bundle: the "Steps" list and every fenced
  command block in the candidate repro report, including the inputs
  (files, config, script) it quotes or says it took verbatim from the
  issue. Compare against the issue's "Steps"/reproduction section and
  any thread note naming the trigger ("only happens with --replace").
  Live mode: the draft's steps, against the issue body.
- What good looks like: starting from a clean state, a stranger could
  type the commands and get to the trigger without guessing: inputs are
  shown or named as the issue's own, nothing lives in a private repo or
  unshared config, and the trigger (operator, flag, syntax, setting) is
  exactly the issue's. Compare the input character by character with
  the issue's: a changed operator, range syntax, or variable binding
  means a different bug was exercised.

## Behavior shown

- Where it lives: eval bundle: the fenced output blocks in the repro
  report (terminal output, tracebacks, logs, console text, exit
  codes, `cat -v` captures), plus "Actual:" lines only as a pointer to
  them. Compare against the issue's described failure: its error
  message, exception type, exit code, panic vs. handled error.
  Live mode: the pasted output in the draft (a stranger sees only what
  is pasted, never a local file).
- What good looks like: the artifact itself shows the issue's specific
  failure. Ask: if I only saw this output block, would I recognise the
  issue's bug? A graceful validation error is not a panic (exit 1 vs.
  exit 101); a compile/unbound-variable error is not a runtime path
  error; garbled text with the process alive is not a crash; a version
  banner or a session list only shows the tool runs. A control run
  (same steps without the trigger, with a different output) is strong
  extra proof.

## Honesty

- Where it lives: the sentences that interpret artifacts: "Actual:",
  "Expected:", "confirmed", "matches the issue", root-cause claims in
  the report, and the claim comment's "I reproduced it" line. Read
  each one against the artifact block it refers to.
- What good looks like: every claim points at a shown artifact, the
  words are no stronger than the artifact, and deviations (version,
  platform, input) are named. An honest cannot-reproduce shows the real
  attempt's output, says what differed from the reporter's setup, and
  offers a hypothesis without asserting it; that is a pass. Red flags:
  "guaranteed", "100% reproducible", "verified the race condition",
  "two machines confirm" over no artifact or the wrong one, an
  "Expected" that contradicts the issue, or extending the bug to a
  release maintainers said is unaffected.

## Comms

- Where it lives: the candidate claim comment (read against the issue
  title/body), both comments' text, and the repo-facts block's
  "contribution policy" line (CONTRIBUTING.md, AI_POLICY.md summaries)
  and "bug reports: template asks for" line. Live mode: the drafts
  against the repo's CONTRIBUTING.md / AI policy files and issue
  templates.
- What good looks like: the claim mentions this issue's specifics and
  a concrete next investigation step, promising no fix or date (not
  "assign me, fix in 2 days guaranteed", not "+1"). For AI policy:
  first decide what the repo requires of issue comments. "All AI usage
  in any form must be disclosed" means a comment must contain an
  explicit disclosure ("I used an AI assistant to ...") or it fails,
  however good the proof is. Policies that only ask for disclosure on
  PRs, or only ask contributors to understand and take responsibility
  for their work, or state no AI policy, need no disclosure in issue
  comments. "Comments in your own words" is met by first-person,
  issue-specific writing.
