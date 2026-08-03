---
name: axiom-autopilot
description: "Orquestación desatendida de lotes de incrementos Axiom: descompone cambios, ejecuta incrementos spec-first, verifica resultados, consolida la spec vigente, reconcilia el contexto técnico y archiva. Úsala para tandas de cambios que deban cerrarse sin pausas intermedias."
argument-hint: "Describe el lote completo de cambios que debe ejecutar Axiom Autopilot"
user-invocable: true
disable-model-invocation: false
---

# Axiom Autopilot para Copilot

## Propósito

Esta skill porta el workflow `axiom-autopilot` desde Claude Code al agente de Copilot dentro de `Axiom.SDD`. Orquesta una tanda completa en la conversación principal y delega el trabajo aislado de cada incremento a `axiom-increment` cuando ese agente esté disponible.

La skill no reemplaza las reglas del repositorio. Antes de actuar, lee `Axiom.SDD/AGENTS.md` y las aplica como fuente normativa del ciclo SDD ligero.

## Contrato outcome-first

Clasifica cada peticion en dos ejes independientes antes de actuar:

- `flow`: `increment`, `bug`, `knowledge_only` o `emergency`.
- `route`: `direct_inline`, `delegated_direct` o `sdd`.

Elige primero el outcome (`flow`) y despues la ruta segun el alcance y el riesgo real. `direct_inline` se reserva para cambios entendidos, pequenos y de bajo riesgo; `delegated_direct` para investigacion o cambios que necesitan un worker sin crear lifecycle SDD; `sdd` para ambiguedad sustancial, trazabilidad duradera o una peticion SDD explicita. Las rutas directas no crean incrementos, fases SDD, artefactos sinteticos, receipts ni registros persistentes de routing. Si `sdd` se ofrece como alternativa, requiere aceptacion explicita antes de iniciar; `axiom-autopilot` sigue siendo el orquestador SDD. `flow=knowledge_only` reutiliza el flujo vigente de `axiom knowledge harvest --increment <id>` y no crea un incremento o bug. `flow=emergency` requiere confirmacion explicita y alcance visible, y nunca habilita auto-push.

### Preflight de ejecucion

Aplica este preflight antes de entrar en el playbook:

1. Si `flow=knowledge_only`, exige el identificador de incremento, ejecuta `axiom knowledge harvest --increment <id>`, informa el resultado y termina. No descompongas, delegues, consolides ni archives un incremento.
2. Si `flow=emergency`, exige confirmacion explicita y un alcance visible de repositorios y archivos antes de cualquier mutacion. Si falta cualquiera, detente y solicita esa decision. El alcance no puede habilitar `auto-push`.
3. Si `route=direct_inline` o `route=delegated_direct`, ejecuta unicamente el trabajo acotado correspondiente y termina sin crear specs, fases SDD, artefactos sinteticos, receipts ni registros persistentes.
4. Ejecuta el resto de este playbook unicamente para `flow=increment` o `flow=bug` con `route=sdd`.

## Fronteras de repositorio

- `Axiom/`: runtime, CLI, adapters, providers, tests y código de producto.
- `Axiom.Spec/`: fuente canónica de requisitos, incrementos, bugs, decisiones, spec general y contexto técnico.
- `Axiom.SDD/`: reglas operativas, custom agents, skills, prompts e instrucciones para construir Axiom.
- No dupliques la spec canónica dentro de `Axiom.SDD`.
- No modifiques un repositorio ajeno al alcance del lote.

## Regla de operación

Ejecuta el lote completo sin detenerte para pedir decisiones intermedias. Cuando haya una ambigüedad, elige la opción más conservadora y compatible con el código existente, registra la decisión y continúa. Solo detén el proceso si falta una información imprescindible para no causar una mutación destructiva o si una herramienta no permite continuar.

## Playbook

### 1. Convertir la petición en una lista de cambios

Lee la petición completa y conviértela en una lista numerada de cambios concretos. Esa lista será el ancla para el resumen final y para comprobar que no se omitió ningún objetivo.

### 2. Leer las fuentes de control

Antes de diseñar incrementos, lee:

1. `Axiom.SDD/AGENTS.md`.
2. `Axiom.Spec/specs/README.md`.
3. `Axiom.Spec/context/TECHNICAL_CONTEXT.md` si la tanda puede cambiar el estado técnico actual.
4. El incremento, bug o decisión existente relacionado, si lo hay.

