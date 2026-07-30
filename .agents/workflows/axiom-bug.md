# Workflow: axiom-bug

## Objective

Resolve a bug with expected-behavior-first discipline, minimal code changes, and clear closure evidence.

## Inputs

- Bug description
- Optional reproduction details
- Optional expected behavior constraints

## Outcome-first routing contract

Classify the request on two independent axes before acting:

- `flow`: `increment`, `bug`, `knowledge_only`, or `emergency`.
- `route`: `direct_inline`, `delegated_direct`, or `sdd`.

Choose the outcome (`flow`) first, then choose the route from actual scope and risk. `direct_inline` is for understood, small, low-risk changes; `delegated_direct` is for investigation or worker-assisted changes without an SDD lifecycle; `sdd` is for substantial ambiguity, durable traceability, or an explicit SDD request. Direct routes do not create increments, SDD phases, synthetic artifacts, receipts, or persisted route records. If `sdd` is offered as an alternative, obtain explicit user acceptance before starting it; `axiom-autopilot` remains the SDD orchestrator. `flow=knowledge_only` reuses `axiom knowledge harvest --increment <id>` and does not create an increment or bug. `flow=emergency` requires explicit confirmation and a visible scope and never enables auto-push.

## Route execution gate

Run the phases below only when `flow=bug` and `route=sdd`. For `direct_inline`, perform only the bounded fix and return without creating a spec, SDD phase, synthetic artifact, receipt, or persisted route record. For `delegated_direct`, delegate only the narrow implementation or exploration needed and return without entering the SDD lifecycle. For `flow=knowledge_only`, invoke `axiom knowledge harvest --increment <id>` and stop after reporting its result. For `flow=emergency`, require explicit confirmation and a visible scope before any mutation; if either is missing, stop with a decision request. Never enable auto-push.

## Phases

1. Read `AGENTS.md` (canonical rules).
2. Understand symptom and impact.
3. Locate `axiom-spec` in the parent workspace.
4. Create or update bug spec in `axiom-spec/bugs/` (or equivalent path).
5. Define current behavior, expected behavior, impact, reproduction steps, suspected cause, and acceptance criteria.
6. Ask critical blocking questions when expected behavior is unclear.
7. Produce short internal plan.
8. Implement minimal focused fix in `axiom-sdd`.
9. Validate fix and add regression coverage when applicable.
10. Review against expected behavior and acceptance criteria.
11. Integrate stable behavior updates into `axiom-spec/general-spec.md` when needed.
12. Set final status to `closed` or `pending` with explicit rationale.
13. Emit concise execution summary.

## Stop Rules

- Do not implement a bug fix until the expected behavior is clear enough.
- Stop and request clarification when expected behavior cannot be distinguished from current behavior.
- Keep `Status: pending` when closure conditions are not fully satisfied.

## Outputs

- Bug created or refined in `axiom-spec`
- Minimal fix implemented in `axiom-sdd`
- Validation or regression evidence (when applicable)
- Review against expected behavior
- `general-spec.md` updated when stable behavior changed
- Final status and next step
