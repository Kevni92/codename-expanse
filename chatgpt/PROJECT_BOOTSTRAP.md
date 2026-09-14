# Codename Expanse – ChatGPT Project Bootstrap

## Repository
Authoritative repository:

https://github.com/Kevni92/codename-expanse

Default branch: `main`

## Purpose
This file is the only static bootstrap context that needs to be stored in the ChatGPT Project. All detailed project rules, design-agent behaviour, workflows, templates, vision documents, concepts, features and milestones must be loaded from the repository so changes made in GitHub are picked up automatically.

Do not treat an older uploaded copy of a repository document as authoritative when the current `main` branch is accessible.

## Mandatory session startup
Before substantial gameplay/design work, load the current versions from the repository in this order:

1. `AGENTS.md`
2. `chatgpt/PROJECT_INSTRUCTIONS.md`
3. `chatgpt/PROJECT_MEMORY.md`
4. `chatgpt/CONCEPT_WRITER_CONTEXT.md`
5. `chatgpt/CONCEPT_SESSION_WORKFLOW.md`
6. `chatgpt/FEATURE_MILESTONE_WORKFLOW.md`
7. `agents/concept-writer.md`
8. `agents/workflows/concept-development.md`
9. `docs/README.md`
10. `docs/vision/**` relevant to the current topic
11. `docs/concepts/README.md`
12. `docs/features/README.md`
13. `docs/milestones/README.md`
14. existing Concepts, Features and Milestones relevant to the current topic
15. the applicable template under `docs/templates/`

Follow relative links from these documents whenever they point to additional normative context relevant to the active work.

## Freshness rule
Always read these files from the current `main` branch at the beginning of a new Concept, Feature or Milestone design session. Do not assume that repository content remembered from an earlier ChatGPT session is still current.

If a repository file changes during the current session and the change is relevant to the active work, reload the affected file before continuing.

## Documentation hierarchy
The project separates final-game rules, capability composition and delivery scope:

`Concepts -> Features -> Milestones`

- `docs/concepts/**` defines detailed, normative final-game behaviour.
- `docs/features/**` composes multiple Concepts into coherent player-facing capabilities and explains how those Concepts interact.
- `docs/milestones/**` composes multiple Features into concrete delivery and validation scopes.

Features and Milestones must never silently redefine gameplay rules owned by Concepts.

## Workflow selection
When the user asks about a **Concept**, follow `chatgpt/CONCEPT_SESSION_WORKFLOW.md`.

When the user asks about a **Feature** or **Milestone**, follow `chatgpt/FEATURE_MILESTONE_WORKFLOW.md`.

Do not immediately turn the user's first description into a final document. Explore boundaries, dependencies, interactions and missing ownership through structured discussion.

## Missing dependency rule
Feature and Milestone planning may legitimately reveal gameplay Concepts that do not exist yet.

When a required Concept is missing:

1. determine its stable title and intended ownership boundary;
2. create `docs/concepts/<topic>.md` using `docs/templates/concept-stub.md`;
3. mark it `Planned` / version `0.0`;
4. add it to `docs/concepts/README.md`;
5. link it from the requiring Feature;
6. leave detailed gameplay behaviour for a later normal Concept session.

A Planned Concept stub is intentionally incomplete and non-normative.

## Repository output
Use the document type that matches the user's request:

- Concept: `docs/concepts/<topic>.md`
- Feature: `docs/features/<topic>.md`
- Milestone: `docs/milestones/mNN-<topic>.md`

Update the corresponding README/index whenever a document is created, renamed or materially reclassified.

## Approval and readiness
Concepts, Features and Milestones must remain below `Approved` until explicitly approved by the project owner.

A Feature cannot be Approved while a required Concept is not Approved.

A Milestone may have approved scope while still declaring `Implementation Readiness: Blocked`. It becomes `Ready` only when the required Feature slices resolve to Approved Concepts and no gameplay behaviour is left for Codex to invent.

## Boundary to Codex
The normal downstream handoff is:

`Approved Concepts -> Approved Features -> Approved/Ready Milestone -> Technical Architecture -> Issues -> Implementation -> Review -> Fixes -> QA`

Concepts remain the normative gameplay source throughout downstream work. Features define composition; Milestones define delivery scope; Codex defines technical implementation.

Do not silently continue into technical architecture or implementation unless the user explicitly asks for an exception.

## Repository access failure
If the repository or required files cannot be accessed in the current session, say so clearly before doing normative design work. Do not pretend to have loaded current repository context and do not silently rely on potentially stale remembered copies.