Haz solo la exploración necesaria para identificar el código propietario del comportamiento. Usa un agente de exploración de solo lectura si está disponible; si no, lee directamente los archivos cercanos.

### 3. Descomponer en incrementos

Divide la lista en incrementos enfocados, verificables e independientes. Nómbralos `INC-<YYYYMMDD>-<slug>` con la fecha actual y un slug corto en kebab-case.

- Ejecuta por defecto en orden secuencial.
- Solo paraleliza incrementos con árboles de archivos completamente disjuntos y sin relación productor-consumidor.
- No mezcles en un mismo incremento cambios de producto sin relación.
- Cada incremento debe tener goal, scope, non-goals y acceptance criteria claros.

### 4. Delegar cada incremento

Antes de delegar el apply de un incremento, verifica que su candidate está congelado ejecutando `axiom freeze --increment <id>`; no envíes a un subagente el apply de un incremento cuyo freeze esté ausente o desactualizado. Esta verificación es un requisito formal del ciclo, no un paso opcional.

Para cada incremento, invoca el custom agent `axiom-increment` con un brief autosuficiente que incluya:

- objetivo y criterios de aceptación;
- decisiones ya tomadas, sin convertirlas en preguntas abiertas;
- un scope tipado y determinista: archivos, paquetes y repositorios exactos (nunca una descripción vaga que deje el alcance a criterio del subagente);
- obligación de crear o actualizar `Axiom.Spec/specs/increments/<INC-id>/README.md` antes de implementar;
- obligación de implementar en `Axiom/`, salvo que el incremento sea explícitamente documental o de tooling;
- validación dirigida desde `Axiom/`;
- prohibición de integrar en `Axiom.Spec/specs/00_Resumen_Ejecutivo.md` a `08_Glosario.md`;
- prohibición de modificar `Axiom.Spec/context/**`;
- prohibición de ejecutar `git add`, `git commit`, `git push` u otras mutaciones Git.

Si el agente delegado no está disponible, ejecuta el mismo ciclo inline en la conversación principal. No abandones el lote por la ausencia del subagente.

### 5. Resolver y registrar decisiones

Para cada ambigüedad registra internamente:

- duda o alternativas observadas;
- opción elegida;
- motivo de una línea.

Prioridad de decisión:

1. comportamiento observable y código actual;
2. decisiones y specs canónicas ya cerradas;
3. patrones de repositorio existentes;
4. límites de bootstrap de `AGENTS.md`;
5. cambio mínimo que satisface la petición.

### 6. Verificar cada incremento de forma independiente

Después de cada subagente, no aceptes su autoinforme sin comprobarlo:

1. Reejecuta `npm run build` desde `Axiom/`.
2. Reejecuta las pruebas dirigidas de los paquetes o apps afectados.
3. Lee directamente la parte de código con mayor riesgo.
4. Comprueba cada criterio de aceptación contra el resultado real.
5. Clasifica cada fallo como preexistente o introducido por el incremento.
6. Captura y verifica los recibos criptográficos del phase log (`axiom phase receipt`) del incremento; es un requisito formal — no des el incremento por verificado ni integres su conocimiento en el paso 7 si los recibos faltan o no validan.

No arregles fallos preexistentes no relacionados. Si la verificación descubre un defecto local introducido por el incremento, corrígelo en esa misma unidad y repite la validación.

### 7. Consolidar la spec canónica al final

Cuando todos los incrementos estén implementados y verificados, haz una única pasada de integración sobre `Axiom.Spec/specs/00_Resumen_Ejecutivo.md` a `08_Glosario.md`, siguiendo la responsabilidad de cada archivo descrita en `Axiom.Spec/specs/README.md`.

Antes de editar, construye un ledger de cambios por incremento con estas categorías:

- capacidades o hechos añadidos;
- hechos modificados;
- hechos eliminados, retirados o renombrados;
- formatos, paths, IDs y conteos afectados;
- conocimiento que debe conservarse solo como historia.

Para cada hecho que ya exista en la spec:

- si sigue siendo cierto, actualiza el texto y los conteos si procede;
- si cambió, modifica la afirmación activa en su lugar o añade una subsección claramente normativa;
- si fue eliminado o retirado por el incremento, borra la afirmación activa o sustitúyela por el estado actual;
- si debe conservarse por trazabilidad, muévela o déjala bajo un título explícito como `Registro histórico`, con una nota que diga que no forma parte del contrato vigente;
- no dejes una afirmación antigua en una sección activa esperando que un bloque `SUPERSEDE` la neutralice: `SUPERSEDE` por sí solo no basta;
- no borres nombres legacy de incrementos, ADRs, archivos archivados o migraciones cuando su conservación sea historia válida.

