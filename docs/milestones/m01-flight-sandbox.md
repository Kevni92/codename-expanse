# M01 – Flight Sandbox

**Status:** Draft  
**Version:** 0.1  
**Owner:** Product / Delivery Scope  
**Last Updated:** 2026-09-14  
**Implementation Readiness:** Blocked

**Included Features:**
- [Playable Star System](../features/playable-star-system.md)
- [Manual Space Flight](../features/manual-space-flight.md)
- [Autopilot Travel](../features/autopilot-travel.md)
- [Flight Navigation Interface](../features/flight-navigation-interface.md)

## Table of Contents

1. [Purpose](#purpose)
2. [Validation Goal](#validation-goal)
3. [Included Features](#included-features)
4. [Required Feature Slices](#required-feature-slices)
5. [Milestone-Only Presentation and Validation Requirements](#milestone-only-presentation-and-validation-requirements)
6. [Explicitly Out of Scope](#explicitly-out-of-scope)
7. [Dependency and Readiness Matrix](#dependency-and-readiness-matrix)
8. [Known Blockers](#known-blockers)
9. [Milestone Acceptance Criteria](#milestone-acceptance-criteria)
10. [Technical Handoff Gate](#technical-handoff-gate)
11. [Change Log](#change-log)

## Purpose

M01 creates the first executable flight sandbox for Codename Expanse. It combines the minimum player-facing capabilities required to evaluate the core flight model in a moving celestial environment without introducing combat, ship fitting, NPC behaviour or production-quality presentation.

The milestone exists to make the approved flight-physics, flight-assist and autopilot rules playable and objectively testable in one coherent loop.

This document scopes delivery only. Detailed final-game behaviour remains owned by the linked Concepts and Feature documents.

## Validation Goal

M01 must answer whether the core space-flight experience works as a foundation for the wider game.

The milestone should make it possible to validate all of the following in one executable build:

- manual inertial translation and rotation feel coherent and controllable;
- Flight Assist produces the intended assisted-flight behaviour without replacing the underlying physics;
- Autopilot can plan and execute a physically valid journey to a moving celestial destination;
- celestial orbital motion and gravity provide a meaningful environment for local and interplanetary travel;
- the final physical state of the ship can be inspected numerically rather than inferred from rendering;
- simulation behaviour required by manual flight, Flight Assist and Autopilot can be tested independently from presentation.

## Included Features

| Feature | Status | Role in Milestone |
| --- | --- | --- |
| [Playable Star System](../features/playable-star-system.md) | Draft | Supplies the authored moving celestial environment and orbital/gravity context. |
| [Manual Space Flight](../features/manual-space-flight.md) | Draft | Supplies direct player-controlled translation, rotation and Flight Assist operation. |
| [Autopilot Travel](../features/autopilot-travel.md) | Draft | Supplies physically valid automated travel to a selected celestial destination. |
| [Flight Navigation Interface](../features/flight-navigation-interface.md) | Draft | Supplies the minimum targeting, flight information and Autopilot interaction needed to operate the sandbox. |

## Required Feature Slices

| Feature | Required in This Milestone | Deferred From This Milestone |
| --- | --- | --- |
| [Playable Star System](../features/playable-star-system.md) | One authored deterministic test system containing the Sun, Earth, Moon and Mars; each celestial body has the orbital state and relationships required by the final orbital model; the Moon is associated with Earth and Earth/Mars with the Sun; celestial state is usable by gravity, navigation and Autopilot. | Procedural system generation; large content variety; additional stars, planets, moons or other celestial content not required for flight validation. |
| [Manual Space Flight](../features/manual-space-flight.md) | One minimalist test ship can be translated and rotated manually using the approved Flight Physics; Flight Assist can be enabled/disabled and its required core stabilization behaviour can be exercised; manual player input can regain control from Autopilot according to the approved interaction rules. | Final ship content, ship classes, modules, fitting, visible hardpoints, damage, structural-breakup gameplay and polished control customization. |
| [Autopilot Travel](../features/autopilot-travel.md) | The player can start Autopilot travel toward a selected celestial body; planning/execution uses the real ship state and Flight Physics; moving celestial targets are respected; the arrival state for a celestial destination can be validated against the approved orbital-arrival rules. | Ship/station rendezvous, combat manoeuvring, projectile avoidance, detector-aware Stealth behaviour, and Autopilot capabilities not required to validate the basic celestial-travel loop. The exact minimum travel-profile slice remains to be confirmed before handoff. |
| [Flight Navigation Interface](../features/flight-navigation-interface.md) | The player can establish a celestial navigation target and initiate Autopilot travel to it; the interface shows at minimum current speed, selected target name, target distance, Flight Assist state and Autopilot state. | Final HUD layout, final interaction styling, advanced navigation information, production-quality presentation and interaction flows not required for M01. The exact target-selection input mapping remains to be confirmed. |

## Milestone-Only Presentation and Validation Requirements

The requirements in this section intentionally belong to M01 rather than to final-game Feature or Concept behaviour unless later promoted through the normal design process.

### Minimal visual presentation

- The ship may be represented by a simple placeholder shape.
- Propulsion does not require production-quality engine or thruster visuals.
- The Sun, Earth, Moon and Mars may be represented by simple distinguishable coloured circles.
- Production-quality art, lighting, effects and environmental presentation are not required for milestone acceptance.

### Debug instrumentation

M01 must expose enough optional debug information to inspect the flight simulation while testing it.

At minimum, the milestone must support inspection of acceleration-related vectors needed to diagnose manual flight, Flight Assist and Autopilot behaviour.

Additional useful vectors or state readouts such as velocity, thrust contribution, gravity contribution, angular state, trajectory/phase information or reference states may be specified by technical architecture when they improve diagnosis without becoming final-game HUD requirements.

### Simulation / presentation separation

M01 must be verifiable without relying on the visual representation of the ship or celestial bodies.

The authoritative physical state must be queryable so tests can inspect relevant values such as position, velocity, orientation and rotational state directly.

Flight-simulation, Flight Assist and Autopilot correctness must not depend on rendering being present.

### Deterministic validation

For controlled initial state, simulation time and input/test conditions, the milestone must support reproducible numerical validation of the resulting simulation state.

Technical architecture owns the concrete determinism strategy, numerical tolerances, test harness and simulation execution model.

## Explicitly Out of Scope

The following are not required for M01:

- combat, weapons or projectiles;
- NPC ships or NPC behaviour;
- stations and station interaction;
- ship fitting, modules, hardpoints or ship editor;
- damage resolution or ship breakup;
- economy, cargo or progression;
- sensors/detection and Stealth-specific validation;
- procedural star-system generation;
- dynamic asteroid gameplay;
- production-quality ship or celestial-body art;
- production HUD polish;
- backend/server functionality;
- multiplayer;
- any Feature capability not needed to evaluate the core manual-flight → Flight Assist → Autopilot → celestial-arrival loop.

Exclusion from M01 does not remove these capabilities from the intended final game.

## Dependency and Readiness Matrix

| Dependency | Type | Status | Required for Handoff | Notes |
| --- | --- | --- | --- | --- |
| [Playable Star System](../features/playable-star-system.md) | Feature | Draft | Yes | Must resolve its celestial/orbit concept dependency and cross-concept interactions. |
| [Manual Space Flight](../features/manual-space-flight.md) | Feature | Draft | Yes | Must resolve player-control semantics and required flight-control interactions. |
| [Autopilot Travel](../features/autopilot-travel.md) | Feature | Draft | Yes | Must resolve dependencies needed for celestial targeting/orbital arrival and M01 profile slice. |
| [Flight Navigation Interface](../features/flight-navigation-interface.md) | Feature | Draft | Yes | Must resolve targeting/action semantics and HUD information ownership. |
| [Flight Physics](../concepts/flight-physics.md) | Concept | Approved | Yes | Existing normative physics model. |
| [Flight Assist](../concepts/flight-assist.md) | Concept | Approved | Yes | Existing normative assisted-flight model. |
| [Autopilot](../concepts/autopilot.md) | Concept | Approved | Yes | Existing normative trajectory-planning and execution model. |
| [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md) | Concept | Planned | Yes | Required for deterministic celestial state, hierarchical orbital motion and orbital destination context. |
| [Player Flight Controls](../concepts/player-flight-controls.md) | Concept | Planned | Yes | Required for final-game manual/assisted flight input semantics. |
| [Navigation Targeting & Actions](../concepts/navigation-targeting-actions.md) | Concept | Planned | Yes | Required for selecting a destination and exposing navigation actions such as Autopilot travel. |
| [Flight HUD & Navigation Information](../concepts/flight-hud-navigation-information.md) | Concept | Planned | Yes | Required for player-facing flight/navigation information semantics. |

## Known Blockers

- [ ] Complete and approve [Celestial Bodies & Orbits](../concepts/celestial-bodies-orbits.md).
- [ ] Complete and approve [Player Flight Controls](../concepts/player-flight-controls.md).
- [ ] Complete and approve [Navigation Targeting & Actions](../concepts/navigation-targeting-actions.md).
- [ ] Complete and approve [Flight HUD & Navigation Information](../concepts/flight-hud-navigation-information.md).
- [ ] Reconcile all four Feature documents against the completed Concepts and resolve any remaining cross-concept ownership gaps.
- [ ] Confirm the exact Autopilot travel-profile capability required by M01; Fast is the current candidate but is not yet made normative by this milestone draft.
- [ ] Confirm the final-game target-selection interaction through the Navigation Targeting & Actions concept; right-click is a candidate interaction, not yet an approved rule.
- [ ] Review and explicitly approve the final M01 delivery scope before setting `Implementation Readiness` to `Ready`.

## Milestone Acceptance Criteria

M01 is successful when all of the following can be demonstrated in the delivered executable and supporting automated validation:

- [ ] Starting the sandbox provides an authored system containing the Sun, Earth, Moon and Mars in their defined celestial/orbital states.
- [ ] The celestial bodies continue to evolve according to the approved celestial/orbit model while the ship is being flown.
- [ ] A single placeholder ship can be translated and rotated manually under the approved Flight Physics.
- [ ] The player can enable/disable and exercise the M01-required Flight Assist behaviour.
- [ ] The player can establish a celestial navigation target.
- [ ] The interface shows current speed, selected target name, target distance, Flight Assist state and Autopilot state.
- [ ] The player can initiate Autopilot travel to an M01-supported celestial target.
- [ ] Autopilot operates through the authoritative physical ship state rather than through a presentation-only or shortcut movement model.
- [ ] At least one interplanetary travel case can be executed end-to-end and reaches the destination state required by the approved Autopilot and celestial/orbit Concepts.
- [ ] Manual input can regain control from Autopilot according to the approved rules.
- [ ] Optional debug instrumentation exposes acceleration-related vectors sufficient to inspect flight behaviour.
- [ ] The milestone can numerically validate relevant ship states such as position, velocity, orientation and rotational state without using rendered pixels as the source of truth.
- [ ] Core flight, Flight Assist and Autopilot behaviour can be exercised by automated tests without requiring the presentation layer to determine correctness.
- [ ] Controlled test scenarios produce reproducible results within the technical tolerances defined by architecture.
- [ ] Placeholder presentation is sufficient to distinguish the ship and the four required celestial bodies; production art is not required.
- [ ] Deferred capabilities are not required for M01 to answer its flight-model validation goal.

## Technical Handoff Gate

`Implementation Readiness` may change to `Ready` only when:

- [ ] the milestone goal and required Feature slices are explicit;
- [ ] all four included Feature documents exist;
- [ ] all gameplay Concepts required by the included slices are `Approved`;
- [ ] required cross-concept interactions are resolved in the relevant Feature documents;
- [ ] the M01 Autopilot-profile slice is explicitly decided;
- [ ] the required target-selection/action behaviour is owned by an approved Concept;
- [ ] no gameplay decision is left for Codex to invent;
- [ ] exclusions and deferred capabilities are explicit;
- [ ] milestone acceptance criteria are testable at product level;
- [ ] the project owner has explicitly approved the M01 scope.

Once this gate is satisfied, Codex may derive technical architecture for the milestone, including simulation/presentation separation, deterministic execution strategy, data definitions, debug/test instrumentation and automated test architecture.

## Change Log

| Version | Date | Change |
| --- | --- | --- |
| 0.1 | 2026-09-14 | Initial M01 Flight Sandbox draft from the agreed first-milestone requirements. |
