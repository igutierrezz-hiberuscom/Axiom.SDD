---
name: axiom-increment
description: "Bootstrap increment workflow for axiom-sdd using lightweight spec-first orchestration."
argument-hint: "Describe the increment request"
agent: agent
---
Read `AGENTS.md` first and treat it as canonical.

Use the user argument as the increment description.

Execute this workflow:

1. Understand the increment request.
2. Locate the `axiom-spec` sibling repository.
3. Create or update an increment file in `axiom-spec/increments/`.
4. If `axiom-spec/increments/` does not exist, use the equivalent increment folder in the spec repository.
5. Refine the increment with:
   - goal
   - context
   - scope
   - non-goals
   - acceptance criteria
   - risks
   - open questions
6. Ask critical questions only when they block safe implementation.
7. Produce a short internal plan.
8. Implement focused changes in `axiom-sdd`.
9. Validate with available commands.
10. Review implementation against acceptance criteria.
11. Update `axiom-spec/general-spec.md` only with stable knowledge when needed.
12. Mark increment status as `closed` or `pending` with explicit reason.
13. Summarize changes, validation, status, and next step.

Plan persistence rule:

- Do not persist a plan by default.
- Persist a plan only for large, risky, cross-repo, architecture-heavy, or multi-session work.

Use this increment template when creating a new increment file:

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

Validation rule:

- Search for validation commands in README files, package scripts, task runners, test configs, build configs, and scripts.
- If no validation command is found, state exactly:

`No validation command was found. Performed best-effort validation by inspecting changed files and checking consistency against the requested behavior.`
