# increment

Run the Axiom Bootstrap increment workflow.

## Goal

Implement an increment through a lightweight spec-first lifecycle without introducing enterprise-heavy orchestration.

## Input

A free-form increment request.

## Outcome-first routing contract

Classify the request on two independent axes before acting:

- `flow`: `increment`, `bug`, `knowledge_only`, or `emergency`.
- `route`: `direct_inline`, `delegated_direct`, or `sdd`.

Choose the outcome (`flow`) first, then choose the route from actual scope and risk. `direct_inline` is for understood, small, low-risk changes; `delegated_direct` is for investigation or worker-assisted changes without an SDD lifecycle; `sdd` is for substantial ambiguity, durable traceability, or an explicit SDD request. Direct routes do not create increments, SDD phases, synthetic artifacts, receipts, or persisted route records. If `sdd` is offered as an alternative, obtain explicit user acceptance before starting it; `axiom-autopilot` remains the SDD orchestrator. `flow=knowledge_only` reuses `axiom knowledge harvest --increment <id>` and does not create an increment or bug. `flow=emergency` requires explicit confirmation and a visible scope and never enables auto-push.

## Route execution gate

Run the required behavior below only when `flow=increment` and `route=sdd`. For `direct_inline`, perform only the bounded change and return without creating a spec, SDD phase, synthetic artifact, receipt, or persisted route record. For `delegated_direct`, delegate only the narrow implementation or exploration needed and return without entering the SDD lifecycle. For `flow=knowledge_only`, invoke `axiom knowledge harvest --increment <id>` and stop after reporting its result. For `flow=emergency`, require explicit confirmation and a visible scope before any mutation; if either is missing, stop with a decision request. Never enable auto-push.

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
11. Update the canonical `Axiom.Spec/specs/00..08` files with stable knowledge when applicable.
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

Describe what was integrated into `Axiom.Spec/specs/00..08`, or why nothing was needed.
```

## Validation fallback

If no validation command is found, state exactly:

`No validation command was found. Performed best-effort validation by inspecting changed files and checking consistency against the requested behavior.`
