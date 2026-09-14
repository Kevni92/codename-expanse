# ChatGPT Project Setup

ChatGPT Projects provide shared project instructions, files/sources and project context. They do not use repository-local `.codex/agents/*.toml` files as a native named-subagent registry.

## Setup
1. Create a ChatGPT Project named `Codename Expanse`.
2. Paste the contents of `chatgpt/PROJECT_INSTRUCTIONS.md` into the project's instructions.
3. Add this GitHub repository or upload the relevant repository documents as project sources.
4. Ensure at minimum these files are available as sources: `AGENTS.md`, `agents/*.md`, `agents/workflows/*.md`, `docs/README.md`, `docs/templates/*`, approved concepts, architecture documents and ADRs.

## Usage
For normal design work, ask for the relevant role explicitly, e.g. `Arbeite als Concept Writer ...`.

For the complete process, start with: `Arbeite als Orchestrator und führe den vollständigen Workflow für <Thema> aus.`

Within a normal ChatGPT Project this coordinates the same role boundaries and artifacts, but it must not pretend that separate native child agents were spawned when the current ChatGPT surface does not expose them. Real named subagent spawning is configured separately for Codex under `.codex/`.
