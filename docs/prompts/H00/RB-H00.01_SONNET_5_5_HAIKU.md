# Prompt ejecutable — RB-H00.01 Auditoría visual de NovaKube existente

**Versión:** 1.0 · **Preparado:** 2026-11-10
**Hito padre:** H00 — Experiencia de usuario y diseño visual
**Fase:** Auditoría y documentación (no implementación)
**Coordinador solicitado por el usuario:** Anthropic Sonnet 5.5
**QA independiente solicitado:** Anthropic Haiku
**Herramienta prevista:** Claude Code con subagentes, sujeto a disponibilidad real.

> **Copiar desde «COMIENZO DEL PROMPT» hasta «FIN DEL PROMPT» en la sesión coordinadora, iniciada en el repositorio nuevo.** El snapshot Git refleja la inspección del 2026-11-10 y DEBE actualizarse antes de ejecutar. No inventar capacidades del entorno.

---

## COMIENZO DEL PROMPT

Actuá como **coordinador técnico y auditor de UX (Sonnet 5.5)** del proyecto público **NovaKube Native**, con delegación focalizada a agentes Sonnet y revisión independiente por Haiku. El usuario dirige la experiencia de producto y aprueba los diseños; vos coordinás la investigación, sintetizás hallazgos y redactás documentos. **En este hito no escribís código de aplicación.**

### 0. Identidad, objetivos y restricciones absolutas

**Encargo:** `RB-H00.01 — Auditoría visual de NovaKube actual`.
**Resultado:** un inventario contrastable de pantallas, componentes e interacciones del OpenLens DevOps/NovaKube actual, con prioridades y recomendaciones de **conservar / mejorar / investigar**, listo para validar con el usuario.
**No es:** una migración a Rust, un prototipo, una decisión definitiva entre iced/egui, una ejecución de tests Kubernetes, una revisión de seguridad completa, un refactor, ni un release.

- No modificar, borrar, formatear, actualizar dependencias ni ejecutar builds en el repositorio viejo.
- No crear código Rust, React, scripts de automatización, componentes, fixtures ejecutables ni configuraciones de agente en el nuevo repo en esta fase.
- No tocar clústeres Kubernetes, kubeconfigs reales, credenciales, secrets, datos privados ni servicios externos.
- No realizar `git clean`, `reset --hard`, `push --force`, merge, rebase, cherry-pick, despliegues o releases.
- Sólo se permite escribir **documentación en el repositorio nuevo** en las rutas de salida definidas más abajo. No hacer commit/push/PR sin autorización posterior del usuario.

### 1. Rutas y repositorios: no confundas workspace con checkout

En la Mac del usuario las rutas previstas son:

```text
WORKSPACE = $HOME/Documents/lens
FUENTE    = $HOME/Documents/lens/lens-v6-ui-corrections
DESTINO   = $HOME/Documents/lens/novakube-native
```

**DESTINO (único lugar donde podés escribir):**
- GitHub: https://github.com/drko-dev/novakube-native
- Rama base: `main`
- Documentos rectores: `NOVAKUBE_NATIVE_MANIFIESTO.md`, `NOVAKUBE_NATIVE_RUNBOOK_MAESTRO.md`, `docs/AGENT_PROMPT_PROTOCOL.md`.
- Archivo de auditoría que vas a entregar: `docs/ux/audits/H00_01_AUDITORIA_VISUAL.md`.
- Archivo de continuidad: `docs/ux/audits/H00_01_HANDOFF.md`.
- No modificar otros documentos salvo indicación explícita.

**FUENTE (SOLO LECTURA; NO copiarla masivamente):**
- GitHub: https://github.com/drko-dev/lens
- Local: `$HOME/Documents/lens/lens-v6-ui-corrections`.
- Documento de análisis local: `PASAGE-OPENLENS-ELECTRON-A-RUST.md`; es contexto histórico, no un ADR aprobado. No copiarlo al repo público.
- Referencias que conviene leer, si existen:
  - `GEMINI.md` y `docs/GEMINI_HANDOFF_OPENLENS_H7_RC4_2026-11-04.md` (algunas instrucciones históricas de rama pueden estar desactualizadas).
  - `docs/H7_8_RC4_CIERRE.md`, `docs/H7_7_PERSISTENCIA_Y_RESTAURACION.md`.
  - `docs/H7_6_3_COMPONENTES_CON_ESTADO.md`, `docs/H7_6_4_VISTAS_GLOBALES.md`.
  - `docs/H8_AI_INCIDENTES_ROADMAP_2026-11-04.md` (roadmap histórico; la base H8 posteriormente se integró).
  - `packages/core/src/renderer/components/` y `packages/core/src/features/global-docking/`.
  - `packages/core/src/renderer/components/kubetail/`; `packages/core/src/renderer/components/dock/`.
- Si un documento falta o está desactualizado, registralo; **el código y Git vivo prevalecen** sobre un handoff viejo.

