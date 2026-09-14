# <Implementation Task>

## Context
Why this Issue exists, which Milestone requirement it advances and which Feature capability it implements.

## Requirement References
- Milestone: [`<document>`](../milestones/mNN-example.md)
- Feature: [`<document>`](../features/example.md)
- Concept: [`<document>`](../concepts/example.md)
- Architecture: [`<document>`](../architecture/example.md)
- ADR: [`<document>`](../architecture/adr/ADR-0000-example.md)

Reference exact headings/rule IDs where useful.

Concepts own gameplay behaviour. Features own capability composition. Milestones own current delivery scope. Architecture/ADRs own technical implementation.

## Goal
One concise statement of the testable outcome within the target Milestone.

## Dependencies
- Depends on #...
- Blocks #...

Use `None` when there are no dependencies.

## Scope
- ...

## Out of Scope
- ...

Preserve Milestone deferrals and do not remove deferred capability from the final Feature/Concept.

## Technical Requirements
List exact constraints the Implementer must follow. Do not repeat whole documents.

- ...

## Data / Configuration
List new/changed JSON/config/schema artifacts and initial values relevant to this Issue.

- ...

Use `None` if no data/config changes are required.

## Expected Behaviour
Describe concrete inputs -> behaviour -> outputs/state changes as already required by the linked design documents.

Do not invent missing gameplay or Feature-interaction behaviour here.

## Edge Cases
- ...

## Tests
### Unit
- ...

### Integration
- ...

### Playwright / E2E
- None required; or one/few justified critical flows.

## Acceptance Criteria
- [ ] ...
- [ ] ...

Every criterion must be observable/verifiable and remain inside target Milestone scope.

## Definition of Done
- [ ] Implementation matches the target Milestone, Feature, Concept and Architecture references.
- [ ] No undocumented scope expansion.
- [ ] No gameplay rule is invented or changed inside implementation.
- [ ] No tunable gameplay/config values are hardcoded in production TypeScript.
- [ ] Data/config changes are schema validated.
- [ ] Required unit/integration tests pass.
- [ ] Required minimal Playwright tests pass, if any.
- [ ] Typecheck/lint/build pass.
- [ ] Documentation is updated if required by the Issue.
