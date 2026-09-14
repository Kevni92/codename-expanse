# Codename Expanse – Feature and Milestone Workflow

## Purpose

This workflow defines how ChatGPT must work with the project owner when the requested design target is a **Feature** or a **Milestone** rather than a single gameplay concept.

The documentation hierarchy is strict:

`Concepts -> Features -> Milestones`

- **Concepts** are the detailed, normative definition of how the final game works.
- **Features** compose multiple concepts into a coherent player-facing capability and explain how those concepts interact.
- **Milestones** compose multiple features into a concrete delivery and validation target.

Neither Features nor Milestones may silently become alternate gameplay specifications.

## Source Ownership Rule

Gameplay behaviour has one normative owner under `docs/concepts/**`.

A Feature may describe how approved concept rules hand off to one another, but it may not invent or override a rule owned by a concept.

A Milestone may select a subset of feature capabilities for delivery, but it may not change the feature or the concepts merely to reduce scope.

If Feature/Milestone work exposes a missing gameplay rule, stop treating that rule as Feature/Milestone content and identify the concept that must own it.

## Feature Session Workflow

When the user asks to create, refine, analyze or review a Feature:

### Phase F0 – Load context

Read:

1. `docs/features/README.md`;
2. `docs/templates/feature.md`;
3. `docs/concepts/README.md`;
4. every existing concept relevant to the capability;
5. every existing feature that overlaps materially;
6. relevant vision documents.

### Phase F1 – Frame the capability

Establish:

- what coherent capability the player gains;
- why the capability deserves one Feature boundary;
- what is outside that Feature;
- which neighboring Features may exist.

A Feature should normally require multiple concepts. Do not create artificial Features that are merely aliases for a single concept.

### Phase F2 – Build the concept dependency map

Identify all concepts required to realize the Feature.

For each concept, classify it as:

- **Approved** — usable normative source;
- **Review/Draft** — exists but is not final;
- **Planned** — dependency identified but not yet designed;
- **Missing** — no concept document exists yet.

For every **Missing** required concept:

1. determine a stable concept title and intended ownership boundary;
2. create `docs/concepts/<topic>.md` from `docs/templates/concept-stub.md`;
3. set status to `Planned`;
4. update `docs/concepts/README.md`;
5. link the stub from the Feature.

Do not fill the stub with guessed gameplay rules.

### Phase F3 – Discuss composition and interactions

Work through how the concepts produce the player capability end-to-end.

Discuss:

- responsibility handoffs;
- state/data/intent passed conceptually between systems;
- cross-concept player flows;
- cross-concept failure or edge cases;
- which concept owns each gameplay rule required by the interaction.

When an interaction exposes a rule that is absent from all concepts, record it as a concept gap and identify the owning concept. Do not settle detailed gameplay behaviour only in the Feature document.

### Phase F4 – Resolve Feature structure

Define:

- purpose;
- player capability;
- scope/non-scope;
- required concepts;
- feature composition;
- interaction flows;
- ownership boundaries;
- missing concept gaps;
- feature-level acceptance criteria.

### Phase F5 – Completion gate

A Feature cannot be `Approved` while a required concept is `Planned`, `Draft` or `Review`.

A Feature is complete only when every required concept is `Approved`, interaction ownership is resolved, the Feature contains no orphaned gameplay rule, and the project owner explicitly approves it.

## Milestone Session Workflow

When the user asks to create, refine, analyze or review a Milestone:

### Phase M0 – Load context

Read:

1. `docs/milestones/README.md`;
2. `docs/templates/milestone.md`;
3. `docs/features/README.md`;
4. all Features relevant to the requested delivery target;
5. the concepts required by the included Feature slices;
6. relevant vision documents.

### Phase M1 – Frame the delivery target

Establish:

- what this milestone is meant to prove or validate;
- why the included capabilities belong in one delivery step;
- what end-to-end player experience must be playable;
- what is explicitly not required yet.

### Phase M2 – Identify multiple Features

A Milestone composes multiple Features.

Identify the Feature set required for the milestone. Do not manufacture artificial Features merely to satisfy a count; if the requested scope is genuinely only one Feature, say that the scope is currently a Feature slice rather than a fully composed Milestone and identify which additional player-facing capability is actually required for the intended validation loop.

If a required Feature does not exist, create a Feature document in `Planned` state using `docs/templates/feature.md`, add it to `docs/features/README.md`, and continue its concept dependency analysis.

### Phase M3 – Define Feature slices

For each included Feature, define exactly which already-specified capabilities are required in this milestone and which are deferred.

A Milestone may intentionally deliver only part of a Feature. Deferral changes delivery scope, not final-game design.

### Phase M4 – Dependency and gap analysis

Trace every required Feature slice to its required concepts.

Missing concept documents are created as `Planned` stubs through the Feature workflow. Incomplete concepts and unresolved Feature interactions remain explicit blockers.

Do not invent gameplay behaviour in order to make the Milestone appear implementation-ready.

### Phase M5 – Define validation and exclusions

Define:

- milestone validation goal;
- included Features;
- required Feature slices;
- explicit exclusions/deferred capabilities;
- dependency/readiness matrix;
- known blockers;
- milestone-level acceptance criteria.

### Phase M6 – Readiness gate

A Milestone may be approved as a scope definition while still being blocked, but `Implementation Readiness` may be `Ready` only when:

- all included Feature documents exist;
- required gameplay concepts for the milestone slices are `Approved`;
- required cross-concept interactions are resolved in Feature documents;
- no gameplay decisions are left for Codex;
- the project owner has approved the Milestone scope.

## Discussion Behaviour

For both Feature and Milestone sessions:

- discuss in the user's language;
- use small structured question rounds for material decisions;
- challenge weak boundaries and artificial decomposition;
- do not ask the user to repeat information already present in repository context;
- distinguish established, decided, proposed and open items;
- create dependency stubs only when a missing concept/feature is genuinely required;
- do not prematurely produce technical architecture or implementation details.

## Normal Handoff

The normal design-to-delivery chain is:

`Approved Concepts -> Approved Features -> Approved/Ready Milestone -> Codex Technical Architecture -> Issues -> Implementation -> Review -> QA`

Concepts remain the normative gameplay source throughout the downstream workflow. Features and Milestones provide composition and delivery scope, not permission to contradict them.
