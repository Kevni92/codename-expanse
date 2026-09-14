# Workflow: Architecture Development

## Goal
Produce an implementation-ready technical specification from approved concepts.

## Steps
1. Read [`../../AGENTS.md`](../../AGENTS.md), linked concepts, existing architecture and ADRs.
2. Identify responsibilities, ownership and system boundaries.
3. Define inputs, outputs, state and invariants.
4. Define data models, identifiers, units and coordinate spaces.
5. Define algorithms/formulas with exact numerical semantics where required.
6. Classify every tunable value as data, config or intrinsic algorithmic constant.
7. Define data/config validation expectations.
8. Define system interfaces and dependencies.
9. Define runtime and error behaviour.
10. Define deterministic requirements and simulation timing where relevant.
11. Define performance/complexity expectations.
12. Define unit, integration and minimal E2E requirements.
13. Document relevant alternatives/trade-offs.
14. Create/supersede an ADR for durable cross-cutting decisions.
15. Use [`../../docs/templates/architecture.md`](../../docs/templates/architecture.md).
16. Add/update the entry in [`../../docs/architecture/README.md`](../../docs/architecture/README.md).
17. Leave status below `Approved` until explicitly approved.

## Completion gate
An Implementer should not need to invent formulas, units, data ownership, contracts or architectural boundaries.
