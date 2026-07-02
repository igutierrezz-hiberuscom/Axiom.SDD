---
name: axiom-review
description: "Bootstrap review workflow for increments, bugs, or current workspace changes."
argument-hint: "Reference increment, bug, or change scope to review"
agent: agent
---
Read `AGENTS.md` first and treat it as canonical.

Use the user argument as the review target.

Execute this workflow:

1. Locate and read the related increment or bug spec when available.
2. Inspect current implementation changes in the relevant repository scope.
3. Compare implementation against acceptance criteria and original intent.
4. Review validation evidence and command coverage.
5. Detect deviations, missing checks, or unresolved risks.
6. Decide whether the work can be closed or should remain pending.
7. Update `axiom-spec/general-spec.md` only if stable knowledge must be consolidated.
8. Provide a suggested commit message aligned with actual outcomes.

Output format:

- compliance summary
- deviations
- risks
- observed validation
- closure recommendation (`closed` or `pending` with reason)
- suggested commit message

Validation rule:

- Do not invent validation commands.
- If no validation command exists, acknowledge best-effort review based on inspected changes and acceptance criteria.
