# Workflow: Concept / Architecture to Issues

## Goal
Create an ordered implementation backlog from approved specifications.

## Steps
1. Read [`../../AGENTS.md`](../../AGENTS.md), Planner role and all relevant approved specifications.
2. Build a dependency graph of required capabilities.
3. Identify the smallest testable implementation slices.
4. Put contracts/schemas/foundations before consumers when necessary.
5. Create Issues using [`../../docs/templates/issue.md`](../../docs/templates/issue.md).
6. Link normative documents rather than copying them wholesale.
7. For each Issue define goal, scope, out-of-scope, dependencies, technical constraints, data/config changes, tests, acceptance criteria and definition of done.
8. Prefer unit/integration verification. Require Playwright only for critical browser journeys.
9. Ensure no Issue asks the Implementer to invent missing architecture.
10. Number/order dependencies in the Issue bodies and link predecessor Issues where available.

## Completion gate
A lower-capability coding model should be able to implement each Issue without making new system-design decisions.
