# NovaKube Native — Runbook maestro y árbol recursivo de hitos

**Versión:** 1.0  
**Fecha:** 10 de noviembre de 2026  
**Documento rector:** NOVAKUBE_NATIVE_MANIFIESTO.md  
**Estado inicial:** planificación documentada; los hitos no están todavía autorizados para implementación.  
**Responsabilidades:** el usuario conduce producto/UX; el asistente diseña arquitectura y runbooks; otras IAs implementan.

## 1. Cómo funciona el árbol

Este runbook es un **árbol vivo**. Cada hito principal se divide en sub-runbooks; cada sub-runbook puede generar otros runbooks y sub-hitos hasta que cada hoja describa un resultado pequeño, delegable y verificable. La profundidad no tiene límite predefinido.

- **H00, H01...** son hitos principales.
- **RB-H00.01** es un sub-runbook.
- **RB-H00.01.01** es un sub-runbook hijo del anterior.
- **ADR-001** es una decisión de arquitectura documentada.
- **EVID-H00.01** identifica un registro de evidencia del trabajo.
- **UX-01** identifica un contrato de experiencia aprobado.

### Estados de cada nodo

PROPOSED → SPECIFIED → READY → DELEGATED → IN_REVIEW → ACCEPTED. Estados alternativos: BLOCKED, REWORK, CANCELLED. Ninguna IA puede declarar ACCEPTED su propio trabajo sin revisión.

### Cuándo dividir un nodo

Se crea un hijo si hay más de una salida funcional, si surge un riesgo nuevo, si hay una decisión no resuelta, si hay tareas en paralelo que requieren contratos distintos o si los criterios de aceptación no pueden verificarse en una revisión acotada. **El hijo hereda los límites de seguridad, alcance y permisos del padre**, y nunca puede ampliarlos sin aprobación.

### Contenido obligatorio de cada runbook hijo

1. Identificador, parent ID, versión, estado y responsable de revisión.
2. Objetivo único, justificación y resultado observable para el usuario.
3. Alcance exacto, exclusiones y archivos/componentes permitidos.
4. Dependencias, ADR relevantes, referencias del legado y precondiciones.
5. Contrato UX: vistas, flujos, teclado y estados normales, vacíos y de error.
6. Contrato técnico: entradas, salidas, ownership, errores, cancelación y límites.
7. Plan de trabajo delegable, sin decisiones implícitas ni acceso innecesario.
8. Casos de prueba positivos, negativos, regresión y mediciones pertinentes.
9. Evidencias: demo, capturas sanitizadas, pruebas, logs depurados, cambios y commit.
10. Condición de rollback, criterios GO / REWORK / HOLD y posibles hijos nuevos.

## 2. Árbol maestro de hitos

### H00 — Experiencia de usuario y diseño visual (empezar acá)
- RB-H00.01 Auditoría visual de NovaKube actual.
- RB-H00.02 Usuarios, tareas prioritarias, mapa de navegación y fricciones.
- RB-H00.03 Sistema de diseño: identidad, espaciados, tipografía, tablas, contraste, accesibilidad.
- RB-H00.04 Wireflows y prototipo navegable con datos sintéticos.
- RB-H00.05 Revisión con el usuario y aprobación del contrato UX-01.

### H01 — Inventario y reutilización del legado
- RB-H01.01 Mapa de monorepo, procesos, renderer y dependencias.
- RB-H01.02 Inventario H7: workspace, docking y ventanas.
- RB-H01.03 Inventario Kubetail, logs, terminal y operaciones.
- RB-H01.04 Inventario H8, incidentes, permisos, almacenamiento y estado.
- RB-H01.05 Matriz R/A/N/X, licencias, contratos y pruebas de equivalencia.

### H02 — Arquitectura y elección del framework UI
- RB-H02.01 Matriz comparativa iced, egui y alternativas nativas.
- RB-H02.02 Experimento controlado: tabla densa, docking, ventanas y teclado.
- RB-H02.03 Diseño de estado, tareas asíncronas, errores y cancelación.
- RB-H02.04 ADR-001: framework; ADR-002: módulos y contratos.

### H03 — Primera carcasa visual Rust
- RB-H03.01 Shell, tema, sidebar, navegación.
- RB-H03.02 Catálogo de clústeres y contextos con fixtures sintéticos.
- RB-H03.03 Pods, detalle y panel de logs sintéticos.
- RB-H03.04 Revisión UX, accesibilidad y regresión visual.

### H04 — Conectividad Kubernetes y seguridad de sesión
- RB-H04.01 Kubeconfig, descubrimiento de contextos y validación.
- RB-H04.02 Autenticación, exec-auth, certificados, TLS y proxies.
- RB-H04.03 Cliente Kubernetes, recursos, RBAC y sesiones.
- RB-H04.04 Streams, reconexión, cancelación y multi-clúster.

