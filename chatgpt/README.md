# ChatGPT Project Setup

ChatGPT is the gameplay/game-design workspace for Codename Expanse. Codex is the downstream technical execution environment.

## Responsibility split

### ChatGPT
- gameplay ideation and discussion
- gameplay/system concepts
- concept handbook structure and cross-linking
- player-facing rules, edge cases and acceptance criteria
- approval-ready files under `docs/concepts/`

### Codex
- technical architecture derived from approved concepts
- ADRs when required
- GitHub issue planning
- implementation
- pull-request review and review fixes
- QA verification

The normal handoff is:

`Idea → ChatGPT Gameplay Concept → Approved Concept → Codex Technical Architecture → Issues → Implementation → Review → QA`

## Setup
1. Create a ChatGPT Project named `Codename Expanse`.
2. Paste `chatgpt/PROJECT_INSTRUCTIONS.md` into the project instructions.
3. Add the GitHub repository as a project source when available, or provide the relevant repository documents.
4. Make at least these files available: `AGENTS.md`, `agents/concept-writer.md`, `agents/workflows/concept-development.md`, `docs/README.md`, `docs/templates/concept.md`, `docs/vision/**` and `docs/concepts/**`.

## Usage
Normal request:

`Lass uns das Gameplay-Konzept für <Thema> ausarbeiten.`

ChatGPT should then use the Concept Writer rules automatically and produce/update the corresponding concept document.

Once the concept is approved, hand it to Codex. The Codex Orchestrator begins with technical architecture; it does not repeat or replace the gameplay concept stage.