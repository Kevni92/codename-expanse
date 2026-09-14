# Workflow: QA Verification

## Goal
Verify the final implementation against observable acceptance criteria.

## Steps
1. Read [`../../AGENTS.md`](../../AGENTS.md), QA role, Issue, PR and review history.
2. Build a checklist from the Issue acceptance criteria.
3. Map existing automated test evidence to each criterion.
4. Run/inspect unit and integration coverage for deterministic behaviour.
5. Use the minimal Playwright/browser checks required for cross-layer behaviour.
6. Verify named edge cases and regressions.
7. Verify data/config schema behaviour where changed.
8. Record PASS / FAIL / NOT VERIFIED per criterion.
9. Separate implementation defects from specification gaps.
10. Give READY TO MERGE or NOT READY recommendation.
