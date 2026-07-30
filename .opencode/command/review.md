# review

Run the Axiom Bootstrap review workflow for an increment, a bug, or current changes.

## Goal

Assess completion quality against acceptance criteria and recommend closure status.

## Input

Reference to an increment, bug, or change scope.

## Outcome-first routing contract

Keep the request classification and execution route separate:

- `flow`: `increment`, `bug`, `knowledge_only`, or `emergency`.
- `route`: `direct_inline`, `delegated_direct`, or `sdd`.

Choose `flow` from the intended outcome, then assess `route` from actual scope and risk. `direct_inline` is only for understood, small, low-risk work; `delegated_direct` is for investigation or worker-assisted work without an SDD lifecycle; `sdd` is for substantial ambiguity, durable traceability, or an explicit SDD request. Direct routes do not create increments, SDD phases, synthetic artifacts, receipts, or persisted route records. If `sdd` is offered as an alternative, obtain explicit user acceptance before starting it; `axiom-autopilot` remains the SDD orchestrator. `flow=knowledge_only` reuses the current `axiom knowledge harvest --increment <id>` flow, and `flow=emergency` requires explicit confirmation and a visible scope and never enables auto-push.

When reviewing direct work, do not demand lifecycle artifacts that the route explicitly forbids. When reviewing SDD work, verify the related spec and acceptance criteria.

## Required behavior

1. Read `AGENTS.md` first.
2. Locate the related increment or bug specification when available.
3. Inspect current implementation changes.
4. Compare outcomes with acceptance criteria and original intent.
5. Review validation evidence and identify gaps.
6. Detect deviations and unresolved risks.
7. Decide closure recommendation (`closed` or `pending` with reason).
8. Update `axiom-spec/general-spec.md` only when stable knowledge should be consolidated.
9. Propose a commit message consistent with the reviewed result.

## Output

- compliance summary
- deviations
- risks
- observed validation
- closure recommendation
- suggested commit message
