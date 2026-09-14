# Agents

Agent role definitions and reusable workflows for Codename Expanse.

The project design-to-delivery chain is:

`Concepts -> Features -> Milestones -> Technical Architecture -> Issues -> Implementation -> Review -> QA`

## Roles

- [Concept Writer](concept-writer.md) — gameplay Concepts plus Feature/Milestone design composition in ChatGPT.
- [Orchestrator](orchestrator.md) — validates an Approved/Ready Milestone and coordinates technical delivery.
- [Technical Architect](technical-architect.md)
- [Planner](planner.md)
- [Implementer](implementer.md)
- [Code Reviewer](code-reviewer.md)
- [QA / Verifier](qa-verifier.md)

## Workflows

### Design
- [Concept Development](workflows/concept-development.md)
- Feature/Milestone design is defined in [`../chatgpt/FEATURE_MILESTONE_WORKFLOW.md`](../chatgpt/FEATURE_MILESTONE_WORKFLOW.md)

### Technical delivery
- [Full Development Cycle](workflows/full-development-cycle.md)
- [Architecture Development](workflows/architecture-development.md)
- [Milestone / Architecture to Issues](workflows/concept-to-issues.md)
- [Issue Implementation](workflows/issue-implementation.md)
- [Pull Request Review](workflows/pull-request-review.md)
- [Review Fix Cycle](workflows/review-fix-cycle.md)
- [QA Verification](workflows/qa-verification.md)

Every agent must read [`../AGENTS.md`](../AGENTS.md) before its role file and respect the document ownership boundaries defined there.
