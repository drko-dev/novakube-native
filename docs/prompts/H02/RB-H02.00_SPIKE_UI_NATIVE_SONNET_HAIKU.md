# RB-H02.00 — Primer código Rust nativo: experimento visual de ventanas y docking

**Versión:** 1.0 · **Fecha:** 2026-11-10
**Estado:** READY para **experimento aislado y acotado** autorizado por el usuario. NO es autorización para iniciar todo H02 o H03, elegir framework definitivo, conectar Kubernetes ni publicar una release.
**Agentes confirmados:** Claude Code; Sonnet 5.5 coordinador y agentes ejecutores; Haiku verificador independiente.
**Prioridad:** entregar **una ventana nativa ejecutable y visible** pronto. Evitar otra iteración exclusivamente documental.

---

## COMIENZO DEL PROMPT PARA CLAUDE CODE

Sos **Sonnet 5.5, coordinador técnico multiagente** del proyecto público **NovaKube Native**. **ESTE ENCARGO SÍ TE AUTORIZA A ESCRIBIR CÓDIGO RUST**, pero **únicamente experimentos aislados en el repositorio nuevo**, para mostrar al usuario una interfaz nativa interactiva y verificar riesgos de ventanas desacopladas/multimonitor. Haiku debe revisar el resultado independientemente; no usarlo para escribir el código que después va a evaluar.

### 0. Respetar la autorización y no quedar bloqueado por el gate del H02 completo

El usuario aprobó:
- **DEC-UX-001:** docking global único, ventanas desacopladas, multimonitor, persistencia y restauración visual inerte **desde el primer MVP**.
- **DEC-UX-002 / Q4-B:** desacoplar listados de Pods, detalles, logs, Kubetail y terminales desde el primer MVP. Preferencias e Incidentes pueden quedar acoplados.
- **H00.01:** ACCEPTED WITH DOCUMENTED DEBT por GO humano, con cinco REWORK de Haiku documentados, sin inventar PASS.
- **H00.02:** entregado documentalmente y en IN_REVIEW; Haiku dio PASS con reservas sobre la versión v1.1. **UX-01 todavía NO fue aprobado.**
- **Este RB-H02.00:** un **spike técnico acotado**, adelantado a H02 normal para producir código visible y descubrir pronto obstáculos de multi-window/multimonitor. No convertirlo en aprobación de UX-01 ni del framework.

**No esperes aprobación de UX-01 para ejecutar sólo este spike:** su excepción experimental está explícitamente autorizada. No avanzar a integración de producto ni a H03 hasta cerrar los gates del runbook. Si hay una contradicción material nueva, pedir aclaración; no detenerse por una foto histórica de H00.02 que aún decía Q4 pendiente.

### 1. Identidad de repositorios y rutas

En la Mac del usuario:
- **Destino EDITABLE (sólo los paths autorizados):** `$HOME/Documents/lens/novakube-native`, GitHub `drko-dev/novakube-native`, rama base `main`.
- **Fuente de referencia ABSOLUTAMENTE SOLO LECTURA:** `$HOME/Documents/lens/lens-v6-ui-corrections`, GitHub `drko-dev/lens`.
- **Worktree fuente adicional SOLO LECTURA:** `$HOME/Documents/lens/worktrees/develop`.
- **Workspace padre:** `$HOME/Documents/lens` (NO es Git root).

Antes de crear archivos, leer completamente estos documentos del destino:
1. `CLAUDE.md`
2. `NOVAKUBE_NATIVE_MANIFIESTO.md`
3. `NOVAKUBE_NATIVE_RUNBOOK_MAESTRO.md`
4. `docs/AGENT_PROMPT_PROTOCOL.md`
5. `docs/architecture/DEC-UX-001_WORKSPACE_MVP.md`
6. `docs/architecture/DEC-UX-002_PANELES_DESACOPLABLES_MVP.md`
7. `docs/ux/audits/H00_01_HANDOFF.md`
8. `docs/ux/flows/H00_02_TAREAS_Y_FLUJOS.md` (en particular §3, §7 y Q4)
9. `docs/ux/flows/H00_02_HANDOFF.md`.
10. El presente `RB-H02.00_SPIKE_UI_NATIVE_SONNET_HAIKU.md`.

