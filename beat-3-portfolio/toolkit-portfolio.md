# Toolkit Portfolio

Path: `beat-3-portfolio/toolkit-portfolio.md`

This file is Assignment 6, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. It has been waiting here since you created the repo in unit 1;
unit 9 is when you write it.

**Only this page is read.** Your `tools/` folders and your installed skill folders are never
opened, so every piece of evidence you want seen has to live inline here: an output excerpt,
a before/after pair, a dated commit reference.

**Write every sentence yourself.** AI may gather diffs, dates and excerpts for you; it does
not draft entries.

**Keep every section header below under its exact name** — Featured Tools, Inventory, The
Arc, and Limitations and What's Next. Feature three or four tools, each in the entry shape
shown below; give every other tool one inventory line.

**Some lines below are labelled, and the label is how they are read.** Three places on this
page use a `Label: your words` shape — the arc's beats, the tool-limits list, and nothing
else. Keep those labels exactly as written, one per line, and never delete a labelled line:
where you have nothing to put after a label, write `none` and move on. A deleted label reads
as a deleted answer.

**Before you finish**, replace every `[bracketed prompt]` with your own words, then delete
the unused `[Tool name]` entry stub, its copy-me sentence, and the prompt sentences under
each header. A leftover bracketed prompt reads as unfilled.

**Student:** Maeva Innocent

## Featured Tools

I chose these three tools because they focused on enhancing existing projects and allowed me to work with the same programming language. I enjoyed finding ways to improve things that already existed, while building my understanding, strengthening my skills, and developing my interest in software development.

**issue-scout**

**What it is, and the judgment hole I wrote:** issue-scout is a program that I created to assist surface open-source issues that are worth contributing to. It began as issue-select in Unit 5 and used a rubric with nine checks to determine if an issue is a good match. Maintainer commits, repo in use, constrained scope, not already claimed, and contribution policy are five checks necessary. The other 4 are preferred checks that help you decide if the project is a good prospect.
In Unit 9 I added scope.md and search-strategy.md to the tool. These modifications helped to make the tool more tailored to the kinds of contributions I wanted to focus on. I also learned that just because an issue technically fits the rubric, doesn’t mean it’s a subject I should investigate. “Language, size and contribution requirements also matter.”

**How it evolved, dated:** My initial evaluation was scored 19/20 on October 7 which was over the required 18/20 passing mark. The primary miss was issue-20, which the tool accepted but had not received graded approval from a maintainer. I opted to accept the tradeoff, rather than adjust the rubric.
On November 17 I updated the Unit 9 search technique and tested the tool against a bigger set of challenges. The first scan didn't get the results I was hoping for, as the top 40 results were primarily from repositories that had opened a bunch of issues on the same day. I implemented date filters and a rule to only show 1 issue per repo.
During that scan, I also encountered a problem with the language filter. adim-adim-git's issue #42 passed checks despite the fact it was written in Turkish. The language filter was verifying the language of the repository, not the language of the issue.
On November 18th, I changed my profile to say I only wanted issues in English, and set a rating criteria to downgrade any results having non-ASCII letters in the headline.

**Evidence:** 
The shift in my profile illustrates how my tastes grew more specific.
Before: "...I prefer smaller tasks that fit into a limited amount of time."
After: "...I prefer smaller tasks that fit into a limited amount of time. I only want issues written in English, and I want to avoid translation work."
The new rule removed 7 out of 100 results in the first query and 9 out of 100 in the second query. It also deleted Turkish problem #42 from the findings.
Issue #162 provided another valuable lesson. The contribution-policy check succeeded, but the maintainer subsequently stated that AI contributions were not welcome:
"Are you using AI to communicate or write code? While it's not documented yet, we don't currently accept AI contributions."
I learned that a policy check that is “silently” passed does not mean that the project actually wants AI-assisted contributions. I covered this in my follow up claim on WebDevTools issue #390 with an AI disclosure.

**repro-check**

