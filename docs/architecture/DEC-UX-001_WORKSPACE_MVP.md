# DEC-UX-001 — Docking global, ventanas desacopladas y multimonitor desde el primer MVP

**Fecha:** 2026-11-10
**Estado:** APROBADA por el responsable de producto durante revisión de RB-H00.01
**Proyectos:** drko-dev/novakube-native (destino); drko-dev/lens (referencia, solo lectura)
**Ámbito:** H00 / UX-01, H02 (arquitectura UI), H03 (carcasa), H07 (workspace), H09 (persistencia) y H11 (QA).

## Decisión del usuario

**El primer MVP de NovaKube Native debe incluir desde su entrega inicial ventanas desacopladas y soporte multimonitor. No se diferirán a una fase posterior.**

Se adopta como dirección de arquitectura **un sistema de docking global único**: el área inferior, las pestañas y los paneles pueden tener representaciones visuales distintas, pero no habrá dos motores independientes de layout/persistencia. La implementación concreta, alcance de paneles compatibles y framework nativo quedan por validar en H00/H02.

## Requisitos mínimos de aceptación para el MVP

1. Abrir el workspace principal y dividir paneles de manera interactiva.
2. Desacoplar y volver a acoplar los tipos de panel que defina y apruebe UX-01.
3. Mover ventanas desacopladas entre monitores disponibles, incluyendo escalas y resoluciones distintas.
4. Redimensionar, enfocar, activar y cerrar ventanas/paneles sin confundir identidad de clúster, namespace o sesión.
5. Guardar y recuperar el layout, geometrías y asignación de monitor cuando estén disponibles.
6. Si se desconecta un monitor, recuperar ventanas fuera de pantalla en una pantalla disponible, sin perder el layout.
7. Restaurar **solo estado visual inerte**: no reabrir automáticamente terminales/PTy, conexiones, autorizaciones PROD, borradores no guardados ni buffers de logs.
8. Cubrir teclado, foco, accesibilidad, errores, cierre de ventanas y pruebas de regresión multi-display, sin afirmar un comportamiento probado antes de ejecutarlas.

## Implicaciones para hitos

- **H00 / UX-01:** incluir flujos visuales para desacoplar, mover entre monitores, volver a acoplar, guardar/restaurar y perder un monitor. Aprobación final de UX pendiente.
- **H02:** comparar frameworks no sólo con docking embebido sino con ventanas nativas multimonitor y su seguridad/persistencia. Un framework que no pueda satisfacerlo bloquea la decisión.
- **H03:** la carcasa de demostración deberá representar el modelo de workspace aprobado, aunque inicialmente use datos sintéticos.
- **H07:** `RB-H07.01` y `RB-H07.02` son **bloqueantes del primer MVP**; sus criterios de aceptación incluyen los puntos de esta decisión.
- **H09:** especificar recuperación ante cambio/desconexión de pantalla y migración segura de layout.
- **H11/H12:** el primer candidato MVP no cumple definición de terminado sin pruebas de ventanas desacopladas y multimonitor.

## No se decide todavía

- Framework definitivo (iced/egui/u otra solución).
- Lista exacta de paneles que podrán desacoplarse; la define UX-01.
- Implementación de la gestión de ventanas, persistencia y permisos.
- Plataformas iniciales adicionales a macOS de desarrollo.
- Aceptación de RB-H00.01: sigue en IN_REVIEW/REWORK menor, con re-QA de Haiku pendiente.

## Estado de la auditoría

Esta decisión **no valida** en vivo el producto legado, no concluye el re-QA de la auditoría, no habilita H00.02 y no autoriza código, releases, conexiones Kubernetes ni modificaciones del repositorio original.

**Registro:** se incorpora a la documentación para que futuros agentes y prompts no releguen estas funciones a un hito posterior.
