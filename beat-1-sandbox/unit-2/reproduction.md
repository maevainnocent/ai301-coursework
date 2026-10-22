# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

maevainnocent

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/63#issuecomment-6324683648

````markdown
Hi! I’d like to make this my first contribution. I’m going to start by running pytest tests/unit/test_readme_scorer.py -q to see the assert 51 > 100 failure for myself. Since the test is marked xfail(strict=True), I’ll also use --runxfail to see the actual assertion failure.

As I looked through agent/tools/readme_scorer.py, I noticed that a README needs at least 500 words to be considered “comprehensive.” Anything between 100 and 499 words is only considered “adequate,” so just making the fixture longer than 100 words wouldn’t fix the word_count_category == "comprehensive" assertion.

I’m going to take a closer look at what the test is actually supposed to check and figure out whether the fixture needs to be 500+ words or if the assertions need to be updated. I’ll share what I find here!
````

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/63#issuecomment-6350330362

````markdown
Reproduced on current main. Report below.

**Environment:** macOS 14.4 (arm64), Python 3.14.8 in a fresh venv, pytest 9.1.1, structlog 26.1.0, repo at commit `99673c7`. This test only needs `pytest` and `structlog`, so I skipped Docker and the database.

**Steps:**

```bash
git clone https://github.com/codepath/pathreview-ai301-fa26-howard.git
cd pathreview-ai301-fa26-howard
python3.14 -m venv .venv && source .venv/bin/activate
pip install pytest structlog
python -m pytest tests/unit/test_readme_scorer.py -q
python -m pytest tests/unit/test_readme_scorer.py -q --runxfail
```

(I used `python -m pytest` instead of plain `pytest`. On my Mac, plain `pytest` picked up an old global Python 3.8 install and stopped with `ModuleNotFoundError: No module named 'structlog'`, which has nothing to do with this issue.)

**Output, the issue's command as-is:**

```
x......................                                                  [100%]
22 passed, 1 xfailed in 0.06s
```

The test is marked `xfail(strict=True)` for this issue, so the failure is hidden on a normal run.

**Output with `--runxfail`:**

```
>       assert data["word_count"] > 100
E       assert 51 > 100

tests/unit/test_readme_scorer.py:60: AssertionError
------------------------------------- Captured stdout call -------------------------------------
2026-10-21 16:08:43 [info     ] readme_scored                  category=minimal score=0.8717142857142858 word_count=51
=================================== short test summary info ====================================
FAILED tests/unit/test_readme_scorer.py::TestReadmeScorer::test_readme_with_all_quality_signals - assert 51 > 100
1 failed, 22 passed in 0.05s
```

**Expected:** the test's fixture is long enough for the test's own assertions (`word_count > 100` and `word_count_category == "comprehensive"`).

**Actual:** The scorer is only counting 51 words in the fixture, so the test fails because 51 is not greater than 100. This is the same problem mentioned in the issue. I also noticed that it labels the fixture as minimal instead of comprehensive.

Next, I’m going to check whether I should add more words to the fixture to reach 500+ words or change the assertions to fit the shorter fixture. I’ll share an update here once I figure out the best approach.
````

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run (20 packages) on 2026-10-08 with my first rubric, kept with `--out run1-results.json`: `"agreement": [17, 20]`. Three accepts missed. pkg-03 failed `honest-outcome`, with the grader's evidence reading: "Dropping -r '$1' ... reports 1, 4, 7, 10 correctly" is asserted with no artifact shown in the report. Also, pkg-05 and pkg-12 failed `steps-rerunnable`.
2. Revised `honest-outcome`: it now asks for the central claim to be backed by a shown artifact, and supporting observations in plain words no longer each need pasted output. No other check changed.
3. Full run (20 packages), saved as `eval-run.txt`: `agreement: 18/20 scored items  (bar: 18/20: PASS)`. pkg-03 and pkg-12 now agree. Still missed: `pkg-05  accept  reject   NO     failed: steps-rerunnable, control-run` and `pkg-09  accept  reject   NO     failed: steps-rerunnable, control-run`.


**Package analysis**

