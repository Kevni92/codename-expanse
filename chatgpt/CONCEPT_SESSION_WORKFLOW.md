# Codename Expanse – Concept Session Workflow

## Purpose
This workflow defines the mandatory structure for each ChatGPT concept-development session. It prevents arbitrary concept writing and ensures that each gameplay concept is deliberately explored before becoming normative documentation.

## Session outcome
A session may end in one of three valid states:
- **Exploration:** the idea is still being shaped; no repository concept document is finalized.
- **Review:** the concept is coherent enough to draft, but still contains explicit open decisions.
- **Approved for handoff:** the concept is complete enough for Codex technical architecture.

Do not force every session to end with an Approved concept.

## Phase 0 – Load context
Before discussing the new concept:
1. read `AGENTS.md`;
2. read `chatgpt/CONCEPT_WRITER_CONTEXT.md`;
3. read `agents/concept-writer.md`;
4. read `docs/vision/**` relevant to the topic;
5. read the concept index and relevant existing concepts;
6. read `docs/templates/concept.md`.

Identify existing constraints, related systems, terminology and likely ownership boundaries.

## Phase 1 – Frame the concept
Establish the design problem before discussing detailed mechanics.

Clarify:
- What is the concept about?
- Why should it exist in the game?
- What player fantasy or gameplay value should it create?
- What system does it own?
- What is explicitly outside its scope?
- Which existing concepts does it interact with?

Output of this phase: a short working definition and scope boundary.

## Phase 2 – Extract existing intent
Summarize what the user has already decided or strongly implied.

Separate:
- established project facts;
- explicit user decisions;
- reasonable but unconfirmed assumptions;
- missing design decisions.

Do not ask the user to repeat information already available.

## Phase 3 – Explore the design space
Before locking rules, test the idea against the wider game.

For important mechanics:
1. explain the intended gameplay effect;
2. identify benefits;
3. identify risks or conflicts;
4. propose alternatives when useful;
5. recommend a direction where justified.

Challenge mechanics that add complexity without corresponding player value or that undermine previously established design pillars.

## Phase 4 – Structured question rounds
Resolve missing decisions through small question groups.

Each round should normally contain 2–5 related questions.

Preferred question format:

### Question
Short decision to make.

**Why it matters:** one concise explanation.

**Options:**
- A — meaningful option and consequence
- B — meaningful option and consequence
- C — only if genuinely distinct

**Recommendation:** preferred option and reason, when appropriate.

The user may answer freely; do not require rigid option letters.

Group questions by topic, for example:
- player interaction;
- rules and constraints;
- scale and timing;
- feedback/UI implications;
- interactions with other systems;
- failure/edge cases.

Do not ask all possible questions at once.

## Phase 5 – Define the normative model
Once the key decisions are sufficiently clear, formulate the concept's precise design model.

Define:
- terminology;
- player-visible behaviour;
- rules and invariants;
- states and transitions where relevant;
- design-level parameters and initial values;
- interactions and ownership boundaries;
- feedback and information the player receives;
- edge-case behaviour.

Rules should be deterministic enough that two readers do not derive incompatible gameplay behaviour from the same text.

## Phase 6 – Consistency review
Before drafting the final document, perform an explicit consistency pass.

Check:
- contradictions with vision or approved concepts;
- duplicated ownership;
- inconsistent terminology;
- unexplained exceptions;
- complexity that no longer serves gameplay;
- missing player feedback;
- parameters with no unit or meaning;
- hidden assumptions;
- unresolved decisions that would force Codex to invent gameplay.

Surface problems to the user before finalizing.

## Phase 7 – Decision recap
Before repository output, provide a concise recap of:
- major decisions;
- important rejected/deferred alternatives;
- remaining open questions;
- related concepts that must be linked or updated.

This recap is a final chance to catch misunderstandings.

## Phase 8 – Create or update the concept document
Use `docs/templates/concept.md` exactly as the structural baseline.

Requirements:
- complete table of contents;
- relative Markdown links;
- stable numbered rule identifiers;
- concrete units for numeric parameters;
- explicit design rationale for major choices;
- rejected/deferred alternatives where relevant;
- open questions clearly marked;
- concept-level acceptance criteria;
- change log entry;
- status `Draft` or `Review` unless the user explicitly approves it.

Update `docs/concepts/README.md` whenever a concept is created, renamed or materially reclassified.

## Phase 9 – Approval gate
A concept may be marked `Approved` only when the user explicitly approves it and all implementation-blocking gameplay decisions are resolved.

Before approval, verify:
- purpose and scope are clear;
- rules are internally coherent;
- important parameters are defined at the design level;
- related concepts are linked;
- no silent contradiction exists;
- no implementation-blocking open question remains;
- acceptance criteria are meaningful;
- Codex can start technical architecture without inventing product behaviour.

## Phase 10 – Handoff
Once approved, state that the concept is ready for Codex technical architecture.

The normal handoff target is:
`docs/concepts/<topic>.md`

Do not automatically continue into technical architecture unless explicitly requested.

## Anti-patterns
Do not:
- turn the first user message directly into a final concept;
- agree with every idea without evaluating it;
- interrogate the user with a huge questionnaire;
- bury unresolved choices inside polished prose;
- invent detailed technical implementation to make the concept look complete;
- duplicate rules from another concept instead of linking them;
- add mechanics merely because they sound realistic or sophisticated;
- optimize for documentation volume rather than design clarity;
- mark a concept Approved without explicit user approval.