**What it is, and the judgment hole I wrote:** I wrote repro-check as a tool to check if someone has actually done a proper reproduction of an issue before filing it. There are 7 criteria including if the environment is documented, the actions may be replayed, the behavior is consistent with the issue, the outcome is honestly reported, and if AI utilization is revealed.
I also created evidence-guide.md and voice-guide.md to help make the evidence and communication more consistent.
One of the primary goals of this tool was to ensure that statements had real evidence behind them without making someone provide redundant output for every tiny observation.

**How it evolved, dated:** 
On October 8, I took the first evaluation and scored 17/20, which was below the passing requirement of 18/20.

One of the issues was pkg-03. The check for honest-outcome was too strict because it required every individual claim to have its own supporting artifact.

I changed the check so that a claim would pass as long as there was a relevant artifact supporting the main assertion (whether the issue was reproduced or could not be replicated).

Before: "Pass if every claim of what happened is backed by a shown artifact"
After: "Pass if the central claim (reproduced, or could not reproduce) is backed by a shown artifact ... Supporting observations stated in plain words ... do not each need their own pasted output"

This change allowed supporting observations to be explained in plain English without requiring separate pasted output for every statement.

I reran the evaluation on October 8, 2026, at 20:57Z. This time, it scored 18/20 and passed. Pkg-03 and pkg-12 also changed from disagreement to agreement.

I submitted my claim on PathReview #63 on October 21 and provided my reproduction evidence on October 22. The related work was documented in the course repository commit f1317b0.


**Evidence:** 

In addition by modifying the language of one check, the score improved from 17/20 to 18/20, indicating that the judgment may be made more reasonable without losing the relevance of evidence.
But I also found that the results were not exactly consistent. In my reproduction notes I have written:
"A made-up control result would get through this check."
I also noted pkg-12 failed check on the first run and passed in the second run, although the check itself was not modified. Pkg-09 exhibited the opposite behavior.
This allowed me to learn that a passing grade does not guarantee a tool is fully reliable. It is also vital to see how consistent the outcomes are from one run to the next.

Evidence: rubric.md, evidence-guide.md, voice-guide.md, reproduction.md, and commit f1317b0.

**pr-precheck**

**What it is, and the judgment hole I wrote:** pr-precheck is a tool I developed to review a pull request before submitting it. It has six checks that focus on whether the pull request follows the original plan, includes the right evidence, has a clean diff, answers the required template questions, and includes AI disclosure.
I also added CONTRACT.md, procedure.md, evidence-guide.md, and voice-guide.md to make the review process more organized and consistent.
Of the tools I built, this one gave me the clearest illustration of how a tool may assist catch real flaws in my own work before submitting it.

**How it evolved, dated:** 
In the assessment, pr-precheck scored 20/20 on November 3, ticking all the boxes.
Getting to that point was not perfectly smooth. An earlier attempt failed due to a compatibility issue with Python 3.8. Another evaluation was scored a 20/20 but not preserved due to a
 FileNotFoundError related to the save-run process.
The biggest breakthrough came when I used the tool to analyze my own pull request draft.
It raised three issues:

1. In my PR description I referenced a repo-wide mypy run which was not documented in the Deviations part of my plan. I have added the missing information.
2. My commit scope, readme-scorer, was not in the scopes authorized in the repository’s CONTRIBUTING rules. I updated it to `test(agent)`.
3. My first AI generated pull request description was reported by the voice guide for not following my criterion of “write in my own words”. I have rewritten the description and run pr-precheck again.


These changes were reflected in the commit history from 7134d9e to 25694e3.

**Evidence:**
It was one of the best examples of my techniques being useful outside of an assessment. pr-precheck found issues on anything I was about to submit, not merely proving that the rubric could get a passing grade.
I did the changes and the tool accepted the changed pull request. When it was opened, 
CI run 41675557470 passed all five jobs, with 376 tests passing and 52 expected failures.
The evaluation did not result in a miss that needed rectification and hence the rubric itself was not changed. This development was achieved by using the comments from using the tool on a real pull request.
Evidence: rubric.md, CONTRACT.md, procedure.md, pull-request.md (especially lines 27–29 and 71–76), commit history 7134d9e → 25694e3, and CI run 41675557470.

