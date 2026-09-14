# Celestial Bodies & Orbits

**Status:** Planned  
**Version:** 0.0  
**Owner:** Concept / Game Design  
**Last Updated:** 2026-09-14

**Required By:**
- [Playable Star System](../features/playable-star-system.md)
- [Autopilot Travel](../features/autopilot-travel.md)

## Purpose of This Stub

This file intentionally reserves a gameplay concept that has been identified as required but has not yet been designed.

It is **not normative gameplay documentation**. It must be expanded through the normal concept-development workflow using [`concept.md`](../templates/concept.md) before it can move to `Draft`, `Review` or `Approved`.

Do not infer final gameplay behaviour from this stub.

## Intended Ownership

- Celestial-body definitions relevant to gameplay.
- Prescribed orbital motion and hierarchical orbital relationships.
- Deterministic celestial-body state as a function of simulation state/time.
- Gameplay ownership of standard orbital destinations required by navigation and autopilot.
- Boundaries between celestial motion, gravity and navigation systems.

## Why It Is Required

The Playable Star System feature requires a stable gameplay owner for moving celestial bodies and their orbital relationships. Autopilot Travel also requires destination motion and orbital-arrival context that must not be invented inside a feature or technical architecture document.

## Known Interaction Boundaries

- [Flight Physics](flight-physics.md) — owns ship motion and the already-approved gravity model; this concept must provide the celestial context used by that model without redefining flight physics.
- [Autopilot](autopilot.md) — consumes celestial destination state and orbital-arrival definitions.
- [Playable Star System](../features/playable-star-system.md) — composes celestial motion with ship physics into a traversable world.
- [Autopilot Travel](../features/autopilot-travel.md) — uses celestial destinations for physical interplanetary travel.

## Design Work Required

- [ ] Run the normal structured concept-design workflow.
- [ ] Replace this stub with the full [`concept.md`](../templates/concept.md) structure.
- [ ] Resolve all implementation-blocking gameplay decisions.
- [ ] Reach explicit project-owner approval before marking the concept `Approved`.
