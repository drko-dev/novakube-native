# Identidad visual maestra — NovaQ Gateway / familia NovaKube

**Carpeta de referencia obligatoria para diseño y desarrollo visual.** Version 1.0.0, 17 noviembre 2026.

## Aprobacion y fuente de verdad

De las propuestas Core, Orbit y Gateway se eligio **NovaKube Core** (la primera);
la identidad elegida se denomino **NovaQ Gateway**. La paleta fue fijada y
utilizada en el SaaS como **SAAS-03**, en:
Documents/NovaKube-SaaS/services/saas-api/app/static/css/novaq_tokens.css

Este manual se apoya en esa fuente; no usar como marca el kit de OpenLens DevOps,
los estilos Lens, paletas de WS-02 ni sugerencias de generadores.

## Paleta oficial aprobada

| Componente | Color |
| --- | --- |
| Fondo principal / graphite | #15181C |
| Tarjetas / superficies | #252B31 |
| Verde primario de marca | #45D6B0 |
| Hover del primario | #36BA97 |
| Verde intenso | #2EA888 |
| Verde claro | #6CE2C3 |
| Texto principal | #E8EDF1 |
| Texto secundario | #9AA6B2 |
| Texto terciario | #7D8996 |
| Borde normal | #323942 |
| Borde sutil | #2C333B |

Los valores tienen equivalentes importables en tokens/brand.json y
tokens/brand.css. La copia literal de la hoja original se guarda en
tokens/novaq_tokens.saas03.source.css.

## Tipografia implementada

Fuente del producto SaaS: -apple-system, BlinkMacSystemFont, SF Pro Display,
SF Pro Text, Helvetica Neue, sans-serif.
Esta es una pila de fuentes de sistema: no hay fuente propietaria aprobada
para redistribuir. Conservar jerarquias y tamanos de cada componente ya
existente; no cambiarlos para forzar una semejanza con otro producto.
Logs y terminales pueden usar monospace de sistema sin alterar la fuente UI.

## Marca y logotipo

Actualmente Gateway y Portal muestran un monograma **N** creado mediante CSS
(.novaq-brand-mark). Medidas de la implementacion: 30 x 30 px, radio 7 px,
borde 1.5 px verde de marca, tipografia negrita. Cabeceras implementadas:
NovaKube Gateway (proveedor) y NovaKube Portal (cliente).
No se encontro archivo maestro SVG/PNG de NovaQ en el directorio de imagenes
del SaaS. No inventar uno ni usar el logo de OpenLens DevOps por defecto.
El inventario y pendientes constan en assets/README.md.

## Componentes de la aplicacion actual

Observado en el CSS del SaaS: topbar 56 px, sidebar 244 px, radios 14 px
(general) y 10 px (pequeno). Estos valores describen **el SaaS existente**,
no ordenan cambiar dimensiones del Workspace ni de otros proyectos.
El boton primario usa fondo #45D6B0 y texto oscuro #15181C; hover #36BA97.
Los badges de cliente usan azul solo como distincion semantica. Advertencias
y errores tienen su propia semantica; no reemplazar con verde.
Conservar colores elegidos por el usuario para los clústeres.

## Interaccion, layout y accesibilidad

Mantener componentes, jerarquias, espaciados, navegacion y diseno responsive
que ya fueron aprobados en cada producto. Contraste WCAG AA como meta para
texto (4.5:1), foco visible, acciones no dependientes solo del color,
estados hover/focus/disabled. Evitar combinaciones de bajo contraste.

## Regla universal de cambios

**Todo desarrollo visual nuevo debe consultar esta carpeta ANTES de diseñar.**
Cambiar de build, framework o dependencia no autoriza alterar marca.
Una correccion de paleta NO debe tocar estructura, rutas, filtros, favoritos,
tabs, adaptadores, datos, autorizacion, RBAC, APIs, conexiones ni responsive.
La evaluacion de las vistas real de desarrollo y produccion, pruebas de
regresion y auditoria de dependencias precede a cualquier merge.
Un cambio visual distinto de la identidad se somete a aprobacion.

## Archivos de este paquete

- tokens/brand.json: valores y metadatos estructurados.
- tokens/brand.css: variables para nuevos proyectos.
- tokens/novaq_tokens.saas03.source.css: copia exacta de fuente original.
- examples/palette.html: vista local con colores, tipografia y componentes.
- assets/README.md: inventario de activos, licencias y pendientes.
- AGENTS.md: instrucciones obligatorias para agentes de codigo.
- SOURCE_MANIFEST.json: SHA-256 de la fuente original.

**Distincion de estado:** la paleta es aprobada por SAAS-03; la fuente,
medidas y monograma son lo actualmente implementado, no un nuevo rebranding.
Los activos ausentes no se presentan como aprobados.
