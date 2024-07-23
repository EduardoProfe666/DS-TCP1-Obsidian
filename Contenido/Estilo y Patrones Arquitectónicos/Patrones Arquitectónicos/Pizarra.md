## Descripción

- El estilo al que pertenece es [[Centrado en Datos]]
- Activa componentes cuando los datos particulares se tornan disponibles.
- Es un repositorio de datos dividido en niveles. Cada nivel almacena soluciones parciales del problema que resuelve el sistema.
- **Fuente de Conocimiento:** Cada Fuente de Conocimiento (FC) implementa una regla o algoritmo que colabora para obtener una solución parcial o final; cada FC es un ”especialista o ”experto” en resolver un aspecto del problema global. Ninguna FC puede resolver el problema por si sola.
- **Control/Estrategia:** Monitorea los cambios en el Blackboard y decide qué FC debe ejecutarse, según la estrategia de control que implementa
- Posibilita la integración de agentes.
- Adecuado para la resolución de  problemas no deterministas.
- Se puede resumir el estado de conocimiento en cada momento del proceso

	![[Pasted image 20240722223151.png]]
## ¿Cuándo se usa?

- Sistema multiagentes que contenga múltiples agentes autónomos con capacidad incompleta para resolver el problema global y que al trabajar en forma integrada son capaces de detectar, evaluar y alertar sobre vulnerabilidades de forma temprana, para que se puedan tomar medidas antes de que ocurran hechos delictivos

## ¿Cómo se representa?

#### Pizarra de Estrada
	![[Pizarra Estrada.jpeg]]

#### Pizarra de Ejercicio Integrador
	![[Pizarra Ejercicio Integrador.png]]

#### Pizarra de Conferencia
	![[Pasted image 20240722223656.png]]