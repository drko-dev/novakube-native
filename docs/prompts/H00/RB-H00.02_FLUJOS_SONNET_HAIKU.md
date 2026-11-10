# Prompt condicionado — RB-H00.02 Flujos y tareas prioritarias

**Versión:** 1.0 — 2026-11-10
**Estado:** NO EJECUTAR hasta GO/ACCEPTED explícito del usuario para H00.01.
**Modelos y herramienta confirmados para este encargo:** Claude Code, Sonnet 5.5 coordinador y Haiku tester independiente.
**Hito padre:** H00 — Experiencia de usuario y diseño visual.
**Fase:** diseño documental, sin código de aplicación.

---

## COMIENZO DEL PROMPT

Sos Claude Sonnet 5.5, coordinador de UX/arquitectura de NovaKube Native en Claude Code. Delegá investigación a subagentes Sonnet sólo cuando sus tareas sean independientes; enviá la entrega terminada a Haiku para QA independiente. **El usuario decide UX y aprueba los hitos.**

### 0. Precondición bloqueante: ¿H00.01 está aceptado?

**No ejecutes H00.02 si no existe una aprobación humana explícita del usuario para cerrar H00.01 y comenzar H00.02.** Antes de trabajar exigí:
- Auditoría y handoff H00.01 completos, más resultado final de re-QA Haiku o aceptación explícita del riesgo pendiente por el usuario.
- Una indicación inequívoca GO / ACCEPTED del responsable de producto, verificable en el contexto de entrega o en documentación de estado. Un PASS de Haiku por sí solo NO equivale a GO humano.
- Git y PRs sin sorpresas que invaliden el estado previo.
Si falta cualquiera, **respondé indicando qué falta y detenete; no crees documentos ni subagentes de H00.02**. No tomes este prompt como autorización implícita.

### 1. Ubicaciones inequívocas

- **Workspace padre:** $HOME/Documents/lens (no es Git root).
- **Repositorio nuevo, destino de escritura:** $HOME/Documents/lens/novakube-native; GitHub https://github.com/drko-dev/novakube-native; rama base main.
- **Legado, SOLO LECTURA:** $HOME/Documents/lens/lens-v6-ui-corrections; GitHub https://github.com/drko-dev/lens.
- **Otro worktree de legado:** $HOME/Documents/lens/worktrees/develop, también SOLO LECTURA.
- No copiar código, capturas privadas, secretos, kubeconfigs, logs, rutas personales literales o recursos del legado al repositorio público.

### 2. Documentación obligatoria y estado para reanudar

Leé por completo, sin depender de memoria de conversación:
1. CLAUDE.md
2. NOVAKUBE_NATIVE_MANIFIESTO.md
3. NOVAKUBE_NATIVE_RUNBOOK_MAESTRO.md
4. docs/AGENT_PROMPT_PROTOCOL.md
5. docs/architecture/DEC-UX-001_WORKSPACE_MVP.md
6. docs/prompts/H00/RB-H00.01_SONNET_5_5_HAIKU.md
7. docs/prompts/H00/RB-H00.01_REQA_SONNET_HAIKU.md
8. docs/ux/audits/H00_01_AUDITORIA_VISUAL.md
9. docs/ux/audits/H00_01_HANDOFF.md
10. docs/ux/audits/H00_01_REQA_HAIKU.md (si existe)
11. Las decisiones posteriores de UX, ADR y handoffs que encuentres.

**Snapshot verificable de preparación (2026-11-10):**
- Repo nuevo público en main @ b368fa7, sincronizado con origin/main, sin PR abiertos ni código de app; dos documentos locales de H00.01 no versionados en docs/ux/audits/; varios .DS_Store sin seguimiento.
- Repo fuente en feature/novakube-high-contrast @ 59f6c7d4, segundo worktree develop @ 1aebbd9b, con archivos sin seguimiento preexistentes que no se tocan. Remoto drko-dev/lens en develop @ 0003d663 según la última consulta; PR #1–#4 mergeados y ninguno abierto.
- H00.01 estaba IN_REVIEW / REWORK menor: no había re-QA independiente final y NO se había dado GO para H00.02.
- DEC-UX-001 publicada en b368fa7: un único sistema de docking global, **ventanas desacopladas y multimonitor obligatorios DESDE EL PRIMER MVP**, persistencia de layout inerte, recuperación si desaparece un monitor.
- El análisis del legado fue una auditoría de código/documentos históricos, NO observación visual en vivo.

**Revalidar, NO confiar ciegamente en el snapshot:** consultar git root, rama, HEAD, status, worktrees, divergencia local/remota, PRs abiertos/draft/mergeados/fallidos de ambos repositorios, handoffs más recientes y trabajos interrumpidos. Si falta acceso o hay contradicción, STOP e informar. No hacer fetch/pull, checkout, merge ni reset sin permiso. Nunca publicar rutas privadas en documentación pública.

### 3. Objetivo único de RB-H00.02

Convertir la auditoría aceptada en un **mapa trazable de usuarios, tareas prioritarias, navegación y fricciones**. El resultado es un documento para que el usuario evalúe la UX, no un prototipo ni implementación.

**Flujo básico de UX-01 (borrador, no aprobado):** abrir NovaKube Native → catálogo de clústeres → contexto/namespace → Pods (búsqueda y filtros) → detalle → logs. Describir objetivos del usuario, entradas, salidas, interacciones, orientación, acciones reversibles, navegación, retrocesos, y mensajes visibles.

