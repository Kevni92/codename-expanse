# Workflow: Pull Request Review

## Goal
Produce a specification-based, actionable review.

## Steps
1. Read [`../../AGENTS.md`](../../AGENTS.md), Reviewer role, PR and linked Issue.
2. Read all normative documents linked by the Issue/PR.
3. Inspect the complete diff, not only the PR summary.
4. Verify scope and every acceptance criterion.
5. Verify ADR and architecture compliance.
6. Verify player/system behaviour against concepts.
7. Check data-driven/configuration rules and schema validation.
8. Check correctness, units, coordinate spaces, timing and edge cases.
9. Evaluate tests according to the test pyramid.
10. Check obvious performance/regression risks.
11. Write findings in the required severity/action format.
12. Distinguish required fixes from suggestions.
13. End with APPROVE, REQUEST CHANGES or COMMENT ONLY.

## Completion gate
Every requested change explains exactly what is wrong, what requirement it violates, how to fix it and how to verify the fix where applicable.