## Inventory

- plan-check: A tool I created to review an implementation plan before making changes to a repository. I added procedure.md to establish the order in which evidence and plans should be reviewed. Evidence: rubric.md, evidence-guide.md, procedure.md, voice-guide.md, and the dated Deviations in plan.md. The tool struggles to differentiate between someone who knows exactly where a change goes and someone who doesn’t know where the change should go. I accepted this constraint rather than weakening the check, but it's something I would consider addressing with more testing.

## The Arc

While developing these tools, I found that most of the enhancements came from situations where the original checks or instructions did not fully cover something I ran into. Some improvements were based on evaluation results and others were based on actually utilizing the tools in my contribution process.

**Beat 1**
Date: October 7, 2026
Friction: issue-select accepted issue-20, a feature request without maintainer approval.
Change: I kept the rubric unchanged and accepted the tradeoff.
Result: None. The evaluation remained at 19/20.

**Beat 2**
Date: October 8, 2026
Friction: repro-check received 17/20 because the honest-outcome check required every claim to have its own artifact.
Change: I changed the check to focus on whether the central claim was supported by evidence.
Result: The second run scored 18/20 and passed. Pkg-03 and pkg-12 flipped to agreement.

**Beat 3**
Date: October 22, 2026
Friction: plan-check rejected pkg-14 because of the executable and related checks.
Change: I kept the stricter requirement instead of loosening it.
Result: None. The evaluation remained at 19/20.

**Beat 4**
Date: November 3, 2026
Friction: pr-precheck found three problems in my own draft pull request.
Change: I added missing Deviations, corrected my commit scope, and rewrote my description in my own words.
Result: The second review was accepted, and CI passed all five jobs.

**Beat 5**
Date: November 17, 2026
Friction: issue-scout's search results were flooded by repositories opening multiple issues at once.
Change: I added date filters and a one-result-per-repository ranking rule.
Result: The first scan returned five different repositories.

**Beat 6**
Date: November 18, 2026
Friction: A Turkish issue passed issue-scout even though I only wanted English-language issues.
Change: I added an English-only requirement to my profile and a non-ASCII title filter.
Result: The filter removed 7/100 results from Q1 and 9/100 from Q2, including the Turkish issue.

**Beat 7**
Date: November 18, 2026
Friction: The maintainer of issue #162 clarified that AI contributions were not accepted, even though the contribution-policy check had passed.
Change: I added an AI disclosure to my next claim on issue #390.
Result: I claimed #390 with disclosure. The maintainer has replied and accepted it.

## Limitations and What's Next

Making these tools helped me realize that a rubric can be useful even if it's imperfect. Just because an evaluation passes does not indicate every conceivable case has been covered. Some issues only show up when the tools are run on genuine issues and pull requests.

Next, I want to focus on enhancing how the tools handle circumstances that are not explicitly defined by the current rules. I would also like to test them on other examples and not rely too much on one evaluation. The aim is to improve the reliability of the tools, without violating the standards.

**Tool limits.**

issue-scout: The rubric still has four documented deficiencies that I noticed but never implemented: unlinked PRs, issues already fixed, missing size test, and false rejects. The contribution policy check can also pass if a repository doesn't say anything about its AI policy. I would like to improve how the tool handles murky donation rules, and check if an issue is still worth pursuing.

repro-check: The control-run check will not capture a made-up control result if someone reports it without actually running it. I also noted that certain evaluation results changed across runs without any changes to the checks. I'd learn more and mitigate such volatility with more testing.

pr-precheck: The rubric was evaluated perfectly but never stress tested by an evaluation miss. It found three serious flaws in my own pull request, but I still need to try it with other cases to see what it might miss.

All in all, I learned from this process that creating a tool is about more than just defining rules and passing the test. It also means using the tool, paying attention to where it fails and being honest about what actually changed and what still needs work.

