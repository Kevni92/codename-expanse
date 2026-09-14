# Technical Delivery Cycle

## Purpose
Defines the canonical Codex workflow after an approved gameplay concept has been created in ChatGPT.

## Upstream handoff
Gameplay concepts are authored in ChatGPT and stored under `docs/concepts/`.

Codex starts from an approved concept. It does not repeat the gameplay concept stage in the normal workflow.

Overall project flow:

`Gameplay Idea → ChatGPT Concept → Approved Concept → Codex Technical Architecture → Issues → Implementation → Review → Fixes → QA`

## Sequence

### 0. Validate gameplay concept
Owner: Orchestrator

Input: approved `docs/concepts/<topic>.md`.

Gate:
- concept exists and is linked to related gameplay concepts;
- intended player/system behaviour is explicit;
- acceptance criteria exist;
- no implementation-blocking gameplay question remains unresolved.

If this gate fails, return the gap to the ChatGPT/game-design stage. Do not invent product behaviour in technical architecture.

### 1. Technical architecture
Agent: `technical_architect`

Input: approved gameplay concept plus existing architecture/ADRs.
Output: `docs/architecture/<topic>.md` using the architecture template, plus ADRs when a durable cross-cutting decision is introduced.

Gate: implementation-critical choices are explicit, including algorithms, formulas, units, data structures, interfaces, configuration/data ownership, performance constraints and tests. The architecture must preserve the approved gameplay behaviour.

### 2. Planning
Agent: `planner`

Input: approved gameplay concept and technical architecture.
Output: ordered GitHub Issues following `.github/ISSUE_TEMPLATE/implementation.md`.

Gate: each issue is independently understandable, narrowly scoped, linked to normative docs and implementable without architecture or gameplay invention.

### 3. Implementation
Agent: `implementer`

Input: exactly one issue and its linked normative documents.
Output: code/data/tests and a pull request.

Gate: issue acceptance criteria and required checks pass.

### 4. Review
Agent: `code_reviewer`

Input: pull request, linked issue and normative documentation.
Output: structured review findings.

Gate: all blocker/high findings are resolved or explicitly rejected through a justified specification change.

### 5. Fix cycle
Agent: `implementer`

Input: accepted review findings.
Output: fixes and regression tests where appropriate.

Repeat review if changes are substantial or findings remain.

### 6. QA
Agent: `qa_verifier`

Input: final pull request state, issue and docs.
Output: verification report.

Gate: acceptance criteria, regression coverage and required CI checks pass.

### 7. Merge / delivery
Only merge when requested/authorized. After merge to `main`, the normal project pipeline should publish the browser build to GitHub Pages once CI/deployment is configured.

## Boundary rule
If Codex discovers that a technical solution requires changing intended gameplay, it must surface that conflict instead of silently modifying `docs/concepts/**`. Gameplay changes return to the ChatGPT concept workflow.

## Test policy
Prefer fast unit tests, then focused integration tests. Add Playwright only for high-value browser journeys that cannot be covered cheaply below E2E level.

## Data policy
Gameplay and other tunable values belong in validated JSON/config files. TypeScript implements behaviour and schemas; it must not become the hidden balance database.