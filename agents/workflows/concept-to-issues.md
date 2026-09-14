# Workflow: Milestone / Architecture to Issues

## Goal
Create an ordered implementation backlog from an Approved/Ready Milestone and its approved technical specifications.

## Inputs
- target Milestone with `Implementation Readiness: Ready`;
- included Feature documents and required Feature slices;
- Approved Concepts required by those slices;
- approved Architecture/ADRs.

## Steps
1. Read [`../../AGENTS.md`](../../AGENTS.md), Planner role, the target Milestone and all linked relevant specifications.
2. Trace Milestone requirements through Features to their owning Concepts and Architecture.
3. Build a dependency graph of required capabilities.
4. Identify the smallest testable implementation slices that remain inside Milestone scope.
5. Put contracts/schemas/foundations before consumers when necessary.
6. Create Issues using [`../../docs/templates/issue.md`](../../docs/templates/issue.md).
7. Link the Milestone, Feature, Concept and Architecture owners rather than copying specifications wholesale.
8. For each Issue define goal, scope, out-of-scope, dependencies, technical constraints, data/config changes, tests, acceptance criteria and definition of done.
9. Prefer unit/integration verification. Require Playwright only for critical browser journeys.
10. Ensure no Issue asks the Implementer to invent missing gameplay rules, Feature handoffs, Milestone scope or Architecture.
11. Number/order dependencies in the Issue bodies and link predecessor Issues where available.

## Completion gate
A lower-capability coding model should be able to implement each Issue without making new product, gameplay or system-design decisions, and the complete Issue set should cover the target Milestone without silently broadening it.
