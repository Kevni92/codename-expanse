# Codename Expanse

Browser-first 2D top-down space simulation prototype.

> **Status:** Early design / prototype preparation

## Project handbook

The project specification and development handbook starts at [`docs/README.md`](docs/README.md).

All AI-assisted development must read [`AGENTS.md`](AGENTS.md) first and then the relevant role and workflow under [`agents/`](agents/).

## Development workflow

Concept → Technical Architecture → GitHub Issues → Implementation → Pull Request Review → QA → Merge

## Current technical baseline

- Browser-only prototype
- TypeScript
- Vite
- Vue for application/UI
- Vitest for fast unit and integration tests
- Small Playwright smoke-test suite
- Data-driven gameplay/configuration
- GitHub Pages deployment after merges to `main` once the executable prototype scaffold exists
