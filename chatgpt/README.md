# ChatGPT Project Setup – Concept Design

ChatGPT is the collaborative game-design workspace for Codename Expanse. Its normal deliverable is a reviewed gameplay concept under `docs/concepts/`, ready to hand off to Codex.

## Files to use as project context
The ChatGPT Project should have access to the repository. At minimum, ensure these files are available as project sources:

### Always-relevant context
- `AGENTS.md`
- `chatgpt/PROJECT_INSTRUCTIONS.md`
- `chatgpt/CONCEPT_WRITER_CONTEXT.md`
- `chatgpt/CONCEPT_SESSION_WORKFLOW.md`
- `agents/concept-writer.md`
- `agents/workflows/concept-development.md`
- `docs/templates/concept.md`
- `docs/vision/**`
- `docs/concepts/README.md`

### Dynamic context
- all approved `docs/concepts/**` documents;
- any Draft/Review concept directly related to the current topic.

## Project instructions
Paste the contents of `chatgpt/PROJECT_INSTRUCTIONS.md` into the ChatGPT Project instructions.

The other files provide detailed working context and should be available to the project as sources.

## Starting a new concept session
A new session does not need a large bootstrap prompt. State the concept you want to work on and any initial idea or goal.

Example intent:

`Ich möchte heute das Gameplay-Konzept für Flight & Navigation ausarbeiten. Ausgangspunkt: ...`

ChatGPT should then follow the mandatory concept-session workflow instead of immediately writing the final Markdown document.

## Expected session behaviour
The Concept Writer should:
1. load existing context and related concepts;
2. frame the design problem and scope;
3. summarize existing decisions and assumptions;
4. discuss ideas with the user;
5. propose improvements where useful;
6. challenge conflicting or weak ideas with concrete reasoning;
7. resolve missing decisions through small structured question rounds;
8. define the normative gameplay model;
9. check consistency against the handbook;
10. recap decisions;
11. create/update the concept document when mature enough;
12. mark it Approved only after explicit user approval.

## Repository result
The normal output is:

`docs/concepts/<topic>.md`

and an updated:

`docs/concepts/README.md`

Related concept documents should be connected with relative Markdown links.

## Handoff boundary
Once a gameplay concept is approved, hand it to the Codex Orchestrator.

Codex then owns:

`Technical Architecture → Issues → Implementation → Review → Fixes → QA`

If Codex discovers a missing gameplay decision, that decision returns to ChatGPT instead of being invented in technical architecture.
