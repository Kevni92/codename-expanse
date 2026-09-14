# Flight Navigation Interface

**Status:** Draft  
**Version:** 0.1  
**Owner:** Feature / Product Design  
**Last Updated:** 2026-09-14

**Related Concepts:**
- [Flight HUD & Navigation Information](../concepts/flight-hud-navigation-information.md)
- [Navigation Targeting & Actions](../concepts/navigation-targeting-actions.md)
- [Flight Physics](../concepts/flight-physics.md)
- [Flight Assist](../concepts/flight-assist.md)
- [Autopilot](../concepts/autopilot.md)
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

Provide the player with a coherent flight/navigation interaction surface that exposes the information and actions needed to understand current movement, identify a navigation target and initiate or monitor assisted/automated travel.

This feature composes information and interaction semantics from multiple gameplay systems. It does not define the underlying physics, target-selection rules, autopilot logic or final visual styling.

## Player Capability

The player can understand essential flight state, identify the current navigation target and relevant target information, see the state of Flight Assist/Autopilot, and invoke navigation actions that are valid for the selected target.

## Scope

- Player-facing flight/navigation information required during normal play.
- Presentation of the selected navigation target and relevant target information.
- Exposure of valid target actions, including Autopilot travel where applicable.
- Presentation of Flight Assist and Autopilot state relevant to navigation decisions.
- Integration of physical/world state into player-readable information without changing that state.

## Out of Scope

- Defining ship physics or Flight Assist behaviour.
- Defining Autopilot route planning or arrival rules.
- Defining celestial orbital motion.
- Final UI visual style, layout polish, animation or art direction.
- Temporary debug overlays unless a debug item is later promoted into intended normal-player information.
- Milestone-specific choices about which subset of the full interface is initially delivered.

## Required Concepts

| Concept | Status | Role in Feature | Required for Completion |
| --- | --- | --- | --- |
| [Flight HUD & Navigation Information](../concepts/flight-hud-navigation-information.md) | Planned | Owns which flight/navigation information the player must receive and its gameplay meaning. | Yes |
| [Navigation Targeting & Actions](../concepts/navigation-targeting-actions.md) | Planned | Owns selected navigation target state and valid player actions. | Yes |
| [Flight Physics](../concepts/flight-physics.md) | Approved | Supplies authoritative physical state that may be presented to the player. | Yes |
| [Flight Assist](../concepts/flight-assist.md) | Approved | Supplies assisted-flight mode/state that requires player feedback. | Yes |
| [Autopilot](../concepts/autopilot.md) | Approved | Supplies route/travel state and player-relevant automated-flight status. | Yes |
| [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md) | Planned | Supplies moving celestial target/world state consumed by navigation information. | Yes |

## Feature Composition

Flight Physics supplies authoritative ship state. Celestial Bodies & Orbits supplies relevant world/target state. Navigation Targeting & Actions owns which navigation object is selected and what actions are available. Flight Assist and Autopilot expose their player-relevant modes/states. Flight HUD & Navigation Information determines which of these facts must be communicated to the player and what they mean.

The interface layer presents and routes these concepts; it does not become a competing owner for physics, target validity or automated-flight rules.

## Cross-Concept Interaction Flows

### Read Current Flight State

1. [Flight Physics](../concepts/flight-physics.md) provides the authoritative current ship state.
2. [Flight HUD & Navigation Information](../concepts/flight-hud-navigation-information.md) defines which parts of that state are player-facing and how their meaning is communicated.
3. The interface presents the information without becoming authoritative gameplay state.

### Select and Inspect a Navigation Target

1. [Navigation Targeting & Actions](../concepts/navigation-targeting-actions.md) establishes the selected target.
2. Relevant target/world data is supplied by its owning gameplay system, including [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md) for celestial destinations.
3. Flight HUD & Navigation Information determines which target facts must be shown to the player.

### Start and Monitor Autopilot

1. Navigation Targeting & Actions exposes Autopilot travel when valid for the selected target.
2. [Autopilot](../concepts/autopilot.md) owns route validation, start and ongoing automated-travel state.
3. Flight HUD & Navigation Information defines the player-facing Autopilot state/route information required during travel.
4. The interface presents those states and actions without altering the Autopilot model.

### Show Assisted-Flight State

1. [Flight Assist](../concepts/flight-assist.md) owns current assisted-flight behaviour/state.
2. Flight HUD & Navigation Information defines which state must be visible to the player.
3. The interface displays that information independently from the simulation logic.

## Ownership and Rule Boundaries

| Interaction / Responsibility | Owning Concept | Consuming Concept(s) | Notes |
| --- | --- | --- | --- |
| Authoritative ship state | [Flight Physics](../concepts/flight-physics.md) | Flight HUD & Navigation Information | UI must never become simulation state. |
| Required player-facing flight/navigation information | [Flight HUD & Navigation Information](../concepts/flight-hud-navigation-information.md) | Interface consumers | Visual styling remains implementation/presentation work. |
| Selected navigation target and valid target actions | [Navigation Targeting & Actions](../concepts/navigation-targeting-actions.md) | Flight HUD, Autopilot | Exact interaction model remains to be designed. |
| Flight Assist state/behaviour | [Flight Assist](../concepts/flight-assist.md) | Flight HUD & Navigation Information | Interface only reports/invokes supported actions. |
| Autopilot travel state/behaviour | [Autopilot](../concepts/autopilot.md) | Flight HUD & Navigation Information | Interface must not infer alternate route rules. |
| Celestial target motion/state | [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md) | Navigation Targeting, Flight HUD, Autopilot | World state has one gameplay owner. |

## Missing Concepts and Gaps

- [ ] [Flight HUD & Navigation Information](../concepts/flight-hud-navigation-information.md) must be fully designed and approved.
- [ ] [Navigation Targeting & Actions](../concepts/navigation-targeting-actions.md) must be fully designed and approved.
- [ ] [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md) must be fully designed and approved.

## Feature-Level Edge Cases

- Target state may change while the player is inspecting or traveling toward it; presentation and actions must reflect the authoritative target/world state rather than stale UI state.
- Autopilot may refuse or terminate travel; the interface must communicate the owning system's outcome rather than masking it.
- Flight Assist and Autopilot modes may change due to player input or handoff; the displayed state must follow authoritative gameplay state.
- Debug-only vectors or diagnostic values must remain distinguishable from information intended for normal player use.

## Acceptance Criteria

- [ ] The player can identify the current navigation target and access the valid navigation actions defined by the targeting concept.
- [ ] The player receives the flight/navigation information required by the HUD concept from authoritative gameplay state.
- [ ] Flight Assist and Autopilot states can be understood without the interface redefining their behaviour.
- [ ] Moving celestial target information is consumed from its owning system rather than duplicated in UI logic.
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
