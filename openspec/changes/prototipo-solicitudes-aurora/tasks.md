# Tareas de implementación

## 1. Base de la demostración

- [ ] 1.1 Crear `aurora.html` con HTML5, CSS3 y JavaScript integrados, estados vacíos y una vista adaptable. Verificar apertura por doble clic con red desactivada y navegación por teclado.
- [ ] 1.2 Incorporar cuatro agentes y un directorio ficticio. Confirmar que la vista los identifica como datos de demostración y que la búsqueda por NIT es utilizable.

## 2. Radicación y seguimiento

- [ ] 2.1 Implementar el formulario, el autocompletado y la validación. Comprobar los tres canales, una radicación sin pedido y los errores de campos obligatorios sin crear registros.
- [ ] 2.2 Implementar ID, asignación y evento inicial. Verificar cinco altas en orden 1, 2, 3, 4 y 1, la unicidad de IDs y el reinicio del consecutivo al cambiar el mes.
- [ ] 2.3 Implementar la bandeja, sus filtros, el detalle y las transiciones. Verificar una gestión que pasa por Pendiente de logística y termina Cerrada con el historial completo.
- [ ] 2.4 Implementar el plazo y el resultado al resolver. Probar los límites con un reloj controlado y comprobar que los avisos se distinguen también por su texto. Incorporar casos ficticios que cubran cada banda.

## 3. Archivos y continuidad

- [ ] 3.1 Implementar la importación de clientes en JSON y CSV. Probar 300 filas válidas, NIT como texto, campos CSV entre comillas y rechazo de duplicados o filas incompletas sin cambios parciales.
- [ ] 3.2 Implementar exportación y restauración JSON con versión de formato y aviso de cambios pendientes. Verificar que el respaldo recupera solicitudes, historial y siguiente asignación, y que un respaldo inválido preserva la sesión.

## 4. Prueba de entrega

- [ ] 4.1 Abrir el archivo descargado en un navegador de escritorio y probar un ancho móvil. Completar un recorrido de radicación, consulta, transición, resolución, exportación, cierre y recuperación.
- [ ] 4.2 Cronometrar una radicación típica frente a la meta de menos de 30 segundos y registrar las observaciones que deban resolverse antes del piloto.
- [ ] 4.3 Entregar el archivo HTML probado e indicar cómo abrirlo y ensayar una alerta de cada nivel.
