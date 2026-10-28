# NovaLog CEDIS

Aplicación web académica basada en el documento `NovaLog CEDIS Documento 1`.
Implementa el flujo PHVA para un centro de distribución ficticio:

- Panel principal con tarjetas, semáforo de riesgos y pendientes.
- Información y alcance del CEDIS.
- Diagnóstico inicial con cálculo de cumplimiento interno.
- Matriz de riesgos con puntuación inicial y residual.
- Catálogo de controles.
- Inspección de unidades con los 17 puntos de revisión y bloqueo de liberación si quedan puntos pendientes o no conformes.
- Registro y seguimiento de incidentes.
- Indicadores, auditoría y acciones correctivas.
- Expediente imprimible y guardable como PDF desde el navegador.
- Pestaña de ayuda con explicación del propósito, funcionamiento y reglas de cada módulo.
- Expediente demostrativo precargado con el caso del Documento 2: NL-024,
  OP-07, EMB-101, tres riesgos orientativos, una inspección no liberada,
  un incidente y una acción correctiva.

## Uso

Abre `index.html` en un navegador moderno. Los registros se almacenan en
`localStorage` del navegador bajo la clave `novalog-cedis-v2`.

La etiqueta **Datos locales del ejercicio** distingue esta versión de una
instalación multiusuario. Para conectar Supabase se deben crear las tablas y
políticas RLS del documento, usar únicamente la clave pública `anon` y
reemplazar las operaciones de `localStorage` por llamadas autenticadas a la
API. Nunca se debe colocar una clave `service_role` en el frontend.

## Datos de demostración

Los datos iniciales son ficticios y se basan en el caso del Documento 2. Se
incluyen los siguientes ejemplos:

- R-01: ingreso sin verificación completa, probabilidad 3 e impacto 4.
- R-02: unidad liberada con inspección incompleta, probabilidad 3 e impacto 4.
- R-03: incidente sin seguimiento formal, probabilidad 4 e impacto 3.
- INS-001: camión NL-024, operador OP-07 y embarque EMB-101, no liberado.
- INC-001: falta de registro completo de una revisión de acceso.
- AC-001: actualización de SOP-04 y revisión de las siguientes cinco
  inspecciones para comprobar eficacia.

Los datos pueden modificarse desde los formularios y se guardan localmente en
el navegador. La pestaña Ayuda incluye ejemplos de llenado de cada módulo.
Los formularios también incluyen **Cargar ejemplo del caso** para completar
rápidamente los datos principales del Documento 2. El ejemplo se carga solo en
el formulario actual, puede editarse antes de guardar y no impide capturar la
información manualmente.

## Pendientes respecto al PDF

Esta versión es una versión funcional local. Todavía no implementa:

1. Persistencia en Supabase, autenticación, usuarios, permisos y políticas RLS.
2. La sincronización con la estructura normalizada de tablas propuesta en una
   base de datos remota.
3. La edición posterior de riesgos y controles desde una pantalla dedicada;
   por ahora se registran desde el flujo inicial y se consultan en tablas.
4. La carga física de archivos de evidencia; actualmente se conserva la
   referencia o descripción textual de la evidencia.
5. Filtros avanzados combinables por fecha, proceso, riesgo, categoría,
   responsable y estado en todos los reportes.
6. El flujo de incidentes con investigación independiente, fecha de cierre y
   creación automática de una acción correctiva.
7. La reapertura automática de acciones cuando falla la verificación de
   eficacia.
