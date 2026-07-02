---
description: Run the Axiom Bootstrap bug workflow (expected-behavior-first).
---

Read `Axiom.SDD/AGENTS.md` and treat it as canonical.

Primary path:
1. Launch the `axiom-bug` agent.
2. Pass `$ARGUMENTS` as the bug report.
3. Ask the agent to produce: bug spec updates, minimal fix, validation/regression evidence, closure status, and next step.

Fallback path (if agent launch is unavailable):
- Execute the same lifecycle inline following `Axiom.SDD/AGENTS.md`.

Guardrails:
- Do not implement any fix until expected behavior is clear enough.
- Keep fixes minimal and focused.
- Do not introduce enterprise lifecycle concepts unless explicitly requested.
