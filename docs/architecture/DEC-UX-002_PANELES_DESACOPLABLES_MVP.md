# DEC-UX-002 — Tipos de panel desacoplables del primer MVP

**Fecha:** 2026-11-10
**Estado:** APROBADA por el usuario (opción B propuesta en RB-H00.02 §7.4 y Q4).
**Referencia vinculante:** `docs/architecture/DEC-UX-001_WORKSPACE_MVP.md`.
**Impacta:** UX-01, H00.03/H00.04, H02, H03, H07, H09 y H11.

## Decisión

Para el **primer MVP** de NovaKube Native se adopta **opción B — Núcleo**. Los siguientes tipos de panel deben poder **desacoplarse, trasladarse entre monitores y volver a acoplarse** dentro del motor único de docking:

- Listados de Pods.
- Detalle de Pod.
- Logs del Pod.
- Kubetail.
- Terminal.

Preferencias y Centro de Incidentes **no necesitan ser desacoplables en el primer MVP**: podrán permanecer integrados en el espacio principal. Esto no elimina sus capacidades del roadmap.

## Requisitos de producto y seguridad que siguen vigentes

- El docking global es **único**, también para el panel inferior, las ventanas secundarias y su persistencia.
- Las ventanas desacopladas funcionan con **multimonitor desde el primer MVP**, no en una versión posterior (DEC-UX-001).
- El estado de sesión de terminal/PTY y los streams de logs son separados del layout. El movimiento entre ventanas no crea una segunda sesión ni confunde el clúster o namespace.
- Al reiniciar solo se restaura **layout visual inerte**: no se reactivan terminales, credenciales, autorizaciones PROD ni streams.
- Al cerrar una terminal con proceso activo debe aplicarse política de cierre seguro, cancelación y pruebas de ausencia de PTY huérfanos.
- La interfaz inicial puede demostrar los paneles con **datos sintéticos** antes de conectar Kubernetes real. La autorización y seguridad de terminales en PROD siguen abiertas para decisión y pruebas específicas.

## Fuera de esta aprobación

Esta decisión **resuelve Q4**, pero no aprueba globalmente UX-01 ni todos los flujos de RB-H00.02. Permanecen sin aprobar entre otras: autorización de terminal PROD (Q3), identidad visual (Q7) y los demás puntos abiertos del documento.

Todavía no constituye una selección de framework UI, una implementación funcional ni autorización para que el asistente escriba código de aplicación. El desarrollo se delegará a IAs ejecutoras con un prompt específico y criterios verificables, después de confirmar modelo y entorno según `docs/AGENT_PROMPT_PROTOCOL.md`.

## Evidencia y continuidad

Aprobación verbal del usuario al confirmar «Sí» ante la propuesta explícita de **opción B** durante la revisión de H00.02. Este archivo registra esa decisión para futuras sesiones; no se declara PASS de QA ni un hito ACCEPTED por inferencia.
