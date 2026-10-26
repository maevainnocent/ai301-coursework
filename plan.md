# Plan: issue #63, README scorer test fixture is too short for its own word-count assertion

Issue: https://github.com/codepath/pathreview-ai301-fa26-howard/issues/63
Repro I'm building on: https://github.com/codepath/pathreview-ai301-fa26-howard/issues/63#issuecomment-6350330362
Branch: `fix/63-readme-scorer-fixture-length`

## Cause

The scorer isn't wrong; the test's fixture is. `agent/tools/readme_scorer.py` counts words with `len(content.split())` and labels a README "minimal" under 100 words, "adequate" from 100 to 499, and "comprehensive" at 500+. The fixture in `test_readme_with_all_quality_signals` is only 51 words. My repro shows exactly that: with `--runxfail` the test fails on `assert 51 > 100`, and the scorer's own log line says `category=minimal ... word_count=51`.

The test's next assertion, `word_count_category == "comprehensive"`, needs 500+ words, so the fixture is short for both assertions, not just the first one. The test is named "all quality signals" and its docstring says it should return a high score, so it means for the README to be comprehensive. The separate tests `test_word_count_category_adequate` and `test_word_count_category_comprehensive` in the same file confirm the scorer's thresholds are the intended ones.

## Change

Extend the fixture so it is over 500 words while keeping every quality signal it already has (installation, usage, features, tech stack, badges, demo link), and delete the `@pytest.mark.xfail(strict=True, reason="issue #63: ...")` marker from that test, as CONTRIBUTING requires for seeded bugs.

- In: `tests/unit/test_readme_scorer.py`, only `test_readme_with_all_quality_signals`: add a prose section to its `readme` fixture, built with the same repetition idiom the file already uses (e.g. `"Content paragraph. " * 100` in `test_score_scales_with_word_count`), so the fixture reaches 500+ words; remove the xfail marker.
- Out: `agent/tools/readme_scorer.py` (the thresholds are correct and other tests pin them), the other tests in the file, and the assertions themselves. `> 100` still holds for a 500+ word fixture, so I'm not changing it.

## Test

1. Re-run my repro steps on the branch: `python -m pytest tests/unit/test_readme_scorer.py -q`. Before: `22 passed, 1 xfailed`. Expected after: `23 passed`, with no xfail and no `XPASS(strict)` failure.
2. `python -m pytest tests/unit/test_readme_scorer.py -q --runxfail` should also give `23 passed`. Before, it failed with `assert 51 > 100`.
3. Check the fixture's real count: the scorer's log line for that test should show `category=comprehensive` and `word_count` above 500 (visible with `-s` or on failure).
4. Run the rest of the unit tests (`python -m pytest tests/unit -q`) to make sure nothing else changed.

## Unknowns

- I haven't confirmed that the extra prose won't trip a section detector. For example, words like "install", "usage", or "example" in the new text would match the scorer's regexes. That wouldn't break this test, since all the signals are already present, but I'll keep the added prose neutral so the fixture still tests what it says.
- `overall_score > 0.7` passed with 51 words (score 0.87). More words should only raise the word-count component, but I'll confirm in step 1.
- I haven't run the repo's full `make check` (ruff/black/mypy) yet. I'll run at least ruff and black on the changed file before opening a PR.

## Deviations

The core change held: I only edited `tests/unit/test_readme_scorer.py`, added a neutral "About" paragraph to the fixture using the file's `"..." * N` repetition style, and removed the issue #63 xfail marker. The fixture now counts 533 words and the scorer labels it `comprehensive`. A few things went differently from what I planned:

- **Branch name.** Before posting the plan comment I changed the branch from `test/63-readme-scorer-fixture-length` to `fix/63-readme-scorer-fixture-length`, because the Path Review house rule says branches are named `fix/<issue-number>-<slug>`. The posted comment already uses the `fix/` name.
- **Running the rest of `tests/unit` (Test step 4).** My repro venv only had `pytest` and `structlog`, so the full unit run first stopped with 9 collection errors (missing modules like `numpy`, `sqlalchemy`, `jose`), the same on `main` and on my branch. I installed the missing packages from `pyproject.toml` into the venv. After that, `tests/unit` shows 6 failures in `tests/unit/test_review_service.py` both on `main` and on my branch (`6 failed, 369 passed, 53 xfailed` before vs `6 failed, 370 passed, 52 xfailed` after). They aren't from my change; they look like the async-mock problem tracked separately in issue #65. I didn't touch them, since that's out of scope.
- **`make check` (Unknowns).** I didn't run the full `make check`. I ran `ruff check` and `black --check` on the file I changed, and both passed. CI will run the rest when I open the PR.
- **Unknowns that turned out fine.** The added paragraph uses words that don't match any of the scorer's section regexes, and `overall_score` went from 0.87 to 1.0, so the `> 0.7` assertion still holds.
