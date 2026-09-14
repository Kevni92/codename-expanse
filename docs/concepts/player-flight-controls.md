# Player Flight Controls

**Status:** Planned  
**Version:** 0.0  
**Owner:** Concept / Game Design  
**Last Updated:** 2026-09-14

**Required By:**
- [Manual Space Flight](../features/manual-space-flight.md)

## Purpose of This Stub

This file intentionally reserves a gameplay concept that has been identified as required but has not yet been designed.

It is **not normative gameplay documentation**. It must be expanded through the normal concept-development workflow using [`concept.md`](../templates/concept.md) before it can move to `Draft`, `Review` or `Approved`.

Do not infer final gameplay behaviour from this stub.

## Intended Ownership

- Player input semantics for manual translational and rotational flight.
- Player-facing commands for Flight Assist, braking and related manual-flight actions.
- Priority and handoff rules between manual player intent and automated flight modes where those rules are not already owned by the automated system concept.
- Control-level terminology independent from any specific keyboard, mouse or controller binding implementation.

## Why It Is Required

Manual Space Flight combines Flight Physics and Flight Assist, but a separate gameplay owner is required for how player intent is expressed as flight commands. Those controls must not be invented by a milestone, UI implementation or technical architecture.

## Known Interaction Boundaries

- [Flight Physics](flight-physics.md) — owns physical ship response to forces and torques.
- [Flight Assist](flight-assist.md) — owns assisted-flight behaviour after player commands are interpreted.
- [Autopilot](autopilot.md) — already defines automated-flight cancellation/handoff behaviour that manual controls must respect.
- [Manual Space Flight](../features/manual-space-flight.md) — composes player control intent with physical and assisted flight.

## Design Work Required

- [ ] Run the normal structured concept-design workflow.
- [ ] Replace this stub with the full [`concept.md`](../templates/concept.md) structure.
- [ ] Resolve all implementation-blocking gameplay decisions.
- [ ] Reach explicit project-owner approval before marking the concept `Approved`.
