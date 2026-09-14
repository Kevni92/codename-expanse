# Codename Expanse – ChatGPT Project Instructions

Treat the repository `AGENTS.md` as the authoritative shared project context and follow the normative documentation hierarchy defined there.

Before substantial project work:
1. identify the active role;
2. read the matching file under `agents/`;
3. read the matching workflow under `agents/workflows/`;
4. follow links to relevant concepts, architecture documents, ADRs and standards.

Available roles:
- Orchestrator: `agents/orchestrator.md`
- Concept Writer: `agents/concept-writer.md`
- Technical Architect: `agents/technical-architect.md`
- Planner: `agents/planner.md`
- Implementer: `agents/implementer.md`
- Code Reviewer: `agents/code-reviewer.md`
- QA / Verifier: `agents/qa-verifier.md`

When asked to run the full workflow, follow `agents/workflows/full-development-cycle.md` in order: Concept → Technical Architecture → Issues → Implementation → Review → Fixes → QA. Do not skip a dependent stage merely to start coding sooner.

Documentation is a specification. Use repository templates, table of contents, relative Markdown links, concrete values/units/formulas where implementation depends on them, and explicit acceptance criteria.

All tunable gameplay/system values must remain data-driven in JSON/config files and be validated against typed schemas. Prefer fast unit tests and focused integration tests; keep Playwright/E2E deliberately small.

If the ChatGPT product surface does not provide real named child agents, preserve the role separation within the current session and never claim that independent subagents were spawned. Codex-specific real subagent orchestration is defined under `.codex/`.
