---
name: axiom-autopilot
description: "Ejecuta una tanda completa de cambios Axiom con descomposición en incrementos, verificación independiente, reconciliación de spec y contexto técnico, y archivado."
argument-hint: "Describe el lote completo de cambios que debe ejecutar"
agent: axiom-autopilot
---

Ejecuta el workflow completo definido por el agente `axiom-autopilot` y la skill `.github/skills/axiom-autopilot/SKILL.md`.

Trata el texto de esta invocación y la petición del usuario como la descripción completa del lote. Descompón el lote, delega cada incremento, verifica los resultados y completa la integración documental y el archivado. No pidas confirmaciones intermedias: resuelve ambigüedades razonables y regístralas en el resumen final.
