# Prototype Scope

**Status:** Draft  
**Version:** 0.2

## Table of Contents

1. [Goal](#goal)
2. [Relationship to Concepts Features and Milestones](#relationship-to-concepts-features-and-milestones)
3. [Directional Prototype Scope](#directional-prototype-scope)
4. [Out of Scope](#out-of-scope)
5. [Quality Bar](#quality-bar)
6. [Technical Baseline](#technical-baseline)
7. [Delivery](#delivery)

## Goal

Build a polished, browser-only prototype program that progressively proves the core simulation and player experience before introducing server complexity.

This document defines broad prototype direction. It is **not** the scope contract for an individual development milestone.

## Relationship to Concepts Features and Milestones

The project uses:

`Concepts -> Features -> Milestones`

- [Concepts](../concepts/README.md) define detailed intended final-game behaviour.
- [Features](../features/README.md) compose multiple Concepts into coherent player-facing capabilities.
- [Milestones](../milestones/README.md) define concrete delivery/validation steps and may deliberately implement only selected Feature capabilities.

A prototype Milestone must not redefine a Concept merely because that Milestone implements only part of the final game.

Concrete questions such as "what is included in Milestone 1?" belong exclusively in the relevant document under `docs/milestones/`.

## Directional Prototype Scope

Across one or more Milestones, browser prototype work may include, as the required Concepts and Features mature:

- top-down ship flight;
- inertial simulation and flight assists;
- large-world coordinates/travel;
- camera and parallax layers;
- lighting/shadow presentation;
- ship hardpoints/modules;
- targeting and target view;
- basic weapons/projectiles;
- selected NPC behaviour;
- selected station interaction;
- compact HUD;
- ship editor;
- procedural sample system content.

This list is intentionally directional. It does not require any item in a particular Milestone and does not authorize Codex to implement the complete list as one scope.

## Out of Scope

Unless explicitly added by later approved design:

- authoritative multiplayer server;
- account backend;
- persistent online economy;
- large-scale live-service infrastructure;
- physical manual docking simulation.

## Quality Bar

The prototype is not disposable throwaway code. Core boundaries, data validation, deterministic simulation, testability and performance should be implemented with production-minded quality while avoiding premature enterprise complexity.

A smaller Milestone scope is preferred over weakening these quality expectations.

## Technical Baseline

- TypeScript
- Vite
- Vue for application/UI
- browser-first client-only runtime
- data-driven JSON content/configuration with validation
- Vitest-first testing
- deliberately small Playwright smoke suite

Any major change to this baseline should be captured by an ADR.

## Delivery

Each concrete delivery target is defined under [Milestones](../milestones/README.md).

A Milestone becomes eligible for normal Codex technical handoff when its required Feature slices resolve to sufficiently complete/Approved gameplay design and its document declares `Implementation Readiness: Ready`.

Pull requests must pass automated quality gates. After the executable application scaffold is introduced, merges to `main` should produce/update a GitHub Pages deployment for convenient browser inspection.

## Change Log

| Version | Date | Change |
| --- | --- | --- |
| 0.2 | 2026-09-14 | Clarified that this document is directional vision and concrete prototype delivery scope belongs to Milestones. |
| 0.1 | 2026-09-14 | Initial prototype scope. |
