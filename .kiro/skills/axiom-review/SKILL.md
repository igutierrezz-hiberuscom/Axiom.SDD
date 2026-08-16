---
name: axiom-review
description: Revisa un incremento, bug o cambio de Axiom contra intención, criterios de aceptación, riesgos y validación observada.
---

# Axiom Review

Usa `$ARGUMENTS` como referencia del incremento, bug o alcance. Lee primero el `AGENTS.md` de la raíz de `Axiom.SDD`.

Trabaja en modo read-only: no edites archivos, no cambies status, no archives artifacts y no ejecutes mutaciones Git.

## Workflow

1. Localiza y lee la spec relacionada cuando exista.
2. Inspecciona los cambios de implementación y la documentación cercana.
3. Compara implementación con intención original y criterios de aceptación.
4. Comprueba la evidencia de validación disponible y no inventes comandos.
5. Detecta desviaciones, riesgos, gaps y afirmaciones activas obsoletas.
6. Distingue rutas directas de trabajo SDD: no exijas lifecycle artifacts que la ruta directa prohíbe.
7. Recomienda `closed` solo si los criterios y reglas de cierre están satisfechos; en otro caso recomienda `pending` con motivo.
8. Señala si debe consolidarse conocimiento estable en `Axiom.Spec/specs/00..08` o `Axiom.Spec/context/**`.

Devuelve: cumplimiento, desviaciones, riesgos, validación observada, recomendación `closed` o `pending` con motivo y mensaje de commit sugerido, sin crear el commit.
