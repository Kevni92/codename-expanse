# Flight HUD & Navigation Information

**Status:** Planned  
**Version:** 0.0  
**Owner:** Concept / Game Design  
**Last Updated:** 2026-09-14

**Required By:**
- [Flight Navigation Interface](../features/flight-navigation-interface.md)

## Purpose of This Stub

This file intentionally reserves a gameplay concept that has been identified as required but has not yet been designed.

It is **not normative gameplay documentation**. It must be expanded through the normal concept-development workflow using [`concept.md`](../templates/concept.md) before it can move to `Draft`, `Review` or `Approved`.

Do not infer final gameplay behaviour from this stub.

## Intended Ownership

- Player-facing flight and navigation information that must be available during normal gameplay.
- Presentation requirements for velocity, navigation-target information and automated/assisted flight state at the gameplay-design level.
- Information priority and semantic meaning independent from final visual styling or UI implementation.

## Why It Is Required

The Flight Navigation Interface feature needs a durable gameplay owner for the information the player must receive while flying and navigating. Temporary debug instrumentation and final visual styling remain outside this concept unless they become intended player-facing behaviour.

## Known Interaction Boundaries

- [Flight Physics](flight-physics.md) — supplies physical state that may require player-facing representation.
- [Flight Assist](flight-assist.md) — supplies assisted-flight mode/state that may require player feedback.
- [Autopilot](autopilot.md) — supplies automated-travel state and route information that may require player feedback.
- [Navigation Targeting & Actions](navigation-targeting-actions.md) — owns the selected navigation target and target actions.
- [Flight Navigation Interface](../features/flight-navigation-interface.md) — composes these information sources into a usable player-facing interface.

## Design Work Required

- [ ] Run the normal structured concept-design workflow.
- [ ] Replace this stub with the full [`concept.md`](../templates/concept.md) structure.
- [ ] Resolve all implementation-blocking gameplay decisions.
- [ ] Reach explicit project-owner approval before marking the concept `Approved`.
