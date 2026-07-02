# Copilot Adapter for Axiom Bootstrap Orchestrator

`AGENTS.md` is the canonical behavior source for this repository.

## Required Startup Behavior

1. Read `AGENTS.md` before planning or editing.
2. Follow Axiom Bootstrap Orchestrator Mode exactly.
3. Use the prompts in `.github/prompts/` for increment, bug, and review workflows.
4. Work with the parent workspace when sibling repositories are available (`axiom-sdd`, `axiom-spec`, optional `axiom-product`).

## Scope Rules

- Refine and maintain canonical increment or bug specs in `axiom-spec`.
- Implement focused technical changes in `axiom-sdd`.
- Consolidate stable knowledge into `axiom-spec/general-spec.md` when applicable.

## Guardrails

- Do not introduce future enterprise lifecycle concepts unless explicitly requested.
- Do not create heavy metadata, index systems, MCP dependencies, Workbench logic, or external work-item integrations by default.
- Do not persist plans by default; persist only for large, risky, cross-repo, or multi-session work.
- Validate using available commands whenever possible.