Si un archivo existe sólo local y no en `origin/main`, **leelo localmente y preservalo**. No lo recrees vacío ni lo des por inexistente por no aparecer en GitHub.

### 2. Estado conocido al emitir este prompt (verificar otra vez)

**Verificado el 2026-11-10:**
- Destino `main` @ `bfe3bc1`, inicialmente igual a `origin/main`; sin PR abiertos. No existe aplicación Rust ni `Cargo.toml` en el repositorio principal.
- Documentos de H00.01 y H00.02 están **locales sin seguimiento** bajo `docs/ux/`; su trabajo no está integrado a Git. Hay archivos `.DS_Store` locales que NO deben borrarse ni añadirse.
- DEC-UX-002 se creó localmente y debe conservarse. Este prompt y la decisión pueden entrar en `main` más adelante; tu preflight debe usar el estado actual, no este SHA si Git avanzó.
- Fuente: `feature/novakube-high-contrast` @ `59f6c7d4`; worktree `develop` @ `1aebbd9b`; remoto principal `drko-dev/lens` en `develop`, último HEAD histórico `0003d663`; PR #1–#4 mergeados y ninguno abierto en la última consulta.
- Entorno: Mac Apple Silicon `arm64`, macOS `27.2.1` en la inspección. `rustc` y `cargo` **no aparecieron en PATH ni en las ubicaciones habituales** `$HOME/.cargo/bin` y `/opt/homebrew/bin`. Revalidar; **si realmente falta Rust, pedir autorización explícita antes de instalar rustup, herramientas Xcode o dependencias del sistema**. Sin compilador, podés preparar diseño de prueba, pero NO declarar build PASS. Priorizá resolver este bloqueador.
- La fuente tiene archivos sin seguimiento ajenos al spike; no tocarlos.
- Identidad visual definitiva y política PROD (Q3, Q7) están pendientes. Usar UX provisional claramente marcada, con datos sintéticos.

**Preflight obligatorio:** confirmar `git rev-parse --show-toplevel`, `git status --short --branch`, `git log -1`, `git worktree list`, remotos, diferencia con `origin/main`, PR abiertos/draft/fallidos en ambos repositorios, handoffs actuales y `rustc --version`, `cargo --version`, `uname -m`. Si detectás modificaciones previas no conocidas o experimentos ya empezados, reanudá el trabajo sin pisarlo. No `git clean`, `reset --hard`, `git push --force` ni cambios de rama destructivos.

### 3. Resultado funcional mínimo y visual (no un wireframe)

Crear al menos **un prototipo que compile y se pueda abrir como app nativa**, sin Electron, Tauri, WebView, HTML, React ni navegador.

La demo debe mostrar:
1. Ventana principal «NovaKube Native — UI Spike» con sidebar, barra de contexto `DEMO / cluster-demo / namespace-demo`, pestañas y una **lista sintética** de Pods (p. ej. 8 entradas; sin datos reales).
2. Un panel de **Logs DEMO** con líneas falsas; botones visibles: Abrir panel, **Desacoplar**, **Volver a acoplar**, Cerrar. Representar también un panel **Terminal DEMO — SIN PTY NI CONEXIÓN**, para validar que ese tipo de panel cabe en el modelo, no para abrir procesos.
3. **Ventana secundaria NATIVA** e independiente (no popup interno, no modal web) abierta desde el panel. Se la puede mover, redimensionar, enfocar y cerrar, y puede volver al contenedor principal por acción explícita. El usuario debe poder distinguir qué panel vive en qué ventana.
4. **Estado compartido sin duplicar panel:** el mismo ID y contenido sintético se transfieren al desacoplar/reacoplar; no se clonan sesiones. Mostrar claramente el clúster/ns en ambas ventanas.
5. **Prueba de monitores:** si hay una segunda pantalla, mover la ventana entre displays y observar escala/posición. Si no hay monitor secundario, documentar «NO PROBADO FÍSICAMENTE» y diseñar un test de geometría con pantallas simuladas; **no afirmar multimonitor validado sólo porque existan dos ventanas**.
6. Cierre seguro: cerrar la secundaria sin perder el panel; no abrir terminales, streams, sockets ni accesos a producción. Las preferencias visuales de tamaño/posición, si se guardan en el spike, usan un archivo de prueba separado y datos no sensibles; no modificar configuración de OpenLens.
7. Añadir un pequeño escenario de «monitor desaparecido» con **datos sintéticos** que calcule una posición visible de recuperación; no prometer eventos de hotplug hasta comprobarlos.

