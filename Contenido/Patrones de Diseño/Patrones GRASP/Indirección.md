## Descripción
- Otros nombres por los que se le conoce es `Indirection`
- El patrón de diseño "Indirección" (Indirection) es un principio de diseño orientado a objetos que sugiere la introducción de un objeto intermedio para desacoplar dos o más objetos que de otra manera estarían directamente acoplados. Este objeto intermedio actúa como un intermediario que facilita la comunicación y la colaboración entre los objetos.

#### Problema

El problema que resuelve el patrón Indirección es el acoplamiento directo entre objetos en un sistema. Cuando dos objetos están directamente acoplados, un cambio en uno de ellos puede requerir cambios en el otro, lo que aumenta la complejidad y la fragilidad del sistema. El patrón Indirección introduce un objeto intermedio que actúa como un intermediario, lo que reduce el acoplamiento y facilita la modificación y la extensión del sistema.
#### Solución

El objetivo principal del patrón Indirección es introducir un intermediario entre dos componentes o sistemas para reducir su acoplamiento directo. Esto promueve la flexibilidad, la modularidad y la facilidad de mantenimiento del sistema.

#### Aplicaciones
El patrón Indirección se utiliza en diversos sistemas de software, especialmente en aquellos que requieren una clara separación de componentes y desacoplamiento. Ejemplos incluyen sistemas empresariales, aplicaciones distribuidas, y cualquier sistema donde sea necesario desacoplar componentes para facilitar cambios y evoluciones.

## Estructura
``` mermaid
classDiagram
	class Intermediario
	class ComponenteA
	class ComponenteB

	ComponenteA: +operacionA()
	ComponenteB: +operacionB()
	Intermediario: +Intermediario(ComponenteA, ComponenteB)
	Intermediario: +operacion()

	ComponenteA --o Intermediario
	ComponenteB --o Intermediario
```

#### Representación
#### Participantes
- **Intermediario**: La clase que actúa como intermediario entre dos componentes o sistemas.

#### Principios de Diseño asociados
1. **Single Responsibility Principle ([[Única Responsabilidad]])**: El patrón Indirección promueve la separación de responsabilidades al introducir un objeto intermedio cuya única responsabilidad es facilitar la comunicación entre otros objetos. Esto ayuda a cumplir con el principio de que una clase debe tener una sola razón para cambiar.
2. **Dependency Inversion Principle ([[Inversión de Dependencia]])**: El patrón Indirección promueve la inversión de dependencias al introducir un objeto intermedio que depende de abstracciones (interfaces) en lugar de implementaciones concretas. Esto facilita la flexibilidad y la modularidad del sistema.
3. **[[Diseñar hacia las interfaces, no hacia las implementaciones]]**: El patrón Indirección se diseña para interactuar con interfaces en lugar de implementaciones concretas, lo que promueve la flexibilidad y la modularidad del sistema.
4. **[[Una y solo una regla]]**: El patrón Indirección tiene una única responsabilidad: facilitar la comunicación entre otros objetos.
5. **[[Modularidad, cohesión y acoplamiento]]**: El patrón Indirección promueve la modularidad al introducir un objeto intermedio que reduce el acoplamiento entre objetos y facilita la colaboración entre ellos.

#### Consecuencias
#### Ventajas
- **Desacoplamiento**: Reduce el acoplamiento directo entre componentes.
- **Flexibilidad**: Facilita la modificación y evolución del sistema.
- **Mantenimiento y evolución facilitados**: Cambios en un componente tienen menos impacto en otros componentes.
#### Desventajas
- Puede introducir una capa adicional de complejidad si no se gestiona adecuadamente.
#### Patrones Relacionados
- **Patrón de Diseño [[Proxy]]**: Para proporcionar un intermediario para otro objeto.
- **Patrón de Diseño [[Mediator]]**: Para definir un objeto que encapsula cómo interactúan un conjunto de objetos.
- **Patrón de Diseño [[Adapter]]**: Para convertir la interfaz de una clase en otra interfaz que los clientes esperan.
#### Código de ejemplo
``` java
public class Intermediario{
	private ComponenteA componenteA;
	private ComponenteB componenteB;

	public Intermediario(ComponenteA componenteA, ComponenteB componenteB){
		this.componenteA = componenteA;
		this.componenteB = componenteB;
	}

	public void operacion(){
		componenteA.operacionA();
		componenteB.operacionB();
	}
}

public class ComponenteA{
	public void operacionA(){
		// Operacion A
	}
}

public class ComponenteB{
	public void operacionB(){
		// Operacion B
	}
}
```