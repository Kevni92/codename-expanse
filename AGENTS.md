# Codename Expanse – Project Agent Context

## Purpose
Codename Expanse is a high-quality browser-first prototype for a modern 2D top-down space simulation. The prototype must run fully in the browser. A later server architecture is expected, but no server is required for the initial prototype.

## Product Direction
The game combines readable arcade controls with a physically grounded simulation. Core themes include large-scale star systems, inertial flight, optional flight assists and autopilot, modular ships with visible hardpoints, long-range combat, layered parallax rendering, stations, NPCs, targeting of ships and subsystems, and a compact HUD.

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
The project documentation is part of the specification, not optional prose.

Priority when sources conflict:
1. Approved ADRs
2. Approved architecture documents
3. Approved concept documents
4. GitHub Issue requirements
5. Implementation details

If an implementation conflicts with an approved higher-priority document, the implementation is considered incorrect unless the document is updated through the normal design process.

## Documentation Rules
- Every concept and architecture document must use its repository template.
- Every substantial document must contain a table of contents.
- Related documents must be linked using relative Markdown links.
- When referring to another defined system, link to the relevant document and, when useful, directly to its heading.
- Documents must declare status and version.
- Approved documents may only be contradicted by an explicit update or ADR.
- Concrete formulas, units, ranges, defaults, constraints and edge cases belong in architecture documents when they are required for implementation.
- Do not leave implementation-critical decisions for the Implementer to invent.

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

## Required Development Workflow
1. **Concept Writer** defines player-facing/system behaviour.
2. **Technical Architect** turns approved concepts into an implementable technical specification.
3. **Planner** creates small, explicit GitHub Issues from approved specifications.
4. **Implementer** implements exactly the scoped Issue and opens/updates a pull request.
5. **Code Reviewer** reviews the pull request against Issue, concepts, architecture, ADRs and project rules.
6. **Implementer** fixes actionable review findings.
7. **QA / Verifier** verifies acceptance criteria and relevant regression behaviour.
8. Merge only when the specification and quality gates are satisfied.

## Agent Behaviour
- Read this file before acting.
- Read the role file under `agents/` for the current task.
- Read the relevant workflow under `agents/workflows/`.
- Follow linked concepts, architecture documents and ADRs before making assumptions.
- Do not silently broaden scope.
- Do not invent architecture where an approved specification exists.
- If a specification is incomplete, identify the gap rather than burying a new design decision inside code.
- Prefer small, reviewable changes.