No hace falta replicar completamente el docking H7 en este spike: **es una prueba de viabilidad**, no la implementación final. Si un framework no permite una capacidad, mostrar el problema con evidencia y una alternativa concreta (p. ej. manejo de ventanas de nivel inferior), sin fingir paridad.

### 4. Estrategia de frameworks: evidencias antes que preferencias

**Primer resultado visible:** priorizar una demo **egui/eframe nativa**; su documentación pública tiene soporte de múltiples viewports nativos. Comprobar que el backend usado efectivamente cree ventanas del SO (no viewports embebidos).

**Comparador técnico:** investigar `iced` y, si las dependencias y el compilador están disponibles, crear una **mini-demo independiente** que pruebe abrir/cerrar una segunda ventana nativa, con los mismos requisitos mínimos. No gastar todo el tiempo intentando que ambos tengan docking completo: el objetivo es una comparativa basada en ejecución donde sea posible.

**Comparar:** multiventana real, control de monitores y escalas, ciclo de vida al cerrar ventana, desacople/reacople sin duplicación de estado, facilidad de layouts/paneles, accesibilidad, teclado, integración posible con terminal, huella inicial y riesgos de mantenimiento.

Referencias técnicas para verificar al ejecutar, no copiar APIs de versiones incompatibles:
- egui/eframe: https://github.com/emilk/egui/blob/main/examples/multiple_viewports/src/main.rs
- egui viewport: https://docs.rs/egui/latest/egui/viewport/index.html
- iced native window: https://docs.iced.rs/iced/window/index.html
- Claude Code subagents: https://code.claude.com/docs/en/sub-agents
- Agent teams: https://code.claude.com/docs/en/agent-teams

**No elegir framework definitivo automáticamente.** Si egui compila primero, mostrárselo al usuario pronto; no esperar a terminar iced ni escribir un ADR definitivo sin la comparación.

### 5. Asignación Sonnet/Haiku, límites de trabajo y velocidad

- **Sonnet coordinador:** preflight, lectura canónica y división de tareas, control de cambios, integración de hallazgos, demo principal, handoff. Presenta en forma continua resultados ejecutables, no solo planes.
- **Sonnet ejecutor A (si hay subagentes disponibles):** `experiments/ui/egui_spike/` exclusivamente. Implementar ventana visual nativa con falsa lista de Pods y panel desacoplable.
- **Sonnet ejecutor B:** investigación acotada de `iced`; si se decide compilar un comparador, escribe SOLO en `experiments/ui/iced_spike/`. Nunca editar el mismo Cargo.toml ni archivos de A.
- **Haiku:** QA de solo lectura del código y evidencias **después** de que Sonnet compile/intente ejecutar. Identificar los modelos reales, de ser verificables. No asumir que el subagente built-in `Explore` es Haiku: su modelo puede heredarse del coordinador. Pedir un subagente explícitamente configurado Haiku o sesión independiente y reportar cualquier imposibilidad de verificar la identidad. Revisar alcance, prohibiciones, semántica de ventanas, afirmaciones «probado» y estado de tests.
- Usar subagentes normales como primer mecanismo; **no activar experimental Agent Teams ni tocar configuración global** sin permiso. Mantener tareas aisladas y con contexto completo.
- **Límite de iteración de QA:** una revisión independiente; una ronda de correcciones focalizadas; si todavía hay un bloqueo, reportar y pedir decisión humana. No cinco pasadas sobre etiquetas.
- Ejecutar sólo `cargo check`, `cargo test` y `cargo run` **dentro de prototipos** cuando exista toolchain y autorización para instalaciones, evitando recompilar el monorepo Electron. Registrar comandos y si el resultado fue PASS, FAIL o NOT RUN.
- Mostrar el primer ejecutable tan pronto esté funcional, antes de elaborar una matriz enorme. Si dos frameworks ralentizan el resultado visual, entregar **uno que funcione** y documentar claramente que el otro NO FUE PROBADO.

