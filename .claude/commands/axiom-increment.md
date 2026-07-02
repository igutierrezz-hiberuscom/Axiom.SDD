---
description: Run the Axiom Bootstrap increment workflow (spec-first, lightweight).
---

Read `Axiom.SDD/AGENTS.md` and treat it as canonical.

Primary path:
1. Launch the `axiom-increment` agent.
2. Pass `$ARGUMENTS` as the increment request.
3. Ask the agent to produce: spec updates, implementation updates, validation outcome, closure status, and next step.

Fallback path (if agent launch is unavailable):
- Execute the same lifecycle inline following `Axiom.SDD/AGENTS.md`.

Guardrails:
- Keep the process lightweight.
- Do not introduce enterprise lifecycle concepts unless explicitly requested.
- Do not persist plans by default.
