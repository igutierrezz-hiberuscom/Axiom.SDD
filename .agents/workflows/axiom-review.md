# Workflow: axiom-review

## Objective

Review an increment, bug, or current implementation scope for acceptance compliance and closure readiness.

## Inputs

- Reference to increment, bug, or current changes
- Optional acceptance criteria and target scope

## Outcome-first routing contract

Keep the request classification and execution route separate:

- `flow`: `increment`, `bug`, `knowledge_only`, or `emergency`.
- `route`: `direct_inline`, `delegated_direct`, or `sdd`.

Choose `flow` from the intended outcome, then assess `route` from actual scope and risk. `direct_inline` is only for understood, small, low-risk work; `delegated_direct` is for investigation or worker-assisted work without an SDD lifecycle; `sdd` is for substantial ambiguity, durable traceability, or an explicit SDD request. Direct routes do not create increments, SDD phases, synthetic artifacts, receipts, or persisted route records. If `sdd` is offered as an alternative, obtain explicit user acceptance before starting it; `axiom-autopilot` remains the SDD orchestrator. `flow=knowledge_only` reuses the current `axiom knowledge harvest --increment <id>` flow, and `flow=emergency` requires explicit confirmation and a visible scope and never enables auto-push.

## Phases

1. Read `AGENTS.md` (canonical rules).
2. Locate and read related increment or bug spec when available.
3. Inspect implementation changes in scope.
4. Compare implementation with acceptance criteria and stated intent.
5. Verify observed validation coverage and identify missing checks.
6. Detect deviations and unresolved risks.
7. Recommend closure state (`closed` or `pending`) with rationale.
8. Update `axiom-spec/general-spec.md` only when stable knowledge consolidation is appropriate.
9. Propose commit message aligned with review outcome.

## Stop Rules

- Do not recommend `closed` when acceptance criteria remain unmet.
- Keep findings evidence-based; avoid speculative conclusions.
- If validation evidence is missing, mark as pending unless risk is explicitly accepted.

## Outputs

- Compliance report
- Deviations
- Risks
- Validation observed
- Closure recommendation
- Suggested commit message
