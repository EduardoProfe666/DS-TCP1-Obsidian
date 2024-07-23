## Descripción

- Puede tener otros nombres como `Bajo acoplamiento` y `Low coupling`
- El patrón de diseño de "Bajo Acoplamiento" se refiere a la idea de que los módulos o clases en un sistema deben estar lo menos interconectados posible. Esto significa que un cambio en un módulo no debería afectar significativamente a otros módulos. El bajo acoplamiento promueve la independencia y la flexibilidad en el diseño del software.
#### Problema
El problema que resuelve el bajo acoplamiento es la dependencia excesiva entre módulos o clases, lo que puede llevar a un sistema frágil y difícil de mantener. Cuando los módulos están altamente acoplados, un cambio en uno de ellos puede requerir cambios en muchos otros, aumentando la complejidad y la probabilidad de errores. El bajo acoplamiento facilita la modificación y la extensión del sistema sin afectar a otros componentes.

#### Solución

- El objetivo principal del patrón Bajo Acoplamiento es diseñar componentes o módulos de tal manera que su dependencia mutua sea mínima. Esto promueve la flexibilidad, la reutilización y la facilidad de mantenimiento del sistema.

#### Aplicaciones

El patrón Bajo Acoplamiento se utiliza en diversos sistemas de software, especialmente en aquellos que requieren una clara separación de responsabilidades y desacoplamiento. Ejemplos incluyen sistemas empresariales, aplicaciones distribuidas, y cualquier sistema donde sea necesario desacoplar componentes para facilitar cambios y evoluciones.
## Estructura

#### Representación
``` mermaid
classDiagram
	class ComponenteA
	class ComponenteB

	ComponenteA: +operacionA()
	ComponenteB: +operacionB()
```

#### Participantes
- **ComponenteA**: Una clase o módulo con baja dependencia de otros componentes.
- **ComponenteB**: Otra clase o módulo con baja dependencia de otros componentes.
#### Principios de Diseño asociados
1. **Single Responsibility Principle ([[Única Responsabilidad]])**: Una clase debe tener una sola razón para cambiar, es decir, debe tener solo una responsabilidad.
2. **Open/Close Principle ([[Open Close]])**: Las entidades de software (clases, módulos, funciones, etc.) deben estar abiertas para la extensión pero cerradas para la modificación.
3. **[[Modularidad, cohesión y acoplamiento]]**: El bajo acoplamiento está directamente relacionado con la modularidad y la alta cohesión, ya que promueve la separación clara de responsabilidades y la independencia entre módulos.

#### Consecuencias
#### Ventajas
- **Flexibilidad**: Facilita la modificación y evolución del sistema.

- **Reutilización**: Los componentes pueden ser reutilizados en diferentes contextos.

- **Mantenimiento y evolución facilitados**: Cambios en un componente tienen menos impacto en otros componentes.
#### Desventajas
- Puede requerir un diseño más cuidadoso y una mayor inversión inicial.
#### Usos Conocidos
El patrón Bajo Acoplamiento es utilizado en muchos frameworks y sistemas de software, incluyendo:
- ·**Java EE**: En la gestión de servicios y componentes.
- **Spring Framework**: En la inyección de dependencias y la gestión de beans.
- **.NET Framework**: En la gestión de servicios y componentes.
#### Patrones Relacionados
- **Patrón de Diseño [[Singleton]]**: Para asegurar que una clase tenga una única instancia.
- **Patrón de Diseño [[Factory Method]]**: Para la creación de objetos.
- **Patrón de Diseño [[Observer]]**: Para notificar cambios a otros objetos.
#### Código de ejemplo
``` java
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