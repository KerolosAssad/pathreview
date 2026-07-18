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