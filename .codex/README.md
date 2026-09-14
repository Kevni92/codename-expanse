# Codex Multi-Agent Setup

This directory contains project-scoped custom Codex agents and the role registry used by the Orchestrator.

## Requirements
- Use a current Codex version. GPT-5.6 support in Codex requires at least Codex CLI 0.144.0; newer is recommended.
- Multi-agent support must be available/enabled in the running Codex environment.

## Roles
- `orchestrator` — GPT-5.6 Sol / high
- `concept_writer` — GPT-5.6 Sol / high
- `technical_architect` — GPT-5.6 Sol / high
- `planner` — GPT-5.6 Terra / high
- `implementer` — GPT-5.6 Luna / high
- `code_reviewer` — GPT-5.6 Sol / high, read-only
- `qa_verifier` — GPT-5.6 Terra / medium, read-only

This intentionally spends more reasoning capacity on concept, architecture and review, while implementation of already well-specified issues is delegated to Luna.

## Recommended usage
From the repository root, start Codex and ask the parent session to use/spawn `orchestrator` for a complete feature workflow, or invoke a specialist role directly for a bounded stage.

Example intent:
`Use the orchestrator for the complete workflow for inertial flight physics.`

The Orchestrator must use dependent stages sequentially and wait for each prerequisite. Independent research/checks may run in parallel.

## Notes
Codex custom-agent support has evolved quickly. If a specific client build fails to expose named project roles, update Codex first. As a fallback, the parent agent can still read the matching TOML/Markdown role instructions and spawn a generic subagent with those instructions, but it must report that fallback rather than pretending the named role loaded successfully.
