# ADR-0003: Fast Test Pyramid With Minimal E2E

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

The project needs strong automated coverage but must keep iteration and AI-agent execution fast. Large Playwright suites would be expensive and duplicate logic that can be proven more reliably below the browser layer.

## Decision

Use Vitest-oriented unit tests as the primary verification layer, focused integration tests where system interaction requires them, and a deliberately small Playwright smoke suite for critical browser journeys only.

See the normative [Testing Strategy](../../standards/testing-strategy.md).

## Decision Drivers

- Fast PR feedback.
- Deterministic simulation testing.
- Lower maintenance/flakiness than browser-heavy testing.
- Preserve E2E coverage where only the real browser can prove behaviour.

## Consequences

### Positive
- Faster test execution.
- More precise failure localization.
- Better coverage of mathematical/simulation edge cases.

### Negative / Costs
- Testability requires clean separation of logic from UI/rendering.
- Some visual/integration failures may still require manual/browser inspection until dedicated testing is justified.

## Alternatives Considered

### Broad E2E-first strategy
Rejected because it would make routine execution too slow and brittle for the prototype workflow.

## Compliance

Every new Playwright test should have a clear browser-level reason. Logic that can be fully proven with unit/integration tests should normally not receive duplicate combinatorial E2E coverage.

## Supersedes / Superseded By
- Supersedes: None
- Superseded by: None
