## Descripción

•       Este principio establece la no repetición de una misma responsabilidad en más de una clase o módulo.

•       En la medida en que una función es repetida en un mayor número de lugares, a la hora de modificar esa función, se pueden quedar varias de las piezas afectadas sin actualizar el cambio.
## Ejemplo

Imaginemos que estamos diseñando una API RESTful para un sistema de gestión de tareas. Podríamos enfrentarnos a varias decisiones de diseño, como cómo manejar la paginación de resultados, cómo validar los datos entrantes y cómo manejar los errores.

Si aplicamos el principio de "Una y solo una regla", decidimos que nuestra API seguirá una única estrategia para cada uno de estos aspectos. Por ejemplo, para la paginación, podemos elegir implementar una paginación basada en cursor, donde cada respuesta incluye un cursor que apunta al siguiente conjunto de resultados. Esta es nuestra única regla para la paginación.

Para la validación de datos, podemos decidir que todos los campos requeridos deben ser validados en el servidor antes de procesar cualquier solicitud. Esta es nuestra única regla para la validación de datos.

Finalmente, para el manejo de errores, podemos decidir que toda la API devolverá códigos de estado HTTP estándar y mensajes de error descriptivos en formato JSON. Esta es nuestra única regla para el manejo de errores.

Aplicar el principio de "Una y solo una regla" en nuestro diseño garantiza que cada decisión de diseño esté claramente definida y que no haya ambigüedad sobre cómo se deben manejar diferentes aspectos de la API. Esto facilita la comprensión del sistema por parte de los desarrolladores y usuarios, y simplifica el proceso de mantenimiento y extensión del sistema en el futuro.

![[Pasted image 20240723120514.png]]