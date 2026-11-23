# AGENTS — NovaKube Native

Antes de toda tarea visual, leer `BRAND_IDENTITY.md` y `docs/brand/novaq-gateway/README.md`. La familia NovaKube usa identidad aprobada NovaKube Core / Nova Gateway (SAAS-03). No modificar marca por merges, actualizaciones técnicas ni nuevos hitos. Native es un proyecto de arquitectura y código Rust: agregar documentación de identidad **no autoriza cambiar lógica, UX o arquitectura**. Si aparece UI, respetar tokens aprobados sin inventar assets.


**Ícono oficial:** NovaKube Core (propuesta 01): N clara dentro de dos marcos redondeados, verde interior, gris exterior y fondo grafito. Fuente versionada `docs/brand/novaq-gateway/assets/novakube-core.svg`, reconstruida desde la imagen de referencia, no el archivo maestro original. **Nombre vigente: Nova Gateway**. No reemplazar con monograma simple ni alterar marca por merges. `--novaq-*` es un identificador de código histórico.

## Frontend obligatorio — GoogleChrome Modern Web Guidance

**Política transversal (22-11-2026):** para toda nueva UI o cambio de frontend web (incluidos renderers Electron y cualquier frontend futuro), el agente DEBE leer y aplicar la skill local [Modern Web Guidance](.agents/skills/modern-web-guidance/SKILL.md), procedente de https://github.com/GoogleChrome/modern-web-guidance (archivo upstream bajo licencia Apache-2.0). Consultarla **antes** de implementar HTML, CSS, componentes, UX, accesibilidad, animaciones, formularios, APIs del navegador, lógica JavaScript cliente, seguridad frontend o mejoras de performance.

Flujo obligatorio:
1. Buscar recomendaciones con una consulta concreta, en inglés, de 2–5 palabras: \`npx -y modern-web-guidance@latest search "responsive data table" --skill-version 2026_11_10-47b4c80e\` (adaptar consulta a la tarea).
2. Recuperar los IDs relevantes con \`npx -y modern-web-guidance@latest retrieve "<guide-id>"\`. Si no hay coincidencia, reformular una vez; no inventar IDs ni aplicar guías no pertinentes.
3. Implementar respetando la compatibilidad real de los navegadores/runtimes soportados y los fallbacks requeridos; validar accesibilidad, comportamiento, seguridad, rendimiento y pruebas existentes. Seguir las instrucciones completas del SKILL.md.
4. Registrar brevemente las guías aplicadas y las decisiones no obvias en el cierre de cada tarea frontend.

No usarla para tareas exclusivamente backend, Kubernetes, CI/CD, infraestructura, contratos, Git o tests sin cambio de UI. La skill **no sustituye** los contratos, gates, identidad de marca, tokens versionados, temas Claro/Oscuro/Auto, i18n \`es-AR/en-US\`, aislamiento multi-tenant, RBAC, convenciones de ingeniería, Gentle AI ni el alcance aprobado de los hitos. No agregar dependencias, migrar arquitectura ni ejecutar scans globales solo por incorporar esta política. Para Google Antigravity/Gemini, la instalación oficial adicional es \`agy plugin install https://github.com/GoogleChrome/modern-web-guidance\` si el agente local lo requiere.