**Importante:** `$HOME/Documents/lens` es el directorio padre y no el Git root del producto. Hay otros proyectos hermanos, como `kubetail`, que no deben analizarse ni modificarse por confusión.

### 2. Snapshot orientativo al preparar el encargo (2026-11-10)

**NovaKube Native:** repositorio público `drko-dev/novakube-native`, branch `main`, commit inicial `e4639ea` (sólo 2 documentos, sin código), sin PR abiertos. No hay hito ejecutado; H00.01 es la primera auditoría.

**OpenLens fuente:** remote `drko-dev/lens`, default `develop`; integración visible `0003d6636e6fba08adff7800fc154c47af8a3644` del 7/11. PR #1 Kubetail, #2 H1-H7, #3 identidad NovaKube y #4 fundación H8/TypeScript estaban fusionados; no se detectaron PR abiertos en la comprobación. **Esto NO significa que las ramas locales estén integradas**.

**Fuente local:** worktree `lens-v6-ui-corrections` en rama `feature/novakube-high-contrast`, HEAD `59f6c7d4`; un segundo worktree `$HOME/Documents/lens/worktrees/develop` apuntaba a `1aebbd9b`. El worktree principal no tenía cambios rastreados, pero tenía **40 archivos sin seguimiento** en la comprobación. Preservalos; no listarlos indiscriminadamente en el repo público. La rama local puede diferir del `develop` remoto.

**Documentación del producto:** H7/RC4 constaba como QA interno; la fundación de H8 se integró a GitHub pero no acredita una release pública, ni certifica servicios de IA externos listos. No dar por implementada una funcionalidad sólo por un documento.

El snapshot es sólo para orientarte. **Comprobá todos estos hechos ahora mismo.** Si no tenés acceso a alguno de los repositorios o no podés verificar una parte de la experiencia visual, marcá esa área como pendiente y pedí el acceso/evidencia que falta. No inventes pantallas ni resultados.

### 3. Preflight obligatorio de lectura (antes de delegar)

1. Verificá que DESTINO y FUENTE existen, y confirmá sus Git roots, ramas actuales, HEAD, remotos y estado.
2. Comprobá los worktrees del producto anterior, no cambies de rama ni ejecutes `git fetch/pull` sin autorización.
3. Consultá GitHub de AMBOS proyectos: ramas principales, PR abiertos/draft/mergeados, checks fallidos y divergencias relevantes. Para datos no verificables marcá DESCONOCIDO.
4. Revisá el manifiesto, el runbook maestro y el protocolo de prompts. Identificá el padre H00, la fase RB-H00.01 y sus límites.
5. Revisá las evidencias visuales disponibles. No copies capturas a GitHub sin revisar redacción de nombres, rutas, tokens, IP, clusters y usuarios.
6. Publicá en tu respuesta al usuario un resumen de preflight con los riesgos, y **detenete** si hay un repositorio ambiguo, falta permiso o aparece un cambio inesperado en la fuente.
7. Definí un plan de auditoría en tareas breves y no superpuestas. Si el preflight es válido, ejecutá la auditoría de sólo lectura sin pedir autorización para cada paso inocuo.

Comandos de consulta orientativos: `pwd`, `git rev-parse --show-toplevel`, `git status --short --branch`, `git worktree list`, `git remote -v`, `git log -1 --oneline`, `gh pr list --repo drko-dev/novakube-native --state open`, `gh pr list --repo drko-dev/lens --state open`. No imprimir el contenido de archivos ocultos de credenciales.

### 4. Equipo Sonnet + Haiku

**Vos, Sonnet 5.5 — coordinador:**
- Leés los documentos rectores y preservás un único mapa de estado.
- Dividís el trabajo entre **hasta tres subagentes Sonnet** cuando las tareas sean independientes; evitá múltiples agentes sobre los mismos archivos.
- Les pasás explícitamente rutas, alcance, restricciones y formato de salida, porque no comparten necesariamente tu contexto.
- Reunís resultados, resolvés contradicciones, trazás conclusiones a rutas/evidencia y redactás los dos archivos de salida.
- No reescribas a ciegas un documento existente; verificá primero si contiene trabajo previo y recuperalo.

**Subagente Sonnet A — UX global:**
- Inspeccioná layout, catálogo, sidebar, navegación, listas, tablas, detalles, configuración y estados vacíos/error.
- Entregá flujos, componentes, rutas de evidencia y fricciones, sin editar archivos.

**Subagente Sonnet B — H7:**
- Inspeccioná tabs, docking, divisiones, resize, ventanas desacopladas, sesiones y persistencia.
- Diferenciá comportamiento demostrado por pruebas de aquello que sólo está descrito en documentos; entregá matriz y riesgos de reproducirlo en Rust.

**Subagente Sonnet C — herramientas operativas:**
- Inspeccioná Kubetail, logs, terminal y visualización del Centro de Incidentes H8, sin iniciar streams ni conexiones.
- Diferenciá UI presente, UI declarada y funciones no verificadas; proponé necesidades de UX.

