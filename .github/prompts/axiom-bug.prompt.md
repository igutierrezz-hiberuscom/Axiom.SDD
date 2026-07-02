---
name: axiom-bug
description: "Bootstrap bug workflow for axiom-sdd with expected-behavior-first discipline."
argument-hint: "Describe the bug"
agent: agent
---
Read `AGENTS.md` first and treat it as canonical.

Use the user argument as the bug description.

Execute this workflow:

1. Understand the reported bug.
2. Locate the `axiom-spec` sibling repository.
3. Create or update a bug file in `axiom-spec/bugs/`.
4. If `axiom-spec/bugs/` does not exist, use the equivalent bug folder in the spec repository.
5. Define and refine:
   - symptom
   - current behavior
   - expected behavior
   - impact
   - reproduction steps (if available)
   - suspected cause
   - acceptance criteria
6. Ask critical questions if expected vs current behavior is not sufficiently clear.
7. Produce a short internal plan.
8. Implement a minimal focused fix in `axiom-sdd`.
9. Validate, ideally with regression coverage when applicable.
10. Review results against expected behavior and acceptance criteria.
11. Update `axiom-spec/general-spec.md` only if stable behavior changed.
12. Mark bug status as `closed` or `pending` with explicit reason.
13. Summarize fix, validation, status, and next step.

Strong rule:

Do not implement a bug fix until the expected behavior is clear enough.

Plan persistence rule:

- Do not persist a plan by default.
- Persist a plan only for large, risky, cross-repo, architecture-heavy, or multi-session work.

Use this bug template when creating a new bug file:

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

Validation rule:

- Search for validation commands in README files, package scripts, task runners, test configs, build configs, and scripts.
- If no validation command is found, state exactly:

`No validation command was found. Performed best-effort validation by inspecting changed files and checking consistency against the requested behavior.`
