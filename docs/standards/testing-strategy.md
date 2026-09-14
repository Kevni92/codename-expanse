# Testing Strategy

**Status:** Approved  
**Version:** 1.0  
**Last Updated:** 2026-09-14

## Table of Contents

1. [Purpose](#purpose)
2. [Test Pyramid](#test-pyramid)
3. [Unit Tests](#unit-tests)
4. [Integration Tests](#integration-tests)
5. [Playwright / E2E](#playwright--e2e)
6. [Performance and Speed](#performance-and-speed)
7. [Bug Fixes](#bug-fixes)
8. [CI Expectations](#ci-expectations)
9. [Review Checklist](#review-checklist)

## Purpose

Keep the suite comprehensive, deterministic and fast enough to run continuously during AI-assisted development and on pull requests.

This standard implements [ADR-0003](../architecture/adr/ADR-0003-fast-test-pyramid.md).

## Test Pyramid

Preferred order:

1. Unit tests
2. Focused integration tests
3. Minimal Playwright end-to-end smoke tests

A behaviour should be tested at the lowest layer that can prove it reliably.

## Unit Tests

Unit tests are the default for:
- vector/matrix/math helpers;
- simulation algorithms;
- physics calculations;
- state machines;
- combat calculations;
- targeting logic;
- autopilot logic;
- data/schema validation;
- deterministic procedural generation logic;
- pure configuration transformations.

Tests should prefer deterministic inputs and avoid browsers/timers/network when not needed.

## Integration Tests

Use focused integration tests when correctness depends on interaction between a small number of real subsystems, for example simulation command → state update → emitted event.

Do not turn integration tests into full browser scenarios merely because multiple modules are involved.

## Playwright / E2E

Playwright exists to prove a small number of high-value browser journeys, for example:
- application boots and renders the playable scene;
- selecting a target produces the expected target UI;
- a core ship-editor flow works end-to-end.

Rules:
- **TEST-001:** Do not mirror the unit test suite through the UI.
- **TEST-002:** Each Playwright test must justify why lower-level testing is insufficient.
- **TEST-003:** Prefer a small Chromium smoke suite in routine CI unless cross-browser coverage becomes a defined requirement.
- **TEST-004:** Avoid combinatorial E2E matrices for balance/config values.

## Performance and Speed

Test runtime is an architectural concern.

- Pure simulation tests should execute without rendering/browser dependencies.
- Avoid real sleeps; use deterministic/fake time where appropriate.
- Keep fixtures small unless scale itself is under test.
- Separate expensive performance/soak tests from the normal fast PR path when they are eventually introduced.

## Bug Fixes

A bug fix should normally add a regression test at the lowest practical level. If no automated test is practical, the PR must explain why and provide alternative verification evidence.

## CI Expectations

The intended pull-request quality path is:

1. Typecheck
2. Lint
3. Data/schema validation
4. Unit tests
5. Focused integration tests
6. Production build
7. Minimal Playwright smoke tests when relevant

The executable project scaffold will implement these jobs once introduced.

## Review Checklist

- Is logic covered primarily by unit tests?
- Are integration tests focused?
- Is every E2E test necessary?
- Are regression tests included for fixed defects?
- Are tests deterministic and fast?
- Does the suite test behaviour rather than private implementation details?
