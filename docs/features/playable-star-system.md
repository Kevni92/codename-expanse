# Playable Star System

**Status:** Draft  
**Version:** 0.1  
**Owner:** Feature / Product Design  
**Last Updated:** 2026-09-14

**Related Concepts:**
- [Flight Physics](../concepts/flight-physics.md)
- [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md)

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

Provide a coherent physical star-system environment in which the player can exist, move and travel while celestial bodies follow the game's defined orbital model and participate in the established gravity model.

This feature composes world/orbital behaviour with ship physics. It does not define orbital equations, gravity rules, rendering style or milestone-specific system content.

## Player Capability

The player can fly a ship through a star system whose celestial bodies have coherent positions and motion, and the ship's physical state responds to the celestial environment according to the game's flight rules.

## Scope

- A traversable star-system environment containing gameplay-relevant celestial bodies.
- Coherent celestial-body motion and hierarchical orbital relationships as defined by the owning concept.
- Integration of celestial state with the gravity rules owned by Flight Physics.
- A stable physical/world context that navigation and travel features can consume.

## Out of Scope

- Procedural generation of star systems or content distribution.
- Final rendering, art style, camera or parallax presentation.
- Manual flight controls.
- Target selection, navigation UI or autopilot interaction.
- Combat, stations, NPCs, economy or other unrelated world content.
- Milestone-specific choices such as the exact bodies present in a test system.

## Required Concepts

| Concept | Status | Role in Feature | Required for Completion |
| --- | --- | --- | --- |
| [Flight Physics](../concepts/flight-physics.md) | Approved | Owns ship motion, celestial gravity interaction and physical response. | Yes |
| [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md) | Planned | Owns celestial-body state, prescribed motion, orbital relationships and orbital destination context. | Yes |

## Feature Composition

Celestial Bodies & Orbits defines the gameplay-relevant state and motion of celestial bodies. Flight Physics consumes the resulting celestial context according to its approved gravity and motion rules when updating the player's ship.

The result is one coherent playable environment: celestial bodies provide the moving physical context, while Flight Physics remains authoritative for the ship. Neither concept should duplicate the other's responsibility.

## Cross-Concept Interaction Flows

### Ship Traversal Through a Moving System

1. [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md) determines the gameplay state of relevant celestial bodies.
2. [Flight Physics](../concepts/flight-physics.md) evaluates the ship within that celestial context using its approved gravity and motion rules.
3. The ship remains governed by the same physical model while celestial bodies continue their prescribed motion.

### Hierarchical Celestial Motion

1. Celestial Bodies & Orbits owns any parent/child orbital relationship between celestial bodies.
2. The resulting world-state positions become available to systems that require celestial position and motion.
3. Flight Physics uses the resulting body state only for the physical interactions it already owns.

## Ownership and Rule Boundaries

| Interaction / Responsibility | Owning Concept | Consuming Concept(s) | Notes |
| --- | --- | --- | --- |
| Ship translational/rotational physics | [Flight Physics](../concepts/flight-physics.md) | Celestial Bodies & Orbits | Celestial-body motion must not redefine ship physics. |
| Celestial gravity effect on ships | [Flight Physics](../concepts/flight-physics.md) | Celestial Bodies & Orbits | Existing gravity rules remain authoritative. |
| Celestial-body state and prescribed motion | [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md) | Flight Physics | Exact orbital gameplay model remains to be designed. |
| Hierarchical orbital relationships | [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md) | Flight Physics | Includes relationships such as a moon orbiting a planet within a stellar system. |
| Standard orbital destination context | [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md) | Autopilot feature/concept | Required by travel features but not defined here. |

## Missing Concepts and Gaps

- [ ] [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md) must be fully designed and approved.

## Feature-Level Edge Cases

- A ship may be affected by multiple celestial gravity sources while those bodies follow prescribed motion; ownership must remain unambiguous between the two concepts.
- Hierarchical body motion must expose one coherent gameplay state to ship physics and downstream navigation systems.
- Visual overlap or rendering-layer behaviour is not a physical collision rule and remains outside this feature unless owned by a separate presentation concept.

## Acceptance Criteria

- [ ] A player ship can exist and move within a star-system environment whose celestial bodies have gameplay-defined motion.
- [ ] Celestial state integrates with Flight Physics without duplicating or overriding its approved ship/gravity rules.
- [ ] Hierarchical celestial relationships can be represented by the owning concept and consumed as one coherent world state.
- [ ] Downstream navigation/travel features can consume celestial position/motion without inventing their own orbital model.
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
| 0.1 | 2026-09-14 | Initial feature draft identified for the first flight milestone. |
