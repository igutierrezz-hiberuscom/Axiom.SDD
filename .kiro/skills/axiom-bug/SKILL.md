---
name: axiom-bug
description: Ejecuta el workflow de bug de Axiom con expected-behavior-first, spec canónica, corrección mínima y validación.
---

# Axiom Bug

Usa `$ARGUMENTS` como informe del bug. Lee primero el `AGENTS.md` de la raíz de `Axiom.SDD` y sigue sus reglas.

## Routing

Clasifica por separado:

- `flow`: `increment`, `bug`, `knowledge_only` o `emergency`.
- `route`: `direct_inline`, `delegated_direct` o `sdd`.

Las rutas directas hacen solo el trabajo acotado y no crean incrementos, fases SDD, artifacts sintéticos, receipts ni registros persistentes. `knowledge_only` reutiliza Knowledge Harvest y no crea un bug. `emergency` exige confirmación explícita y alcance visible, y nunca auto-push. Ejecuta el lifecycle siguiente solo para `flow=bug` y `route=sdd`.

## Workflow

1. Entiende síntoma, impacto, comportamiento actual y comportamiento esperado.
2. Identifica `Axiom.SDD`, `Axiom.Spec` y `Axiom` en el workspace padre.
3. Localiza o crea/refina el bug bajo `Axiom.Spec/specs/bugs/` usando Axiom CLI/Core para metadata, IDs, enlaces, índices y status.
4. Define reproducción, causa sospechada y criterios de aceptación.
5. Produce un plan breve.
6. Implementa una corrección mínima en el repositorio propietario.
7. Ejecuta la validación disponible, incluyendo regresión cuando corresponda.
8. Revisa cada criterio y separa fallos preexistentes de nuevos.
9. Integra conocimiento estable en `Axiom.Spec/specs/00..08` solo si aplica.
10. Cierra únicamente si se cumplen todas las reglas de `AGENTS.md`; si no, deja `pending` con motivo mediante Axiom/Core.

No implementes mientras expected behavior no sea claro. No modifiques archivos no relacionados ni introduzcas arquitectura enterprise.

Si no existe validación, informa exactamente: `No validation command was found. Performed best-effort validation by inspecting changed files and checking consistency against the requested behavior.`
