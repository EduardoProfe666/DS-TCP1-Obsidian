## Descripción

- Separa los datos y la lógica de negocio de una aplicación de la interfaz de usuario y el módulo encargado  de gestionar los eventos y las comunicaciones.
- Pertenece al estilo [[Llamada y Retorno]]
- El patrón MVC, separa elementos de un sistema, permitiéndoles cambiar de forma independiente. Por ejemplo, agregar una nueva vista o cambiar una vista existente puede hacerse sin modificación alguna a los datos subyacentes en el modelo.
- Es una versión del N-capa por Responsabilidad
- **Modelo:**
	- Se representa la información con la que trabaja la aplicación y su lógica de negocio.
	- Encapsula los datos y las funcionalidades.
	- Es independiente de cualquier representación de salida y/o comportamiento de entrada.
- **Vista:**
	- Maneja la visualización de la información.
	- Requiere de que se le suministre del modelo la información a mostrar,  lo que se hace a través del controlador.
- **Controlador:**
	- Interpreta las acciones que recibe de la vista, informando al modelo y/o a la vista para que cambie según resulte apropiado.
	- Respuesta a eventos que recibe de la vista
	- Invoca peticiones al modelo
	- Envía comandos a la vista
- Separa presentación e interacción de los datos del sistema. El sistema se estructura en tres componentes lógicos que interactúan entre sí. El componente MODELO maneja los datos de sistema y las operaciones asociadas a esos datos. El componente VISTA define y gestiona cómo se presentan los datos al usuario. El componente CONTROLADOR dirige la interacción del usuario y las pasa a Vista y Modelo.

	![[Pasted image 20240722220858.png]]

## ¿Cuándo se usa?

Se usa cundo existen múltiples formas de ver e interactuar con los datos. También se utiliza al desconocerse los requerimientos futuros para la interacción y la presentación.

## ¿Cómo se representa?

![[Pasted image 20240722220922.png]]

## MVC como Antipatrón

Un propósito común de numerosas aplicaciones es el de tomar datos de un almacenamiento y mostrarlos al usuario. Cuando el usuario introduce modificaciones se reflejan en el almacenamiento.

Como solución se sugiere unir ambas piezas para reducir la cantidad de código y optimizar la ejecución porque el flujo de información ocurre entre el almacenamiento y la interfaz.

La programación de interfaz y la lógica de negocios requiere de habilidades distintas.

Las aplicaciones incorporan lógica de negocio que va más allá de la trasmisión de datos.

Principios de diseño que incumple:

•Encapsular la variabilidad
•Principio Hollywood
•Single Responsability Principle
•…