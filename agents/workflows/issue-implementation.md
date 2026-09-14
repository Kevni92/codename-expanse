# Workflow: Issue Implementation

## Goal
Implement one scoped Issue and produce a reviewable pull request.

## Steps
1. Read [`../../AGENTS.md`](../../AGENTS.md), Implementer role and the complete Issue.
2. Follow all linked concepts, architecture documents and ADRs.
3. Inspect affected code/tests/data before editing.
4. Restate internally the acceptance criteria and non-scope.
5. Implement the smallest coherent change.
6. Put tunable values in data/config and validate them.
7. Add/adjust unit tests first where practical.
8. Add focused integration tests where system boundaries need coverage.
9. Add Playwright only when required and justified.
10. Run relevant fast checks continuously; run the full required project checks before completion.
11. Re-read the Issue and verify every acceptance criterion.
12. Create/update the pull request using the repository PR template.
13. Explicitly disclose specification gaps or deviations.

## Completion gate
The PR is self-contained, tested, within scope and traceable to its Issue/specification.