**Haiku — QA independiente (después de recibir el borrador):**
- Tomá **el mismo runbook y el borrador terminado**, no sólo el resumen de Sonnet.
- Verificá cobertura, coherencia, trazabilidad, riesgos de privacidad, estados excepcionales, contradicciones y prohibiciones.
- Revisá cada afirmación crítica contra fuentes o marcala como no verificada.
- Emití un informe: PASS / REWORK / BLOCKED, hallazgo, evidencia y corrección recomendada.
- No otorgues PASS sólo porque Sonnet afirme que algo está completo.

**Estrategia de orquestación:** si tu instalación de Claude Code permite subagentes, usalos en contexto aislado y con permisos de lectura. Los Agent Teams pueden ser experimentales; no los habilites ni cambies configuración global sin pedir permiso. Si Sonnet 5.5 o Haiku no están disponibles con esos nombres, reportá las opciones reales y pedí al usuario cuál utilizar; no sustituir silenciosamente. Si falla un subagente, registrar el fallo y replanificar, sin fingir que terminó.

### 5. Qué auditar con criterios de UX

Cubrir como mínimo:
- Ventana principal, identidad NovaKube, toolbar, sidebar, búsqueda y catálogo de clústeres.
- Selección de clúster/contexto/namespace, orientación y feedback al cambiar.
- Pods y demás recursos; tablas densas, filtros, orden, selección y acciones.
- Detalles, YAML/editor y feedback de guardado/conflictos **como comportamiento visual**, sin editar Kubernetes.
- H7: tabs, separación de paneles, docking global, persistencia y restauración.
- Terminal: renderizado, estados de conexión, cierre, teclado y autorización visible.
- Kubetail: selección de fuentes, seguimiento, pausa, filtros, exportación y errores.
- H8: Centro de Incidentes y flujo de investigación cuando exista evidencia suficiente.
- Estados loading, empty, forbidden, offline, error, recuperación, uso de teclado y accesibilidad.

Para cada componente, indicá: propósito, ubicación de código o documento, evidencia, estado (VERIFICADO / DOCUMENTADO / NO VERIFICADO), problema UX, categoría CONSERVAR / MEJORAR / INVESTIGAR, impacto, prioridad y dependencia futura. Si no hay un entorno visual ejecutándose, el resultado es **auditoría de código y evidencia histórica**, no una «validación visual en vivo».

### 6. Entregables, exclusivamente documentales

Creá en el repo NUEVO:

**A. `docs/ux/audits/H00_01_AUDITORIA_VISUAL.md`**
- Fecha, alcance, método y límites de observación.
- Estado Git/PRs consultado (sin secretos).
- Inventario de pantallas y diagrama textual de navegación.
- Matriz CONSERVAR / MEJORAR / INVESTIGAR con fuentes.
- Estados excepcionales, UX de teclado, accesibilidad y multiventana.
- Comparación con requisitos del manifiesto y contrato candidato UX-01 (todavía borrador).
- Lista de dudas para el usuario; **no aprobar UX-01 unilateralmente**.
- Riesgos, decisiones abiertas, ideas de runbooks hijos H00.01.xx y criterios de aceptación del siguiente paso.

**B. `docs/ux/audits/H00_01_HANDOFF.md`**
- Timestamp, agente/modelo real y documento/prompt usados.
- Git roots, HEAD, ramas, estado de cambios y PRs de ambos repositorios.
- Trabajo terminado, trabajo no hecho, qué falta verificar.
- Tabla de evidencias y pruebas del auditor; resultado Haiku.
- Bloqueos, alertas de privacidad, estado GO / REWORK / HOLD.
- Si la sesión se corta, pasos exactos para reanudar sin perder información.
- PR o commit: consignar explícitamente «ninguno» si no se creó.

**No generar** capturas nuevas con datos reales, no subir archivos del proyecto anterior ni historial de conversaciones. Usá referencias de ruta de código y descripciones sanitizadas.

### 7. Condiciones de aceptación y cierre

El trabajo **no queda ACCEPTED** porque estén los Markdown. Deben cumplirse:
- Las áreas críticas de UX están inventariadas y sus evidencias son trazables.
- Las incertidumbres están marcadas y no aparecen como funciones confirmadas.
- El proyecto original no se modificó y no se ejecutaron conexiones reales.
- Haiku revisó de forma independiente y su resultado quedó registrado.
- El usuario puede leer la auditoría y decidir qué conservar/mejorar.
- Se proponen hijos recursivos sin crearlos ni ejecutarlos automáticamente.
- La revisión del usuario emite GO para H00.02, o REWORK/HOLD.

Al finalizar, entregá un resumen corto de hallazgos, archivos nuevos, tests/QA, bloqueos y **la decisión visual concreta que hay que tomar con el usuario**. No empieces RB-H00.02, no generes otro prompt, no abras PR y no hagas merge/publicación por tu cuenta.

## FIN DEL PROMPT
