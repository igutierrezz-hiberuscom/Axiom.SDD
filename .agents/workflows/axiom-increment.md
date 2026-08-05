# Workflow: axiom-increment

## Objective

Deliver an increment using Axiom Bootstrap Orchestrator Mode with lightweight spec refinement, focused implementation, and explicit closure.

## Inputs

- Free-form increment description
- Optional constraints, risks, and acceptance notes from the user

## Outcome-first routing contract

Classify the request on two independent axes before acting:

- `flow`: `increment`, `bug`, `knowledge_only`, or `emergency`.
- `route`: `direct_inline`, `delegated_direct`, or `sdd`.

Choose the outcome (`flow`) first, then choose the route from actual scope and risk. `direct_inline` is for understood, small, low-risk changes; `delegated_direct` is for investigation or worker-assisted changes without an SDD lifecycle; `sdd` is for substantial ambiguity, durable traceability, or an explicit SDD request. Direct routes do not create increments, SDD phases, synthetic artifacts, receipts, or persisted route records. If `sdd` is offered as an alternative, obtain explicit user acceptance before starting it; `axiom-autopilot` remains the SDD orchestrator. `flow=knowledge_only` reuses `axiom knowledge harvest --increment <id>` and does not create an increment or bug. `flow=emergency` requires explicit confirmation and a visible scope and never enables auto-push.

## Route execution gate

Run the phases below only when `flow=increment` and `route=sdd`. For `direct_inline`, perform only the bounded change and return without creating a spec, SDD phase, synthetic artifact, receipt, or persisted route record. For `delegated_direct`, delegate only the narrow implementation or exploration needed and return without entering the SDD lifecycle. For `flow=knowledge_only`, invoke `axiom knowledge harvest --increment <id>` and stop after reporting its result. For `flow=emergency`, require explicit confirmation and a visible scope before any mutation; if either is missing, stop with a decision request. Never enable auto-push.

## Phases

1. Read `AGENTS.md` (canonical rules).
2. Understand request intent and boundaries.
3. Locate `axiom-spec` in the parent workspace.
4. Create or update increment spec in `axiom-spec/increments/` (or equivalent path).
5. Refine goal, context, scope, non-goals, acceptance criteria, risks, and open questions.
6. Ask critical blocking questions only if needed.
7. Produce short internal plan.
8. Implement focused changes in `axiom-sdd`.
9. Run available validation commands.
10. Review against acceptance criteria.
11. Integrate stable knowledge into the canonical `Axiom.Spec/specs/00..08` files if applicable.
12. Set final status to `closed` or `pending` with explicit rationale.
13. Emit concise execution summary.

## Stop Rules

- Stop and ask for clarification when acceptance criteria are too ambiguous for safe execution.
- Keep `Status: pending` when closure conditions are not fully satisfied.
- Do not introduce enterprise lifecycle constructs unless explicitly requested.

## Outputs

- Increment created or refined in `axiom-spec`
- Changes implemented in `axiom-sdd`
- Validation performed (or explicit fallback statement)
- Review against acceptance criteria
- `Axiom.Spec/specs/00..08` updated when stable knowledge applies
- Final status and next step
