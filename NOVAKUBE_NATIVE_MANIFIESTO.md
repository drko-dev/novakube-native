# NovaKube Native — Manifiesto fundacional

**Versión:** 1.0  
**Fecha:** 10 de noviembre de 2026  
**Estado:** planificación y decisiones para revisión; no constituye autorización para modificar producción o desplegar.  
**Proyecto original de referencia:** OpenLens DevOps / NovaKube (drko-dev/lens).  
**Documento relacionado:** PASAGE-OPENLENS-ELECTRON-A-RUST.md, dentro de lens-v6-ui-corrections. Este documento no lo reemplaza ni altera.

## 1. Propósito

Crear **NovaKube Native**, un proyecto nuevo, independiente y público que aproveche los conocimientos, decisiones de producto, contratos de comportamiento, flujos de operación, pruebas y recursos legítimamente reutilizables del proyecto OpenLens DevOps / NovaKube. Su producto objetivo será una aplicación de escritorio **nativa en Rust, sin Electron, Tauri ni WebView como motor de interfaz**.

No se trata de tirar lo construido ni de importar indiscriminadamente el monorepo anterior. El objetivo es una evolución controlada, con mejor estabilidad, mantenibilidad y experiencia de usuario, demostrada con evidencia y no con promesas sobre el lenguaje.

## 2. Objetivos de igual importancia

**Ingeniería y mantenimiento:** módulos con responsabilidades claras, límites verificables, errores explícitos, pruebas reproducibles, concurrencia cancelable, menores acoplamientos, diagnósticos seguros y facilidad para incorporar mejoras sin romper funcionalidades.

**Experiencia de usuario:** una interfaz NovaKube coherente, fluida, accesible, configurable y predecible, pensada para el trabajo diario con Kubernetes; preservar lo que ya funciona y mejorar lo que hoy resulte confuso o pesado.

**Eficiencia y robustez:** comparar arranque, memoria, latencia, estabilidad bajo carga, recuperaciones y comportamiento ante fallas contra una línea base del producto existente. Rust por sí solo no garantiza mejores resultados.

## 3. Acuerdos del proyecto

1. Es un **proyecto nuevo** y tendrá **un repositorio GitHub nuevo y público**, con historia y ciclo de publicación propios.
2. El proyecto de origen permanece **intacto**. Es referencia de producto, no un destino para merges del proyecto nuevo.
3. El producto final es **Rust nativo**, sin interfaz basada en navegador.
4. **Primero lo visual:** cada etapa relevante comienza con un contrato de experiencia que el usuario pueda evaluar antes de acoplarle backend.
5. **Implementación progresiva y verificable**: hitos, runbooks y sub-runbooks recursivos en árbol, con entradas, salidas, dependencias y aceptación.
6. El usuario dispone de **otras IAs para programar**. El asistente se ocupa de arquitectura, manifiesto, documentación, contratos, descomposición de hitos, coordinación y revisión, **no de escribir código de aplicación**.
7. No se dan por completadas capacidades porque estén en el roadmap o porque un agente reporte éxito: siempre se requieren pruebas y una evaluación del resultado.
8. Publicar el repositorio no equivale a autorizar un release público de la aplicación.

## 4. Decisiones abiertas que no se deben cerrar sin evidencia

- **Framework gráfico:** comparar iced, egui y otras opciones nativas viables mediante el mismo conjunto de pantallas y pruebas. Considerar docking, tablas grandes, multiventana, teclado, accesibilidad, terminal, rendimiento, mantenimiento y licencias.
- **Plataformas:** usar macOS Apple Silicon como entorno inicial candidato, sin asumir que ya están aprobadas las demás plataformas.
- **Extensiones:** decidir si el producto necesita API nativa, WASM u otra opción, y qué grado de compatibilidad funcional se pretende.
- **Licencia y procedencia:** definir licencia pública y revisar derechos sobre fragmentos, diseños, imágenes y dependencias del proyecto anterior.
- **Distribución:** firma, notarización, actualizaciones y soportes se deciden en un hito posterior.
- **Métricas:** fijar umbrales una vez instrumentadas mediciones comparables.

Toda decisión material debe quedar en un **ADR**: contexto, alternativas, experimentos, decisión, consecuencias y plan de reversión.

## 5. Inventario y estrategia de reutilización

Los sistemas del legado a estudiar son:
- Shell, catálogo de clústeres, navegación y tema visual NovaKube.
- Explorador Kubernetes, namespaces, workloads, Pods, tablas, acciones y detalle.
- H7: tabs, docking global, paneles desacoplados, ventanas y restauración.
- Kubetail: logs combinados, seguimiento, pausa, filtros y exportación.
- Terminal, sesiones, Helm y kubectl.
- Preferencias, persistencia, kubeconfig y autenticación.
- H8: Centro de Incidentes, evidencias, ayudas de IA y permisos.
- Pruebas E2E, criterios QA, reportes, contratos y patrones de errores.

Cada elemento se clasifica como:

| Clase | Tratamiento |
| --- | --- |
| R — Reutilizar | Especificaciones, datos de prueba sintéticos, formatos estándar, recursos o código legalmente compatibles y separables del runtime web |
| A — Adaptar | Reglas de negocio, modelos, preferencias, pruebas y flujos que requieren traducción de contratos |
| N — Implementar nativo | Electron, React, SCSS, MobX, IPC de Electron, xterm.js, docks HTML y otras piezas acopladas a la interfaz web |
| X — Excluir | Credenciales, kubeconfigs reales, rutas privadas, logs de producción, secretos, activos sin derechos claros y dependencias inapropiadas |

