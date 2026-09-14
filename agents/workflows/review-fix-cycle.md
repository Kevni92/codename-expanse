# Workflow: Review Fix Cycle

## Goal
Resolve review findings without introducing unrelated redesign.

## Steps
1. Read each review finding and classify it as accepted, disputed or specification-gap.
2. For accepted findings, implement the smallest compliant fix.
3. Add/update the lowest-level regression test capable of proving the fix.
4. Do not respond to a review by changing normative architecture unless the review identifies a genuine specification problem.
5. For disputed findings, cite the exact specification/code evidence.
6. For specification gaps, stop that part of implementation and route it back to concept/architecture work.
7. Re-run relevant checks and the required final suite.
8. Reply with concise evidence for each resolved blocking finding.
9. Request re-review when all required findings are resolved.
