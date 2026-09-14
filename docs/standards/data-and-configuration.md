# Data and Configuration Standard

**Status:** Approved  
**Version:** 1.0  
**Last Updated:** 2026-09-14

## Table of Contents

1. [Purpose](#purpose)
2. [Classification](#classification)
3. [Required Locations](#required-locations)
4. [Validation](#validation)
5. [Rules](#rules)
6. [Examples](#examples)
7. [Review Checklist](#review-checklist)

## Purpose

Ensure that gameplay/balance/configuration values can be inspected and changed without editing behavioural TypeScript code.

This standard implements [ADR-0002](../architecture/adr/ADR-0002-data-driven-tunable-values.md).

## Classification

Every non-trivial value introduced by implementation must be classified as one of:

1. **Game data** — content/balance values describing ships, weapons, modules, stations, world generation or similar domain content.
2. **Configuration** — application/system/runtime tuning such as camera, rendering or simulation configuration.
3. **Runtime state** — values produced by the running simulation.
4. **Intrinsic algorithmic constant** — a value inseparable from the algorithm/mathematical definition and not intended to be tuned.

## Required Locations

- Game data: `src/data/**`
- Configuration: `src/config/**`
- Type/validation definitions: `src/schemas/**`
- Runtime/behavioural code: appropriate TypeScript subsystem

Architecture documents define exact subpaths for each system.

## Validation

All externally stored game data/configuration consumed by production code must be validated against an explicit typed schema before use.

Validation must cover at least:
- required fields;
- numeric ranges where known;
- enum/discriminated values;
- identifier/reference validity where practical;
- units/semantic constraints where practical.

Invalid required core data must fail clearly rather than silently falling back to unrelated values.

## Rules

1. **DATA-001:** Tunable gameplay/balance values must not be embedded as unexplained numeric/string literals in production TypeScript.
2. **DATA-002:** Ship, weapon, module and comparable content definitions are data, not code.
3. **DATA-003:** Data/configuration is validated before becoming authoritative runtime input.
4. **DATA-004:** Units must be documented in schema/type naming or architecture when ambiguity exists.
5. **DATA-005:** Defaults must have one clear owner; do not duplicate a default in both JSON and TypeScript fallback logic unless architecture explicitly requires it.
6. **DATA-006:** IDs used for cross-file references must be stable and machine-readable.
7. **DATA-007:** A reviewer should be able to identify a balance change by inspecting data/config diffs without searching behavioural code.

## Examples

### Game data

```json
{
  "id": "fighter_mk1",
  "massKg": 12000,
  "baseHull": 1000,
  "maxThrustN": 180000
}
```

### Allowed in code

Values such as `Math.PI`, a conversion mathematically defined as `1000` metres per kilometre, or an algorithm's structural sentinel may remain in code when they are not balance/configuration knobs.

## Review Checklist

- Are new tunable values stored outside behavioural TypeScript?
- Is there schema validation?
- Are units explicit?
- Is there exactly one authoritative default/source?
- Do tests cover invalid/boundary data where relevant?
