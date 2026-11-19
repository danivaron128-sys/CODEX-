# Radicación de solicitudes

## Purpose

Estandarizar la captura manual de solicitudes de Comercial Aurora y garantizar que cada caso válido tenga identificación y responsable desde su registro.

## ADDED Requirements

### Requirement: Captura por canal y búsqueda de cliente

El formulario SHALL admitir llamada telefónica, mensajería y correo electrónico. Debe buscar al cliente por NIT y completar su razón social desde el directorio. Debe permitir asociar de forma opcional un identificador de pedido ingresado manualmente.

#### Scenario: Radicación de un reclamo telefónico
- **WHEN** se elige llamada telefónica, se selecciona un cliente del directorio y se completa una inconformidad de envío con una descripción válida
- **THEN** el formulario muestra la razón social del cliente y permite guardar la solicitud con o sin pedido asociado

#### Scenario: Radicación asistida de un mensaje o correo
- **WHEN** el usuario selecciona mensajería o correo electrónico y registra manualmente una solicitud válida
- **THEN** el caso y su evento inicial conservan el canal elegido

### Requirement: Validación antes de registrar

El formulario SHALL exigir canal, cliente del directorio, tipo y descripción de al menos diez caracteres sin contar espacios al inicio o al final. Los tipos son consulta de stock, estado de pedido, inconformidad de envío, facturación o cobro y devolución.

#### Scenario: Formulario incompleto o inválido
- **WHEN** se guarda sin canal o sin cliente, con un tipo inválido o con una descripción demasiado corta
- **THEN** la vista muestra los errores correspondientes, mantiene los valores introducidos y conserva sin cambios la bandeja, el historial y los contadores de asignación

### Requirement: Identificación y asignación por turnos

Cada radicación exitosa SHALL crear un ID inmutable `AUR-YYYYMM-XXXX` con consecutivo mensual, registrar la recepción en ISO 8601, asignar el siguiente de cuatro agentes de prueba en orden circular y crear el caso en estado Nuevo con un evento inicial de historial.

#### Scenario: Apertura de cinco solicitudes válidas
- **WHEN** se radican cinco solicitudes sucesivas en una sesión de prueba vacía
- **THEN** los cinco IDs son distintos y los agentes asignados siguen el orden 1, 2, 3, 4 y 1
- **AND** cada solicitud aparece en estado Nuevo con la recepción, el responsable y un evento que identifica el canal de radicación

#### Scenario: Primer registro de un mes en Colombia
- **GIVEN** que la sesión conserva solicitudes registradas durante el mes anterior
- **WHEN** se guarda la primera solicitud del nuevo mes según la zona horaria de Colombia
- **THEN** el ID contiene el año y mes nuevos y el consecutivo `0001`
- **AND** la asignación continúa en el siguiente turno y los IDs anteriores se conservan

#### Scenario: Consecutivo mensual agotado
- **WHEN** se intenta registrar otra solicitud después de emitir el consecutivo `9999` en el mismo mes
- **THEN** se informa el límite y se conservan las solicitudes, el historial y el turno de asignación
