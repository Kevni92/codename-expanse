# ADR-0001: Browser-First Client-Only Prototype

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

The first objective is a high-quality playable prototype. Server/multiplayer architecture is expected later but would add substantial complexity before the core simulation, rendering and interaction model are proven.

## Decision

The prototype runs completely in the browser and must not require an application server for gameplay execution.

The architecture should nevertheless keep authoritative simulation logic sufficiently separated from UI/rendering so that a future server-authoritative design is not unnecessarily blocked.

## Decision Drivers

- Fast iteration and easy inspection.
- Simple GitHub Pages delivery.
- Focus on proving gameplay and rendering architecture first.
- Avoid premature networking/backend complexity.

## Consequences

### Positive
- Simple local execution/deployment.
- Faster prototype iteration.
- Easier automated testing of pure simulation logic.

### Negative / Costs
- Browser performance/memory constraints apply.
- Current client state is not secure/authoritative for a future multiplayer game.
- Networking/persistence contracts still need later design.

## Alternatives Considered

### Server-first architecture
Rejected for the prototype because it would increase scope before core gameplay is validated.

## Compliance

A prototype feature violates this ADR if normal gameplay requires a custom backend/server process. External development tooling is not considered runtime dependency.

## Supersedes / Superseded By
- Supersedes: None
- Superseded by: None
