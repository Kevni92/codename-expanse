# Codename Expanse Handbook

This directory is the normative project handbook. Documents are structured and cross-linked so humans and AI agents can navigate design, composition, delivery scope and technical implementation without mixing their responsibilities.

## Table of Contents

1. [Vision](#vision)
2. [Documentation Hierarchy](#documentation-hierarchy)
3. [Concepts](#concepts)
4. [Features](#features)
5. [Milestones](#milestones)
6. [Technical Architecture](#technical-architecture)
7. [Templates](#templates)
8. [Ownership and Conflict Rules](#ownership-and-conflict-rules)
9. [Document Rules](#document-rules)
10. [Status Model](#status-model)

## Vision

- [Game Vision](vision/game-vision.md)
- [Prototype Scope](vision/prototype-scope.md)

Vision documents describe long-term product direction and broad development intent. Concrete delivery composition belongs to Milestones.

## Documentation Hierarchy

The game-design delivery chain is:

`Concepts -> Features -> Milestones -> Technical Architecture -> Issues -> Implementation`

These layers answer different questions:

| Layer | Primary question | May define final gameplay rules? |
| --- | --- | --- |
| Concept | How does this game system work in the final game? | **Yes — normative owner** |
| Feature | How do multiple concepts combine into one coherent player capability? | No; must link to concept owners |
| Milestone | Which multiple features or feature slices are delivered and validated together now? | No |
| Architecture | How are approved requirements implemented technically? | No gameplay changes |
| Issue | What bounded implementation work is performed? | No |

## Concepts

See the [Concept Index](concepts/README.md).

Concepts are the authoritative gameplay/system handbook. They define the intended final-game behaviour in enough detail that downstream work does not need to invent product rules.

A concept is not a prototype or milestone document. Temporary delivery scope must never be used to weaken or silently redefine the final-game concept.

## Features

See the [Feature Index and Rules](features/README.md).

Features compose multiple concepts into coherent player-facing capabilities. They explain how concept responsibilities interact end-to-end while preserving each concept as the normative owner of its rules.

A Feature may expose missing Concepts. Missing required Concepts are created as `Planned` stubs and must be fully developed before the Feature can be complete/Approved.

## Milestones

See the [Milestone Index and Rules](milestones/README.md).

Milestones compose multiple Features into a concrete delivery and validation target. They define what is required now, what is deferred, dependency blockers and milestone-level success criteria.

Milestones do not redefine the final game. Deferring a Feature capability from one Milestone does not remove it from the Feature or underlying Concepts.

## Technical Architecture

See the [Architecture Index](architecture/README.md).

Architecture documents define how approved gameplay requirements are implemented: ownership, data, units, formulas, interfaces, algorithms, constraints, validation, performance and tests.

Architecture Decision Records live under [`architecture/adr/`](architecture/adr/).

Architecture and ADRs may make technical decisions, but they may not silently alter approved gameplay behaviour. A required gameplay change must return to the owning Concept.

## Templates

- [Concept Template](templates/concept.md)
- [Planned Concept Stub](templates/concept-stub.md)
- [Feature Template](templates/feature.md)
- [Milestone Template](templates/milestone.md)
- [Architecture Template](templates/architecture.md)
- [ADR Template](templates/adr.md)
- [Implementation Issue Template](templates/issue.md)
- [Review Template](templates/review.md)

## Ownership and Conflict Rules

There is no single global priority list that allows one documentation layer to overwrite another. Authority is separated by concern:

1. **Final gameplay behaviour:** the owning Approved Concept is authoritative.
2. **Cross-concept capability composition:** the owning Approved Feature is authoritative only for composition and handoffs; it cannot override Concepts.
3. **Delivery scope:** the owning Approved Milestone is authoritative for what is delivered in that milestone; it cannot override Features or Concepts.
4. **Technical implementation:** Approved architecture and ADRs are authoritative for implementation details within the gameplay/product constraints above.
5. **Implementation tasks:** GitHub Issues scope work but cannot change higher-level requirements.

If a lower layer needs behaviour that conflicts with a higher ownership layer, update the owning document explicitly rather than silently overriding it.

## Document Rules

### Linking

Use relative Markdown links for internal references.

Example:

```md
See [Flight Physics](concepts/flight-physics.md) and its
[Linear Movement](concepts/flight-physics.md#linear-movement) section.
```

Do not refer to an existing project document only by plain text when a stable document/heading exists.

### Single source of truth

A gameplay rule has one owning Concept. Features link and compose; Milestones scope; architecture implements.

Do not duplicate normative rules across layers.

### Concrete specifications

Implementation-critical gameplay rules must ultimately be concrete in the owning Approved Concept. Technical implementation details belong to Architecture.

Use:

- SI units unless an approved architecture document defines another unit;
- exact formulas where implementation algorithms require them;
- explicit ranges/defaults/constraints;
- examples for non-obvious transformations;
- defined coordinate spaces and time bases.

### Tunable values

Values intended for balancing/configuration are ultimately stored outside production TypeScript in validated data/configuration files. Concepts define intended gameplay semantics; architecture defines executable representation and ownership; runtime data becomes the executable source once implemented.

### Table of contents

Every substantial Concept, Feature, Milestone and Architecture document must contain a manually readable table of contents with relative heading links.

## Status Model

Design/handbook documents use one of:

- **Planned** — identified and intentionally incomplete; may be a dependency placeholder and is not normative.
- **Draft** — actively being designed; not normative.
- **Review** — believed complete enough for review; not yet final.
- **Approved** — explicitly approved and normative within that document type's ownership boundary.
- **Deprecated** — retained for history but must not drive new work.
- **Superseded** — replaced by a named newer document.

For Concepts specifically, a `Planned` file may be a minimal stub created because a Feature or Milestone exposed a missing required game system. It must be expanded through the normal concept workflow before approval.

Milestones additionally declare **Implementation Readiness** as `Blocked` or `Ready`. An Approved milestone scope can still be `Blocked` when required Features or Concepts are unfinished.
