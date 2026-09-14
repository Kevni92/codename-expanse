# <System> Technical Architecture

**Status:** Draft  
**Version:** 0.1  
**Owner:** Technical Architecture  
**Last Updated:** YYYY-MM-DD

**Implements Concepts:**
- [Concept](../concepts/example.md)

**Related ADRs:**
- [ADR-0000 Example](../architecture/adr/ADR-0000-example.md)

## Table of Contents

1. [Purpose and Responsibility](#purpose-and-responsibility)
2. [Scope](#scope)
3. [Constraints and Invariants](#constraints-and-invariants)
4. [System Context](#system-context)
5. [Data Ownership and Model](#data-ownership-and-model)
6. [Units and Coordinate Spaces](#units-and-coordinate-spaces)
7. [Interfaces](#interfaces)
8. [Algorithms and Mathematical Model](#algorithms-and-mathematical-model)
9. [Runtime Behaviour](#runtime-behaviour)
10. [Data and Configuration](#data-and-configuration)
11. [Validation and Error Handling](#validation-and-error-handling)
12. [Performance Requirements](#performance-requirements)
13. [Determinism and Timing](#determinism-and-timing)
14. [Testing Requirements](#testing-requirements)
15. [Dependencies](#dependencies)
16. [Security and Trust Boundaries](#security-and-trust-boundaries)
17. [Alternatives and Trade-offs](#alternatives-and-trade-offs)
18. [Implementation Constraints](#implementation-constraints)
19. [Acceptance Criteria](#acceptance-criteria)
20. [Open Questions](#open-questions)
21. [Change Log](#change-log)

## Purpose and Responsibility
Define exactly what this technical subsystem owns.

## Scope
List included technical responsibilities and explicit non-responsibilities.

## Constraints and Invariants
Number normative constraints so Issues/reviews can reference them.

1. **A-<SHORT>-001:** ...
2. **A-<SHORT>-002:** ...

## System Context
Describe upstream/downstream systems and ownership boundaries. Link related architecture documents.

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

Approved architecture must not contain implementation-blocking open questions.

## Change Log
| Version | Date | Change |
| --- | --- | --- |
| 0.1 | YYYY-MM-DD | Initial draft |