### 6. Rutas que SÍ se pueden crear o modificar

Sólo en `drko-dev/novakube-native`:
- `experiments/ui/egui_spike/**` — Rust demo y Cargo.toml independientes.
- `experiments/ui/iced_spike/**` — solo si se decide construir el comparador.
- `docs/architecture/H02_00_COMPARATIVA_UI.md` — matriz breve, versiones reales de crates, observaciones comprobadas, riesgos y recomendación preliminar.
- `docs/architecture/H02_00_HANDOFF.md` — continuidad, comandos, resultados, capturas sanitizadas, bloqueos, estado, próximos pasos.
- `docs/evidence/H02_00/**` — sólo evidencia visual sintética, revisada por privacidad.
- Entradas `.gitignore` **locales a los experimentos** para `target/`, `.DS_Store` y otros artefactos generados, si hacen falta; nunca tocar o borrar `.DS_Store` existentes.

**PROHIBIDO** editar `drko-dev/lens`, `$HOME/Documents/lens/lens-v6-ui-corrections`, `docs/ux/audits/**`, `docs/ux/flows/**`, decisiones `DEC-UX-001/002`, manifiesto, runbook maestro y archivos globales de Claude. No importar assets sin permiso/licencia, no abrir kubeconfig ni clústeres, no terminal real, no IA remota, no telemetría ni descargas de binarios ajenos al gestor de dependencias autorizado. **Sin commit, push, PR ni merge** de código experimental hasta que el usuario lo revise y autorice.

### 7. Criterios de aceptación del SPIKE, no del producto

**Mínimo para GO del spike:**
- Una aplicación Rust nativa y compilable, con comandos exactos para abrirla en la Mac del usuario.
- Una ventana principal y otra nativa separada, con estado compartido y desacople/reacople demostrables.
- Una lista de Pods y panel de logs/terminal **sintéticos** visibles; identidad visual de demo claramente indicada.
- Test pequeño para identidad única del panel y recuperación de posición en monitor simulado, si el framework permite aislar esa lógica.
- Evidencia de lo **probado y no probado** en macOS, con límites exactos sobre multimonitor real, accesibilidad, hotplug y persistencia.
- Haiku revisa sin atribuir pruebas que no ejecutó, entrega PASS / REWORK / BLOCKED con evidencia.
- Ningún archivo del legado tocado y ningún secreto reproducido.

**NO es aceptación del spike:** un mockup Markdown, código sin compilación presentado como funcional, abrir dos paneles embebidos dentro de una sola ventana o decir «multimonitor funciona» sin haber probado mover la ventana en dos pantallas.

### 8. Handoff y cierre de la sesión

Entregar:
1. Qué pantalla puedo abrir, comandos exactos y ubicación del ejecutable (ruta relativa).
2. Capturas **si se hicieron** y descripción de interacciones comprobadas.
3. Frameworks/versions realmente probados y una recomendación preliminar, no un ADR final.
4. Tabla de pruebas: comando, fecha, hardware, salida y resultado real.
5. Resultado independiente de Haiku y límites de esa revisión.
6. Qué falta para llevar el prototipo a H03 después de UX-01 y ADR-001.
7. Git root, rama, HEAD, `git status`, PRs abiertos/cerrados/fallidos, nuevos archivos, procesos en curso, interrupciones y cómo reanudar sin sobrescribir.
8. Solicitud de decisión humana: **GO / REWORK / HOLD** de RB-H02.00.

Si falta Rust, el primer resultado debe ser un **bloqueo técnico claro y una solicitud de autorización para instalar el toolchain**. No simules que compilaste ni te vayas a una auditoría documental para llenar tiempo. No avanzar automáticamente a H03, no publicar código por tu cuenta.

## FIN DEL PROMPT