### H05 — Recursos y operaciones
- RB-H05.01 Namespaces, workloads y Pods.
- RB-H05.02 Búsqueda, filtros, detalles, actualización y eventos.
- RB-H05.03 Operaciones de escritura con permisos y confirmación.
- RB-H05.04 Estados de error, permisos, recuperación y accesibilidad.

### H06 — Logs y Kubetail
- RB-H06.01 Lectura concurrente, origen, fusión y orden de streams.
- RB-H06.02 Pausa, seguimiento, filtros y exportación.
- RB-H06.03 Reintentos, límites de memoria, seguridad y resiliencia.

### H07 — Workspace, docking y terminal
**Gate obligatorio del primer MVP (DEC-UX-001):** docking global único, ventanas desacopladas y multimonitor; no diferir estas capacidades.
- RB-H07.01 Pestañas, paneles y layout persistente.
- RB-H07.02 Ventanas desacopladas, restauración y múltiples monitores (**obligatorio para el primer MVP**).
- RB-H07.03 PTY, renderizado, teclado y sesiones.
- RB-H07.04 Cierre limpio, cancelación, permisos y procesos.

### H08 — Centro de Incidentes y asistencia IA
- RB-H08.01 Modelo de incidentes y evidencias.
- RB-H08.02 Interacción visual de investigación.
- RB-H08.03 Análisis con datos sintéticos y límites de lectura.
- RB-H08.04 Auditoría, autorización de acciones y privacidad.

### H09 — Persistencia, configuración e importación
- RB-H09.01 Formatos existentes y esquema versionado.
- RB-H09.02 Importación con vista previa, respaldos y conflicto.
- RB-H09.03 Restauración, rollback y pruebas de no pérdida.

### H10 — Helm, kubectl y extensibilidad
- RB-H10.01 Ejecución de binarios y control de procesos.
- RB-H10.02 Flujos de Helm y operaciones permitidas.
- RB-H10.03 Estudio separado de API de extensiones y aislamiento.

### H11 — Calidad, seguridad y medición
- RB-H11.01 Tests unitarios, de integración, E2E y regresión visual.
- RB-H11.02 Licencias, dependencias, privacidad y cadena de suministro.
- RB-H11.03 Baseline y comparación de arranque, memoria, fluidez, estabilidad.
- RB-H11.04 Matriz de plataformas y recuperación ante fallas.

### H12 — Publicación y mantenimiento
- RB-H12.01 Empaquetado nativo y dependencias.
- RB-H12.02 Firma, notarización cuando corresponda, updates y rollback.
- RB-H12.03 Documentación, diagnóstico y soporte.
- RB-H12.04 Gate de publicación: GO / HOLD / NO-GO.

## 3. Secuencia y dependencias

**Empezar por H00.** La revisión visual produce UX-01. **Decisión de producto aprobada:** `docs/architecture/DEC-UX-001_WORKSPACE_MVP.md` exige ventanas desacopladas y multimonitor desde el primer MVP, con motor de docking global único; el alcance visual exacto se define en UX-01. H01 puede iniciarse en paralelo en modo auditoría de solo lectura. La especificación temprana de H09 se nutre de H01, para que la arquitectura contemple migraciones desde el principio.

H02 requiere UX-01 y un inventario preliminar; H03 requiere el ADR de UI y el UX aprobado. H04 puede diseñarse mientras se desarrolla H03, pero las conexiones reales se prueban solamente en entornos autorizados. H05 depende de H04; H06 depende de H04/H05; H07 depende de H02/H03 y de H04 para terminales conectadas; H08 depende de dominios y permisos. H11 define controles durante todos los hitos. H12 solo certifica una publicación tras gates completas.

El orden es **por dependencias y experiencia validada**, no por preferencia de una IA. Cada nodo se convierte en READY únicamente después de cerrar entradas y criterios.

## 4. Plan detallado de cada hito troncal

### H00 — Experiencia visual
**Entrada:** referencias y capturas seguras del legado, casos de uso, restricciones visuales.  
**Ejecución documental:** auditar pantallas y comportamientos; escribir flujo catálogo → clúster → namespace → Pods → detalle → logs; registrar ajustes visuales y estados empty/loading/error/forbidden.  
**Entregable de la IA de diseño futura:** wireflows, esquema de componentes y prototipo visual con datos falsos.  
**Prueba de aceptación:** el usuario puede recorrer y comentar el flujo sin depender de Kubernetes real; quedan documentadas las decisiones y diferencias con NovaKube.  
**Gate:** UX-01 aprobado por el usuario o REWORK. UX-01 debe incluir estados y recorridos de desacoplar, mover paneles entre monitores, acoplar, guardar/restaurar y desconectar un monitor (DEC-UX-001).

