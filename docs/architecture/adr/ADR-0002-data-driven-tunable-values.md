# ADR-0002: Data-Driven Tunable Values

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

Ship/module/weapon/world values will change frequently during prototyping and balancing. Embedding such values in behavioural TypeScript would make balancing harder, obscure reviews and couple content to code changes.

## Decision

Gameplay content, balance values and tunable runtime/application settings must be stored in dedicated data/configuration files and validated before use.

Default target ownership:
- game content/balance → `src/data/**` JSON;
- runtime/application/system tuning → `src/config/**`;
- validation/type definitions → `src/schemas/**`.

Intrinsic mathematical/algorithmic constants that are not tuning knobs may remain in code.

See the normative [Data and Configuration Standard](../../standards/data-and-configuration.md).

## Decision Drivers

- Fast balancing without behavioural code edits.
- Clear review diffs.
- Future tooling/editors/modding potential.
- Reliable validation of content.

## Consequences

### Positive
- Content and behaviour are clearly separated.
- Balance changes are discoverable.
- Automated validation can catch malformed definitions.

### Negative / Costs
- Schema/loader infrastructure is required.
- Cross-file references need validation/discipline.

## Alternatives Considered

### TypeScript object literals as content
Rejected as the default because content changes would remain coupled to source code and bundling semantics.

## Compliance

A reviewer should flag tunable balance/config values hardcoded in production behavioural TypeScript unless an approved architecture document proves they are intrinsic algorithm constants.

## Supersedes / Superseded By
- Supersedes: None
- Superseded by: None
