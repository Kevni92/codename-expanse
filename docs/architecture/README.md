# Architecture Index

Architecture documents translate an Approved/Ready Milestone and its linked Features/Concepts into technical specifications used by implementation, review and QA.

The requirement chain is:

`Concepts -> Features -> Milestones -> Architecture`

- Concepts remain authoritative for final gameplay behaviour.
- Features define cross-concept capability composition.
- Milestones define the delivery slice to implement now.
- Architecture defines the technical realization of those approved requirements.

Architecture must not silently change gameplay rules, Feature composition or Milestone scope.

## Architecture Documents

No detailed subsystem architecture has been approved yet.

## Architecture Decision Records

See [`adr/README.md`](adr/README.md).

When adding Architecture:

1. use [`../templates/architecture.md`](../templates/architecture.md);
2. link the target Milestone;
3. link every implemented Feature and owning Concept;
4. define concrete units, formulas, ownership, contracts, validation, performance and tests;
5. add it to this index;
6. create an ADR for durable cross-cutting technical decisions;
7. keep status below `Approved` until explicitly approved.

If technical work exposes a missing gameplay rule, Feature handoff or Milestone scope decision, return it to the correct design layer instead of resolving it silently in Architecture.