### H01 — Inventario del legado
**Entrada:** acceso de solo lectura al árbol antiguo y documentación vigente.  
**Ejecución:** revisar componentes y comportamientos de shell, docking H7, Kubetail, terminal, H8, persistencia, pruebas y seguridad.  
**Entregable:** matriz componente → fuente → categoría R/A/N/X → licencia → dependencias → contrato UX → prueba de equivalencia.  
**Gate:** trazabilidad de las capacidades prioritarias; no transferir secretos ni copiar el monorepo.

### H02 — Arquitectura y selección UI
**Entrada:** UX-01 y mapa preliminar de H01.  
**Ejecución:** pruebas equivalentes para iced, egui y alternativas justificadas: paneles, tabla grande, múltiples ventanas **desacopladas y multimonitor obligatorias en MVP**, navegación de teclado, accesibilidad, terminal y redimensionado. Diseñar límites entre presentación, aplicación, dominio y adaptadores.
**Entregable:** matriz con resultados observados, riesgos, ADR-001 y ADR-002.  
**Gate:** decisión revisable fundamentada; no fijar framework antes del experimento.

### H03 — Carcasa nativa inicial
**Entrada:** UX-01 y ADR-001 aprobados.  
**Ejecución de otras IAs:** construir shell visual y pantallas con fixtures sintéticos.  
**Entregable:** demo ejecutable, capturas sanitizadas, instrucciones de revisión, tests de UI.  
**Gate:** flujo UX-01 recorrible, teclado/foco correctos, estados de error visibles y revisión de producto.

### H04 — Kubernetes
**Entrada:** contratos de arquitectura y seguridad aprobados.  
**Ejecución:** lectura de kubeconfig, autenticación externa, expiraciones, TLS/CA, contextos múltiples, RBAC, errores, streams y cancelación.  
**Entregable:** tests de escenarios positivos y negativos en entorno autorizado, y límites explícitos sobre credenciales.  
**Gate:** conexiones no mezclan estados; fallas se recuperan o informan sin filtrar secretos.

### H05 — Recursos y operaciones
**Entrada:** H04 verificado y vistas H03.  
**Ejecución:** listas de namespaces/workloads/Pods, detalles, filtros, events, permisos y operaciones con confirmación.  
**Entregable:** pruebas de flujos reales, casos de error y UX de operaciones.  
**Gate:** sin escrituras implícitas, RBAC comprobado, UX aprobado.

### H06 — Logs
**Entrada:** H04/H05.  
**Ejecución:** múltiples streams con procedencia, filtros, pause/follow, exportación, buffers acotados, cierre y reconexión.  
**Entregable:** escenario multistream comprobable, pruebas de cancelación y memoria.  
**Gate:** sin pérdida silenciosa relevante, errores observables y equivalencia con Kubetail acordada.

### H07 — Workspace y terminal
**Entrada:** UI seleccionada y shell validado; H04 para sesiones remotas.  
**Ejecución:** docking, multiventana, layout persistente, PTY, comandos y limpieza de procesos.  
**Entregable:** demo de restauración y pruebas de ciclo de vida.  
**Gate:** no se abandonan procesos al cerrar vistas ni se mezclan sesiones; desacoplar, mover entre monitores, reacoplar y restaurar layout visual inerte deben verificarse antes de aceptar el primer MVP (DEC-UX-001).

### H08 — Incidentes
**Entrada:** recursos y observabilidad, modelo de permisos definido.  
**Ejecución:** incidentes locales, evidencia trazable, flujos visuales, análisis de IA controlado.  
**Entregable:** pruebas sintéticas, auditoría de decisiones y límites de escritura.  
**Gate:** ninguna conclusión se presenta como observación real sin fuente; acciones externas exigen autorización.

### H09 — Persistencia
**Entrada:** formatos del legado identificados desde H01.  
**Ejecución:** migraciones versionadas, importación preview, backup, tests de integridad, rollback.  
**Entregable:** evidencia de importación y restauración con fixtures representativos.  
**Gate:** la configuración original permanece intacta y la pérdida de datos es bloqueante.

### H10 — Helm, kubectl y extensibilidad
**Entrada:** seguridad H04 y recursos H05.  
**Ejecución:** invocación segura de procesos, timeouts, límites de argumentos y permisos; extensiones solo tras ADR separado.  
**Gate:** comandos reproducibles y auditados; no inyección de shell ni extensiones con privilegios implícitos.

### H11 — Calidad y rendimiento
**Entrada:** pruebas y métricas definidas desde los primeros hitos.  
**Ejecución:** unitarias, integración, E2E, visual, análisis de vulnerabilidades, pruebas de errores y medición comparativa.  
**Entregable:** matriz de regresiones y benchmark con hardware, condiciones y resultados.  
**Gate:** no afirmar mejoras sin medición y sin registrar limitaciones.

