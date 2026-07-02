# review

Run the Axiom Bootstrap review workflow for an increment, a bug, or current changes.

## Goal

Assess completion quality against acceptance criteria and recommend closure status.

## Input

Reference to an increment, bug, or change scope.

## Required behavior

1. Read `AGENTS.md` first.
2. Locate the related increment or bug specification when available.
3. Inspect current implementation changes.
4. Compare outcomes with acceptance criteria and original intent.
5. Review validation evidence and identify gaps.
6. Detect deviations and unresolved risks.
7. Decide closure recommendation (`closed` or `pending` with reason).
8. Update `axiom-spec/general-spec.md` only when stable knowledge should be consolidated.
9. Propose a commit message consistent with the reviewed result.

## Output

- compliance summary
- deviations
- risks
- observed validation
- closure recommendation
- suggested commit message
