## Descripción

- Conjunto de piezas de distintos tipos, que encajan entre sí y cumplen una función determinada
- **Pieza** == **Componente**
- El objetivo es la mantenibilidad, construir para el cambio
- La idea es que los componentes no se reusan, se reemplazan, sin afectar el resto de los componentes.
- La arquitectura de componentes dice qué tipos de componentes hay que implementar y cuáles son las relaciones entre ellos
- Describe un acercamiento al diseño de sistemas como un conjunto de componentes que exponen interfaces bien definidas y de colaboración conjunta para la resolución de problemas.
- Las aplicaciones se diseñan a partir de componentes individuales.
- Los componentes se diseñan para diferentes entornos y contextos, se les debe pasar toda la  información, no deben contener ninguna información
- Cada componente cumple una función clara en el contexto de una arquitectura bien definida
- **Componente:** Unidades de software. Es un paquete de software o un módulo que encapsula un proceso específico, obteniendo unos resultados acordes con el proceso realizado.
- Cada cliente de un componente depende exclusivamente de la especificación del componente y no  de su implementación; lo cual es clave para reducir el acoplamiento.
- Componentes tiene asociadas interfaces que a su vez:
	- Describen el comportamiento del componente en función de un modelo de información.
	- Las dependencias entre componentes son dependencias de uso de interfaces, no directas sobre el componente.
- Pertenece al estilo [[Llamada y Retorno]]

Se encuentra regido por los siguientes principios:
- Unificación de datos y comportamiento
- Identidad
- Encapsulamiento
- Interfaces

Se tienen los siguientes beneficios:
- Facilidad de despliegue
- Reducción de los costos (Utilizar componentes de terceros)
- Reusabilidad por independencia de contexto
- Reducción de la complejidad
## ¿Cuándo se usa?

- Facilidad para conseguir esos componentes.
- Ejecución de aplicaciones con pocos o ningún dato de entrada.
- Combinación de componentes escritos en diferentes leguajes.
- Actualización de componentes de forma sencilla.
## ¿Cómo se representa?

Pasos para la obtención de componentes:
1. **Identificar componentes**
	1. Para cada caso de uso se define una interfaz.
	2. Para cada sistema externo que participa en la realización de un caso de uso se define una interfaz por relación.
2. **Interacción de componentes**
	1. Definir las interacciones entre los componentes indicando operaciones en las interfaces de los componentes de negocio y determinando las dependencias entre componentes.
3. **Especificación de componentes**
	1. Precondiciones/Postcondiciones
	2. Entradas/Salidas
	3. Relaciones
	4. Excepciones

#### Ejemplo de Representación de la Conferencia

 1. Sistema de Reserva  de habitaciones

	![[Pasted image 20240722214607.png]]

2. Identificación de componentes

	![[Pasted image 20240722214708.png]]

3.  Interacción de componentes

	![[Pasted image 20240722214755.png]]