Cada clasificación debe registrar fuente, licencia, motivo, dependencias, prueba de equivalencia, riesgos y decisión. No se copiará de forma masiva el árbol ni la historia Git de OpenLens.

## 6. Contrato de producto: empezar visualmente

El primer flujo revisable, **UX-01**, será: catálogo de clústeres → selección de contexto/namespace → listado de Pods → detalle → panel de logs. La demostración inicial utilizará **datos sintéticos** y tendrá que mostrar también estados vacíos, carga, error, permisos insuficientes y desconexión.

La revisión visual incluye:
- Navegación, orientación, jerarquía, espaciado y densidad de información.
- Identidad NovaKube, tipografía, contraste y tema.
- Tablas, filtros, orden, búsqueda y acciones.
- Pestañas, paneles y comportamiento de cambios de tamaño.
- Navegación de teclado, foco, accesibilidad y feedback.
- Continuidad entre vistas y manejo de estados de carga, errores y permisos.

**Importante:** una maqueta aprobada valida UX, no conectividad Kubernetes, streaming ni seguridad. Es el contrato inicial para implementar después.

## 7. Arquitectura por capas y dominios

**Presentación nativa:** sistema de diseño, pantallas, ventanas, widgets, docking y accesibilidad. Nunca maneja secretos directamente.

**Aplicación:** navegación, estado, comandos, tareas asíncronas, cancelación, sincronización entre ventanas y políticas de error.

**Dominio:** clústeres, recursos, permisos, operaciones, logs, terminales, incidentes y preferencias, con modelos independientes del framework UI.

**Adaptadores:** Kubernetes, autenticación, filesystem, almacenamiento, procesos, PTY, empaquetado y servicios externos. Todo borde privilegiado debe tener una interfaz auditable.

### 7.1 Seguridad Kubernetes
Preservar compatibilidad real con kubeconfig, exec-auth, certificados, CA, TLS, proxies, RBAC, expiración y renovación de credenciales, múltiples contextos, streams y desconexiones. No exponer tokens en estados de UI, logs ni fixtures. Comenzar con lectura. Las acciones de escritura requieren autorización y confirmación explícita.

### 7.2 Datos y migración
Diseñar temprano almacenamiento versionado y manejo de secretos separado de preferencias exportables. Toda importación tendrá vista previa, respaldo, prueba de integridad y rollback. El producto original debe permanecer legible y sin alteraciones.

### 7.3 UI y terminal
El docking, las ventanas separadas, las tablas densas y el emulador de terminal son riesgos centrales de elección tecnológica. Evaluar en prototipos de igual complejidad. No comprometer el proyecto con un framework antes del ADR correspondiente.

### 7.4 IA y automatización
Las capacidades de incidentes se diseñan con evidencia trazable, límites de lectura, explicaciones de resultados y autorizaciones explícitas. Nada debe ejecutar cambios destructivos en clústeres por inferencia de una respuesta de IA.

## 8. Método multi-IA y responsabilidades

**Usuario — Producto/UX:** define prioridades, evalúa prototipos, aprueba comportamientos, decisiones de alto impacto y publicaciones.

**Asistente — Arquitectura y coordinación:** redacta y mantiene manifiesto, ADR, runbooks, contratos, dependencias, gates de calidad y revisiones; prepara encargos para otras IAs. No programa la aplicación.

**IAs ejecutoras — Implementación:** reciben un runbook hijo en estado READY, con contexto, límites, pruebas y entregables, trabajan en ramas aisladas y reportan cambios y evidencias. Si detectan nuevo alcance, proponen otro hijo; no lo ejecutan por iniciativa propia.

**Revisión — Integración:** confirma correspondencia con UX aprobado, pruebas técnicas, seguridad, licencias, datos y métricas. Todo merge requiere revisión y autorización según la política del repositorio.

## 9. Gobierno de hitos

El documento **NOVAKUBE_NATIVE_RUNBOOK_MAESTRO.md** es el árbol rector. Cada nodo contiene:
- ID, padre, estado, dependencias y alcance.
- Resultado visible o medible, exclusiones y contratos UX/técnicos.
- Riesgos, autorización y límites de permisos.
- Pruebas, evidencias y criterios de aceptación.
- Posibles nuevos nodos y decisiones ADR.
- Resultado GO / REWORK / HOLD.

No se aceptará una entrega sin evidencia comprobable; un PASS de tests no reemplaza la revisión UX y una demo atractiva no reemplaza pruebas de seguridad.

## 10. Repositorio público, privacidad y releases

El nuevo repositorio está separado del original y solo aloja material apropiado para publicación. Antes de incorporar recursos o fragmentos de código heredados, verificar licencias, atribuciones, secretos, metadatos, capturas y rutas personales. Usar contenido sintético por defecto. El repositorio público podrá albergar documentación antes de tener una aplicación.

El código, los clústeres, las credenciales y la configuración de la aplicación existente no se alteran como consecuencia de crear o documentar el proyecto nuevo. Un release requiere un gate específico de empaquetado, firma, soporte, vulnerabilidades y rollback.

## 11. Definición de éxito

NovaKube Native se considerará exitoso al reproducir las tareas operativas prioritarias de manera segura, con una UX validada, una arquitectura modular y mantenible, datos preservados, pruebas de regresión, y mejoras de estabilidad y rendimiento **medidas**. La paridad se decide por función, no por recuento de archivos.

**Primera regla práctica:** empezamos con diseño y revisión de UX; no con una migración masiva ni con un backend aislado de la experiencia.
