# Codename Expanse – Concept Session Workflow

## Purpose
This workflow defines the mandatory structure for each ChatGPT Concept-development session. It prevents arbitrary concept writing and ensures that each gameplay Concept is deliberately explored before becoming normative final-game documentation.

Concepts are the detailed gameplay foundation of the hierarchy:

`Concepts -> Features -> Milestones`

A Concept must describe how the final game system should work, not what one prototype or Milestone happens to implement first.

## Session outcome
A session may end in one of these states:

- **Planned** — only a dependency stub exists; detailed design has not started.
- **Exploration/Draft** — the idea is being shaped and documented but is not normative.
- **Review** — the Concept is believed complete enough for review but is not final.
- **Approved** — the project owner explicitly approved a complete final-game Concept.

Do not force every session to end with an Approved Concept.

## Planned dependency stubs
A Concept may first appear because Feature or Milestone planning identified a missing gameplay owner.

Such a file uses `docs/templates/concept-stub.md`, status `Planned` and version `0.0`.

The stub may record only:
- stable title;
- intended ownership boundary;
- why the Concept is required;
- already-known neighboring documents.

It must not invent detailed gameplay rules.

When active Concept design begins, expand/replace the stub using `docs/templates/concept.md` and move to `Draft`.

## Phase 0 – Load context
Before discussing the Concept:

1. read `AGENTS.md`;
2. read `chatgpt/PROJECT_INSTRUCTIONS.md`;
3. read `chatgpt/CONCEPT_WRITER_CONTEXT.md`;
4. read `agents/concept-writer.md`;
5. read `docs/README.md`;
6. read relevant `docs/vision/**`;
7. read `docs/concepts/README.md` and relevant existing Concepts;
8. read Features/Milestones that require or interact with this Concept;
9. read `docs/templates/concept.md`.

Identify existing constraints, terminology, ownership boundaries and why this Concept is needed.

## Phase 1 – Frame the Concept
Establish the design problem before detailed mechanics.

Clarify:
- What system does this Concept own?
- Why should it exist in the final game?
- What player fantasy/value should it create?
- What is explicitly outside its scope?
- Which existing Concepts interact with it?
- Which Features depend on it?

## Phase 2 – Extract existing intent
Summarize:
- established project facts;
- explicit user decisions;
- reasonable but unconfirmed assumptions;
- missing gameplay decisions.

Do not ask the user to repeat information already available.

## Phase 3 – Explore the design space
For important mechanics:
1. explain intended gameplay effect;
2. identify benefits;
3. identify risks/conflicts;
4. propose alternatives where useful;
5. recommend a direction where justified.

Challenge mechanics that add complexity without corresponding player value or undermine approved design pillars.

## Phase 4 – Structured question rounds
Resolve missing decisions through small groups, normally 2–5 related questions.

For material choices:
- explain why the answer matters;
- present meaningful alternatives;
- recommend a default when one direction clearly fits better.

Do not ask all possible questions at once.

## Phase 5 – Define the normative model
Once key decisions are sufficiently clear, define:
- terminology;
- player-visible behaviour;
- rules and invariants;
- states/transitions;
- design-level parameters and initial values;
- interactions and ownership boundaries;
- player feedback/information;
- edge-case behaviour.

Rules must be precise enough that readers do not derive incompatible gameplay behaviour.

## Phase 6 – Consistency review
Check:
- contradictions with Vision or Approved Concepts;
- duplicated ownership;
- rules that belong to another Concept;
- inconsistent terminology;
- unexplained exceptions;
- unnecessary complexity;
- missing feedback;
- parameters with unclear meaning/units;
- hidden assumptions;
- unresolved decisions that downstream work would need to invent.

Also verify that the Concept is not encoding a temporary Milestone limitation as permanent final-game behaviour.

## Phase 7 – Decision recap
Before repository output, recap:
- major decisions;
- rejected/deferred alternatives;
- remaining open questions;
- related Concepts/Features that must be linked or updated.

## Phase 8 – Create or update the Concept
Use `docs/templates/concept.md` as the structural baseline.

Requirements:
- complete table of contents;
- relative links;
- stable numbered rule identifiers;
- concrete units for numeric design parameters;
- rationale for major choices;
- rejected/deferred alternatives where relevant;
- explicit open questions;
- concept-level acceptance criteria;
- change log;
- truthful status.

Update `docs/concepts/README.md` whenever a Concept is created, renamed or reclassified.

Update requiring Features when the Concept status or ownership meaningfully changes.

## Phase 9 – Approval gate
A Concept may be marked `Approved` only when the user explicitly approves it and:
- purpose/scope/ownership are clear;
- rules are internally coherent;
- important parameters are defined at design level;
- related Concepts are linked;
- no implementation-blocking gameplay question remains;
- acceptance criteria are meaningful;
- downstream Feature composition can reference it without inventing behaviour.

## Phase 10 – Next design layer
An Approved Concept is a normative building block for Features.

The normal next design step is to create/update the relevant `docs/features/**` document and ensure the Concept is integrated into the Feature interaction model.

The normal technical handoff occurs later:

`Approved Concepts -> Approved Features -> Approved/Ready Milestone -> Codex Technical Architecture`

Do not automatically continue into technical architecture unless the user explicitly asks for an exception.

## Anti-patterns
Do not:
- turn the first user message directly into a final Concept;
- agree with every idea without evaluating it;
- interrogate the user with a giant questionnaire;
- bury unresolved choices inside polished prose;
- invent implementation architecture to make the Concept appear complete;
- duplicate rules from another Concept;
- encode temporary Milestone scope as permanent final-game behaviour;
- add mechanics merely because they sound realistic or sophisticated;
- optimize for documentation volume over design clarity;
- mark a Concept Approved without explicit user approval.
