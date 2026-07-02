# bug

Run the Axiom Bootstrap bug workflow.

## Goal

Fix a bug with expected-behavior-first discipline and minimal focused changes.

## Input

A free-form bug description.

## Required behavior

1. Read `AGENTS.md` first.
2. Work in Bootstrap Orchestrator Mode.
3. Locate `axiom-spec` in the parent workspace.
4. Create or update a bug spec in `axiom-spec/bugs/` (or equivalent path if the folder differs).
5. Define: symptom, current behavior, expected behavior, impact, reproduction steps (if available), suspected cause, acceptance criteria.
6. Ask critical questions when expected behavior is not clear enough.
7. Produce a short internal plan (do not persist by default).
8. Implement a minimal fix in `axiom-sdd` only when context is sufficient.
9. Validate, ideally with regression coverage when applicable.
10. Review against expected behavior and acceptance criteria.
11. Update `axiom-spec/general-spec.md` if stable behavior changed.
12. Close as `closed` or `pending` with explicit reason.

## Strong rule

Do not implement a bug fix until the expected behavior is clear enough.

## Bug template

```md
# Bug: <short-title>

Status: draft | in-progress | pending | closed
Date: YYYY-MM-DD

## Symptom

## Current behavior

## Expected behavior

## Impact

## Reproduction steps

## Suspected cause

## Acceptance criteria

- [ ] ...

## Fix notes

## Validation

## Result

## General spec integration

Describe what was integrated into `general-spec.md`, or why nothing was needed.
```

## Validation fallback

If no validation command is found, state exactly:

`No validation command was found. Performed best-effort validation by inspecting changed files and checking consistency against the requested behavior.`
