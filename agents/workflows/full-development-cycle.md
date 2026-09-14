# Technical Delivery Cycle

## Purpose
Defines the canonical Codex workflow after ChatGPT has completed the required design hierarchy for a delivery target.

## Upstream handoff
Game/product design is authored in ChatGPT as:

`Concepts -> Features -> Milestones`

Codex normally starts from an **Approved Milestone** whose **Implementation Readiness is `Ready`**.

The Milestone links the Feature slices to be delivered. Those Features link the Approved Concepts that define final gameplay behaviour.

Overall project flow:

`Gameplay/Product Idea -> Concepts -> Features -> Approved/Ready Milestone -> Codex Technical Architecture -> Issues -> Implementation -> Review -> Fixes -> QA`

## Sequence

### 0. Validate design handoff
Owner: Orchestrator

Input:
- approved `docs/milestones/<milestone>.md` with `Implementation Readiness: Ready`;
- all included Feature documents required by the Milestone;
- all Approved Concepts required by those Feature slices.

Gate:
- Milestone goal and Feature slices are explicit;
- Milestone exclusions/deferred capabilities are explicit;
- required Features exist and their cross-concept interactions are resolved;
- every gameplay Concept required by the selected Feature slices is Approved;
- no implementation-blocking gameplay/product question remains unresolved.

If this gate fails, return the gap to the correct ChatGPT design layer:
- gameplay rule gap -> Concept;
- cross-concept capability/handoff gap -> Feature;
- delivery/scope gap -> Milestone.

Do not invent product behaviour in technical architecture.

### 1. Technical architecture
Agent: `technical_architect`

Input: target Milestone, included Feature slices, required Approved Concepts, plus existing Architecture/ADRs.

Output: one or more `docs/architecture/<topic>.md` documents using the Architecture template, plus ADRs when a durable cross-cutting technical decision is introduced.

Gate: implementation-critical choices are explicit, including algorithms, formulas, units, data structures, interfaces, configuration/data ownership, performance constraints and tests. Architecture must preserve Concept gameplay rules, Feature composition and Milestone scope.

### 2. Planning
Agent: `planner`

Input: Milestone, Features, Concepts and approved technical Architecture.

Output: ordered GitHub Issues following `.github/ISSUE_TEMPLATE/implementation.md`.

Gate: each Issue is independently understandable, narrowly scoped, linked to its normative/scoping documents and implementable without architecture or gameplay invention.

### 3. Implementation
Agent: `implementer`

Input: exactly one Issue and its linked Milestone/Feature/Concept/Architecture documents.

Output: code/data/tests and a pull request.

Gate: Issue acceptance criteria and required checks pass without exceeding the selected Milestone scope.

### 4. Review
Agent: `code_reviewer`

Input: pull request, linked Issue and design/technical documentation.

Output: structured review findings.

Gate: all blocker/high findings are resolved or explicitly rejected through a justified specification change in the correct owning layer.

### 5. Fix cycle
Agent: `implementer`

Input: accepted review findings.

Output: fixes and regression tests where appropriate.

Repeat review if changes are substantial or findings remain.

### 6. QA
Agent: `qa_verifier`

Input: final pull request state, Issue, target Milestone and linked documents.

Output: verification report.

Gate: relevant Milestone/Issue acceptance criteria, regression coverage and required CI checks pass.

### 7. Merge / delivery
Only merge when requested/authorized. After merge to `main`, the normal project pipeline should publish the browser build to GitHub Pages once CI/deployment is configured.

## Boundary rule
Codex must respect the layer that owns each requirement:

- Concept = final gameplay behaviour;
- Feature = capability composition/handoffs;
- Milestone = current delivery scope;
- Architecture/ADR = technical implementation.

If a technical solution requires changing gameplay, it must surface that conflict instead of silently modifying Concepts.

If implementation reveals an unresolved Feature handoff or Milestone scope gap, return it to ChatGPT rather than burying a design decision inside code.

## Test policy
Prefer fast unit tests, then focused integration tests. Add Playwright only for high-value browser journeys that cannot be covered cheaply below E2E level.

## Data policy
Gameplay and other tunable values belong in validated JSON/config files. TypeScript implements behaviour and schemas; it must not become the hidden balance database.
