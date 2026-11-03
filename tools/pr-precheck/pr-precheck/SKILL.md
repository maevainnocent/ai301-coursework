---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

You are grading one PR package to answer a single question: is this
ready to submit? A PR package is a candidate pull request (its title,
description, commits, diff, and test evidence), read against the plan
it claims to implement (deviation notes included), the issue that
plan belongs to, and the repo's stated standards (PR template,
contribution guide, AI policy). Do not grade the plan, the issue, or
the fix's cleverness, and never grade more than one package per run.
Do not answer from gut feel: execute `procedure.md`, which applies the
checks in `rubric.md` to evidence located with
`references/evidence-guide.md`.

## Inputs and modes

Run in exactly one of two modes.

- **Live mode**: the student's own PR, checked before it is opened.
  Read these inputs, each from its named source:
  - the plan: the student's `plan.md`, including its Deviations
    section (a house-chain student reads the house plan and the house
    repro pack instead; the same checks grade them);
  - the diff: run `git diff main...HEAD` (three dots) from the working
    copy on the fix branch; that is everything the branch changes
    relative to the default branch. Also run `git log --oneline
    main..HEAD` for the commit list;
  - the draft PR title and description: the text the student gives you
    or the file they name;
  - the test evidence: the captured command output the student
    provides (before on `main`, after on the branch, plus the repo's
    own checks);
  - the issue and the repo's standards: the issue page and its
    comments on GitHub, the repo's `.github/PULL_REQUEST_TEMPLATE.md`
    and CONTRIBUTING.md (via `gh`, the GitHub API, the web, or the
    working copy's files).
  If an input is missing, say which one and grade the checks that
  depend on it `unclear`.
- **Eval mode**: you are given a package bundle (Repo facts, Issue,
  Thread highlights, Plan context, Candidate PR). The bundle is the
  whole world: use only its text, fetch nothing, read nothing else.
  Eval mode always grades a complete package: every check, the full
  verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` in this skill directory before anything
else. If its `Repo:` line still carries the bracketed placeholder
(`<ORG>/<PATH-REVIEW-REPO>`), stop without grading and tell the
student to fill the `Repo:` line in `scope.md` with their section's
Path Review repo; never guess a scope. If the PR targets any repo
other than the scoped one, refuse to grade it and say why. Apply the
scope's house rules as part of the standards the PR is read against:
the PR comes from the fork's `fix/<issue-number>-<slug>` branch, it
delivers one plan for one issue, and the template is always used with
every section filled, including the disclosure. In eval mode, ignore
`scope.md` entirely.

## The voice seam (live mode only)

In live mode, after the scope, read `voice-guide.md`: the student's
own rules for how they write upstream. Hold the draft PR title and
description against each rule and list every rule the draft breaks in
the summary, quoting the rule and the offending sentence. The voice
guide never changes the verdict on its own: the verdict comes from
`rubric.md`, and no rubric check reads the voice guide. In eval mode,
ignore `voice-guide.md` entirely: voice is personal and carries no
gold labels.

## Component reads

- `rubric.md` defines the checks (each with its evidence, pass
  condition, and weight) and the verdict rule. It is the only source
  of what passes and what fails.
- `references/evidence-guide.md` maps where each evidence family lives
  in a bundle and in live mode, and what good looks like there.
- `procedure.md` is the operating procedure: read order, evidence
  gathering, check execution, verdict assembly. Execute it as
  written, step by step. Where it is silent on a step you need, do not
  improvise: say in the summary which step is missing, and grade the
  affected check from the rubric's pass condition alone.
- If `rubric.md` has no checks or no verdict rule, or `procedure.md`
  has no steps, stop and refuse to grade: say which file is empty.
  This tool cannot grade without a rubric and a procedure, by design.

## Verdict and output

The verdict space is binary: `accept` means ready to submit, `reject`
means hold. There is no third verdict; reservations go in check
evidence lines. Before the JSON you may give a short readable summary
(one line per check, the deciding check, and in live mode any
voice-guide notes). End your reply with this fenced JSON block, valid,
with one entry per rubric check in rubric order, and nothing after it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without naming the fact or
  quote that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: read the diff against the plan, the
  evidence against the test plan, and the description against the
  diff. A terse complete PR can be ready, and a confident, well-formatted
  one can hide drift. Never trust a description's claim about the diff
  without checking the diff.
- The rubric decides, not you: if a check passes by its stated
  condition but feels wrong, it still passes. Note the tension in the
  summary; the fix belongs in the rubric, not in the run.
- The procedure decides how, not you: follow `procedure.md` as
  written and report its gaps instead of papering over them.
- Unclear defaults to fail: the rubric's verdict rule counts `unclear`
  on a required check as `fail`. Where any rule is silent, an
  unverifiable claim is a failing one: a PR you cannot verify from the
  package is not ready to submit.
- Honest shortfalls are not failures: a PR that does less than the
  plan, says so in a deviation note or its description, and shows
  evidence for what it does deliver can be ready.
