# Full Development Cycle

## Purpose
Defines the canonical end-to-end workflow for a feature or system in Codename Expanse.

## Sequence

### 1. Concept
Agent: `concept_writer`

Input: user requirement, existing concepts and vision.
Output: `docs/concepts/<topic>.md` using the concept template.
Gate: behaviour, scope, links, edge cases and acceptance criteria are explicit.

### 2. Technical architecture
Agent: `technical_architect`

Input: approved concept plus existing architecture/ADRs.
Output: `docs/architecture/<topic>.md` using the architecture template, plus ADRs when a durable cross-cutting decision is introduced.
Gate: implementation-critical choices are explicit, including algorithms, formulas, units, data structures, configuration/data ownership, performance constraints and tests.

### 3. Planning
Agent: `planner`

Input: approved concept and architecture.
Output: ordered GitHub Issues following `.github/ISSUE_TEMPLATE/implementation.md`.
Gate: each issue is independently understandable, narrowly scoped, linked to normative docs and implementable without architecture invention.

### 4. Implementation
Agent: `implementer`

Input: exactly one issue and its linked normative documents.
Output: code/data/tests and a pull request.
Gate: issue acceptance criteria and required checks pass.

### 5. Review
Agent: `code_reviewer`

Input: pull request, linked issue and normative documentation.
Output: structured review findings.
Gate: all blocker/high findings are resolved or explicitly rejected with a justified specification change.

### 6. Fix cycle
Agent: `implementer`

Input: accepted review findings.
Output: fixes and regression tests where appropriate.
Repeat review if changes are substantial or findings remain.

### 7. QA
Agent: `qa_verifier`

Input: final pull request state, issue and docs.
Output: verification report.
Gate: acceptance criteria, regression coverage and required CI checks pass.

### 8. Merge / delivery
Only merge when requested/authorized. After merge to `main`, the normal project pipeline should publish the browser build to GitHub Pages once CI/deployment is configured.

## Test policy
Prefer fast unit tests, then focused integration tests. Add Playwright only for high-value browser journeys that cannot be covered cheaply below E2E level.

## Data policy
Gameplay and other tunable values belong in validated JSON/config files. TypeScript implements behaviour and schemas; it must not become the hidden balance database.
