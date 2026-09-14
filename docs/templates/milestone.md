# <Milestone Name>

**Status:** Planned  
**Version:** 0.1  
**Owner:** Product / Delivery Scope  
**Last Updated:** YYYY-MM-DD  
**Implementation Readiness:** Blocked

**Included Features:**
- [Example Feature](../features/example.md)

## Table of Contents

1. [Purpose](#purpose)
2. [Validation Goal](#validation-goal)
3. [Included Features](#included-features)
4. [Required Feature Slices](#required-feature-slices)
5. [Explicitly Out of Scope](#explicitly-out-of-scope)
6. [Dependency and Readiness Matrix](#dependency-and-readiness-matrix)
7. [Known Blockers](#known-blockers)
8. [Milestone Acceptance Criteria](#milestone-acceptance-criteria)
9. [Technical Handoff Gate](#technical-handoff-gate)
10. [Change Log](#change-log)

## Purpose

Explain what development step this milestone represents and why these features are being delivered together.

A milestone groups multiple features. It must not define gameplay rules or replace feature/concept documentation.

## Validation Goal

State the concrete product/design question this milestone should answer once playable.

Examples: prove that a complete travel loop feels good; validate combat readability; validate ship-fitting decisions.

## Included Features

| Feature | Status | Role in Milestone |
| --- | --- | --- |
| [Example Feature](../features/example.md) | Planned / Draft / Review / Approved | `<role>` |

A milestone should combine multiple coherent features rather than artificially moving concept rules into milestone scope.

## Required Feature Slices

Define which already-specified capabilities of each feature are required now.

| Feature | Required in This Milestone | Deferred From This Milestone |
| --- | --- | --- |
| [Example Feature](../features/example.md) | `<capability slice>` | `<approved feature capabilities intentionally deferred>` |

This section scopes delivery. It does not modify the full feature definition.

## Explicitly Out of Scope

List features or feature capabilities deliberately excluded from this milestone.

- `<excluded capability>`

Exclusion from a milestone does not mean rejection from the final game.

## Dependency and Readiness Matrix

| Dependency | Type | Status | Required for Handoff | Notes |
| --- | --- | --- | --- | --- |
| [Example Feature](../features/example.md) | Feature | Draft | Yes | `<blocker>` |
| [Example Concept](../concepts/example.md) | Concept | Planned | Yes | `<why needed>` |

If planning reveals a missing feature, create a feature document and mark it `Planned`.

If planning reveals a missing gameplay concept, create a `Planned` concept stub using [`concept-stub.md`](concept-stub.md), add it to the concept index, and reference it through the owning feature.

## Known Blockers

- [ ] `<unfinished feature, planned concept or unresolved interaction>`

A milestone can remain useful and well scoped while blocked. Do not invent gameplay behaviour merely to clear a blocker.

## Milestone Acceptance Criteria

Define observable end-to-end outcomes for this delivery target.

- [ ] `<multiple included features work together to produce the intended validation experience>`
- [ ] Deferred capabilities are not required for the milestone to satisfy its stated validation goal.

## Technical Handoff Gate

`Implementation Readiness` may change to `Ready` only when:

- [ ] the milestone goal and required feature slices are explicit;
- [ ] all included feature documents exist;
- [ ] all gameplay concepts required by the included slices are `Approved`;
- [ ] required cross-concept interactions are resolved in the relevant feature documents;
- [ ] no gameplay decision is left for Codex to invent;
- [ ] exclusions and deferred capabilities are explicit;
- [ ] milestone acceptance criteria are testable at product level;
- [ ] the project owner has approved the milestone scope.

## Change Log

| Version | Date | Change |
| --- | --- | --- |
| 0.1 | YYYY-MM-DD | Initial milestone definition |
