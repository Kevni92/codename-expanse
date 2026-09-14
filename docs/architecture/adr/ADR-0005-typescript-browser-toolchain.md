# ADR-0005: TypeScript Browser Toolchain Baseline

**Status:** Accepted  
**Date:** 2026-09-14  
**Decision Owners:** Project Owner / Technical Architecture

## Table of Contents

1. [Context](#context)
2. [Decision](#decision)
3. [Decision Drivers](#decision-drivers)
4. [Consequences](#consequences)
5. [Alternatives Considered](#alternatives-considered)
6. [Compliance](#compliance)
7. [Supersedes / Superseded By](#supersedes--superseded-by)

## Context

The prototype needs a modern strongly typed browser development baseline that supports fast iteration, testability and static GitHub Pages delivery.

## Decision

Production application code uses TypeScript. Vite is the build/development baseline and Vue is the application/UI framework baseline. Vitest is the default unit/integration runner and Playwright is the E2E tool.

A future rendering engine/library decision is intentionally not made by this ADR and requires separate architecture evaluation if needed.

## Decision Drivers

- Strong typing for data-heavy simulation code.
- Fast browser development/build loop.
- Mature Vue/Vite ecosystem.
- Straightforward static deployment.
- Vitest compatibility with Vite/TypeScript.

## Consequences

### Positive
- Unified typed application codebase.
- Fast development feedback.
- Simple static production build.

### Negative / Costs
- Framework/toolchain migrations require an explicit decision.
- Simulation code must remain framework-independent despite Vue being used for application/UI.

## Alternatives Considered

Alternative frontend/build stacks may be reconsidered only through an ADR when they provide a material project benefit.

## Compliance

New production application code is TypeScript unless an explicit tool/config file convention requires another format. Core simulation/domain logic must not depend on Vue component lifecycle.

## Supersedes / Superseded By
- Supersedes: None
- Superseded by: None
