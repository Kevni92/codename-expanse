# Autopilot Travel

**Status:** Draft  
**Version:** 0.1  
**Owner:** Feature / Product Design  
**Last Updated:** 2026-09-14

**Related Concepts:**
- [Autopilot](../concepts/autopilot.md)
- [Flight Physics](../concepts/flight-physics.md)
- [Flight Assist](../concepts/flight-assist.md)
- [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md)
- [Navigation Targeting & Actions](../concepts/navigation-targeting-actions.md)

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

Provide the player with a coherent way to select a valid destination and have the ship travel there autonomously while obeying the same physical rules and ship capabilities used during manual flight.

This feature composes target intent, moving-world state, autonomous trajectory planning/execution, Flight Physics and post-autopilot handoff. It does not redefine any of those underlying systems.

## Player Capability

The player can choose an eligible navigation destination, request autopilot travel, observe the ship execute a physically valid trajectory toward the destination, and regain control in a defined physical arrival/handoff state.

## Scope

- Supplying a valid navigation destination to Autopilot.
- Autonomous route execution using the approved Autopilot model.
- Consumption of moving celestial destination state where relevant.
- Physical thrust, rotation and braking through Flight Physics.
- Handoff to Flight Assist or manual flight according to approved system rules.
- Player interruption/cancellation according to the owning concepts.

## Out of Scope

- Defining detailed orbital mechanics or celestial-body motion.
- Defining target-selection controls or context-menu presentation.
- Defining HUD visual styling.
- Combat automation or projectile avoidance.
- Ship/module construction or engine configuration systems.
- Milestone-specific restrictions on which Autopilot profiles or destination types are implemented first.

## Required Concepts

| Concept | Status | Role in Feature | Required for Completion |
| --- | --- | --- | --- |
| [Autopilot](../concepts/autopilot.md) | Approved | Owns route planning, travel profiles, execution, replanning, arrival and cancellation behaviour. | Yes |
| [Flight Physics](../concepts/flight-physics.md) | Approved | Owns the authoritative physical state and ship response during travel. | Yes |
| [Flight Assist](../concepts/flight-assist.md) | Approved | Owns assisted-flight state used by post-autopilot handoff where applicable. | Yes |
| [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md) | Draft | Owns moving celestial destination state and orbital destination context. | Yes |
| [Navigation Targeting & Actions](../concepts/navigation-targeting-actions.md) | Planned | Owns destination selection and the player's request to initiate travel. | Yes |

## Feature Composition

Navigation Targeting & Actions establishes the player's selected destination and travel intent. Celestial Bodies & Orbits provides the authoritative gameplay state of moving celestial destinations. Autopilot consumes that target state and plans/executes a route according to its approved profiles and arrival rules. Flight Physics remains authoritative for every resulting movement and rotation. Flight Assist receives the ship after automated travel where the approved Autopilot handoff requires it.

The feature therefore turns player destination intent into autonomous physical travel without allowing the navigation or UI layers to invent movement behaviour.

## Cross-Concept Interaction Flows

### Start Autopilot Travel

1. [Navigation Targeting & Actions](../concepts/navigation-targeting-actions.md) establishes a valid selected destination and exposes an Autopilot travel action.
2. [Autopilot](../concepts/autopilot.md) validates whether a physically valid route can be planned for the current ship state and selected destination.
3. For moving celestial targets, [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md) supplies the destination state required by Autopilot.
4. Autopilot begins execution only according to its approved route-start rules.

### Execute Physical Travel

1. Autopilot determines the required trajectory/control intent according to its approved rules.
2. [Flight Physics](../concepts/flight-physics.md) remains authoritative for thrust, rotation, gravity and resulting ship state.
3. Celestial destination motion continues independently according to Celestial Bodies & Orbits.
4. Autopilot replans or terminates according to its approved behaviour when relevant state changes.

### Arrival and Handoff

1. Autopilot performs the arrival behaviour owned by its concept for the destination type.
2. For celestial destinations, required orbital context comes from Celestial Bodies & Orbits.
3. When Autopilot ends, [Flight Assist](../concepts/flight-assist.md) receives the current physical state where the approved handoff specifies assisted flight.
4. The ship's physical position, velocity and rotation are never reset merely because the automated mode ended.

## Ownership and Rule Boundaries

| Interaction / Responsibility | Owning Concept | Consuming Concept(s) | Notes |
| --- | --- | --- | --- |
| Destination selection and travel action | [Navigation Targeting & Actions](../concepts/navigation-targeting-actions.md) | Autopilot | UI presentation must not own these gameplay semantics. |
| Route planning/execution and profiles | [Autopilot](../concepts/autopilot.md) | Flight Physics, Celestial Bodies & Orbits | Existing approved Autopilot rules remain authoritative. |
| Ship movement and rotation | [Flight Physics](../concepts/flight-physics.md) | Autopilot | Autopilot cannot bypass ship physics. |
| Celestial destination motion/orbital context | [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md) | Autopilot | Concept is actively being designed; final approval remains pending. |
| Post-autopilot assisted state | [Flight Assist](../concepts/flight-assist.md) | Autopilot | Handoff uses the current physical state. |

## Missing Concepts and Gaps

- [ ] [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md) must be completed and approved.
- [ ] [Navigation Targeting & Actions](../concepts/navigation-targeting-actions.md) must be fully designed and approved.

## Feature-Level Edge Cases

- A selected destination may move materially while travel is underway; Autopilot owns replanning while the celestial concept owns destination state.
- A previously valid target may become unavailable or invalid; Navigation Targeting & Actions and Autopilot must have compatible ownership for target loss and travel termination.
- Manual interruption must preserve current physical state and follow approved Autopilot/Flight Assist handoff rules.
- Failure to find a valid route must remain a player-visible travel outcome rather than causing hidden non-physical movement.

## Acceptance Criteria

- [ ] The player can select an eligible destination and request Autopilot travel through a defined navigation action.
- [ ] Autopilot consumes moving destination state without duplicating the celestial orbital model.
- [ ] Autonomous travel uses the same authoritative Flight Physics as manual flight.
- [ ] Arrival and cancellation preserve the ship's physical state and hand off according to approved concepts.
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
