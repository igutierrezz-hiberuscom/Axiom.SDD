---
name: axiom-increment
description: "Bootstrap increment workflow for Axiom using lightweight spec-first orchestration."
argument-hint: "Describe the increment request"
agent: axiom-increment
---
Read `Axiom.SDD/AGENTS.md` first and treat it as canonical.

Use the user argument as the increment description.

## Outcome-first routing contract

Classify the request on two independent axes before running this workflow:

- `flow`: `increment` (change lifecycle), `bug` (expected-behavior fix), `knowledge_only` (reuse the current Knowledge Harvest flow), or `emergency` (confirmed urgent work).
- `route`: `direct_inline` (understood, small, low-risk change), `delegated_direct` (investigation or worker-assisted change without SDD lifecycle), or `sdd` (substantial ambiguity, durable traceability, or explicit SDD request).

Choose the outcome (`flow`) first, then choose the route from the actual scope and risk. Direct routes do not create increments, SDD phases, synthetic artifacts, receipts, or persisted route records. Run the lifecycle below only for `flow=increment` with `route=sdd`; direct work must skip lifecycle artifact creation. If `sdd` is offered as an alternative, obtain explicit user acceptance before starting it. `axiom-autopilot` remains the SDD orchestrator. `flow=knowledge_only` reuses `axiom knowledge harvest --increment <id>` and does not create an increment or bug. `flow=emergency` requires explicit confirmation and a visible scope, and never enables auto-push.

Execute this workflow:

1. Understand the increment request.
2. Locate the `Axiom.Spec` sibling repository.
3. Create or update an increment file in `Axiom.Spec/specs/increments/`.
4. If `Axiom.Spec/specs/increments/` does not exist, use the equivalent increment folder in the spec repository.
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
8. Implement focused changes in `Axiom/` or, when the increment is tooling-only, in `Axiom.SDD/`.
9. Validate with available commands.
10. Review implementation against acceptance criteria.
11. Update the canonical `Axiom.Spec/specs/00..08` files only with stable knowledge when needed.
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

Describe what was integrated into `Axiom.Spec/specs/00..08`, or why nothing was needed.
```

Validation rule:

- Search for validation commands in README files, package scripts, task runners, test configs, build configs, and scripts.
- If no validation command is found, state exactly:

`No validation command was found. Performed best-effort validation by inspecting changed files and checking consistency against the requested behavior.`
