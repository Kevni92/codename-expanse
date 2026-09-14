# <Concept Name>

**Status:** Draft  
**Version:** 0.1  
**Owner:** Concept / Game Design  
**Last Updated:** YYYY-MM-DD

**Related Documents:**
- [Example Related Concept](../concepts/example.md)
- [Example Requiring Feature](../features/example.md)

> **Concept ownership rule:** This document defines the intended final-game behaviour of its system. It must not encode temporary prototype or Milestone shortcuts as permanent gameplay rules. If this system is only partially delivered in a Milestone, the Milestone scopes the delivery; this Concept still describes the complete intended system.

## Table of Contents

1. [Purpose](#purpose)
2. [Design Goals](#design-goals)
3. [Scope](#scope)
4. [Out of Scope](#out-of-scope)
5. [Terminology](#terminology)
6. [Player Experience](#player-experience)
7. [Functional Design](#functional-design)
8. [Rules and Invariants](#rules-and-invariants)
9. [Parameters and Initial Values](#parameters-and-initial-values)
10. [States and Transitions](#states-and-transitions)
11. [Interactions With Other Systems](#interactions-with-other-systems)
12. [Player Feedback and Information](#player-feedback-and-information)
13. [Edge Cases](#edge-cases)
14. [Examples](#examples)
15. [Design Decisions and Rationale](#design-decisions-and-rationale)
16. [Rejected or Deferred Alternatives](#rejected-or-deferred-alternatives)
17. [Open Questions](#open-questions)
18. [Acceptance Criteria](#acceptance-criteria)
19. [Change Log](#change-log)

## Purpose
Explain why this final-game system exists, what player/gameplay problem it solves and what value it adds.

## Design Goals
List the outcomes this Concept is intentionally designed to achieve. Goals should help evaluate later proposals and trade-offs.

- **G-<SHORT>-001:** ...
- **G-<SHORT>-002:** ...

## Scope
Define what this Concept owns normatively in the intended final game.

Do not reduce Concept scope solely because an early Milestone implements only part of it.

## Out of Scope
Define what this Concept explicitly does not own. Link to the owning Concept when known.

## Terminology
Use canonical project terminology consistently.

| Term | Definition |
| --- | --- |
| `<term>` | `<precise definition>` |

## Player Experience
Describe what the player perceives, understands, decides and does. Explain intended feel without prescribing implementation details.

## Functional Design
Describe the complete intended behaviour of the system. Use subsections for distinct capabilities and flows.

The design must be precise enough that multiple readers derive the same gameplay behaviour and downstream Features do not need to invent missing system rules.

## Rules and Invariants
Number important normative rules so other documents can reference them directly.

1. **C-<SHORT>-001:** ...
2. **C-<SHORT>-002:** ...

Rules should describe gameplay truth, not implementation technique or temporary Milestone constraints.

## Parameters and Initial Values
Define concept-level values/ranges required to make intended behaviour concrete. Mark balance values as tunable where appropriate. Technical architecture will define executable representation and ownership.

| Parameter | Initial value/range | Unit | Tunable | Design purpose / notes |
| --- | ---: | --- | --- | --- |
| `<name>` | `<value>` | `<unit>` | Yes/No | ... |

Do not leave implementation-critical gameplay quantities without units or semantic meaning.

## States and Transitions
Define relevant states, triggers, transitions and forbidden transitions when the system is stateful.

| From | Trigger / Condition | To | Player-visible result |
| --- | --- | --- | --- |
| ... | ... | ... | ... |

If the Concept has no meaningful state model, state that explicitly.

## Interactions With Other Systems
Link to the normative owner of each related gameplay rule instead of duplicating it.

- [Related Concept](../concepts/example.md) — describe the interaction boundary and which document owns which rule.

Feature documents may later compose these Concept interactions into broader player-facing capabilities, but gameplay rules still belong here or in another owning Concept.

## Player Feedback and Information
Describe the information and feedback the player requires to understand and use the system correctly.

Cover only design requirements, for example:
- important visible state;
- warnings or thresholds;
- target/selection information;
- consequences the player must be able to predict;
- required feedback after an action.

Detailed UI layout belongs in the appropriate Concept when UI behaviour itself needs a dedicated owner.

## Edge Cases
Enumerate important boundary, failure and unusual situations and define expected gameplay behaviour.

Do not hide unresolved edge cases behind implementation assumptions or defer them merely because the first Milestone will not exercise them.

## Examples
Provide concrete scenarios or calculations where they improve understanding. Examples illustrate the normative rules; they do not override them.

## Design Decisions and Rationale
Record important decisions whose reasoning matters for future design work.

| ID | Decision | Rationale | Consequences |
| --- | --- | --- | --- |
| D-<SHORT>-001 | ... | ... | ... |

Do not record every trivial choice. Capture decisions that future contributors might otherwise question or accidentally reverse.

## Rejected or Deferred Alternatives
Record serious alternatives discussed during design when remembering why they were not selected has future value.

| Alternative | Status | Reason |
| --- | --- | --- |
| ... | Rejected / Deferred | ... |

`Deferred` here means deferred as a design decision, not merely omitted from one Milestone. Milestone-specific delivery deferrals belong in `docs/milestones/**`.

## Open Questions
Only unresolved product/gameplay decisions belong here.

- [ ] ...

For each important open question, explain what decision is missing and what downstream behaviour it affects.

An `Approved` Concept must not contain implementation-blocking gameplay questions.

## Acceptance Criteria
Define concept-level, observable criteria that must be true for an implementation to satisfy the intended gameplay.

- [ ] ...
- [ ] ...

Acceptance criteria describe final intended behaviour, not source-code structure or one Milestone's reduced delivery scope.

## Change Log
| Version | Date | Change |
| --- | --- | --- |
| 0.1 | YYYY-MM-DD | Initial draft |
