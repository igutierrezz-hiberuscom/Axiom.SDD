# Workflow: axiom-increment

## Objective

Deliver an increment using Axiom Bootstrap Orchestrator Mode with lightweight spec refinement, focused implementation, and explicit closure.

## Inputs

- Free-form increment description
- Optional constraints, risks, and acceptance notes from the user

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
11. Integrate stable knowledge into `axiom-spec/general-spec.md` if applicable.
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
- `general-spec.md` updated when stable knowledge applies
- Final status and next step
