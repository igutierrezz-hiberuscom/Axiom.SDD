---
name: axiom-autopilot
description: Orquesta lotes de cambios Axiom de principio a fin: descompone, ejecuta incrementos spec-first, verifica, consolida spec/contexto y archiva.
---

# Axiom Autopilot para Kiro

Usa `$ARGUMENTS` como descripción completa del lote. Lee `AGENTS.md` de la raíz de `Axiom.SDD` antes de actuar. Esta skill no reemplaza el contrato canónico: lo aplica.

## Contrato outcome-first

Clasifica cada petición en dos ejes:

- `flow`: `increment`, `bug`, `knowledge_only` o `emergency`.
- `route`: `direct_inline`, `delegated_direct` o `sdd`.

Elige primero el outcome y después la ruta según alcance y riesgo. Las rutas directas no crean incrementos, fases SDD, artifacts sintéticos, receipts ni registros persistentes. `knowledge_only` reutiliza `axiom knowledge harvest --increment <id>` y termina. `emergency` exige confirmación explícita y alcance visible, y nunca auto-push. Ejecuta el playbook completo solo para `flow=increment` o `flow=bug` con `route=sdd`.

## Fronteras

- `Axiom/`: runtime, CLI, adapters, providers, tests y producto.
- `Axiom.Spec/`: requisitos, incrementos, bugs, decisiones, specs canónicas y contexto técnico.
- `Axiom.SDD/`: reglas, agentes, skills, prompts y workflows.

No dupliques la spec canónica en Axiom.SDD ni modifiques un repositorio fuera del alcance del lote.

## Playbook

### 1. Descomponer

Convierte la petición en una lista numerada de cambios. Divide en incrementos verificables e independientes, con goal, scope, non-goals y acceptance criteria. Usa nombres `INC-<YYYYMMDD>-<slug>` cuando el ciclo requiera un nuevo incremento.

### 2. Leer control y contexto

Lee `AGENTS.md`, `Axiom.Spec/specs/README.md`, `Axiom.Spec/context/TECHNICAL_CONTEXT.md` si puede cambiar el estado técnico y el artifact relacionado. Usa solo la exploración necesaria.

### 3. Preparar cada incremento

Antes de delegar apply verifica el freeze requerido por el runtime: `axiom freeze --increment <id>`. Si el freeze no existe o está desactualizado, no delegues apply. Usa el agente Kiro `axiom-increment` con un brief autosuficiente que incluya criterios, decisiones y scope exacto.

El brief debe exigir:

- spec bajo `Axiom.Spec/specs/increments/<INC-id>/README.md` mediante Axiom CLI/Core;
- implementación en `Axiom/`, salvo tooling/documentación explícitos en `Axiom.SDD`;
- validación dirigida;
- no editar `specs/00..08` ni `context/**` durante el trabajo delegado;
- no ejecutar `git add`, `git commit`, `git push`, `git reset` ni checkout destructivo.

Si no hay delegación disponible, ejecuta el ciclo inline.

### 4. Resolver decisiones

Registra duda, alternativas, decisión y motivo. Prioriza comportamiento observable y tests, decisiones cerradas, patrones existentes, límites de `AGENTS.md` y cambio mínimo.

### 5. Verificar independientemente

Después de cada worker:

1. Reejecuta build y pruebas dirigidas desde `Axiom/`.
2. Lee directamente la zona de mayor riesgo.
3. Comprueba cada criterio contra el resultado real.
4. Clasifica fallos preexistentes frente a nuevos.
5. Captura y valida `axiom phase receipt` cuando el phase log exista.

No integres conocimiento ni cierres un incremento si la verificación requerida falta. Corrige defectos locales y repite validación.

### 6. Integrar al final

Haz una única pasada sobre `Axiom.Spec/specs/00_Resumen_Ejecutivo.md` a `08_Glosario.md`, siguiendo `specs/README.md`. Actualiza o elimina claims activos obsoletos; un bloque `SUPERSEDE` aislado no neutraliza texto vigente antiguo. Conserva historia solo en secciones históricas o artifacts archivados.

Después reconcilia `Axiom.Spec/context/**` con el estado real del runtime. Si ningún cambio afecta contexto técnico, decláralo explícitamente y no inventes documentos.

### 7. Cierre y archivo

Actualiza el artifact del incremento con la integración de spec y contexto y usa Axiom CLI/Core para archivarlo. Archivar no autoriza a marcar `closed` un trabajo que no cumple las reglas de `AGENTS.md`.

## Guardrails

- Usa Axiom CLI/Core para crear, renombrar, mover o cambiar status de incrementos, bugs, ADRs, decisiones e índices; nunca edites manualmente su metadata estructural.
- No ejecutes mutaciones Git.
- No introduzcas índices obligatorios, arquitectura enterprise, MCP obligatorio, Workbench ni integraciones externas no solicitadas.
- Mantén scaffolding best-effort, no-clobber y con gating de creación.
- No presentes snapshots históricos como estado actual.

## Informe final

Devuelve una sola síntesis con lista original, incrementos y estados, decisiones, validación por unidad, fallos preexistentes/nuevos, integración de `specs/00..08`, cambios en `context/**`, archivado y confirmación de que no hubo mutaciones Git.
