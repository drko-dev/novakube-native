# Prompt de cierre QA — RB-H00.01 / REQA independiente Haiku

**Versión:** 1.0 — 2026-11-10
**Fase:** corrección y segunda verificación de auditoría documental H00.01.
**Estado inicial:** IN_REVIEW / REWORK menor; **NO ACCEPTED**.
**Modelo y entorno acordados para este prompt:** Claude Code; coordinador Sonnet 5.5; auditor independiente Haiku.
**Proyecto:** https://github.com/drko-dev/novakube-native

---

## COMIENZO DEL PROMPT

Sos **Sonnet 5.5, coordinador de re-QA**, usando Claude Code y **Haiku como revisor independiente**. La tarea es **cerrar únicamente las brechas de revisión del runbook RB-H00.01**, NO comenzar H00.02. El usuario conserva la aprobación final. No hay autorización de programar aplicaciones ni publicar documentos de auditoría por ahora.

### A. Repositorios inequívocos

- **Destino, único repositorio editable:** `$HOME/Documents/lens/novakube-native`, GitHub `drko-dev/novakube-native`, rama base `main`.
- **Fuente de referencia, estrictamente solo lectura:** `$HOME/Documents/lens/lens-v6-ui-corrections`, GitHub `drko-dev/lens`.
- **Workspace padre:** `$HOME/Documents/lens` (NO es un repositorio Git).
- **Rutas de escritura autorizadas:** `docs/ux/audits/H00_01_AUDITORIA_VISUAL.md`, `docs/ux/audits/H00_01_HANDOFF.md`, y `docs/ux/audits/H00_01_REQA_HAIKU.md`. Preservar datos y revisiones previas; no sobrescribir a ciegas.
- **No modificar** `NOVAKUBE_NATIVE_MANIFIESTO.md`, `NOVAKUBE_NATIVE_RUNBOOK_MAESTRO.md`, `CLAUDE.md`, `docs/AGENT_PROMPT_PROTOCOL.md`, ni la decisión de producto `docs/architecture/DEC-UX-001_WORKSPACE_MVP.md` sin autorización.

### B. Lecturas iniciales completas

Leé, sin resumir antes de revisar:
1. `CLAUDE.md`
2. `NOVAKUBE_NATIVE_MANIFIESTO.md`
3. `NOVAKUBE_NATIVE_RUNBOOK_MAESTRO.md`
4. `docs/AGENT_PROMPT_PROTOCOL.md`
5. `docs/architecture/DEC-UX-001_WORKSPACE_MVP.md`
6. `docs/prompts/H00/RB-H00.01_SONNET_5_5_HAIKU.md` **completo, especialmente §5, §6.A y criterios de aceptación**.
7. `docs/ux/audits/H00_01_AUDITORIA_VISUAL.md` completo.
8. `docs/ux/audits/H00_01_HANDOFF.md` completo.

No dependas de un resumen de la conversación. Comprobá que todos existen y usá lectura por fragmentos si el entorno trunca la respuesta. El revisor Haiku debe recibir acceso al **texto íntegro** y poder leer las secciones pendientes por sí mismo.

### C. Snapshot útil, para contrastar con Git vivo

**Verificado al preparar este prompt (2026-11-10, sin fetch/pull):**
- Repositorio nuevo público: `drko-dev/novakube-native` `main` en `b368fa7`, sincronizado con `origin/main`, sin PR abiertos.
- Estado local nuevo: dos documentos de auditoría sin seguimiento en `docs/ux/audits/`; también `.DS_Store`, `docs/.DS_Store`, `docs/prompts/.DS_Store` sin seguimiento. **No agregarlos al staging ni borrarlos.**
- Fuente: `drko-dev/lens`, branch local `feature/novakube-high-contrast`, HEAD `59f6c7d4`; segundo worktree `$HOME/Documents/lens/worktrees/develop` en `1aebbd9b`. Sin cambios rastreados, múltiples archivos sin seguimiento preexistentes; intocables.
- GitHub fuente: branch principal `develop` (último HEAD público previamente comprobado `0003d663`); PR #1–#4 mergeados, ninguno abierto en la consulta.
- `DEC-UX-001` registrada en commit `b368fa7`: **docking global único, ventanas desacopladas y multimonitor obligatorios desde el PRIMER MVP**. No inferir que la fuente ya los implementa.
- Auditoría actual: IN_REVIEW, re-QA pendiente; no se ejecutó la aplicación ni tests.

**No tomes este snapshot como verdad permanente.** Antes de delegar verificá los Git roots y `git status --short --branch`, `git log -1 --oneline`, `git worktree list`, remotos, divergencia y PR de ambos repos vía GitHub. Detectá cambios posteriores y trabajos interrumpidos. Si hubo una entrega más nueva o un GO explícito, no pises trabajo: detenete y reportá.

### D. Alcance exacto del re-QA

El primer QA de Haiku emitió **REWORK**. Sonnet corrigió partes de la auditoría, pero Haiku todavía no validó el documento **después de las correcciones**. Los puntos concretos pendientes son:

