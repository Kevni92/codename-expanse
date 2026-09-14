# Codename Expanse – Project Agent Context

## Purpose
Codename Expanse is a high-quality browser-first prototype for a modern 2D top-down space simulation. The prototype must run fully in the browser. A later server architecture is expected, but no server is required for the initial prototype.

## Product Direction
The game combines readable arcade controls with a physically grounded simulation. Core themes include large-scale star systems, inertial flight, optional flight assists and autopilot, modular ships with visible hardpoints, long-range combat, layered parallax rendering, stations, NPCs, targeting of ships and subsystems, and a compact HUD.

## Workspace Responsibility Split
The project intentionally separates gameplay/product design from technical delivery.

### ChatGPT owns gameplay/product design
ChatGPT is the primary environment for:
- gameplay ideation and discussion;
- detailed final-game system rules under `docs/concepts/**`;
- cross-concept player capabilities under `docs/features/**`;
- delivery/validation scopes under `docs/milestones/**`;
- gameplay ownership boundaries, edge cases and acceptance criteria;
- identification of missing concepts exposed by feature or milestone planning.

The Concept Writer role is the main design role used in ChatGPT and follows the repository workflows for Concepts, Features and Milestones.

### Codex owns technical delivery
Codex starts from an implementation-ready Milestone backed by approved Features and Concepts and owns:
- technical architecture under `docs/architecture/**`;
- ADRs;
- implementation planning and GitHub Issues;
- implementation;
- pull-request review and review fixes;
- QA verification.

Codex must not silently alter approved gameplay behaviour. If a technical conflict requires a gameplay change, return the issue to the owning Concept.

Canonical project flow:

`Gameplay/Product Idea -> Concepts -> Features -> Milestones -> Codex Technical Architecture -> Issues -> Implementation -> Review -> Fixes -> QA`

## Documentation Layer Ownership

### Concepts
`docs/concepts/**` is the normative final-game gameplay handbook.

A Concept owns how a game system works in detail. Temporary prototype or milestone scope must not be encoded as alternative concept behaviour.

### Features
`docs/features/**` composes multiple Concepts into a coherent player-facing capability.

A Feature explains how concept-owned behaviours interact. It must not invent or override gameplay rules that belong to Concepts.

A Feature may identify missing Concepts. Missing required Concepts are created as `Planned` stubs and remain blockers until designed and approved.

### Milestones
`docs/milestones/**` composes multiple Features into a concrete delivery and validation target.

A Milestone may require only a subset of an otherwise larger Feature, but this only changes delivery scope. It does not modify the Feature or final-game Concepts.

A Milestone may be approved as a scope definition while `Implementation Readiness` is still `Blocked`.

## Technology Baseline
- TypeScript is mandatory for production code.
- Vite is the default browser build tool unless an approved ADR changes it.
- Vue is the preferred application/UI framework unless an approved ADR changes it.
- Vitest is the default unit/integration test runner.
- Playwright is used for a deliberately small set of high-value end-to-end smoke tests.
- The prototype is client-only.

## Architectural Principles
1. Simulation and rendering are strictly separated.
2. The simulation state is the source of truth; visual state must not become gameplay state.
3. Gameplay, balance, ship, weapon, module, station, world-generation and tunable simulation values must be data-driven.
4. Tunable values must not be hidden as magic numbers in TypeScript source files.
5. Static game content is stored in dedicated JSON data files and validated against typed schemas at load/build time.
6. Application/runtime settings belong in explicit configuration files.
7. Mathematical constants intrinsic to an algorithm are allowed in code; balance/configuration values are not.
8. Systems should be deterministic where practical and testable without a browser.
9. Physics/simulation should use a fixed simulation timestep where specified by architecture.
10. UI components must not own gameplay logic.
11. Avoid unnecessary dependencies and abstractions.
12. Performance is a first-class requirement, especially for simulation, rendering and large world coordinates.
13. The browser prototype must not make a later authoritative server architecture unnecessarily difficult.

## Documentation Is Normative
Project documentation is part of the specification, not optional prose.

Authority is separated by concern rather than by one global priority stack:

1. **Final gameplay behaviour:** the owning Approved Concept is authoritative.
2. **Cross-concept capability composition:** the owning Approved Feature is authoritative only for composition and handoffs and may not contradict Concepts.
3. **Delivery scope:** the owning Approved Milestone is authoritative for that delivery and may not contradict Features or Concepts.
4. **Technical implementation:** approved Architecture and ADRs are authoritative for technical decisions inside the product constraints above.
5. **Implementation work:** GitHub Issues and code must satisfy the owning higher-level documents.

An Architecture document or ADR may not silently override final-game behaviour defined by an Approved Concept. If gameplay must change, update the Concept explicitly.

