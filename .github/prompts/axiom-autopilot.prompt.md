---
name: axiom-autopilot
description: "Ejecuta una tanda completa de cambios Axiom con descomposición en incrementos, verificación independiente, reconciliación de spec y contexto técnico, y archivado."
argument-hint: "Describe el lote completo de cambios que debe ejecutar"
agent: axiom-autopilot
---

Ejecuta el workflow completo definido por el agente `axiom-autopilot` y la skill `.github/skills/axiom-autopilot/SKILL.md`.

Trata el texto de esta invocación y la petición del usuario como la descripción completa del lote. Descompón el lote, delega cada incremento con un scope tipado y determinista, verifica el freeze del candidate (`axiom freeze --increment <id>`) antes de delegar su apply, verifica los resultados capturando y validando sus recibos (`axiom phase receipt`) antes de integrar conocimiento, y completa la integración documental y el archivado. No pidas confirmaciones intermedias: resuelve ambigüedades razonables y regístralas en el resumen final.

Este entrypoint opera como `route=sdd` y conserva a `axiom-autopilot` como orquestador SDD. La clasificación `flow` sigue siendo independiente (`increment`, `bug`, `knowledge_only`, `emergency`); las rutas directas no deben entrar en este lifecycle. Si se ofrece `sdd` como alternativa, requiere aceptación explícita antes de iniciar el lote. `flow=emergency` requiere confirmación explícita y alcance visible, y nunca habilita auto-push.
