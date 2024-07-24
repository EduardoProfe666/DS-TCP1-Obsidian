## Descripción
- Puede tener otros nombres como `Pure Fabrication`
- El patrón de diseño "Fábrica Pura" (Pure Fabrication) es un principio de diseño orientado a objetos que sugiere la creación de una clase completamente nueva cuya única responsabilidad es proporcionar un servicio que no está relacionado con un concepto del dominio del problema. Esta clase se crea específicamente para promover la alta cohesión y el bajo acoplamiento en el sistema.

#### Problema

El problema que resuelve el patrón Fábrica Pura es la necesidad de centralizar la lógica de negocio que no encaja naturalmente en ninguna de las clases del dominio del problema. Esto puede ser necesario para evitar la violación de principios de diseño como el Single Responsibility Principle (SRP) o para reducir el acoplamiento entre clases.
#### Solución
El objetivo principal del patrón Fabricación Pura es introducir una clase que no tiene una contraparte en el dominio del problema, pero que ayuda a mejorar la cohesión, reducir el acoplamiento y facilitar la reutilización del código. Esto promueve un diseño más limpio y mantenible.

#### Aplicaciones
El patrón Fabricación Pura se utiliza en diversos sistemas de software, especialmente en aquellos que requieren una clara separación de responsabilidades y un diseño flexible. Ejemplos incluyen sistemas empresariales, aplicaciones de gestión, y cualquier sistema donde sea necesario introducir clases adicionales para mejorar la estructura del sistema.

## Estructura

#### Representación
``` mermaid
classDiagram
	class ServicioNotificaciones
	class Usuario

	ServicioNotificaciones: +enviarNotificacion(String)
	Usuario: +Usuario(ServicioNotificaciones)
	Usuario: +realizarAccion()
	ServicioNotificaciones --o Usuario
```

#### Participantes
- **Servicio**: La clase que no representa un concepto del dominio del problema, pero que ayuda a mejorar la estructura del sistema.
#### Principios de Diseño asociados
1. **Single Responsibility Principle ([[Única Responsabilidad]])**: El patrón Fábrica Pura promueve la separación de responsabilidades al crear una clase completamente nueva cuya única responsabilidad es proporcionar un servicio específico. Esto ayuda a cumplir con el principio de que una clase debe tener una sola razón para cambiar.
2. **Open/Close Principle ([[Open Close]])**: El patrón Fábrica Pura facilita la extensión del sistema sin modificar el código existente. Por ejemplo, se pueden agregar nuevos servicios sin cambiar las clases del dominio del problema, siempre y cuando se sigan las interfaces definidas.
3. **[[Encapsular la variabilidad]]**: El patrón Fábrica Pura encapsula la lógica de negocio en una clase completamente nueva, lo que ayuda a minimizar el impacto de los cambios en el sistema.
4. **[[Una y solo una regla]]**: El patrón Fábrica Pura tiene una única responsabilidad: proporcionar un servicio específico que no está relacionado con un concepto del dominio del problema.
5. **[[Modularidad, cohesión y acoplamiento]]**: El patrón Fábrica Pura promueve la modularidad al crear una clase completamente nueva para proporcionar un servicio específico, lo que reduce el acoplamiento entre componentes.

#### Consecuencias
#### Ventajas
- **Mejora de la cohesión**: La clase puede agrupar responsabilidades relacionadas.
- **Reducción del acoplamiento**: La clase puede servir como intermediario entre otras clases.
- **Facilita la reutilización**: La clase puede ser reutilizada en diferentes contextos.
#### Desventajas
- Puede introducir una capa adicional de complejidad si no se gestiona adecuadamente.
#### Patrones Relacionados
- **Patrón de Diseño [[Singleton]]: Para asegurar que una clase tenga una única instancia.
- **Patrón de Diseño [[Factory Method]]**: Para la creación de objetos.
- **Patrón de Diseño [[Observer]]**: Para notificar cambios a otros objetos.
#### Código de ejemplo
``` java
public class ServicioNotificaciones{
	public void enviarNotificacion(string mensaje){
		// Enviar Notificacion
	}
}

public class Usuario{
	private ServicioNotificaciones servicioNotificaciones;

	public Usuario(ServicioNotificaciones servicioNotificaciones){
		this.servicioNotificaciones = servicioNotificaciones;
	}

	public void realizarAccion(){
		servicioNotificaciones.enviarNotificacion("Accion Realizada");
	}
}
```