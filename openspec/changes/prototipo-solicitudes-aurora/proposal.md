# Propuesta para Comercial Aurora · Prototipo de gestión de solicitudes A05

## Why

Comercial Aurora atiende 300 clientes activos y procesa unos 1.200 pedidos y 600 solicitudes al mes. La especificación A05 estima que se pierde el 10 % de las solicitudes y que el 30 % queda sin responsable. Validar la radicación y el seguimiento en el navegador permitirá ajustar el flujo antes de invertir en un piloto multiusuario, donde la confiabilidad de la atención y de las entregas influye en la recompra.

## What Changes

- Entregar un único archivo `aurora.html`, adaptable y listo para abrir con doble clic, con el formulario, la bandeja, el detalle y el historial en una sola vista de demostración.
- Radicar manualmente solicitudes de llamadas, mensajería y correo, consultar el directorio por NIT, generar un identificador `AUR-YYYYMM-XXXX` y asignar cada caso a uno de cuatro agentes de prueba por turnos.
- Consultar y filtrar solicitudes, actualizar sus estados y registrar cada acción en el historial.
- Mostrar el plazo de 48 horas corridas, avisos visuales a las 24 y 36 horas, vencimiento y cumplimiento al resolver.
- Cargar clientes desde JSON o CSV y respaldar y recuperar la sesión mediante JSON descargable. Incluir casos ficticios para probar el flujo y los avisos sin esperar a que transcurran las horas.

## Capabilities

### New Capabilities

- `radicacion-solicitudes`: captura, validación e identificación de solicitudes con asignación automática.
- `seguimiento-solicitudes`: bandeja, ciclo de estados, historial y control visual del plazo.
- `datos-demostracion`: apertura local, datos ficticios, importación de clientes y respaldo de la sesión.

### Modified Capabilities

## Impact

El prototipo valida el flujo en una sesión local. El piloto posterior contempla los cinco usuarios concurrentes, autenticación, perfiles, reloj de servidor, datos compartidos y auditoría de producción. La hoja de ruta conserva las integraciones de correo, mensajería y ERP y las notificaciones automáticas para H2, y el portal, la analítica y la sincronización bidireccional para H3.

En la demostración se medirá si un caso típico puede radicarse en menos de 30 segundos y se verificará el recorrido completo desde la radicación hasta la recuperación del respaldo. El piloto medirá los resultados operativos del A05, incluidos registro y asignación del 100 %, resolución del 90 % dentro de 48 horas, reducción del tiempo administrativo de 20 a 12 minutos y reducción de los costos mensuales de COP 800.000 a COP 400.000.
