# <Feature Name>

**Status:** Draft  
**Version:** 0.1  
**Owner:** Feature / Product Design  
**Last Updated:** YYYY-MM-DD

**Related Concepts:**
- [Example Concept](../concepts/example.md)

## Table of Contents

1. [Purpose](#purpose)
2. [Player Capability](#player-capability)
3. [Scope](#scope)
4. [Out of Scope](#out-of-scope)
5. [Required Concepts](#required-concepts)
6. [Feature Composition](#feature-composition)
7. [Cross-Concept Interaction Flows](#cross-concept-interaction-flows)
8. [Ownership and Rule Boundaries](#ownership-and-rule-boundaries)
9. [Missing Concepts and Gaps](#missing-concepts-and-gaps)
10. [Feature-Level Edge Cases](#feature-level-edge-cases)
11. [Acceptance Criteria](#acceptance-criteria)
12. [Completion Gate](#completion-gate)
13. [Change Log](#change-log)

## Purpose

Explain what coherent player-facing capability this feature represents and why it exists.

A feature composes multiple gameplay concepts. It must not redefine the detailed rules owned by those concepts.

## Player Capability

Describe what the player can accomplish when this feature is available.

Focus on the end-to-end capability rather than implementation or milestone scope.

## Scope

Define the capability boundary owned by this feature composition.

## Out of Scope

State adjacent capabilities that belong to other features or later feature definitions.

## Required Concepts

| Concept | Status | Role in Feature | Required for Completion |
| --- | --- | --- | --- |
| [Example Concept](../concepts/example.md) | Approved / Review / Draft / Planned | `<role>` | Yes |

Every gameplay system used by this feature should have a concept owner.

If a required concept does not exist, create a `Planned` concept stub using [`concept-stub.md`](concept-stub.md), add it to the concept index, and link it here.

## Feature Composition

Explain how the required concepts combine into this capability.

Describe responsibility handoffs and dependencies between concepts, but do not create new gameplay rules here. If an interaction requires a rule not defined by any concept, record it under [Missing Concepts and Gaps](#missing-concepts-and-gaps) and move that rule into the appropriate concept-design workflow.

## Cross-Concept Interaction Flows

Describe important end-to-end player flows that cross concept boundaries.

### Example Flow

1. Concept A owns `<state or action>`.
2. Concept B consumes `<result>` according to its approved rules.
3. Concept C owns `<player-visible outcome>`.

Use links to the normative concept sections where practical.

## Ownership and Rule Boundaries

| Interaction / Responsibility | Owning Concept | Consuming Concept(s) | Notes |
| --- | --- | --- | --- |
| `<responsibility>` | [Concept](../concepts/example.md) | [Concept](../concepts/example.md) | `<boundary>` |

This table exists to prevent duplicated or orphaned gameplay rules.

## Missing Concepts and Gaps

List unresolved dependencies exposed while composing the feature.

- [ ] `<missing concept or missing ownership rule>`

For a missing concept, create and link a `Planned` concept stub immediately. Do not resolve detailed gameplay behaviour inside this feature document.

## Feature-Level Edge Cases

Cover only edge cases created by interaction between multiple concepts.

Single-system edge cases belong in the owning concept.

## Acceptance Criteria

Define observable criteria for the combined capability.

- [ ] The player can `<end-to-end capability>` through the interaction of the required concepts.
- [ ] No required gameplay behaviour is defined only in this feature document without a concept owner.

## Completion Gate

This feature may be marked `Approved` only when:

- [ ] every required concept exists;
- [ ] every required concept is `Approved`;
- [ ] all cross-concept interactions needed by the feature are described;
- [ ] every required gameplay rule has a concept owner;
- [ ] no unresolved concept gap remains;
- [ ] feature-level acceptance criteria are complete;
- [ ] the project owner explicitly approves the feature.

## Change Log

| Version | Date | Change |
| --- | --- | --- |
| 0.1 | YYYY-MM-DD | Initial draft |
