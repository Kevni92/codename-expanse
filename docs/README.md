# Codename Expanse Handbook

This directory is the normative project handbook. Documents are intentionally structured and cross-linked so humans and AI agents can navigate the design as a connected specification.

## Table of Contents

1. [Vision](#vision)
2. [Concepts](#concepts)
3. [Technical Architecture](#technical-architecture)
4. [Templates](#templates)
5. [Document Rules](#document-rules)
6. [Status Model](#status-model)

## Vision

- [Game Vision](vision/game-vision.md)
- [Prototype Scope](vision/prototype-scope.md)

## Concepts

See the [Concept Index](concepts/README.md).

Concepts define what a system does from a game/product perspective. They should not own low-level implementation architecture.

## Technical Architecture

See the [Architecture Index](architecture/README.md).

Architecture documents define how approved concepts are implemented: ownership, data, units, formulas, interfaces, algorithms, constraints, validation, performance and tests.

Architecture Decision Records live under [`architecture/adr/`](architecture/adr/).

## Templates

- [Concept Template](templates/concept.md)
- [Architecture Template](templates/architecture.md)
- [ADR Template](templates/adr.md)
- [Implementation Issue Template](templates/issue.md)
- [Review Template](templates/review.md)

## Document Rules

### Linking
Use relative Markdown links for internal references.

Example:

```md
See [Flight Physics](../concepts/flight-physics.md) and its
[Inertial Flight](../concepts/flight-physics.md#inertial-flight) section.
```

Do not refer to an existing project concept only by plain text when a stable document/heading exists.

### Single source of truth
A rule should have one owning document. Other documents link to it rather than creating subtly different copies.

### Concrete specifications
Implementation-critical rules must be concrete. Use:
- SI units unless an approved architecture document defines another unit.
- exact formulas where algorithms depend on them;
- explicit ranges/defaults/constraints;
- examples for non-obvious transformations;
- defined coordinate spaces and time bases.

### Tunable values
Values intended for balancing/configuration are ultimately stored outside production TypeScript in validated data/configuration files. Architecture documents define the initial values and ownership; runtime data files become the executable source once implemented.

### Table of contents
Every substantial concept and architecture document must include a manually readable table of contents with relative heading links.

## Status Model

Documents use one of:
- **Draft** — actively being designed; not normative.
- **Review** — believed complete enough for review; not yet final.
- **Approved** — normative and may be used for implementation/review.
- **Deprecated** — retained for history but must not drive new work.
- **Superseded** — replaced by a named newer document/ADR.

Changing approved behaviour requires an explicit document update and, for durable cross-cutting technical decisions, an ADR.
