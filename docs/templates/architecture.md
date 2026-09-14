# <System> Technical Architecture

**Status:** Draft  
**Version:** 0.1  
**Owner:** Technical Architecture  
**Last Updated:** YYYY-MM-DD

**Target Milestone:**
- [Milestone](../milestones/mNN-example.md)

**Implements Features:**
- [Feature](../features/example.md)

**Implements Concepts:**
- [Concept](../concepts/example.md)

**Related ADRs:**
- [ADR-0000 Example](../architecture/adr/ADR-0000-example.md)

## Table of Contents

1. [Purpose and Responsibility](#purpose-and-responsibility)
2. [Requirement Traceability](#requirement-traceability)
3. [Scope](#scope)
4. [Constraints and Invariants](#constraints-and-invariants)
5. [System Context](#system-context)
6. [Data Ownership and Model](#data-ownership-and-model)
7. [Units and Coordinate Spaces](#units-and-coordinate-spaces)
8. [Interfaces](#interfaces)
9. [Algorithms and Mathematical Model](#algorithms-and-mathematical-model)
10. [Runtime Behaviour](#runtime-behaviour)
11. [Data and Configuration](#data-and-configuration)
12. [Validation and Error Handling](#validation-and-error-handling)
13. [Performance Requirements](#performance-requirements)
14. [Determinism and Timing](#determinism-and-timing)
15. [Testing Requirements](#testing-requirements)
16. [Dependencies](#dependencies)
17. [Security and Trust Boundaries](#security-and-trust-boundaries)
18. [Alternatives and Trade-offs](#alternatives-and-trade-offs)
19. [Implementation Constraints](#implementation-constraints)
20. [Acceptance Criteria](#acceptance-criteria)
21. [Open Questions](#open-questions)
22. [Change Log](#change-log)

## Purpose and Responsibility
Define exactly what this technical subsystem owns.

Architecture owns technical realization only. It must preserve Concept-owned gameplay behaviour, Feature composition/handoffs and target Milestone scope.

## Requirement Traceability
Trace the technical subsystem to the selected delivery requirements.

| Milestone requirement / Feature slice | Feature | Owning Concept(s) | Architecture section |
| --- | --- | --- | --- |
| `<required capability>` | [Feature](../features/example.md) | [Concept](../concepts/example.md) | `<section>` |

Do not use Architecture to fill a missing gameplay rule, Feature interaction or Milestone scope decision. Return those gaps to the owning design layer.

## Scope
List included technical responsibilities and explicit non-responsibilities. Preserve the target Milestone's deferred/out-of-scope capabilities.

## Constraints and Invariants
Number normative technical constraints so Issues/reviews can reference them.

1. **A-<SHORT>-001:** ...
2. **A-<SHORT>-002:** ...

## System Context
Describe upstream/downstream systems and ownership boundaries. Link related Architecture documents.

## Data Ownership and Model
Define entities/value objects/state, identifiers, lifecycle and source of truth.

Use concrete tables when useful:

| Field | Type | Unit | Required | Source | Constraints |
| --- | --- | --- | --- | --- | --- |
| `<field>` | `<type>` | `<unit>` | Yes | Data/Config/Runtime | ... |

## Units and Coordinate Spaces
Define units and reference frames explicitly. Prefer SI units unless this document establishes a justified alternative.

## Interfaces
Define inputs, outputs, events/commands/queries and public contracts. Include preconditions/postconditions where important.

## Algorithms and Mathematical Model
Specify implementation-critical formulas precisely.

Example form:

```text
acceleration_mps2 = thrust_N / mass_kg
velocity_mps_next = velocity_mps + acceleration_mps2 * dt_s
```

For every formula define:
- input units;
- output units;
- clamping/overflow/precision rules;
- update order when order matters;
- exceptional/boundary behaviour.

## Runtime Behaviour
Describe lifecycle, update order and state transitions from a technical perspective.

## Data and Configuration
Every tunable value must be classified and assigned a target location.

| Value/group | Classification | Target | Validation | Default/source |
| --- | --- | --- | --- | --- |
| ship definitions | Game data | `src/data/ships/*.json` | schema | content file |
| simulation tuning | Config | `src/config/...` | schema | config file |

Production TypeScript must not contain tunable balance/config magic numbers.

## Validation and Error Handling
Define schema validation, invalid-data behaviour, invariants and failure policy.

## Performance Requirements
Define measurable budgets/complexity expectations where relevant, e.g. target entity counts, per-frame/per-tick constraints, allocation rules, culling or spatial-query expectations.

## Determinism and Timing
Define fixed/variable timesteps, ordering, randomness/seeding and replay/server-readiness constraints where relevant.

## Testing Requirements
### Unit Tests
List deterministic logic and edge cases to test.

### Integration Tests
List system boundaries that need focused integration coverage.

### Playwright / E2E
List only critical browser journeys that genuinely require E2E. State `None required` when lower-level tests suffice.

### Performance / Regression Tests
Define only when justified.

## Dependencies
List internal/external dependencies and why they are needed.

## Security and Trust Boundaries
For browser-only systems this may be brief, but note untrusted loaded data, future server-authority implications or dangerous assumptions where relevant.

## Alternatives and Trade-offs
Record significant considered alternatives and why the selected approach wins.

## Implementation Constraints
List rules the Planner/Implementer must preserve.

## Acceptance Criteria
- [ ] Architecture-level criterion ...

## Open Questions
- [ ] ...

Approved Architecture must not contain implementation-blocking technical questions and must not hide unresolved product/gameplay questions.

## Change Log
| Version | Date | Change |
| --- | --- | --- |
| 0.1 | YYYY-MM-DD | Initial draft |