### H12 — Distribución
**Entrada:** gates de seguridad, funcionalidad, UX y medición completadas para el alcance elegido.  
**Ejecución:** build, empaquetado, firma, update, instalación, rollback, documentación pública.  
**Gate:** autorización explícita de release y plan de contingencia probado; publicar código no implica publicar binarios.

## 5. Primeros paquetes para entregar a otras IAs

### Paquete A — RB-H00.01 (auditoría visual, sin código)
**Pedido:** observá la aplicación NovaKube de referencia y sus capturas sin modificarla. Documentá sidebar, catálogo, tablas, tabs, docking, terminal, logs y configuraciones.  
**Entrega:** mapa de pantallas, evidencia sanitizada, fricciones y tabla conservar / mejorar / investigar.  
**Aceptación:** el responsable de producto reconoce el flujo y dispone de material para decidir UX-01.

### Paquete B — RB-H00.02 + RB-H00.03 (contrato UX, sin código)
**Pedido:** definí tareas prioritarias, wireflows, sistema de diseño, estados y teclado para catálogo → Pods → detalle → logs.  
**Entrega:** UX-01 en borrador, decisiones visuales y preguntas abiertas.  
**Aceptación:** flujos revisables por el usuario y sin dependencia de una API todavía inexistente.

### Paquete C — RB-H00.04 (prototipo futuro, con implementación delegada)
**Pedido futuro, solo tras aprobar UX-01:** construir una maqueta navegable con datos sintéticos, aislada de Kubernetes real, basada en el contrato aprobado.  
**Entrega:** demo, capturas y pruebas de interacción.  
**Aceptación:** el usuario puede recorrer las pantallas, dar feedback y solicitar ajustes.

### Paquete D — RB-H01.01 (auditoría técnica, sin código)
**Pedido:** elaborar matriz R/A/N/X de los componentes legados y destacar licencias, seguridad, comportamientos y pruebas reutilizables.  
**Entrega:** mapa de dependencias, contratos y riesgos.  
**Aceptación:** cada componente prioritario tiene fuente y decisión justificadas.

### Paquete E — RB-H02.01 + RB-H02.02 (experimento futuro)
**Pedido futuro:** comparar frameworks UI bajo las mismas exigencias de UX, docking, tablas, ventanas, accesibilidad y terminal.  
**Entrega:** matriz técnica con evidencia y propuesta ADR.  
**Aceptación:** la selección puede justificarse con experimentos, no con suposiciones.

## 6. Plantilla para nuevos sub-runbooks

**ID / Padre / Versión / Estado / Revisor:** completar.  
**Objetivo único:** describir un resultado comprobable.  
**Valor UX:** explicar qué mejora observará el usuario.  
**Entradas / Dependencias:** listar documentación, fixtures, ADR y otros runbooks aprobados.  
**Alcance / Exclusiones:** definir qué se puede editar y qué no.  
**Contrato UX:** pantallas, interacción, teclado, estados normales y excepciones.  
**Contrato técnico:** inputs, outputs, estado, concurrencia, seguridad, errores y persistencia.  
**Pruebas:** positivas, negativas, visuales y de regresión.  
**Evidencia:** cambios, commit, test logs sanitizados, capturas y demo.  
**Criterios de aceptación:** checks verificables, condición de rollback y GO / REWORK / HOLD.  
**Riesgos / ADR / Hijos nuevos:** registrar cada descubrimiento sin ampliar alcance automáticamente.

## 7. Protocolo de revisión de trabajos de otras IAs

1. Recibir el ID del runbook, lista de archivos afectados, rama y commit.
2. Revisar diferencias contra el alcance permitido y los ADR vigentes.
3. Reproducir las pruebas o declarar con precisión qué no se pudo verificar.
4. Comparar pantalla y comportamiento con el contrato UX aprobado.
5. Revisar seguridad, permisos, licencias, logs, datos y procesos asíncronos.
6. Emitir GO, REWORK o HOLD con evidencia y acciones pendientes.
7. Crear sub-runbooks nuevos si aparecen dependencias o riesgos nuevos.
8. Integrar solo tras autorización y gates satisfechos; no desplegar por defecto.

## 8. Primera acción tras aprobar esta documentación

Abrir **RB-H00.01 — Auditoría visual** como primer encargo independiente para una IA. Traer su resultado a la conversación con el usuario, definir UX-01 y recién entonces autorizar la construcción visual. El asistente continuará manteniendo arquitectura y árbol de runbooks mientras las IAs ejecutoras construyen por separado.

**Prohibición de esta fase:** este runbook no solicita ni autoriza escribir código de aplicación, conectarse a clústeres reales, usar secretos, modificar el proyecto original ni publicar releases.
