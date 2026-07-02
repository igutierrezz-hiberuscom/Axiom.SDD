---
description: Run the Axiom Bootstrap review workflow for increment, bug, or current changes.
---

Read `Axiom.SDD/AGENTS.md` and treat it as canonical.

Primary path:
1. Launch the `axiom-review` agent.
2. Pass `$ARGUMENTS` as the review target.
3. Ask the agent to produce: compliance report, deviations, risks, validation observed, closure recommendation, and suggested commit message.

Fallback path (if agent launch is unavailable):
- Execute the same lifecycle inline following `Axiom.SDD/AGENTS.md`.

Guardrails:
- Keep findings evidence-based.
- Do not recommend closure when acceptance criteria remain unmet.
