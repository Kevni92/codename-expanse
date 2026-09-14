# ADR-0004: Simulation Is Independent From Rendering and UI

**Status:** Accepted  
**Date:** 2026-09-14  
**Decision Owners:** Project Owner / Technical Architecture

## Table of Contents

1. [Context](#context)
2. [Decision](#decision)
3. [Decision Drivers](#decision-drivers)
4. [Consequences](#consequences)
5. [Alternatives Considered](#alternatives-considered)
6. [Compliance](#compliance)
7. [Supersedes / Superseded By](#supersedes--superseded-by)

## Context

The game requires large-world simulation, multiple render views/cameras, long-lived projectiles, deterministic physics testing and a possible future authoritative server. Treating sprites/UI components as gameplay state would make these goals fragile.

## Decision

Authoritative gameplay state and rules live in simulation/domain systems independent of rendering and UI. Rendering consumes simulation state (or derived render snapshots) and must not become the source of truth for gameplay position, velocity, damage, targeting or similar state.

UI emits commands/intents and displays state; it must not own simulation rules.

## Decision Drivers

- Multiple cameras/views of one world.
- Headless unit testing.
- Future server-readiness.
- Deterministic simulation.
- Rendering optimization/culling without changing gameplay.

## Consequences

### Positive
- Simulation can execute without a browser renderer.
- Rendering can use interpolation/culling/LOD safely.
- Secondary target views are easier to support.

### Negative / Costs
- Explicit boundaries/adapters are needed.
- Some display state must be derived/synchronized instead of mutated directly on sprites.

## Alternatives Considered

### Sprite-centric game state
Rejected because rendered objects would become tightly coupled to authoritative simulation and camera lifecycle.

## Compliance

A reviewer must reject gameplay correctness that depends on sprite/UI position/state being authoritative. Rendering-side interpolation or effects may alter presentation but not authoritative simulation state.

## Supersedes / Superseded By
- Supersedes: None
- Superseded by: None
