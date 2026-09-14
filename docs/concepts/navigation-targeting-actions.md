# Navigation Targeting & Actions

**Status:** Planned  
**Version:** 0.0  
**Owner:** Concept / Game Design  
**Last Updated:** 2026-09-14

**Required By:**
- [Autopilot Travel](../features/autopilot-travel.md)
- [Flight Navigation Interface](../features/flight-navigation-interface.md)

## Purpose of This Stub

This file intentionally reserves a gameplay concept that has been identified as required but has not yet been designed.

It is **not normative gameplay documentation**. It must be expanded through the normal concept-development workflow using [`concept.md`](../templates/concept.md) before it can move to `Draft`, `Review` or `Approved`.

Do not infer final gameplay behaviour from this stub.

## Intended Ownership

- Selection and persistence of navigation targets.
- Player-facing target actions such as requesting travel to a selected destination.
- Target eligibility and interaction boundaries between world objects, navigation and autopilot.
- Gameplay semantics of target changes, target loss and action availability.

## Why It Is Required

Autopilot Travel needs a defined source of destination intent, while Flight Navigation Interface needs a defined target state to present and act upon. The exact targeting interaction must be owned by a gameplay concept rather than by milestone UI or input code.

## Known Interaction Boundaries

- [Autopilot](autopilot.md) — consumes a valid destination and owns automated trajectory execution.
- [Celestial Bodies & Orbits](celestial-bodies-orbits.md) — provides moving celestial destinations relevant to navigation.
- [Autopilot Travel](../features/autopilot-travel.md) — composes target selection with automated travel.
- [Flight Navigation Interface](../features/flight-navigation-interface.md) — exposes target state and actions to the player.

## Design Work Required

- [ ] Run the normal structured concept-design workflow.
- [ ] Replace this stub with the full [`concept.md`](../templates/concept.md) structure.
- [ ] Resolve all implementation-blocking gameplay decisions.
- [ ] Reach explicit project-owner approval before marking the concept `Approved`.
