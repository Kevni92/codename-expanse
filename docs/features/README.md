# Feature Index and Rules

Features are player-facing or product-facing capabilities composed from multiple gameplay concepts.

A feature does **not** replace a concept and does **not** own the detailed rules of an individual gameplay system. Concepts remain the normative definition of how the final game behaves. A feature explains how several concepts combine into one coherent capability that the player can use or experience.

## What a Feature Is

A feature:

- represents a coherent player-facing capability or experience;
- is composed from multiple documents under [`../concepts/`](../concepts/);
- identifies which concepts participate and what role each concept has;
- explains how those concepts interact end-to-end to produce the feature;
- defines the feature boundary and the player-visible outcome of that composition;
- identifies missing concept ownership when the composition exposes a gameplay gap;
- provides feature-level acceptance criteria for the combined capability.

Examples of suitable feature scopes include space flight, ship fitting, space combat, navigation, station interaction or another capability that requires several gameplay systems to work together.

## What a Feature Is Not

A feature is **not**:

- a replacement for detailed gameplay concepts;
- a place to invent rules, formulas, values or edge-case behaviour that should belong to a concept;
- a milestone, release plan or implementation schedule;
- a technical architecture document;
- a GitHub Issue or implementation task;
- a temporary prototype specification that changes the intended final-game behaviour.

If a feature discussion discovers a new gameplay rule that is not owned by an existing concept, the rule must not be hidden inside the feature document. A concept owner must be identified or created.

## Relationship to Concepts

The ownership direction is:

`Concepts -> Feature`

Concepts define the final-game rules. Features compose those rules.

Feature documents may summarize an interaction for readability, but must link to the normative concept and must not maintain a competing definition.

A feature can be created before all required concepts are complete. When a required concept does not yet exist:

1. give the missing concept a stable title and ownership purpose;
2. create `../concepts/<topic>.md` using [`../templates/concept-stub.md`](../templates/concept-stub.md);
3. mark that concept `Planned`;
4. add it to [`../concepts/README.md`](../concepts/README.md);
5. link the planned concept from the feature;
6. record the feature as incomplete until the required concept has been fully developed and approved.

A `Planned` concept stub is a dependency marker, not a gameplay specification. Detailed rules must be developed through the normal concept workflow before approval.

## Feature Completion Gate

A feature may be discussed and documented while dependencies are incomplete, but it is only complete enough to be marked `Approved` when:

- every required concept exists;
- every required concept is `Approved`;
- the interaction between the concepts is explicitly described;
- every gameplay rule needed by those interactions has a clear concept owner;
- no gameplay gap is being silently resolved inside the feature document;
- feature-level acceptance criteria describe the combined player capability;
- the project owner explicitly approves the feature.

If a required concept is `Planned`, `Draft` or `Review`, the feature must remain below `Approved`.

## Feature Discussion Workflow

When ChatGPT is asked to design or review a feature, it should discuss:

1. the player capability and intended outcome;
2. feature scope and non-scope;
3. the concepts required to realize it;
4. how those concepts interact from the player's perspective;
5. ownership boundaries between the concepts;
6. missing concepts or missing concept rules exposed by the interaction;
7. feature-level edge cases that are actually cross-concept interactions;
8. completion blockers and acceptance criteria.

The discussion must not use the feature layer to bypass detailed concept design.

## Status Model

Feature documents use the repository documentation status model:

- **Planned** — identified but not yet sufficiently designed;
- **Draft** — actively being composed and discussed;
- **Review** — composition is believed complete enough for review;
- **Approved** — all required concepts are approved, interactions are resolved, and the project owner explicitly approved the feature;
- **Deprecated** — retained for history but should not drive new work;
- **Superseded** — replaced by a named newer feature.

## Feature Documents

No feature documents have been created yet.

When adding a feature:

1. use [`../templates/feature.md`](../templates/feature.md);
2. place it in this directory with a stable kebab-case filename;
3. add it to this index;
4. link every required concept using relative links;
5. create `Planned` concept stubs for missing required concepts;
6. keep the feature below `Approved` until the completion gate is satisfied.
