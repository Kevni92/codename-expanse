# Workflow: Concept Development

## Goal
Produce a coherent, handbook-quality gameplay/system Concept through deliberate exploration, structured decisions and consistency checks.

A Concept defines detailed final-game behaviour and is the normative gameplay foundation for downstream Features and Milestones.

ChatGPT sessions must also follow [`../../chatgpt/CONCEPT_SESSION_WORKFLOW.md`](../../chatgpt/CONCEPT_SESSION_WORKFLOW.md).

## Documentation chain

`Concepts -> Features -> Milestones -> Technical Architecture`

Concept work must not contain Milestone-specific shortcuts or implementation architecture.

## Steps
1. **Load context.** Read [`../../AGENTS.md`](../../AGENTS.md), [`../../chatgpt/CONCEPT_WRITER_CONTEXT.md`](../../chatgpt/CONCEPT_WRITER_CONTEXT.md), project Vision, Concept index, related Concepts, requiring Features/Milestones and the Concept template.
2. **Handle Planned stubs.** If the Concept began as a `Planned` dependency stub, preserve its dependency rationale but replace/expand it into the normal Concept structure when active design begins.
3. **Frame the design problem.** Establish purpose, player value, scope, non-scope and system ownership for the final game.
4. **Extract known decisions.** Separate established facts, current-session decisions, assumptions and unresolved questions.
5. **Explore the design space.** Evaluate the idea against project Vision, related Concepts, player value, depth/complexity, learnability and systemic interaction.
6. **Challenge weak/conflicting ideas.** Explain concrete concerns and propose better alternatives rather than agreeing automatically.
7. **Resolve major choices.** Use small structured question rounds, normally 2–5 related questions at a time.
8. **Define the normative model.** Establish terminology, player-facing behaviour, rules/invariants, parameters, states/transitions, interactions, feedback requirements and edge cases.
9. **Record rationale.** Capture important decisions and serious rejected/deferred alternatives.
10. **Run a consistency review.** Check contradictions, duplicated ownership, terminology, hidden assumptions, unnecessary complexity, missing player feedback and accidental Milestone-specific rules.
11. **Recap decisions.** Summarize major decisions, rejected/deferred alternatives, remaining open questions and cross-document changes.
12. **Create/update the Concept.** Use [`../../docs/templates/concept.md`](../../docs/templates/concept.md) and relative Markdown links.
13. **Update the Concept index.** Add/update the entry in [`../../docs/concepts/README.md`](../../docs/concepts/README.md).
14. **Update dependent Features.** Repair links/status/dependency information in relevant `docs/features/**` documents when the Concept meaningfully changes their dependency state.
15. **Set status correctly.** Leave status as `Draft` or `Review` until explicitly approved by the project owner.
16. **Approval gate.** Mark `Approved` only when no implementation-blocking gameplay question remains and the project owner explicitly approves the Concept.
17. **Move to composition.** Approved Concepts become building blocks for Feature design. Do not skip directly to implementation unless the user explicitly requests an exception.

## Completion gate
The Concept must read as one chapter of the final game-design handbook and be understandable without reading source code.

It is ready to be consumed by Features only if Feature composition will not need to invent missing gameplay rules.

The normal technical handoff occurs later:

`Approved Concepts -> Approved Features -> Approved/Ready Milestone -> Codex`
