# Workflow: Concept Development

## Goal
Produce a coherent, handbook-quality gameplay/system concept through deliberate exploration, structured decisions and consistency checks.

This workflow is the compact repository workflow. ChatGPT sessions must also follow [`../../chatgpt/CONCEPT_SESSION_WORKFLOW.md`](../../chatgpt/CONCEPT_SESSION_WORKFLOW.md).

## Steps
1. **Load context.** Read [`../../AGENTS.md`](../../AGENTS.md), [`../../chatgpt/CONCEPT_WRITER_CONTEXT.md`](../../chatgpt/CONCEPT_WRITER_CONTEXT.md), project vision, concept index, related concepts and the concept template.
2. **Frame the design problem.** Establish purpose, player value, scope, non-scope and likely system ownership.
3. **Extract known decisions.** Separate established facts, current-session decisions, assumptions and unresolved questions.
4. **Explore the design space.** Evaluate the idea against project vision, related concepts, player value, depth/complexity, learnability and systemic interaction.
5. **Challenge weak/conflicting ideas.** Explain concrete concerns and propose better alternatives rather than agreeing automatically.
6. **Resolve major choices.** Use small structured question rounds, normally 2–5 related questions at a time. Offer materially distinct options and recommendations where useful.
7. **Define the normative model.** Establish terminology, player-facing behaviour, rules/invariants, parameters, states/transitions, interactions, feedback requirements and edge cases.
8. **Record rationale.** Capture important design decisions and serious rejected/deferred alternatives.
9. **Run a consistency review.** Check contradictions, duplicated ownership, terminology, hidden assumptions, unnecessary complexity and missing player feedback.
10. **Recap decisions.** Summarize major decisions, rejected/deferred alternatives, remaining open questions and cross-document changes before finalizing.
11. **Create/update the concept.** Use [`../../docs/templates/concept.md`](../../docs/templates/concept.md) and relative Markdown links.
12. **Update the handbook index.** Add/update the entry in [`../../docs/concepts/README.md`](../../docs/concepts/README.md).
13. **Set status correctly.** Leave status as `Draft` or `Review` until explicitly approved by the project owner.
14. **Approval gate.** Mark `Approved` only when no implementation-blocking gameplay question remains and the project owner explicitly approves the concept.
15. **Handoff.** Once approved, the next normal stage is Codex technical architecture. Do not automatically continue into technical implementation design.

## Completion gate
The concept must read as one chapter of a larger game-design handbook and be understandable without reading source code.

It is ready for Codex only if a Technical Architect can derive an implementation design without inventing missing gameplay rules.
