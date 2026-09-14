# Concept Index

Concept documents are handbook chapters describing game/system behaviour.

## Concepts

- [Flight Physics](flight-physics.md) — **Approved** — inertial movement, thrust, rotation, gravity, collisions and structural loading.
- [Flight Assist](flight-assist.md) — **Approved** — manual-flight stabilization, braking, reference trajectories and position holding.
- [Autopilot](autopilot.md) — **Approved** — gravity-aware trajectory planning, rendezvous, orbital arrival and travel profiles.

When adding a concept:
1. copy [`../templates/concept.md`](../templates/concept.md);
2. place it in this directory with a stable kebab-case filename;
3. add it to this index;
4. add relative links to related concepts;
5. keep its status below `Approved` until explicitly approved.

Suggested early chapters include world scale, coordinate system, camera, parallax/environment rendering, ships, hardpoints, modules, combat, projectiles, targeting, energy, stations, NPCs, HUD, sensors/detection and ship editor.
