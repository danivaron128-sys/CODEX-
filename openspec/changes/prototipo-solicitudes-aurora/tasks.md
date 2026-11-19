# Tareas de implementación

## 1. Base de la demostración

- [x] 1.1 Crear `aurora.html` con HTML5, CSS3 y JavaScript integrados, estados vacíos y una vista adaptable. Verificar apertura por doble clic con red desactivada y navegación por teclado.
- [x] 1.2 Incorporar cuatro agentes y un directorio ficticio. Confirmar que la vista los identifica como datos de demostración y que la búsqueda por NIT es utilizable.

## 2. Radicación y seguimiento

- [x] 2.1 Implementar el formulario, el autocompletado y la validación. Comprobar los tres canales, una radicación sin pedido y los errores de campos obligatorios sin crear registros.
- [x] 2.2 Implementar ID, asignación y evento inicial. Verificar cinco altas en orden 1, 2, 3, 4 y 1, la unicidad de IDs y el reinicio del consecutivo al cambiar el mes.
- [x] 2.3 Implementar la bandeja, sus filtros, el detalle y las transiciones. Verificar una gestión que pasa por Pendiente de logística y termina Cerrada con el historial completo.
- [x] 2.4 Implementar el plazo y el resultado al resolver. Probar los límites con un reloj controlado y comprobar que los avisos se distinguen también por su texto. Incorporar casos ficticios que cubran cada banda.

## 3. Archivos y continuidad

- [x] 3.1 Implementar la importación de clientes en JSON y CSV. Probar 300 filas válidas, NIT como texto, campos CSV entre comillas y rechazo de duplicados o filas incompletas sin cambios parciales.
- [x] 3.2 Implementar exportación y restauración JSON con versión de formato y aviso de cambios pendientes. Verificar que el respaldo recupera solicitudes, historial y siguiente asignación, y que un respaldo inválido preserva la sesión.

## 4. Prueba de entrega

- [x] 4.1 Abrir el archivo descargado en un navegador de escritorio y probar un ancho móvil. Completar un recorrido de radicación, consulta, transición, resolución, exportación, cierre y recuperación.
- [x] 4.2 Cronometrar una radicación típica frente a la meta de menos de 30 segundos y registrar las observaciones que deban resolverse antes del piloto.
- [x] 4.3 Entregar el archivo HTML probado e indicar cómo abrirlo y ensayar una alerta de cada nivel.

## Resultado de la prueba de entrega

- Chromium abrió el HTML directamente desde `file://` con la red desactivada en escritorio y a 390 px. La prueba automatizada completó la radicación, el seguimiento y la recuperación desde JSON.
- Una radicación típica tardó aproximadamente 0,15 s en la prueba automatizada. Para evaluar la meta de 30 s con personas, el piloto deberá medir la captura de casos reales por agentes.
