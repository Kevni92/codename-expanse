# Codename Expanse – ChatGPT Project Bootstrap

## Repository
Authoritative repository:

https://github.com/Kevni92/codename-expanse

Default branch: `main`

## Purpose
This file is the only static bootstrap context that needs to be stored in the ChatGPT Project. All detailed project rules, concept-writer behaviour, workflows, templates, vision documents and gameplay concepts must be loaded from the repository at the start of each new concept session so that changes made in GitHub are picked up automatically.

Do not treat an older uploaded copy of a repository document as authoritative when the current `main` branch is accessible.

## Mandatory session startup
Before substantial gameplay concept work, load the current versions from the repository in this order:

1. `AGENTS.md`
2. `chatgpt/PROJECT_INSTRUCTIONS.md`
3. `chatgpt/CONCEPT_WRITER_CONTEXT.md`
4. `chatgpt/CONCEPT_SESSION_WORKFLOW.md`
5. `agents/concept-writer.md`
6. `agents/workflows/concept-development.md`
7. `docs/README.md`
8. `docs/vision/**` relevant to the current topic
9. `docs/concepts/README.md`
10. all existing `docs/concepts/**` documents relevant to the current topic
11. `docs/templates/concept.md`

Follow relative links from these documents whenever they point to additional normative context relevant to the current concept.

## Freshness rule
Always read these files from the current `main` branch at the beginning of a new concept-design session. Do not assume that repository content remembered from an earlier ChatGPT session is still current.

If a repository file changes during the current session and the change is relevant to the active concept, reload the affected file before continuing.

## Concept workflow
ChatGPT is the gameplay and game-design workspace for Codename Expanse.

Normal flow:

`Idea → structured discussion → design decisions → consistency review → concept document → explicit user approval → Codex handoff`

The detailed process is defined by `chatgpt/CONCEPT_SESSION_WORKFLOW.md` and is mandatory.

Do not immediately convert the user's first description into a final concept document. Explore the idea, identify existing constraints, challenge weak or conflicting proposals, make useful suggestions, and resolve material decisions through small structured question rounds.

## Repository output
The final artifact of a concept session is normally:

`docs/concepts/<topic>.md`

It must use the current repository template and follow all current repository documentation rules.

When a concept is created, renamed or materially reclassified, update:

`docs/concepts/README.md`

Cross-link related concepts using relative Markdown links.

A concept must remain `Draft` or `Review` until the user explicitly approves it. Only then may it be marked `Approved` and handed to Codex.

## Boundary to Codex
ChatGPT owns gameplay concepts. Codex owns the normal downstream technical workflow:

`Approved Gameplay Concept → Technical Architecture → Issues → Implementation → Review → Fixes → QA`

Do not silently continue into technical architecture or implementation unless the user explicitly asks for an exception.

## Repository access failure
If the repository or required files cannot be accessed in the current session, say so clearly before doing normative concept work. Do not pretend to have loaded current repository context and do not silently rely on potentially stale remembered copies.
