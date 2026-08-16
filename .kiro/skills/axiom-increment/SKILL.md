---
name: axiom-increment
description: Ejecuta un incremento de Axiom con workflow spec-first, alcance enfocado, implementación y validación explícita.
---

# Axiom Increment

Usa `$ARGUMENTS` como descripción del incremento. Lee primero el `AGENTS.md` de la raíz de `Axiom.SDD` y sigue sus reglas.

## Routing

Clasifica por separado `flow` (`increment`, `bug`, `knowledge_only`, `emergency`) y `route` (`direct_inline`, `delegated_direct`, `sdd`). Las rutas directas no crean artifacts de lifecycle, fases, receipts ni registros persistentes. `knowledge_only` reutiliza Knowledge Harvest. `emergency` exige confirmación y alcance visible y nunca auto-push. Ejecuta este lifecycle solo para `flow=increment` y `route=sdd`.

## Workflow

1. Define resultado, límites y repositorios implicados.
2. Trata `Axiom.SDD` como hogar de tooling/workflows, `Axiom.Spec` como fuente canónica y `Axiom` como runtime/producto.
3. Localiza o crea/refina el incremento bajo `Axiom.Spec/specs/increments/` usando Axiom CLI/Core para operaciones estructurales; no edites manualmente IDs, enlaces, índices o status.
4. Refina goal, context, scope, non-goals, acceptance criteria, risks, open questions y assumptions.
5. Implementa en el repositorio propietario.
6. Ejecuta validación dirigida; desde `Axiom/`, usa `npm run build` y pruebas focalizadas cuando corresponda.
7. Revisa criterios y clasifica fallos preexistentes frente a nuevos.
8. Integra conocimiento estable en `Axiom.Spec/specs/00..08` solo cuando aplique.
9. Marca `closed` solo con todas las condiciones de cierre; en otro caso deja `pending` con explicación mediante Axiom/Core.

No introduzcas arquitectura enterprise ni persistas un plan salvo que el trabajo sea grande, riesgoso, transversal o multi-sesión.

Si no existe validación, informa exactamente: `No validation command was found. Performed best-effort validation by inspecting changed files and checking consistency against the requested behavior.`