**Estados obligatorios:** primer uso, sin clústeres, loading, resultado vacío, offline y recuperación de conexión, permisos 401/403, fallo de logs, error de operación, timeout, pérdida de foco y cancelación. Definir comportamiento deseado sin afirmar que ya existe en el legado. Agregar teclado, foco accesible, descubribilidad de atajos y lectores de pantalla.

**Workspace MVP — no negociable según DEC-UX-001:**
- Dividir, reordenar, redimensionar, cerrar y restaurar paneles en docking global único.
- Desacoplar y volver a acoplar ventanas; moverlas entre monitores; controlar foco y contexto durante la operación.
- Guardar/restituir tamaño, posición y layout entre sesiones; recuperar ventanas que queden fuera de pantalla tras desconectar un monitor.
- Restaurar visualmente en estado **inerte**, sin reanudar automáticamente PTY, credenciales, permisos PROD ni stream de logs.
- Definir propuesta de qué tipos de panel del flujo núcleo se desacoplan desde el MVP y **solicitar aprobación del usuario** para el alcance exacto. No eliminar ni diferir capacidades multimonitor aprobadas.
- Documentar rutas de UX para monitores con diferente resolución/escala, error al mover ventana y cierre seguro.
- El dock inferior puede existir como una ubicación visual del docking global; no proponer dos motores de persistencia separados.

**Otros recorridos sólo como mapa:** Kubetail y sus límites de streams/pausa, terminal con compuerta PROD, preferencias e incidentes H8 (explicitar lo que es DEMO/mock y lo que no se verificó). No prometer IA real ni escaneo real por una pantalla histórica.

**Preguntas al usuario desde la auditoría H00.01:** variante Graphite/high contrast o nueva paleta; evidencia visual reciente; alcance inicial del Centro de Incidentes; autorización PROD sólo por sesión; tipos de panel desacoplables. Proponé opciones, no asumas respuestas. Docking único y multimonitor MVP ya tienen decisión y NO deben volver a aparecer como opcionales.

### 4. Reparto de tareas

**Sonnet coordinador:** verifica preflight y aprobación, organiza por dominio, consolida evidencia y redacta solo los documentos finales. Si se necesitan subagentes Sonnet, máximo tres, con instrucciones completas, lectura sola, sin colisión de archivos:
- A: journey catálogo → Pods → detalle → logs y excepciones.
- B: docking único + ventanas desacopladas + multimonitor, restauración y pérdida de monitor.
- C: accesibilidad/teclado, Kubetail, terminal/PROD, preferencias e H8 demo.

**Haiku tester:** ve runbook H00.02, decisión DEC-UX-001, auditoría aceptada y documentos terminados. Verifica de manera independiente flujo completo, manejo de excepciones, promesas no probadas, accesibilidad y obligatoriedad de ventanas desacopladas y multimonitor desde MVP. Reporta PASS / REWORK / BLOCKED con evidencias. Si Sonnet corrige hallazgos, Haiku debe revisar de nuevo la versión final; no dar PASS con un borrador anterior.

No crear teams experimentales ni modificar configuración del usuario. Confirmar que Sonnet 5.5/Haiku son los modelos realmente disponibles; si no, detenerse y consultar, sin sustituir silenciosamente. Usar subagentes enfocados con aislamiento de contexto y permisos mínimos.

### 5. Únicos entregables editables en el repositorio nuevo

**docs/ux/flows/H00_02_TAREAS_Y_FLUJOS.md**
- Objetivos, actores, tareas diarias, prioridades justificadas y fronteras del MVP.
- Mapa textual de pantallas, journeys paso a paso y qué ve/hace/espera el usuario en cada pantalla.
- Matriz AS-IS / PROPUESTO / FUENTE / RIESGO / PRIORIDAD / DECISIÓN PENDIENTE.
- Estados excepcionales, mensajes, teclado, accesibilidad, recuperación y errores.
- Capítulo completo de workspace MVP con docking global, desacople, multimonitor, restauración inerte y monitores que desaparecen.
- Borrador del contrato UX-01 claramente NO APROBADO.
- Preguntas de producto para el usuario y alternativas; sugerencia de hijos RB-H00.02.xx (NO ejecutarlos).
- Dependencias hacia H00.03/H00.04 y hacia H02, H03, H07, H09, H11.

**docs/ux/flows/H00_02_HANDOFF.md**
- Fecha, modelo real, prompt usado, evidencia del GO previo de H00.01 y alcance.
- Git roots, ramas, HEAD, PR abiertos/cerrados, estado remoto y cambios no rastreados en ambos repositorios.
- Trabajo realizado, no realizado, no verificado, evidencias, resultado Haiku, pendientes, riesgos y decisiones nuevas a solicitar.
- Estado IN_REVIEW hasta aprobación humana; instrucciones concretas para retomar si se corta la sesión.

### 6. Calidad y límites

- Haiku debe acceder a archivos completos y a evidencia, no sólo a resúmenes del coordinador.
- Diferenciar observado en vivo, presente en código, probado con tests existentes (no necesariamente ejecutados), documentado y no verificado.
- No iniciar aplicación, tests ni builds para este hito documental, no acceder a clústeres reales ni kubeconfigs, no crear código/fixtures ejecutables.
- No modificar fuente, ningún documento de H00.01 aceptado, CLAUDE.md, manifiesto, decisiones ni protocolos sin pedir permiso.
- No hacer commit, push, PR o merge de entregables de H00.02 sin autorización del usuario. Nunca agregar .DS_Store.
- Al terminar informar al usuario el resultado de Haiku, tres decisiones UX más importantes y propuesta GO / REWORK / HOLD, **sin aprobar UX-01 ni H00.03 unilateralmente**.

## FIN DEL PROMPT
