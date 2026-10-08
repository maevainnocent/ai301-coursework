# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/63

**Verdict output**

````
Graded all three in live mode against your installed rubric (scope: codepath/pathreview-ai301-fa26-howard, all three in scope; house rule noted). Today = 2026-10-08.

Repo-level evidence (shared): last 5 commits by Andrew Burke (Aburke225), newest 2026-09-16 (22 days); last push 2026-09-16, not archived, 0 stars, no releases; docs/CONTRIBUTING.md has no AI statement (silence passes); maintainer first-response sample (#53, #69, PR #76 threads): no Owner/Member/Collaborator replies.

### Accepted (ranked by fit)

**1. #63 — README scorer test fixture is too short for its own word-count assertion** — all required checks pass. Preferred: invited ✓ (good first issue), acceptance ✓, responsive ✗, release ✗.
*Fit:* smallest task (tier-1, one test fixture), minimal setup (just pytest) — matches your "smaller tasks, limited setup" preference; Python, which you've used.

**2. #70 — README parser test fixture is indented** — all required checks pass. Preferred: invited ✗ (no label/maintainer comment), acceptance ✓, responsive ✗, release ✗.
*Fit:* tier-2, 2–4 hrs across 3 files — larger than you want; also Python.


### Rejected

**#72 — `verify_password` raises UnknownHashError** — fails **not-already-claimed**: open PR #76 is formally cross-referenced and mentioned in the thread. The house rule exempts other students' *claim comments*, not open PRs, and your rubric fails any open linked PR. (Tension worth noting for your Trade-offs field: if you think the house rule should cover open PRs, that's a rubric change, not a run change.)

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/63",
    "checks": [
      {"name": "maintainer-commits", "grade": "pass", "evidence": "Last commit 2026-09-16 by human author Andrew Burke (Aburke225), 22 days before today"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "Sampled threads #53, #69, PR #76 show no OWNER/MEMBER/COLLABORATOR first response"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; last push 2026-09-16 (22 days ago)"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "Single test fixture/assertion fix with repro: 'pytest tests/unit/test_readme_scorer.py -q' -> assert 51 > 100"},
      {"name": "not-already-claimed", "grade": "pass", "evidence": "No assignees, 0 comments, no linked or cross-referenced PRs in timeline"},
      {"name": "contribution-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI policy; no AI_POLICY.md (silence passes)"},
      {"name": "maintainer-invited", "grade": "pass", "evidence": "Labeled 'good first issue' (and tier-1) on 2026-09-14"},
      {"name": "acceptance-stated", "grade": "pass", "evidence": "'Extend the fixture (or correct the assertion) so the test validates what it intends to'"},
      {"name": "recent-release", "grade": "fail", "evidence": "No releases published"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/70",
    "checks": [
      {"name": "maintainer-commits", "grade": "pass", "evidence": "Last commit 2026-09-16 by human author Andrew Burke (Aburke225), 22 days before today"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "Sampled threads #53, #69, PR #76 show no OWNER/MEMBER/COLLABORATOR first response"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; last push 2026-09-16 (22 days ago)"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "Fixture de-indent plus xfail removal; body says 'The parser isn't wrong'; est. 2-4 hours, not umbrella or core-internals"},
      {"name": "not-already-claimed", "grade": "pass", "evidence": "No assignees, 0 comments, no linked or cross-referenced PRs in timeline"},
      {"name": "contribution-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI policy; no AI_POLICY.md (silence passes)"},
      {"name": "maintainer-invited", "grade": "fail", "evidence": "Labels are bug, ingestion, tier-2 only; no comments"},
      {"name": "acceptance-stated", "grade": "pass", "evidence": "'the fixture shouldn't be indented' ... 'remove the marker as part of the fix'"},
      {"name": "recent-release", "grade": "fail", "evidence": "No releases published"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/72",
    "checks": [
      {"name": "maintainer-commits", "grade": "pass", "evidence": "Last commit 2026-09-16 by human author Andrew Burke (Aburke225), 22 days before today"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "Sampled threads #53, #69, PR #76 show no OWNER/MEMBER/COLLABORATOR first response"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; last push 2026-09-16 (22 days ago)"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "Single function fix in core/security.py to return False on malformed hash; est. 1-2 hours"},
      {"name": "not-already-claimed", "grade": "fail", "evidence": "Open PR #76 by SHEKHAR-Y cross-referenced in timeline and mentioned in thread 2026-09-20; house rule exempts claim comments, not open PRs"},
      {"name": "contribution-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI policy; no AI_POLICY.md (silence passes)"},
      {"name": "maintainer-invited", "grade": "pass", "evidence": "Labeled 'good first issue' (and tier-1) on 2026-09-14"},
      {"name": "acceptance-stated", "grade": "pass", "evidence": "'Verification against a malformed hash should fail closed (return False), not raise'"},
      {"name": "recent-release", "grade": "fail", "evidence": "No releases published"}
    ],
    "verdict": "reject"
  }
]
```
````

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. Full run (20 issues), saved as `eval-run.txt` on 2026-10-07: `agreement: 19/20 scored items  (bar: 18/20: PASS)`

**Issue analysis**

`issue-20` (excalidraw/excalidraw#11811, "Add company logo shape to the toolbar", category: scope)

- My rubric's decision: `accept` (eval-run.txt: `issue-20  reject  accept   NO     graded accept`)
- Gold label: `reject` — gold note: "one-line feature wish with no spec and a product decision hiding inside"

The rubric accepted it because all the required checks passed: the repo was active, not archived, had no assignee, linked PRs, or comments, and the CONTRIBUTING.md did not mention AI. The issue also included expected behavior, so it passed the bounded-scope check.

What the rubric missed was that it was opened by cursor[bot], had no labels or maintainer approval, and involved changes to the toolbar, element model, and export. Whether the app should even include a fixed company-logo shape is ultimately a product decision.

**Check rationale**

From `tools/issue-select/rubric.md`:

> | bounded-scope | Issue body, Comments section, any linked or mentioned closed PRs | None of these hold: explicit umbrella, tracking, or "megaissue" list; design debated with no maintainer decision; maintainer says the fix touches core internals; a usage or support question; 2 or more closed unmerged PRs from earlier attempts; a feature request with no stated expected behavior where a maintainer has not specified or approved what to build. Body length and polish are not graded | required |

The rubric uses specific fail conditions instead of just saying “well scoped” so the decision is clear and consistent. “Body length and polish are not graded” is included because a short or rough bug report can still be a good first issue. The feature-request rule requires both no expected behavior and no maintainer approval so that a feature that has already been approved by a maintainer can still pass.

**Trade-offs**

Bounded-scope misses issue-20 because its feature-request rule only rejects issues with no stated expected behavior. This means a feature request with clear expected behavior but no maintainer approval can still pass. I accepted that tradeoff because 19/20 is still above the bar. If the rule were tightened to reject any feature request without maintainer approval, I would re-run the clear-accept issues with `--only` to make sure they still pass.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. Fit to my interests and time: I wanted to keep up with my understanding of python and it is tier-1. With time i think it is the perfect first issue fit for my skills and space for growth

2. What the verdict got right, and what I weighed that the rubric couldn't: The verdict got that nobody was on it, the repo is alive, the scope is small and clear. The rubric could not weigh the language, which fix is right, and no maintainer replies.

3. Anticipated difficulty in claiming it: No maintaner has replied so it might take a while for me to get a response. I also fear someone else might have clained it already.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
