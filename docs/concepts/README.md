# Concept Index and Rules

Concept documents are the detailed, normative gameplay/system handbook for the final intended game.

A Concept answers:

> **How does this part of the game work?**

Concepts are intentionally independent from temporary prototype scope, a specific milestone or implementation strategy. If a gameplay rule should exist in the final game, its normative definition belongs in an owning Concept.

## What a Concept Is

A Concept:

- owns a coherent gameplay/system responsibility;
- defines intended final-game behaviour in detail;
- owns terminology, rules, invariants, gameplay states, parameters, feedback requirements and relevant edge cases for that system;
- defines enough behaviour that downstream Feature composition and technical architecture do not need to invent gameplay decisions;
- may be changed only through an explicit concept update and approval process.

## What a Concept Is Not

A Concept is **not**:

- a prototype specification;
- a milestone scope;
- a Feature composition document;
- a technical architecture document;
- an implementation plan or GitHub Issue;
- a place to describe temporary simplifications that contradict the intended final game.

Prototype or milestone delivery scope belongs under [`../milestones/`](../milestones/). Cross-concept player capabilities belong under [`../features/`](../features/).

## Planned Concept Stubs

Feature or Milestone work may reveal a required gameplay concept before that concept has been designed.

In that case:

1. create `docs/concepts/<topic>.md` using [`../templates/concept-stub.md`](../templates/concept-stub.md);
2. set **Status: Planned** and **Version: 0.0**;
3. state only the intended high-level ownership boundary and why the concept is required;
4. add it to this index;
5. link it from the Feature that requires it;
6. do **not** invent detailed gameplay rules in the stub.

A `Planned` concept is a dependency marker, not normative gameplay documentation.

When concept design begins, replace/expand the stub using [`../templates/concept.md`](../templates/concept.md) and move it to `Draft`.

## Concept Completion Gate

A Concept may be marked `Approved` only when:

- purpose, ownership and scope are explicit;
- final-game gameplay rules are sufficiently detailed and internally coherent;
- relevant parameters, states, player feedback and edge cases are resolved at the design level;
- related Concepts are linked and ownership boundaries are clear;
- no implementation-blocking gameplay question remains;
- acceptance criteria are meaningful;
- the project owner explicitly approves it.

Features and Milestones cannot grant approval to an unfinished Concept.

## Concepts

- [Flight Physics](flight-physics.md) — **Approved** — inertial movement, thrust, rotation, gravity, collisions and structural loading.
- [Flight Assist](flight-assist.md) — **Approved** — manual-flight stabilization, braking, reference trajectories and position holding.
- [Autopilot](autopilot.md) — **Approved** — gravity-aware trajectory planning, rendezvous, orbital arrival and travel profiles.
- [Celestial Bodies & Orbits](celestial-bodies-orbits.md) — **Draft** — celestial-body classification, environmental identity, prescribed/hierarchical orbital motion, multi-star barycenters and orbital destination context.
- [Player Flight Controls](player-flight-controls.md) — **Planned** — player input semantics for manual and assisted flight control.
- [Navigation Targeting & Actions](navigation-targeting-actions.md) — **Planned** — navigation-target selection, target state and player-facing navigation actions.
- [Flight HUD & Navigation Information](flight-hud-navigation-information.md) — **Planned** — player-facing flight/navigation information and its gameplay meaning.

## Adding a Concept

For active concept design:

1. use [`../templates/concept.md`](../templates/concept.md);
2. place it in this directory with a stable kebab-case filename;
3. add it to this index;
4. add relative links to related Concepts and Features;
5. keep its status below `Approved` until explicitly approved.

For a dependency identified but not yet designed, use the Planned Concept Stub process above.

Suggested future Concepts include world/orbits, coordinate/world scale, camera/presentation, ships, hardpoints, modules, combat, projectiles, targeting, energy, stations, NPCs, HUD/navigation, sensors/detection and ship editor. These suggestions are not themselves approved scope.
