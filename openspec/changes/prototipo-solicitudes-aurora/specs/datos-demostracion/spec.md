# Datos de demostración

## Purpose

Permitir que una persona abra, pruebe y retome el prototipo de Comercial Aurora con datos locales y archivos portables.

## ADDED Requirements

### Requirement: Apertura autónoma en navegador

El prototipo SHALL entregarse como un único archivo HTML que pueda abrirse con doble clic y funcione sin servidor, instalación ni conexión a internet. El formulario, la bandeja y el detalle deben seguir siendo utilizables en pantallas de escritorio y móviles.

#### Scenario: Primera apertura sin conexión
- **WHEN** se abre el archivo descargado con la red desactivada en un navegador compatible
- **THEN** se pueden consultar casos ficticios de demostración y radicar una solicitud sin descargar recursos adicionales

### Requirement: Casos ficticios para probar el plazo

La demostración SHALL ofrecer datos ficticios identificados como tales, con cuatro agentes y casos representativos sin aviso, con aviso de 24 horas, con riesgo de 36 horas y vencidos.

#### Scenario: Prueba de alertas en una sesión nueva
- **WHEN** se abre una sesión nueva con los casos de demostración
- **THEN** las cuatro condiciones pueden inspeccionarse inmediatamente sin modificar el reloj del equipo

### Requirement: Importación del directorio de clientes

El prototipo SHALL aceptar una lista JSON o un CSV UTF-8 con los campos `cliente_nit` y `cliente_nombre`. Debe tratar el NIT como texto, validar todo el archivo antes de aplicarlo, incorporar NIT nuevos y actualizar los conocidos. El resultado de la carga debe ser visible y conservar los datos registrados en solicitudes anteriores.

#### Scenario: Carga de un directorio válido
- **WHEN** se importa un archivo válido de 300 clientes con NIT distintos
- **THEN** la interfaz confirma la carga y permite seleccionar por NIT un cliente recién importado

#### Scenario: Actualización de un cliente ya registrado
- **GIVEN** una solicitud histórica vinculada a un cliente cuyo NIT tiene ceros a la izquierda
- **WHEN** se importa un CSV con ese NIT y una razón social actualizada entre comillas que contiene una coma
- **THEN** el directorio conserva el NIT completo y muestra la razón social actualizada
- **AND** el detalle de la solicitud histórica conserva la razón social registrada al radicarla

#### Scenario: Archivo con registros inválidos
- **WHEN** se importa un archivo con NIT duplicados o sin razón social en una fila
- **THEN** se identifica el error y se conserva el directorio previo completo

### Requirement: Respaldo y recuperación de una sesión

El prototipo SHALL exportar un respaldo JSON versionado con clientes, agentes, solicitudes, historial y estado de numeración y asignación. Debe validar el respaldo antes de reemplazar la sesión, solicitar confirmación si se reemplazan cambios sin exportar e informar cómo guardar el trabajo antes de cerrar.

#### Scenario: Continuación después de cerrar el navegador
- **WHEN** se exporta un respaldo, se cierra el archivo y se restaura el JSON en una sesión nueva
- **THEN** la bandeja, los detalles y el historial coinciden con lo exportado
- **AND** una nueva radicación continúa el turno y conserva la unicidad de los identificadores

#### Scenario: Restauración inválida
- **WHEN** se selecciona un respaldo ilegible, incompatible o con referencias incoherentes
- **THEN** se explica el error y la sesión activa se mantiene completa

#### Scenario: Cancelación al reemplazar trabajo pendiente
- **GIVEN** una sesión activa con cambios sin exportar
- **WHEN** se selecciona un respaldo válido y se cancela el reemplazo
- **THEN** se conservan las solicitudes, el historial y los cambios pendientes de la sesión activa