Integra solo conocimiento estable de producto y comportamiento. No copies narrativas completas de implementación ni inventes requisitos futuros.

### 7b. Reconciliar y generar contexto técnico

Después de integrar la spec, revisa el efecto de cada incremento sobre `Axiom.Spec/context/**`. El contexto técnico describe cómo está construido el runtime hoy, no el roadmap.

Busca al menos estos impactos:

- paquetes, comandos, adapters o providers añadidos, retirados o renombrados;
- cambios de paths, artefactos generados, schemas o datos persistidos;
- cambios en onboarding, lifecycle, MCP, toolchain o checks de doctor;
- cambios de ownership, aislamiento, fallback o límites operativos.

Para cada impacto:

1. Lee el documento de contexto propietario y su fuente de código.
2. Corrige en el sitio la afirmación actual que haya quedado obsoleta.
3. Borra o reemplaza las afirmaciones de estado actual sobre capacidades retiradas; no las mantengas como si siguieran existiendo.
4. Añade los hechos nuevos con una cita a la ruta de código, README o documento verificable.
5. Si no existe un documento adecuado para un concepto estable nuevo, genera un documento técnico breve bajo el subdirectorio correcto y añádelo al índice de `TECHNICAL_CONTEXT.md`.
6. Si el cambio elimina un concepto y deja un documento sin contenido actual útil, elimina el documento solo si no contiene conocimiento vigente; conserva la historia en incrementos archivados o referencias históricas, no en una descripción activa falsa.
7. Actualiza `TECHNICAL_CONTEXT.md` con la fecha de última validación y el índice cuando corresponda.

No generes documentos para rellenar huecos especulativos. Si ningún incremento cambió el estado técnico actual, escribe explícitamente `context/**: sin cambios requeridos` en el resultado y no inventes una actualización.

### 8. Archivar los incrementos

Para cada incremento procesado:

1. Actualiza su `README.md` antes de moverlo.
2. Añade o completa `## General spec integration` con los archivos `00..08` modificados y el conocimiento integrado.
3. Añade en esa misma sección el resultado de contexto técnico: archivos modificados, archivos creados/eliminados o `ninguno`.
4. Mueve la carpeta de `Axiom.Spec/specs/increments/<INC-id>/` a `Axiom.Spec/specs/increments/_archive/<INC-id>/`.
5. Conserva su historia y su estado real (`closed` o `pending`); archivar no autoriza a marcar como cerrado algo que no cumple las reglas de `AGENTS.md`.

No borres la evidencia del incremento. No ejecutes comandos Git mutantes.

### 9. Resumen final obligatorio

Entrega un único resumen con:

- lista original de cambios;
- incrementos creados, objetivo y estado;
- decisiones y ambigüedades resueltas;
- validación por incremento, incluyendo fallos preexistentes frente a nuevos;
- archivos de `specs/00..08` actualizados y motivo;
- archivos de `context/**` actualizados, creados o eliminados, o declaración explícita de que no aplicó;
- confirmación de que las carpetas fueron archivadas;
- confirmación de que no se ejecutaron mutaciones Git y el worktree queda sin commit para revisión humana.

## Guardrails

- No ejecutes `git add`, `git commit`, `git push`, `git reset`, `git checkout` destructivo ni comandos equivalentes.
- No modifiques `Axiom.SDD` por cambios que pertenezcan a `Axiom` o `Axiom.Spec`, salvo los archivos de workflow necesarios para esta skill.
- No introduzcas arquitectura enterprise, índices obligatorios, integraciones externas, MCP obligatorios ni Workbench si la petición no lo exige.
- Mantén la regla `best-effort + no-clobber + created-gating` para cualquier scaffolding.
- Trata la verificación del freeze (`axiom freeze --increment <id>`) antes de delegar el apply, y la captura/verificación de recibos (`axiom phase receipt`) antes de integrar conocimiento, como requisitos formales del ciclo; nunca los omitas.
- No presentes un snapshot histórico como estado actual.
- No finalices diciendo que el trabajo está cerrado si falta implementación, validación, integración documental o archivo.