## Documentation Rules
- Every Concept, Feature, Milestone and Architecture document must use its repository template.
- Every substantial document must contain a table of contents.
- Related documents must be linked using relative Markdown links.
- When referring to another defined system/capability, link to the relevant document and heading when useful.
- Documents must declare status and version.
- `Planned` means deliberately incomplete and non-normative.
- Approved documents may only be changed through an explicit update in the owning layer.
- A gameplay rule must have one Concept owner; Features compose it and Milestones scope it.
- Do not leave implementation-critical gameplay decisions for the Implementer to invent.

## Missing Concept Rule
When Feature or Milestone planning reveals a required game system that has no Concept:

1. create a stable concept title and ownership purpose;
2. create `docs/concepts/<topic>.md` using `docs/templates/concept-stub.md`;
3. set `Status: Planned` and `Version: 0.0`;
4. update `docs/concepts/README.md`;
5. link it from the requiring Feature;
6. do not put guessed gameplay rules in the stub.

The Concept must later go through the normal structured design process before it can be Approved.

## Data-Driven Rule
All values expected to be changed without changing program behaviour belong outside production TypeScript where practical.

Examples:
- ship mass, hull, thrust, hardpoints
- weapon damage, projectile speed, range, energy cost, cooldown
- module attributes
- rendering quality parameters
- camera tuning
- simulation tuning
- generation parameters

Preferred locations:
- `src/data/**` for game content and balance data
- `src/config/**` for application/system configuration
- `src/schemas/**` for TypeScript schemas and validation definitions

## Testing Strategy
Testing must be comprehensive but fast.

Order of preference:
1. Unit tests for pure logic, mathematics, simulation and data validation.
2. Focused integration tests for interactions between systems.
3. A small Playwright suite for critical browser user journeys only.

Do not duplicate large numbers of unit-level assertions in Playwright. Browser tests are intentionally scarce because CI speed matters.

Every implementation issue must state its required tests. Bug fixes should normally add a regression test at the lowest practical level.

## CI and Delivery
Every pull request should be able to run:
- TypeScript type checking
- linting
- data/schema validation
- unit tests
- focused integration tests
- production build
- limited Playwright smoke tests when relevant

After merge to `main`, the current production build should be deployable to GitHub Pages so the prototype can be inspected in-browser.

## Orchestrator
`agents/orchestrator.md` defines the canonical coordinator for Codex multi-stage technical work. When the user asks for the complete Codex workflow, orchestration, or explicitly asks to use the Orchestrator, the active parent agent should coordinate specialist roles instead of collapsing the whole task into one undifferentiated implementation pass.

When real subagents are supported, use the named specialist agents configured under `.codex/agents/`. Dependent stages must run in workflow order and wait for their prerequisites. Independent work may run in parallel.

Canonical Codex workflow: `agents/workflows/full-development-cycle.md`.

## Required Development Workflow
### Gameplay/product stage – ChatGPT
1. **Concept Writer** develops detailed final-game Concepts with the user.
2. Required Concepts are explicitly approved.
3. **Feature design** composes multiple Concepts and resolves cross-concept ownership/handoffs.
4. Required Features are explicitly approved.
5. **Milestone design** groups multiple Features/feature slices into a delivery target and evaluates implementation readiness.
6. The Milestone is handed to Codex only when `Implementation Readiness: Ready` unless the user explicitly requests an earlier technical exploration.

### Technical stage – Codex
7. **Orchestrator** validates the Milestone, Features and Concepts and delegates downstream work.
8. **Technical Architect** turns the approved requirements into an implementable technical specification.
9. **Planner** creates small, explicit GitHub Issues from approved specifications.
10. **Implementer** implements exactly the scoped Issue and opens/updates a pull request.
11. **Code Reviewer** reviews the pull request against Issue, Milestone, Features, Concepts, Architecture, ADRs and project rules.
12. **Implementer** fixes actionable review findings.
13. **QA / Verifier** verifies acceptance criteria and relevant regression behaviour.
14. Merge only when the specification and quality gates are satisfied and merging is requested/authorized.

## Agent Behaviour
- Read this file before acting.
- Read the role file under `agents/` for the current task.
- Read the relevant workflow.
- Follow linked Concepts, Features, Milestones, Architecture documents and ADRs before making assumptions.
- Do not silently broaden scope.
- Do not invent architecture where an approved specification exists.
- Do not silently invent or alter gameplay behaviour in Codex.
- If a specification is incomplete, identify the gap rather than burying a new design decision inside code.
- Prefer small, reviewable changes.
- If a runtime claims to support named subagents but the named role cannot actually be loaded, report the fallback instead of pretending the requested agent was spawned.
