# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-commits | Repo facts: "last 5 default-branch commits" (dates and authors) | At least 1 of the 5 commits is within 90 days of the capture date and is human-authored, or is a bot merging a human's pull request | required |
| maintainer-responsive | Repo facts: "maintainer first-response sample" | At least 1 of the sampled issues got a maintainer first response within 45 days of the capture date | preferred |
| repo-in-use | Repo line: "archived:" and stars; Repo facts: "last push to any branch" and "latest release" | Not archived, and the last push to any branch is within 180 days of the capture date | required |
| bounded-scope | Issue body, Comments section, any linked or mentioned closed PRs | None of these hold: explicit umbrella, tracking, or "megaissue" list; design debated with no maintainer decision; maintainer says the fix touches core internals; a usage or support question; 2 or more closed unmerged PRs from earlier attempts; a feature request with no stated expected behavior where a maintainer has not specified or approved what to build. Body length and polish are not graded | required |
| not-already-claimed | Repo facts: "this issue: assignees:" and "linked PRs:" with state; Comments section | No assignee, no open linked PR (formal or mentioned in the thread), and no claim comment ("I'll take this", "working on this") within 60 days of the capture date. A closed unmerged PR is an abandoned attempt, not a claim. If sidebar and thread disagree, the thread wins | required |
| contribution-policy | Repo facts: "contribution policy" line | The policy does not outright ban AI-generated contributions. Conditions (disclosure, testing, human review) and silence both pass | required |
| maintainer-invited | Labels, label event dates, Comments section | Labeled good first issue or help wanted, or a maintainer comment (`author_association` Owner, Member, or Collaborator) invites contributors | preferred |
| acceptance-stated | Issue body | Body states expected behavior or an acceptance checklist | preferred |
| recent-release | Repo facts: "latest release" | A release within 365 days of the capture date | preferred |

## Verdict rule

Accept if every `required` check passes. Reject if any `required` check fails. `unclear` on a required check counts as fail. `preferred` checks never change the verdict; they only rank the accepted issues.

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
