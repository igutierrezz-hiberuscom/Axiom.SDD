---
name: axiom-review
description: "Bootstrap review workflow for increments, bugs, or current workspace changes."
argument-hint: "Reference increment, bug, or change scope to review"
agent: agent
---
Read `AGENTS.md` first and treat it as canonical.

Use the user argument as the review target.

## Outcome-first routing contract

Keep the request classification and execution route separate:

- `flow`: `increment`, `bug`, `knowledge_only`, or `emergency`.
- `route`: `direct_inline`, `delegated_direct`, or `sdd`.

Choose `flow` from the intended outcome, then assess `route` from actual scope and risk. `direct_inline` is only for understood, small, low-risk work; `delegated_direct` is for investigation or worker-assisted work without SDD lifecycle; `sdd` is for substantial ambiguity, durable traceability, or an explicit SDD request. Direct routes do not create increments, SDD phases, synthetic artifacts, receipts, or persisted route records. If `sdd` is offered as an alternative, obtain explicit user acceptance before starting it; `axiom-autopilot` remains the SDD orchestrator. `flow=knowledge_only` reuses the current `axiom knowledge harvest --increment <id>` flow, and `flow=emergency` requires explicit confirmation and a visible scope and never enables auto-push.

When reviewing direct work, do not demand lifecycle artifacts that the route explicitly forbids. When reviewing SDD work, verify the related spec and acceptance criteria.

Execute this workflow:

1. Locate and read the related increment or bug spec when available.
2. Inspect current implementation changes in the relevant repository scope.
3. Compare implementation against acceptance criteria and original intent.
4. Review validation evidence and command coverage.
5. Detect deviations, missing checks, or unresolved risks.
6. Decide whether the work can be closed or should remain pending.
7. Update the canonical `Axiom.Spec/specs/00..08` files only if stable knowledge must be consolidated.
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
