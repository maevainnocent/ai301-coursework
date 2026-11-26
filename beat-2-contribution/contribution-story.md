# Contribution: Add Jest tests for the Markdown Editor (#390)

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Maeva Innocent
**GitHub Username:** maevainnocent
**Issue:** https://github.com/Bashamega/WebDevTools/issues/390
**Pull Request:** https://github.com/Bashamega/WebDevTools/pull/707

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 9: Built the issue-scout search strategy and patched it after real scans**

I wrote two `gh search issues` queries from my fit profile (JavaScript good-first-issues, one also tagged documentation) and added date filters and a one-per-repo ranking rule after my first test run was flooded by repos that opened dozens of issues that same day. My first scan let through a Turkish-language issue, because `--language` matches the code, not the issue text, so I added "English only" to my profile and a ranking rule that drops non-English titles. Grading issues by hand showed gaps the rubric can't see: a PR that wasn't linked to its issue (WebDevTools #402), an issue that was already fixed in the code (Ocelot #4743), and a contribution-policy check that passed on silence for juxtaposition #162, whose maintainer told me after I claimed it that they don't accept AI help. I withdrew from #162, logged patches in scan-notes.md (search PRs for the issue's key terms, check for unwritten AI rules, disclose AI use upfront), and claimed WebDevTools #390 with that disclosure in my claim comment.


## Why I Chose This Issue

I chose issue #390 because I wanted to work on an existing project and get more experience with JavaScript and testing. The issue was about adding Jest tests to the Markdown Editor in WebDevTools. I liked that the issue had a clear goal and gave me a chance to understand how the project worked and how its features could be tested.

I also used my issue-scout tool to help me decide if the issue was worth working on. It passed all nine checks, which made me feel more confident about choosing it.

**Finding and Claiming the Issue**

While looking for issues, I learned that I should not always follow my tool's verdict without looking into the details. For example, the scout rejected issue #162 because it failed the bounded-scope check due to having two or more closed, unmerged pull requests. I still chose to pursue it because I looked into those pull requests and saw that one was blocked by an unsigned CLA, while the other was waiting on a style change that was never addressed.

I also learned that just because an issue passes my tool's contribution-policy check does not mean the project will accept every contribution. The policy check passed for #162 because the project did not have a clear AI policy listed, but the maintainer later explained that they did not accept AI-assisted contributions.

After that experience, I wanted to be more upfront about using AI when claiming an issue. When I commented on issue #390, I explained that I use Claude Code to help me understand the code and draft tests, but that I would review the code myself, make sure I understood it, and run the tests locally.

I posted my claim on November 18, and the maintainer assigned the issue to me on November 19.

Claim: https://github.com/Bashamega/WebDevTools/issues/390#issuecomment-6994456853

**How My Toolkit Helped**

My issue-scout tool helped me narrow down the issues and decide which ones were worth looking into. However, I also had to make changes to my search process because the first results were not always what I was looking for.

On November 17, I noticed that many of the results were coming from repositories that had opened a lot of issues on the same day. I added date filters and a rule to only show one issue per repository.

I also ran into a problem when a Turkish issue passed the language check. This made me realize that the tool was checking the repository's language, not the language of the actual issue. I updated my preferences to focus on English issues and avoid translation work.

These changes helped me find issues that were a better fit for what I wanted to work on.

**What I Learned**

One thing I learned from this experience is that a tool can help me make decisions, but I still have to use my own judgment. An issue can pass all the checks and still not be the right issue to work on. I also learned that I should look into why an issue received a certain verdict instead of relying only on the final result.

I also learned how important it is to communicate with maintainers and be honest about using AI. My experience with issue #162 taught me not to assume that a project accepts AI contributions just because its guidelines do not say otherwise.

Overall, this process helped me become more careful when choosing open-source issues. I also got a better understanding of how to use my tools to support my work instead of relying on them to make every decision for me.

**Current Status**

The maintainer assigned issue #390 to me on November 19. My next step is to work on the Jest tests for the Markdown Editor, make sure I understand the tests I write, and run them locally before submitting a pull request.

**Toolkit**

- Tool: I used my issue-scout tool to search for open-source issues and help me decide which ones were worth working on. It uses my search strategy and rubric to check issues before I choose one.
- What it produced: My first scan checked 5 issues and accepted 2. After that, I checked 12 more issues myself. For issue #390, the scout gave an accept verdict, and all 9 checks passed.
- Difficulties: Some of the results were from hobby projects that were not a good fit for me. A Turkish issue also passed the language check because the tool was checking the repository's language instead of the actual issue. Another problem was that the policy check passed for #162 because there was no AI policy listed, but the maintainer later said they did not accept AI contributions.
- What changed: I added date filters and a rule to only show one issue per repository. I also added an English-only rule because I wanted to avoid translation work. After what happened with #162, I started being more open about using AI when claiming issues. I also wrote down four rubric changes I could make, but I never applied them.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
