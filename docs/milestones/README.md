# Milestone Index and Rules

Milestones are delivery scopes composed from multiple features.

A milestone defines what combination of player-facing capabilities should be delivered and validated together at a specific stage of development. It does not redefine how the game works. Gameplay truth remains in concepts, and cross-concept capability composition remains in features.

## What a Milestone Is

A milestone:

- combines multiple feature documents into a coherent delivery target;
- defines the purpose and validation goal of that delivery target;
- states which parts of each included feature are required for the milestone;
- explicitly records what is deferred or out of scope;
- identifies concept and feature dependencies that block implementation readiness;
- defines milestone-level success criteria;
- provides the scope contract that can later be handed to Codex for technical planning and implementation.

## What a Milestone Is Not

A milestone is **not**:

- a gameplay concept;
- a place to define final-game rules, formulas, values or system behaviour;
- a substitute for a feature document;
- a technical architecture specification;
- a collection of implementation details or source-code tasks;
- permission to simplify or contradict an approved concept unless the concept itself is explicitly changed.

A milestone may implement only a subset of an approved feature, but that does not change the full feature or the underlying concepts. The milestone simply states which capabilities are required now and which are deferred.

## Relationship to Features and Concepts

The documentation direction is:

`Concepts -> Features -> Milestones`

- **Concepts** define how the final game works in detail.
- **Features** explain how multiple concepts work together to create a coherent capability.
- **Milestones** group multiple features into a concrete delivery and validation scope.

A milestone may be planned before every included feature or concept is complete. Missing dependencies are allowed during planning, but they must remain explicit blockers rather than being silently invented in the milestone.

If milestone planning exposes a missing feature, create a feature document in `Planned` status and continue decomposition there.

If feature or milestone planning exposes a missing gameplay concept, create a `Planned` concept stub under [`../concepts/`](../concepts/) using [`../templates/concept-stub.md`](../templates/concept-stub.md) and add it to the concept index.

## Milestone Readiness Gate

A milestone may exist in `Planned`, `Draft` or `Review` state while dependencies remain incomplete.

A milestone is ready for normal Codex technical handoff only when:

- its delivery goal and success criteria are explicit;
- all included features exist and their required milestone slices are clear;
- every gameplay concept required by those feature slices is `Approved`;
- cross-concept interactions required by the milestone are resolved in the relevant feature documents;
- no milestone requirement requires Codex to invent gameplay behaviour;
- milestone exclusions and deferred capabilities are explicit;
- the project owner has approved the milestone scope.

A milestone can therefore be structurally well defined while still being marked as blocked by unfinished features or concepts.

## Milestone Discussion Workflow

When ChatGPT is asked to design or review a milestone, it should discuss:

1. the milestone's development and validation goal;
2. the multiple features that must be combined to achieve that goal;
3. the exact capability slice required from each feature;
4. explicit exclusions and deferred feature capabilities;
5. dependency status of the included features and concepts;
6. missing feature or concept documents that need to be created;
7. milestone-level success criteria observable in the playable product;
8. readiness blockers before Codex handoff.

Milestone discussion should focus on delivery composition and validation, not detailed gameplay design.

## Status Model

Milestone documents use the repository documentation status model:

- **Planned** — identified delivery target; dependencies and scope may still be incomplete;
- **Draft** — actively being defined;
- **Review** — believed coherent enough for scope review;
- **Approved** — scope explicitly approved by the project owner; implementation readiness is still evaluated separately against the readiness gate;
- **Deprecated** — retained for history but no longer intended for delivery;
- **Superseded** — replaced by a named newer milestone.

Milestone documents also declare **Implementation Readiness**:

- **Blocked** — one or more required feature/concept dependencies are incomplete or unresolved;
- **Ready** — the readiness gate is satisfied and Codex can begin the normal technical workflow without inventing gameplay decisions.

## Milestone Documents

- [M01 – Flight Sandbox](m01-flight-sandbox.md) — **Draft** / **Blocked** — first executable flight sandbox validating manual inertial flight, Flight Assist, Autopilot travel and celestial/orbital context with minimal presentation.

When adding a milestone:

1. use [`../templates/milestone.md`](../templates/milestone.md);
2. place it in this directory using a stable ordered filename such as `m01-flight-sandbox.md`;
3. add it to this index;
4. link all included features using relative links;
5. record dependency blockers explicitly;
6. never define gameplay rules that belong to concepts or feature composition that belongs to feature documents.
