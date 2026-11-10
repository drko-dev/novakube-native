# CLAUDE.md — Instrucciones del proyecto NovaKube Native

Proyecto público: https://github.com/drko-dev/novakube-native
Objetivo: nueva aplicación de escritorio Rust nativa, sin Electron, Tauri ni WebView; evolución visual y funcional de OpenLens DevOps, sin modificar el producto original.

## Lectura obligatoria al comenzar

1. `NOVAKUBE_NATIVE_MANIFIESTO.md` — visión, límites y responsabilidades.
2. `NOVAKUBE_NATIVE_RUNBOOK_MAESTRO.md` — árbol de hitos y sub-runbooks.
3. `docs/AGENT_PROMPT_PROTOCOL.md` — reglas OBLIGATORIAS para preparar cada prompt, preflight, roles, calidad y continuidad.
4. Runbook/prompt específico de la tarea: primero `docs/prompts/H00/RB-H00.01_REQA_SONNET_HAIKU.md` para cerrar el QA de H00.01; solamente después de GO humano, `docs/prompts/H00/RB-H00.02_FLUJOS_SONNET_HAIKU.md`. El prompt inicial archivado es `docs/prompts/H00/RB-H00.01_SONNET_5_5_HAIKU.md`.

## Antes de redactar un nuevo prompt

Preguntá explícitamente al usuario **qué IA/modelo y plataforma** usará para ejecutar, y **qué IA/modelo** usará para testing. Si lo indicó en el pedido actual, no repitas la pregunta. Verificá prácticas específicas y capacidades de esa IA, sin asumir funciones que no estén disponibles.

**En el primer hito ya están elegidos:** Sonnet 5.5 como coordinador y Haiku como tester independiente. Es una decisión SOLO para RB-H00.01: volver a consultar antes de otro prompt.

## Contexto y rutas

- Repo NUEVO, único destino de escritura: `$HOME/Documents/lens/novakube-native`, GitHub `drko-dev/novakube-native` (main).
- Repo LEGADO de referencia, SOLO LECTURA: `$HOME/Documents/lens/lens-v6-ui-corrections`, GitHub `drko-dev/lens`.
- `$HOME/Documents/lens` es el workspace PADRE; no usarlo como Git root.
- Trabajo de código del nuevo producto estará reservado a IAs ejecutoras autorizadas en hitos posteriores; la fase actual es de auditoría y documentación.
- No leer ni publicar secretos, kubeconfigs, capturas privadas o contenido sensible.
- Nunca alterar, borrar o sincronizar automáticamente el repositorio original.

## Protocolo de ejecución

Antes de trabajar, comprobar Git root, status, rama, HEAD, remotos, worktrees, PRs abiertos/cerrados, cambios locales, último hito aprobado y entregas interrumpidas. El snapshot de documentos viejos NO es autoridad sobre el estado vivo.

Aplicar el modelo de árbol de runbooks. Delegar tareas independientes con contexto completo y límites de herramientas, probar con agente independiente, entregar evidencia y HANDOFF. No dar por ACCEPTED un hito sin revisión del usuario. No iniciar hijos nuevos automáticamente. No modificar producción ni hacer merges/releases sin autorización.

Si una tarea no tiene todos los datos, detenerse y preguntar. Para detalles operativos, **no sustituir** el protocolo `docs/AGENT_PROMPT_PROTOCOL.md` por este índice.
