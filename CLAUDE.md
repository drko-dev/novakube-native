# CLAUDE.md — Instrucciones del proyecto NovaKube Native

Proyecto público: https://github.com/drko-dev/novakube-native
Objetivo: nueva aplicación de escritorio Rust nativa, sin Electron, Tauri ni WebView; evolución visual y funcional de OpenLens DevOps, sin modificar el producto original.

## Lectura obligatoria al comenzar

1. `NOVAKUBE_NATIVE_MANIFIESTO.md` — visión, límites y responsabilidades.
2. `NOVAKUBE_NATIVE_RUNBOOK_MAESTRO.md` — árbol de hitos y sub-runbooks.
3. `docs/AGENT_PROMPT_PROTOCOL.md` — reglas OBLIGATORIAS para preparar cada prompt, preflight, roles, calidad y continuidad.
4. **Estado actual:** H00.01 ACCEPTED WITH DOCUMENTED DEBT; H00.02 IN_REVIEW (Haiku PASS con reservas, UX-01 NO aprobado). DEC-UX-001 y DEC-UX-002 aprobadas. **Encargo activo de implementación experimental:** `docs/prompts/H02/RB-H02.00_SPIKE_UI_NATIVE_SONNET_HAIKU.md` (únicamente código Rust aislado en `experiments/ui/`, no H03). Los prompts H00 permanecen como historial.

## Antes de redactar un nuevo prompt

Preguntá explícitamente al usuario **qué IA/modelo y plataforma** usará para ejecutar, y **qué IA/modelo** usará para testing. Si lo indicó en el pedido actual, no repitas la pregunta. Verificá prácticas específicas y capacidades de esa IA, sin asumir funciones que no estén disponibles.

**Para RB-H02.00, confirmado nuevamente por el usuario:** Claude Code con Sonnet 5.5 coordinador multiagente y Haiku revisor independiente. Para el siguiente prompt nuevo, volver a consultar el modelo/entorno según protocolo.

## Contexto y rutas

- Repo NUEVO, único destino de escritura: `$HOME/Documents/lens/novakube-native`, GitHub `drko-dev/novakube-native` (main).
- Repo LEGADO de referencia, SOLO LECTURA: `$HOME/Documents/lens/lens-v6-ui-corrections`, GitHub `drko-dev/lens`.
- `$HOME/Documents/lens` es el workspace PADRE; no usarlo como Git root.
- En RB-H02.00 las IAs ejecutoras están autorizadas a **crear exclusivamente prototipos Rust aislados** bajo `experiments/ui/` y documentación/evidencia del spike según el prompt. No equivale a permiso de modificar el producto original ni de comenzar H03. H00.02 sigue en revisión. El asistente de arquitectura no escribe código de aplicación.
- No leer ni publicar secretos, kubeconfigs, capturas privadas o contenido sensible.
- Nunca alterar, borrar o sincronizar automáticamente el repositorio original.

## Protocolo de ejecución

Antes de trabajar, comprobar Git root, status, rama, HEAD, remotos, worktrees, PRs abiertos/cerrados, cambios locales, último hito aprobado y entregas interrumpidas. El snapshot de documentos viejos NO es autoridad sobre el estado vivo.

Aplicar el modelo de árbol de runbooks. Delegar tareas independientes con contexto completo y límites de herramientas, probar con agente independiente, entregar evidencia y HANDOFF. No dar por ACCEPTED un hito sin revisión del usuario. No iniciar hijos nuevos automáticamente. No modificar producción ni hacer merges/releases sin autorización.

Si una tarea no tiene todos los datos, detenerse y preguntar. Para detalles operativos, **no sustituir** el protocolo `docs/AGENT_PROMPT_PROTOCOL.md` por este índice.
