# increment

Run the Axiom Bootstrap increment workflow.

## Goal

Implement an increment through a lightweight spec-first lifecycle without introducing enterprise-heavy orchestration.

## Input

A free-form increment request.

## Required behavior

1. Read `AGENTS.md` first.
2. Work in Bootstrap Orchestrator Mode.
3. Locate `axiom-spec` in the parent workspace.
4. Create or update an increment spec in `axiom-spec/increments/` (or equivalent path if the folder differs).
5. Refine: goal, context, scope, non-goals, acceptance criteria, risks, and open questions.
6. Ask critical questions only when required for safe execution.
7. Produce a short internal plan (do not persist by default).
8. Implement focused changes in `axiom-sdd` only after context is sufficient.
9. Validate with available commands.
10. Review against acceptance criteria.
11. Update `axiom-spec/general-spec.md` with stable knowledge when applicable.
12. Close as `closed` or `pending` with explicit reason.

## Increment template

```md
# Increment: <short-title>

Status: draft | in-progress | pending | closed
Date: YYYY-MM-DD

## Goal

## Context

## Scope

## Non-goals

## Acceptance criteria

- [ ] ...

## Open questions

## Assumptions

## Implementation notes

## Validation

## Result

## General spec integration

Describe what was integrated into `general-spec.md`, or why nothing was needed.
```

## Validation fallback

If no validation command is found, state exactly:

`No validation command was found. Performed best-effort validation by inspecting changed files and checking consistency against the requested behavior.`
