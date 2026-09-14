# Prototype Scope

**Status:** Draft  
**Version:** 0.1

## Table of Contents

1. [Goal](#goal)
2. [In Scope](#in-scope)
3. [Out of Scope](#out-of-scope)
4. [Quality Bar](#quality-bar)
5. [Technical Baseline](#technical-baseline)
6. [Delivery](#delivery)

## Goal

Build a polished, browser-only vertical prototype that proves the core simulation, rendering, ship fitting and combat interaction architecture before introducing server complexity.

## In Scope

Initial prototype work may include, as concepts are approved:
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

This list is directional, not an instruction to implement all items in the first Issue.

## Out of Scope

Unless explicitly added by a later approved concept:
- authoritative multiplayer server;
- account backend;
- persistent online economy;
- large-scale live service infrastructure;
- physical manual docking simulation.

## Quality Bar

The prototype is not disposable throwaway code. Core boundaries, data validation, deterministic simulation, testability and performance should be implemented with production-minded quality while avoiding premature enterprise complexity.

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

Pull requests must pass automated quality gates. After the executable application scaffold is introduced, merges to `main` should produce/update a GitHub Pages deployment for convenient browser inspection.
