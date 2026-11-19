# Seguimiento de solicitudes

## Purpose

Dar visibilidad sobre responsables, avance, historial y plazos de atención de cada solicitud durante la demostración de Comercial Aurora.

## ADDED Requirements

### Requirement: Bandeja y detalle en una sola vista

La demostración SHALL ofrecer una sola vista de trabajo sin inicio de sesión ni cambio de perfil. La bandeja debe mostrar ID, cliente, responsable, estado y plazo, permitir buscar por ID, NIT o razón social y filtrar por estado o responsable.

#### Scenario: Consulta de una solicitud existente
- **WHEN** el usuario busca por NIT, filtra por estado y selecciona una solicitud de los resultados
- **THEN** la vista muestra el detalle y su historial junto con el acceso a la bandeja

### Requirement: Estados e historial de seguimiento

El ciclo SHALL admitir Nuevo → En proceso, En proceso → Pendiente de logística o Pendiente de ventas, ambos pendientes → En proceso, En proceso → Resuelto y Resuelto → Cerrado. Cada transición válida debe agregar una entrada consultable con fecha, actor de prueba, acción, estado anterior y nuevo, y comentario cuando se proporcione.

#### Scenario: Seguimiento de un caso que depende de logística
- **WHEN** una solicitud pasa de Nuevo a En proceso, luego a Pendiente de logística y vuelve a En proceso
- **THEN** el estado actual es En proceso y se conservan las tres transiciones en orden con sus datos de seguimiento

#### Scenario: Caso cerrado
- **WHEN** se consulta una solicitud en estado Cerrado
- **THEN** el detalle conserva el caso y su historial y ofrece solo consulta del estado

### Requirement: Indicadores visuales del plazo

La vista SHALL calcular el plazo de 48 horas corridas desde la recepción y mostrar el vencimiento y el tiempo restante para los casos abiertos, incluso en estados pendientes. Debe distinguir el aviso desde las 24 horas, el aviso de riesgo desde las 36 y el vencimiento al superar las 48, usando texto además de color.

#### Scenario: Límites de las alertas
- **WHEN** se consultan casos abiertos con 23 h 59 min, 24 h, 36 h, 48 h y 48 h 01 min de antigüedad
- **THEN** se observan, respectivamente, sin aviso, aviso de 24 h, riesgo de 36 h, riesgo de 36 h con saldo cero y vencimiento

#### Scenario: El plazo continúa durante una espera
- **GIVEN** una solicitud con 35 horas y 59 minutos de antigüedad en Pendiente de ventas
- **WHEN** alcanza 36 horas de antigüedad con la aplicación abierta o se vuelve a la aplicación después de ese umbral
- **THEN** el indicador muestra el riesgo de 36 horas y conserva el vencimiento calculado desde la recepción original

### Requirement: Cumplimiento al resolver

Al pasar a Resuelto, el sistema SHALL pedir una respuesta de fondo, registrar la fecha de resolución, calcular las horas corridas y marcar cumplimiento cuando el tiempo sea menor o igual a 48 horas. Al cerrar el caso debe mantener el resultado de esa resolución.

#### Scenario: Resolución dentro o fuera del plazo
- **WHEN** se resuelve un caso a las 48 horas exactas y otro a las 48 horas y un minuto, con respuesta de fondo en ambos
- **THEN** el primero queda como cumplido y el segundo como incumplido
- **AND** cerrar cada solicitud conserva el momento de resolución y su resultado

#### Scenario: Resolución sin respuesta de fondo
- **WHEN** se intenta resolver una solicitud con una respuesta vacía o compuesta solo por espacios
- **THEN** la vista solicita la respuesta y conserva el estado, los datos de resolución y el historial previos