`pkg-09` (sharkdp/fd#2033, "`--exec-batch` doesn't always run commands in order")

- My rubric's decision: `reject`. From `eval-run.txt`: `pkg-09  accept  reject   NO     failed: steps-rerunnable, control-run`
- Gold label: `accept`. Gold note: "honest cannot-reproduce: real attempt at the argument-size reordering with marker-order artifacts, names what differed (uniform name lengths, 2 MiB ARG_MAX) and what a triggering setup likely needs"

pkg-09 is an honest cannot-reproduce. It opens with "Result: I could NOT reproduce scenario 2", shows the exact commands (creating 120000 files, then two `--exec-batch` commands writing ONE and TWO to a log), shows `cat /tmp/order.log` with every ONE before every TWO, and then explains what probably differed: "fd appears to flush both command buffers at the same file-count boundary on this input (uniform name lengths)".

My rubric failed it on `steps-rerunnable`, which requires that "the steps contain the issue's trigger itself, unchanged". The issue's trigger for scenario 2 is one command hitting the size limit before the other. The report admits its run never reached that state, so the trigger was never actually in the steps. On top of that, the second attempt ("re-ran with the second command's arguments padded to be ~40% longer ... (a longer wrapper string)") is described but its command is never shown, so a stranger couldn't re-run that part exactly. Read literally, both points fail my check.

The gold label is right that this is good work. The report is honest about what happened and the artifact matches its claim. My check was written to catch reports that quietly change the input to a different bug, and it can't tell that apart from a report that tried to hit the trigger, failed, and said so. My `honest-outcome` check passes evidenced cannot-reproduces, but `steps-rerunnable` still blocks them when the trigger is the thing they couldn't reach. `control-run` also failed because there is no contrasting run, but that check is preferred and did not change the verdict.

**Check rationale**

From `tools/repro-check/rubric.md`:

> | honest-outcome | The report's stated conclusion and the claim comment's description of the reproduction, read against what the artifacts actually show. | Pass if the central claim (reproduced, or could not reproduce) is backed by a shown artifact, deviations from the issue are named, and an inability to reproduce is stated as such with what differed. Supporting observations stated in plain words (a control run's result, a version note) do not each need their own pasted output, as long as they do not contradict the artifacts shown. An evidenced cannot-reproduce PASSES. Fail if the words claim more than the artifacts show: "confirmed", "guaranteed reproducible", "verified the root cause", or "matches the issue" over an artifact that does not show it, or a generalization to environments the report never tested (especially ones maintainers said they could not reproduce on). | required |

My first version said "Pass if every claim of what happened is backed by a shown artifact". On my first full run that wording rejected pkg-03, which the gold label accepts. pkg-03 pastes the exact ripgrep command and the wrong line numbers, then adds one sentence with no pasted output: "Dropping `-r '$1'` from the same command reports 1, 4, 7, 10 correctly". The grader read "every claim" literally and failed the whole package over that one sentence, even though the main reproduction was fully shown.

So I narrowed it to the central claim, reproduced or could not reproduce, and added that supporting observations like a control run's result or a version note don't each need their own pasted output, as long as they don't contradict what is shown. I kept the fail list the same on purpose, because that list is what the check exists for: words like "confirmed", "guaranteed reproducible", or "verified the root cause" over an artifact that doesn't show it still fail, and so does stretching the bug to environments the report never tested. I also kept "An evidenced cannot-reproduce PASSES" so an honest failed attempt isn't punished for not finding the bug.

**Trade-offs**

Loosening `honest-outcome` could have let over-claiming packages through. I didn't run separate `--only` canaries. My second full run is the check instead, because it graded every package after the change. The packages most likely to flip were still rejected: `pkg-15  reject  reject   yes` (a root cause asserted with no evidence), `pkg-17  reject  reject   yes` (the bug generalized to a release the maintainers could not reproduce on), and `pkg-20  reject  reject   yes` (the only disclosure package; `categories: ... disclosure 1/1`).

What the change gives up: a report can now state a control run's result in words without pasting it, and `honest-outcome` will accept that as long as the main reproduction is shown and nothing contradicts it. A made-up control result would get through this check.

A miss I accept: `steps-rerunnable` still rejects pkg-05 and pkg-09. pkg-09 is an honest cannot-reproduce, so it never reaches the issue's trigger, and my check reads "contain the issue's trigger itself" literally. I left the check alone because it names the failure in pkg-02 and pkg-08, which changed the input and got a different bug. Those two also fail `behavior-matches-issue`, so loosening `steps-rerunnable` probably would not flip them. It would weaken the one check that names the real problem in a package like pkg-18, though, where the whole reproduction lives in a private monorepo. I also saw that `steps-rerunnable` is not fully stable between runs. pkg-12 failed it in run 1 and passed it in run 2 with no change to that check, and pkg-09 went the other way.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
