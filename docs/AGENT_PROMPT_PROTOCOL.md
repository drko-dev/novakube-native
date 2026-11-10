# Protocolo obligatorio para preparar prompts de agentes — NovaKube Native

**ID:** GOV-AI-001 · **Versión:** 1.0 · **Fecha:** 2026-11-10
**Estado:** vigente para toda propuesta de prompt posterior.
**Documentos rectores:** `NOVAKUBE_NATIVE_MANIFIESTO.md` y `NOVAKUBE_NATIVE_RUNBOOK_MAESTRO.md`.

## A. Confirmar la IA antes de CADA prompt

**Antes de redactar o regenerar cualquier nuevo prompt**, preguntar explícitamente qué IA, modelo y herramienta/entorno utilizará el usuario, y qué IA/modelo hará el testing. No perpetuar la última combinación como decisión para futuros hitos. Si el usuario especifica esos datos en su pedido actual, esa confirmación ya existe: no preguntar otra vez.

Verificar si se trata de Claude Code, Anthropic API, otro IDE o entorno con agentes; las capacidades de delegación varían. Si no es claro, preguntar primero; no inventar soporte de agentes, permisos ni nombres de modelo. Consultar buenas prácticas actuales y específicas del proveedor/modelo en su documentación oficial antes de escribir instrucciones operativas. La decisión del modelo se documenta en el encabezado de cada encargo, con fecha y alternativas si no está disponible.

**Configuración confirmada PARA RB-H00.01:** Sonnet 5.5 como coordinador multiagente; Haiku como verificador independiente. Es una preferencia del usuario, no una certificación de que esos identificadores estén disponibles en su instalación concreta.

## B. Reconstituir el contexto real, no usar sólo un resumen de chat

Antes de crear cada prompt, comprobar el estado vivo de los dos proyectos y registrar FECHA y ORIGEN de los datos:

- **Proyecto nuevo (destino):** repositorio público `drko-dev/novakube-native`; carpeta local por defecto `$HOME/Documents/lens/novakube-native`; rama principal `main`.
- **Proyecto de referencia (fuente, SOLO LECTURA):** `drko-dev/lens`; carpeta local `$HOME/Documents/lens/lens-v6-ui-corrections`. La carpeta `$HOME/Documents/lens` es el workspace padre, NO el checkout Git original.
- **Documento histórico local:** `$HOME/Documents/lens/lens-v6-ui-corrections/PASAGE-OPENLENS-ELECTRON-A-RUST.md`. Es un análisis, no una decisión definitiva de framework ni un archivo que deba publicarse íntegro.
- **Estado de ambos repos:** rutas realmente existentes, `git rev-parse --show-toplevel`, `git status --short --branch`, `git worktree list`, `git remote -v`, ramas y SHA HEAD.
- **Comparación:** conocer default branch, HEAD de la rama remota, divergencias locales-remotas, cambios sin seguimiento, commits pendientes, ramas de trabajo y worktrees. No asumir que dos copias llamadas develop son idénticas.
- **PRs:** consultar GitHub de AMBOS repos para detectar abiertos, borradores, cerrados/mergeados, checks fallidos, revisiones pendientes, conflictos y tareas parcialmente entregadas. Registrar enlaces y bloqueo concreto. Un PR cerrado no implica un release válido.
- **Continuidad:** identificar último hito ACCEPTED, actual READY/DELEGATED/IN_REVIEW, artefactos previos, evidencia, deuda, decisiones ADR, riesgos, interrupciones, intentos fallidos y próximos pasos. Si falta información, marcar DESCONOCIDO; no inventar ni dar un hito por cerrado.
- **Sensibilidad:** jamás publicar tokens, kubeconfig, rutas personales literales, nombres reales de clusters/usuarios, logs privados, capturas no sanitizadas ni archivos de trabajo no revisados. En documentos públicos usar `$HOME` y datos sintéticos.

El prompt debe contener un **snapshot con fecha**, aclarar que podría envejecer, y ordenar al agente que valide el entorno otra vez al comenzar. Prohibido iniciar ejecución si repo, rama, permisos o precondiciones no coinciden.

## C. Estructura mínima de un prompt nuevo