1. **Revisar íntegramente la versión corregida**, no la versión original que rechazó Haiku.
2. **Cubrir de forma independiente §5 y §6.A del prompt original**. En la primera ronda Haiku no pudo leerlas; no alcanza la autoverificación del coordinador.
3. Reabrir los **16 chequeos del primer QA** y contrastar contra las fuentes de código que corresponda; etiquetar CONFIRMADO / REFUTADO / NO VERIFICABLE, con ruta y línea si se dispone.
4. Confirmar el hallazgo de `prefers-reduced-motion` (existe en `midnight-graphite.scss`, no decir que está ausente), rango ARIA dependiente del patrón, texto de errores y ratios divergentes de split, sin depender del resumen del coordinador.
5. Revisar expresamente **Kubetail**: límite de 50 streams, pausa/buffer de 2000, advertencia disponible, si existen contadores de descarte y diferencia entre silencio total y visibilidad parcial. No afirmar «descarta sin avisar» cuando hay indicación de buffer capped; expresar con precisión qué se informa y qué no.
6. Verificar —o señalar sin ambigüedad como no contrastado— las rutas mencionadas en el handoff: `kubetail-page.tsx:242,261`, `odd/tasks/h7-6-3d-terminal.md`, `docs/evidence/h7-4/`, `table-row.tsx:44-45`, HEAD remoto `ce90eaf` del snapshot anterior (ya desactualizado).
7. Comprobar **estados excepcionales, accesibilidad, evidencia y trazabilidad** de la auditoría, distinguiendo código presente, test nombrado (no ejecutado), documentación y comportamiento NO VERIFICADO.
8. Revisar que **DEC-UX-001 esté representada como decisión del MVP**: docking global único, ventanas desacopladas y multimonitor en la PRIMERA versión MVP. No confundir la decisión con implementación completa ni con UX-01 aprobado.
9. Hacer un control de privacidad del contenido destinado a repositorio público: rutas personales, kubeconfigs, tokens, datos de clúster, IP, correos, capturas privadas o rutas locales específicas que identifiquen al usuario.

**No hacer tests/builds ni iniciar la app:** este re-QA es lectura, comparación de fuentes, documentación y QA de integridad. No leer kubeconfigs ni conectarse a Kubernetes. La evidencia histórica no sustituye pruebas ejecutadas.

### E. Orquestación Sonnet + Haiku

- **Sonnet:** realiza preflight y prepara la lista numerada de afirmaciones para QA; **no emite PASS sobre su propia corrección**. Puede asignar UNA lectura puntual a otro subagente Sonnet si una evidencia es demasiado extensa; no crear un equipo experimental sin permiso.
- **Haiku:** debe hacer revisión real e independiente, leyendo código fuente relevante, documento corregido y secciones del prompt original; reportar cada hallazgo con evidencia. Su resultado debe quedar preservado **antes de que Sonnet cambie el documento**.
- **Sonnet:** para cada REWORK, corrige de manera mínima la auditoría o marca el punto no verificado, registrando cambios y motivos.
- **Haiku (segunda pasada si hubo nuevas correcciones):** revisa el documento final modificado. No aceptar una aprobación de una versión anterior como aprobación de la final.
- Si el entorno no permite un Haiku real, informá el bloqueo y parate. No simular un informe Haiku ni hacer autocalificación.
- Preferir subagente aislado con herramientas de lectura; verificar la identidad/modelo que efectivamente ejecuta el subagente, porque `Explore` puede heredar el modelo del coordinador. Si hay duda, ejecutar Haiku como sesión independiente de sólo lectura.

### F. Entregables

**`docs/ux/audits/H00_01_REQA_HAIKU.md`**
- Fecha, modelo real Haiku, qué leyó, método y límites.
- Tabla de requisitos 1–9, 16 afirmaciones y estado por evidencia.
- Veredicto independiente: **PASS / REWORK / BLOCKED**, detalles de los fallos y qué se revisó luego de cada corrección.
- Evidencia reproducible de forma segura y nota de que no hubo ejecución visual ni tests.

**`docs/ux/audits/H00_01_AUDITORIA_VISUAL.md`**
- Sólo correcciones trazables imprescindibles a partir de QA, sin reescribir la auditoría íntegra ni proclamar UX-01 aprobado. Las incertidumbres permanecen visibles.

**`docs/ux/audits/H00_01_HANDOFF.md`**
- Actualizar estado de QA y lista de pendientes, no borrar hallazgos históricos ni fingir que las pruebas fueron ejecutadas.
- Registrar Git/PR al cerrar, archivos cambiados, riesgos, PASS/REWORK/BLOCKED de Haiku, solicitudes de decisión del usuario, siguiente paso y mecanismo de recuperación tras interrupción.
- El estado del hito sigue **IN_REVIEW** hasta que el usuario dé aceptación explícita. El QA por sí solo NO autoriza H00.02.

### G. Finalización y prohibiciones

Presentá en pantalla al usuario un resumen muy corto: qué verificó realmente Haiku, qué faltó, qué cambió, veredicto y recomendación de **GO / REWORK / HOLD** para la revisión humana. **NO declarar GO humano por tu cuenta.**

No hacer commit, push, PR, merge, release, rollback, modificar la fuente ni comenzar H00.02 sin autorización explícita. No incluir jamás `.DS_Store` en los commits futuros.

## FIN DEL PROMPT
