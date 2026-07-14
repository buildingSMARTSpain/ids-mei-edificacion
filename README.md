# IDS MEI Edificación

**Especificación IDS (Information Delivery Specification) que traduce los requisitos mínimos del [MEI Edificación](https://www.buildingsmart.es/recursos/manual-de-entrega-de-informacion-edificacion/) (Manual de Entrega de Información en Edificación) de buildingSMART Spain a comprobaciones automáticas sobre modelos IFC.**

[![IDS y resultados: CC BY 4.0](https://img.shields.io/badge/IDS%20y%20resultados-CC%20BY%204.0-blue.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Modelo IFC: CC BY-ND 4.0](https://img.shields.io/badge/Modelo%20IFC-CC%20BY--ND%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nd/4.0/)

> **Acceso abierto.** buildingSMART Spain comparte en esta ocasión, públicamente y sin necesidad de ser socio, el fichero IDS completo. Cualquier persona u organización puede descargar, usar y adaptar el fichero bajo los términos de la licencia (ver más abajo).

## Contexto: el MEI y los estándares IDS y BCF

El [**MEI Edificación**](https://www.buildingsmart.es/recursos/manual-de-entrega-de-informacion-edificacion/) establece los requisitos de información recomendados para mejorar la coherencia y la estructura de los modelos IFC en proyectos de edificación. Se articula sobre cuatro principios: la definición del punto de origen del proyecto, la denominación de los niveles, el uso correcto de las entidades y sus propiedades, y la aplicación de sistemas de clasificación.

Un manual describe el requisito, pero no lo comprueba. Verificar a mano si un modelo cumple el MEI es lento, poco repetible y depende del criterio de quien revisa. El propio MEI ya señala IDS como vía de validación automática de su cumplimiento: este repositorio es esa vía, desarrollada y publicada para que pueda usarse directamente.

**IDS (Information Delivery Specification)** es el estándar abierto de buildingSMART que expresa un requisito de información en un formato legible por máquina. Traducir el MEI a IDS convierte el manual en una comprobación que cualquier herramienta compatible ejecuta sobre un IFC de la misma forma, sin depender de interpretaciones.

**BCF (BIM Collaboration Format)** es el estándar abierto de buildingSMART para intercambiar incidencias sobre un modelo. Con BCF, el resultado de la validación no se queda en un informe: vuelve al flujo de trabajo como incidencias localizadas en el elemento concreto, que se abren en cualquier visor compatible.

La cadena que ilustra este repositorio es, por tanto: **MEI** (el requisito) → **IDS** (la comprobación) → **BCF** (el resultado, accionable sobre el modelo).

## Descripción y alcance

Este repositorio contiene el fichero IDS que comprueba el cumplimiento de los requisitos mínimos de información del **MEI Edificación**, el manual de entrega de información BIM para edificación publicado por buildingSMART Spain. El fichero ha sido desarrollado, revisado y auditado por el equipo técnico de buildingSMART Spain (Coordinación Técnica).

**Qué comprueba automáticamente:**

> El fichero IDS comprueba automáticamente la presencia de la información mínima del MEI: ordenación de niveles, uso de entidades, clasificación (GuBIMclass), denominación de espacios, propiedades de los objetos (carga portante, interior/exterior, resistencia al fuego, transmitancia térmica) y material.

**Qué NO comprueba:**

- Los **valores concretos** de la información: el IDS comprueba que la información existe, no que sea correcta (un `FireRating` presente pero erróneo pasa la validación; el código GuBIMclass no se valida contra la tabla oficial de códigos).
- Los **requisitos geométricos** del MEI (nivel de detalle, coherencia dimensional).
- La **coherencia entre modelos** (federación, no duplicación de información).

La validación de valores concretos y requisitos geométricos es responsabilidad del Requeridor de Información de cada proyecto.

## Contenido del repositorio

| Fichero | Descripción |
|---|---|
| `ids/MEIE01-BSSP-ZZZ-ZZZ-EIR-MIC-001-ControlBasicoMEI-S2-0500.ids` | Especificación IDS vigente (rev 0500). Pasa el [IDS Audit Tool oficial de buildingSMART](https://github.com/buildingSMART/IDS-Audit-tool) sin errores. |
| `sample-validation/MEIE01-BSSP-ZZZ-ZZZ-INF-MIC-001-MuestraBCFValidacionMEI-S2-0200.bcf` | Muestra de resultados de validación en formato **BCF (BIM Collaboration Format)**, el estándar abierto de buildingSMART para intercambiar incidencias y comentarios sobre un modelo IFC. Se abre con cualquier visor compatible con BCF. |
| `sample-validation/informe-validacion-visor-0500-ARQ.html` | Informe de validación en HTML, legible en cualquier navegador. |
| `model/20-900084_HabitatgesDotacionals_PE_ARQ_R24.ifc` | Modelo IFC de arquitectura usado para generar la muestra de validación (43 MB). Permite reproducir la validación de principio a fin. Cedido por el **Àrea Metropolitana de Barcelona (AMB)**. |

> **Nota sobre la muestra de validación:** al igual que las [muestras de test de la comunidad buildingSMART](https://github.com/buildingsmart-community/Community-Sample-Test-Files), estos ficheros son **ejemplos ilustrativos**, no una validación oficial ni certificación de cumplimiento del MEI. El resultado depende del modelo IFC concreto que se valide.
>
> El modelo IFC de edificación residencial/dotacional usado para generar esta muestra fue cedido por el **Àrea Metropolitana de Barcelona (AMB)** para su uso en talleres y actividades de buildingSMART Spain. El modelo se incluye en la carpeta `model/`, de modo que cualquiera puede reproducir la validación completa: ejecutar el IDS sobre el mismo IFC y obtener los mismos resultados.

### Reproducibilidad

El informe y el BCF de esta muestra se generaron con un motor de validación IDS basado en **[IFC Lite](https://ifclite.dev)** (proyecto de código abierto de LTplus-AG, licencia MPL-2.0), en la versión `@ifc-lite/ids` 1.15.25. Código fuente: [github.com/LTplus-AG/ifc-lite](https://github.com/LTplus-AG/ifc-lite).

Se indica el motor y su versión porque distintas implementaciones del estándar IDS pueden diferir en la interpretación de alguna faceta. Si reproduces la validación con otra herramienta compatible y obtienes resultados distintos, abre un issue: es información útil tanto para este IDS como para el ecosistema de herramientas.

## Cómo usar este IDS

1. Descarga el fichero `.ids` de la carpeta `ids/`.
2. Valida tu modelo IFC con una herramienta compatible con el estándar IDS v1.0.0, por ejemplo:
   - [IDS Audit Tool](https://github.com/buildingSMART/IDS-Audit-tool) (oficial de buildingSMART, línea de comandos)
   - [ifctester](https://github.com/IfcOpenShell/IfcOpenShell) (módulo `src/ifctester`, proyecto de código abierto IfcOpenShell, licencia LGPL-3.0)
   - Cualquier otra herramienta compatible con el esquema IDS 1.0

**Compatibilidad:** esquema IDS v1.0.0 (XSD oficial), modelos IFC4 e IFC4X3_ADD2.

## Cómo contribuir / reportar incidencias

Este repositorio usa **GitHub Issues** como canal estructurado de feedback. Si detectas un error en el fichero IDS, una ambigüedad en el alcance, o quieres proponer una mejora:

1. Revisa si ya existe un issue similar.
2. Abre un nuevo issue describiendo el problema o la propuesta, idealmente con un ejemplo reproducible (modelo IFC o fragmento).
3. El equipo técnico de buildingSMART Spain hace triage y responde.

## Licencia

Este repositorio combina dos licencias, según el contenido y su titularidad:

| Contenido | Licencia | Autoría |
|---|---|---|
| Fichero IDS (`ids/`), muestra de validación (`sample-validation/`) y esta documentación | **[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.es)** | buildingSMART Spain |
| Modelo IFC (`model/`) | **[CC BY-ND 4.0](https://creativecommons.org/licenses/by-nd/4.0/deed.es)** | Àrea Metropolitana de Barcelona (AMB) |

**El IDS y los resultados de validación (CC BY 4.0):** puedes usarlos, modificarlos y redistribuirlos, incluso con fines comerciales, siempre que cites la autoría original (buildingSMART Spain). Adaptar el IDS a los requisitos de tu propio proyecto es un uso previsto.

**El modelo IFC (CC BY-ND 4.0):** puedes descargarlo, redistribuirlo íntegro y usarlo para validar o probar herramientas, incluso con fines comerciales, citando al AMB. No puedes publicar versiones modificadas del modelo. Ejecutar validaciones sobre él no constituye una obra derivada. Detalle en [`model/README.md`](model/README.md).

## Contacto

**buildingSMART Spain**
Web: [https://www.buildingsmart.es](https://www.buildingsmart.es)
Email: info@buildingsmart.es