1. **Identidad:** ID exacto de runbook, versión, fase, objetivo único y resultado observable.
2. **Modelos y roles:** coordinador, subagentes, tester; límites de herramienta y responsabilidades. No sobredimensionar el equipo.
3. **Rutas inequívocas:** repositorio donde LEER, donde ESCRIBIR y ramas permitidas. Qué NO tocar.
4. **Contexto verificado:** estado Git y PRs; documentos canónicos; alcance implementado/no implementado, impedimentos y worktrees.
5. **Preflight obligatorio:** comandos no destructivos, verificación de divergencia y recuperación de sesión anterior.
6. **Plan y desglose:** tareas pequeñas independientes, dueño, dependencias, salida y posibles hijos recursivos.
7. **Contrato de producto/UX:** pantallas, flujos, estados normales/error/denegado, accesibilidad y feedback del usuario.
8. **Permisos y seguridad:** lectura/escritura limitada, prohibiciones, datos sintéticos, ausencia de cambios en producción.
9. **Entrega verificable:** archivos autorizados, formato, evidencias sanitizadas, criterios de aceptación.
10. **Testing independiente:** Haiku valida contra el runbook y busca omisiones, no confirma por cortesía.
11. **Checkpoint y handoff:** qué se hizo, qué no, pruebas, problemas, decisiones, PR/branch/commit, estado y siguiente tarea.
12. **Puntos de aprobación:** detenerse para dudas críticas, aceptar UX, ampliar alcance, publicar o mergear.

Si un runbook aún es documental, no permitir escribir código. Si la tarea implica código más adelante, no crear un encargo de implementación sin un contrato aprobado.

## D. Buenas prácticas para Claude (sujetas a verificación al iniciar sesión)

- Sonnet coordina y sintetiza, divide por dominios *independientes*; no hace que varios agentes editen los mismos archivos.
- Subagentes especialistas con contexto aislado, tarea delimitada, lectura de documentos canónicos y reporte estructurado; el coordinador conserva la decisión de integración.
- Haiku se reserva para QA focalizado y verificaciones repetibles, con una lista de requisitos y evidencias; si necesita juicio arquitectónico profundo, escala el hallazgo a Sonnet.
- En auditorías, usar subagentes **de solo lectura** y preferir tareas breves: navegación/UI, módulos de docking, logs/terminal y revisión de privacidad.
- Los agent teams de Claude Code son experimentales y pueden no estar activados; comprobar su disponibilidad y usar subagentes comunes si no existen. No activar opciones experimentales ni modificar configuración global por cuenta propia.
- Dar a cada agente las rutas de repositorios, documentación y límites en su encargo individual: los agentes no deben depender de conocer la conversación del coordinador.
- Limitar tamaño del equipo y coste; evitar agentes duplicados, ejecuciones paralelas innecesarias y revisiones con el mismo autor sin independencia real.
- Al terminar, Sonnet debe esperar los resultados de todos, reconciliar contradicciones y solicitar revisión de Haiku antes de declarar la entrega lista para el usuario.

**Referencias de proveedor:** [Subagentes en Claude Code](https://code.claude.com/docs/en/sub-agents) y [Equipos de agentes en Claude Code](https://code.claude.com/docs/en/agent-teams). Consultarlas nuevamente si cambian capacidades o modelos.

## E. Protocolo anti-pérdida de contexto

Cada sesión deja un bloque **HANDOFF** en la entrega del hito y en su resultado visible:

| Campo | Obligatorio |
| --- | --- |
| Timestamp / agente / versión del prompt | Sí |
| Repo destino + rama + HEAD + estado de cambios | Sí |
| Repo fuente + rama + HEAD (solo lectura) | Sí |
| Hito actual y padres/hijos | Sí |
| Hecho realmente / pendiente / no verificado | Sí |
| Archivos entregados y ubicación | Sí |
| Pruebas/evidencias, resultados y límites | Sí |
| PR abiertos, fallidos, en revisión o bloqueados | Sí |
| Riesgos, bloqueos, decisiones ADR | Sí |
| Próxima acción concreta y condición para ejecutarla | Sí |

Si hay interrupción o se pierde contexto, el primer paso es leer el último HANDOFF, verificar Git/PRs y reanudar **sin borrar ni repetir trabajo aprobado**. Registrar las diferencias con el estado anterior. No usar `git clean`, `reset --hard`, `push --force`, merges automáticos ni acceso a producción para recuperar una sesión.

## F. Calidad, revisión y límites de publicación

- La ejecución y el testing se documentan por separado. Haiku devuelve PASS / REWORK / BLOCKED con evidencia y pendientes.
- No confundir una auditoría visual aprobada con un prototipo implementado ni una demo con una integración Kubernetes.
- Ningún sub-runbook aumenta permisos ni modifica el código de `drko-dev/lens`. Toda ampliación de alcance requiere consulta.
- Las entregas documentales van únicamente a `drko-dev/novakube-native`; no publicar capturas con datos reales.
- En futuros cambios de código, ramas/PR revisables por tema y gates de calidad; no desplegar ni fusionar por inercia.
- Antes de redactar el SIGUIENTE prompt, **volver al apartado A** y preguntar otra vez la IA y su entorno, sin depender de memoria conversacional.

**Norma de uso:** todo nuevo prompt debe enlazar a este protocolo y al runbook padre; no basta decir «seguí las buenas prácticas».
