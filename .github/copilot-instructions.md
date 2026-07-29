# Copilot Adapter for Axiom Bootstrap Orchestrator

`AGENTS.md` is the canonical behavior source for this repository.

## Required Startup Behavior

1. Read `AGENTS.md` before planning or editing.
2. Follow Axiom Bootstrap Orchestrator Mode exactly.
3. Use the prompts in `.github/prompts/` for increment, bug, and review workflows.
4. Work with the parent workspace when sibling repositories are available (`Axiom.SDD`, `Axiom.Spec`, optional `Axiom`).

## Axiom Autopilot

- Use the custom agent `.github/agents/axiom-autopilot.agent.md` for unattended batches of changes.
- The agent loads `.github/skills/axiom-autopilot/SKILL.md`; the skill is also invocable as `/axiom-autopilot`.
- `axiom-increment` and `axiom-review` are delegated worker agents. The autopilot verifies their results independently.
- The final integration must reconcile active claims in `Axiom.Spec/specs/00..08` and `Axiom.Spec/context/**`: update changed facts, remove retired current-state claims, and preserve history only under explicit historical/archive sections.
- `SUPERSEDE` alone does not make stale active prose safe. The old assertion must be removed, rewritten, or explicitly marked as historical.

## Scope Rules

- Refine and maintain canonical increment or bug specs in `Axiom.Spec/specs/increments/` or `Axiom.Spec/bugs/`.
- Implement focused product changes in `Axiom/` and workflow/tooling changes in `Axiom.SDD/`.
- Consolidate stable knowledge into the owning files in `Axiom.Spec/specs/` when applicable.

## Guardrails

- Do not introduce future enterprise lifecycle concepts unless explicitly requested.
- Do not create heavy metadata, index systems, MCP dependencies, Workbench logic, or external work-item integrations by default.
- Do not persist plans by default; persist only for large, risky, cross-repo, or multi-session work.
- Validate using available commands whenever possible.
