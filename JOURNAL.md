## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/151

**Issue title:** Bias detector patterns are too narrow to match common phrasings

**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**
This is a safety issue: the bias detector in bias_detector.py uses regex patterns that require near-exact wording, so it misses common natural phrasings of the same bias (dismissive educational-background language; age-based assumptions). The fix needs to broaden the patterns to catch these variations while preserving the detector's intent: flagging genuine bias without over-triggering on neutral text. Success means the 9 currently failing unit tests pass without breaking the 23 that already pass, and that the patterns generalize to catch similarly-phrased bias, not just the exact wording used in the 9 test cases.

**Selection reasoning:**
I chose Tier 1 because, while I've navigated large codebases and fixed
issues before, this is my first time doing so in this kind of simulated
open-source workflow: an actively maintained repo I didn't build, with no
prior context on its structure or conventions, following a PR-based
contribution process. I worked through the "Is this right for me?"
checklist: reproduced the bug locally and confirmed it matches the issue
description, located and read bias_detector.py and its test file
end-to-end, and traced how the current patterns fail against several of the
9 failing tests, for example missing plural word forms and requiring a
fixed word order. I confirmed the fix is scoped to a single file with 9
failing tests that specify the expected behavior. Comment count on the
issue was low with no linked PRs, so collision risk is low, and the
estimated 3–6 hour Tier 1 scope fits comfortably within the Week 8–9
window. I also chose this issue because it fits skills I recently acquired,
and because regex and automated bias detection in text sounded like
interesting topics to explore further in future projects.

**Branch name:** fix/151-bias-detector-narrow-patterns

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger

## Week 8 — Reproduction & solution planning

**Reproduction commit link:** https://github.com/KerolosAssad/pathreview/commit/483621f

**Reproduction summary:**
I ran the exact snippet from the issue description directly in Python and got the same output, (False, ""), confirming the described bug. I then ran the scoped test file (tests/unit/test_bias_detector.py) and the full make test-unit suite, both confirming the same 9 failing tests noted in the issue.

**PLAN.md link:** https://github.com/KerolosAssad/pathreview/blob/fix/151-bias-detector-narrow-patterns/PLAN.md

**Walkthrough video (recommended):** [Loom walkthrough](https://www.loom.com/share/3cbb505daa5d4c10b130428ccba47223)

**Blockers or open questions:**
No blockers, but some of the original designers' intentions are unknown, and the exact way certain patterns should be structured to fix the issue is still uncertain.

## Week 9 — Solution building & PR submission

### Check-in 1 (mid-week)

**Current progress:**
Completed all sub-tasks from PLAN.md for issue #151. Widened DISMISSIVE_PATTERNS and DEMOGRAPHIC_PATTERNS to cover the 9 originally-failing tests (noun/verb form gaps, missing plural forms, word-order variation in the self-taught/university comparison, and a new causal "means" construction). Also fixed two clause-split phrasings quoted directly in the issue's own reproduction steps ("bootcamp... so this project lacks..." and "their age... they likely cannot..."), which weren't covered by the 9 tests alone. While testing the clause-split fix with adversarial inputs, found and fixed a real false-positive risk (an unbounded regex wildcard that could bridge across unrelated sentences), backed by new edge-case tests. Updated PLAN.md's Risks & Unknowns section to document what was confirmed during implementation, including a negation/reported-speech false-positive limitation that was deliberately left unaddressed (documented as a known limitation for the PR).

**Next steps:**
Push the branch, open a draft PR with the template filled in, self-review it, and finalize Check-in 2 with the PR link.

**Blockers:**
None.

---

### Check-in 2 (end of week)

**PR link:** [link to your submitted pull request]

**Branch:** fix/151-bias-detector-narrow-patterns

**What you built:**
[1–3 sentences summarizing what your fix does and how it works]

**Tests added or updated:**
[Which test files did you touch? What do they cover?]

**Self-review confirmation:** [ ] make check passes  [ ] make test-unit passes

**Draft PR feedback received from:** [name or Slack handle, or "none"]