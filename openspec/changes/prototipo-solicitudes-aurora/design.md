# Diseño del prototipo A05

## Context

El repositorio parte de la configuración de OpenSpec. La entrega se ejecutará desde `file://` en un navegador instalado. El PDF A05 ofrece el vocabulario, las reglas de negocio y la hoja de ruta que sirven de referencia al diseño.

## Goals / Non-Goals

- Validar en una sesión el recorrido desde captura, asignación y seguimiento hasta recuperación del respaldo.
- Mantener el esquema de datos separado de la presentación para facilitar una futura implementación multiusuario.
- Reservar para el piloto la persistencia central, las escrituras concurrentes, la autenticación y el historial con garantías de auditoría.

## Decisions

1. **HTML5, CSS3 y JavaScript integrados.** `aurora.html` incorpora estilos, lógica y datos ficticios. Se abre con doble clic y la validación de entrega se hace con el archivo descargado y la red desactivada.
2. **Una vista adaptable.** El formulario, la bandeja y el detalle con historial comparten una navegación de página única. En pantallas estrechas se apilan. Las acciones y los estados usan etiquetas visibles, foco por teclado y texto además del color.
3. **Estado en memoria y operaciones explícitas.** Objetos y arreglos contienen clientes, agentes, solicitudes y eventos. La radicación válida produce el ID, la asignación y la entrada inicial como una sola operación. Se revisan referencias y unicidad al restaurar. Los IDs se agrupan por el mes de Colombia, con fechas almacenadas en ISO 8601. Si se agota el consecutivo mensual de cuatro dígitos, se informa y se conserva el estado.
4. **Estados con reglas simples de demostración.** Nuevo pasa a En proceso. Desde En proceso se puede pasar a Pendiente de logística, Pendiente de ventas o Resuelto. Los estados pendientes vuelven a En proceso. Resuelto pasa a Cerrado. El cierre se modela como terminal y el actor del historial es una etiqueta de demostración.
5. **Plazo calculado con el reloj del navegador.** Se compara la diferencia de instantes en milisegundos y se formatea para mostrarla. Los estados pendientes consumen el plazo. El indicador se actualiza con la aplicación abierta y al recuperar el foco. Los casos iniciales usan edades relativas y la prueba de límites usa instantes controlados.
6. **Importación y respaldo separados.** El directorio usa una lista JSON de registros o un CSV UTF-8 con encabezados `cliente_nit,cliente_nombre`. Los NIT se leen como texto y las filas se validan antes de aplicar. Los clientes nuevos se incorporan por NIT y los ya existentes se actualizan sin reescribir el nombre guardado en solicitudes anteriores. El respaldo integral tiene una versión de formato y restaura la sesión completa previa validación.

## Risks / Trade-offs

- **Pérdida de avances al cerrar** → Mostrar el estado de cambios pendientes y permitir exportar el JSON desde la vista principal.
- **Archivos de prueba ambiguos o manipulados** → Validar estructura, tamaño razonable y referencias. Tratar texto importado como datos al renderizarlo.
- **Diferencias por reloj local o copias separadas** → Usar el prototipo con datos ficticios y validar plazos con instantes controlados. El piloto deberá probar reloj de servidor y concurrencia.
- **Traslado al piloto** → Revisar el formato de datos y las reglas de flujo con el equipo antes de definir migración, permisos y operación real.
