# ChatGPT Project Setup – Game Design

ChatGPT is the collaborative game-design workspace for Codename Expanse.

The design handbook uses three deliberate layers:

`Concepts -> Features -> Milestones`

- **Concepts** define detailed final-game gameplay/system behaviour.
- **Features** compose multiple Concepts into coherent player-facing capabilities and explain their interactions.
- **Milestones** compose multiple Features into concrete delivery/validation scopes.

The normal Codex technical workflow begins only after the relevant Milestone is approved and `Implementation Readiness` is `Ready`.

## Files to use as project context
The ChatGPT Project should have repository access. At minimum, ensure these files are available as project sources.

### Always-relevant context
- `AGENTS.md`
- `chatgpt/PROJECT_INSTRUCTIONS.md`
- `chatgpt/PROJECT_MEMORY.md`
- `chatgpt/CONCEPT_WRITER_CONTEXT.md`
- `chatgpt/CONCEPT_SESSION_WORKFLOW.md`
- `chatgpt/FEATURE_MILESTONE_WORKFLOW.md`
- `agents/concept-writer.md`
- `agents/workflows/concept-development.md`
- `docs/README.md`
- `docs/vision/**`
- `docs/concepts/README.md`
- `docs/features/README.md`
- `docs/milestones/README.md`
- `docs/templates/concept.md`
- `docs/templates/concept-stub.md`
- `docs/templates/feature.md`
- `docs/templates/milestone.md`

### Dynamic context
- all Approved Concepts relevant to the current topic;
- any Draft/Review/Planned Concept directly related to the current topic;
- relevant Feature documents;
- relevant Milestone documents.

## Project bootstrap
The preferred static project source is `chatgpt/PROJECT_BOOTSTRAP.md`.

That bootstrap instructs ChatGPT to reload the current repository-backed rules and workflows at the start of design sessions so repository changes take effect without maintaining a large static prompt.

## Starting a Concept session
State the game system you want to design and any initial intent.

ChatGPT should follow `chatgpt/CONCEPT_SESSION_WORKFLOW.md`, design the intended final-game behaviour in detail and avoid temporary Milestone shortcuts.

## Starting a Feature session
State the coherent player-facing capability you want to compose.

ChatGPT should follow `chatgpt/FEATURE_MILESTONE_WORKFLOW.md` and work through:

1. player capability and boundary;
2. required multiple Concepts;
3. how those Concepts interact;
4. ownership/handoffs;
5. missing Concept dependencies;
6. cross-concept edge cases;
7. Feature acceptance criteria and completion blockers.

If a required Concept is missing, ChatGPT creates a `Planned` Concept stub and adds it to the Concept index rather than inventing gameplay rules inside the Feature.

## Starting a Milestone session
State what playable development step you want to deliver or validate.

ChatGPT should follow `chatgpt/FEATURE_MILESTONE_WORKFLOW.md` and work through:

1. delivery/validation goal;
2. the multiple Features required;
3. required capability slice from each Feature;
4. explicit deferred/out-of-scope capabilities;
5. dependency/readiness status;
6. missing Feature/Concept documents;
7. Milestone acceptance criteria;
8. blockers before Codex handoff.

A Milestone may exist while dependencies are incomplete. It remains `Implementation Readiness: Blocked` until Codex can proceed without inventing gameplay/product behaviour.

## Planned dependency documents
A Feature or Milestone may identify a required game system before its detailed Concept has been designed.

Create such a dependency with `docs/templates/concept-stub.md`:

- Status: `Planned`
- Version: `0.0`
- only title, intended ownership, dependency reason and known boundaries
- no invented gameplay rules

Later Concept work expands the stub through the normal workflow.

## Expected design behaviour
The design agent should:

1. load current repository context;
2. identify the correct documentation layer;
3. frame purpose/scope before detailed writing;
4. summarize established decisions and assumptions;
5. challenge weak/conflicting ideas;
6. resolve material decisions through small structured question rounds;
7. preserve one gameplay-rule owner under Concepts;
8. create dependency stubs where genuinely required;
9. run consistency/readiness checks;
10. update the correct document and index only when sufficiently defined.

## Repository results
Depending on the session type:

- Concept: `docs/concepts/<topic>.md` + Concept index
- Feature: `docs/features/<topic>.md` + Feature index
- Milestone: `docs/milestones/mNN-<topic>.md` + Milestone index

## Handoff boundary
The normal handoff is:

`Approved Concepts -> Approved Features -> Approved/Ready Milestone -> Codex Orchestrator`

Codex then owns:

`Technical Architecture -> Issues -> Implementation -> Review -> Fixes -> QA`

If Codex discovers a gameplay rule gap, it returns to a Concept. If it discovers a cross-concept capability gap, it returns to a Feature. If delivery scope is unclear, it returns to the Milestone.
