# Workflow: axiom-bug

## Objective

Resolve a bug with expected-behavior-first discipline, minimal code changes, and clear closure evidence.

## Inputs

- Bug description
- Optional reproduction details
- Optional expected behavior constraints

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
