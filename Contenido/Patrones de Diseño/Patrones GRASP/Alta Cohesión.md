## Descripción
- Puede tener otros nombres como `Alta Cohesión` y `High Cohesion`
- El patrón de diseño de "alta cohesión" se refiere a la idea de que las responsabilidades de un módulo o clase deben estar estrechamente relacionadas y enfocadas en una sola tarea o funcionalidad. Esto promueve la claridad, la mantenibilidad y la reusabilidad del código.
#### Problema

El problema que resuelve la alta cohesión es la dispersión de responsabilidades en una clase o módulo, lo que puede llevar a un código confuso, difícil de mantener y de testear. Cuando una clase tiene múltiples responsabilidades, cualquier cambio en una de ellas puede afectar a otras, aumentando la complejidad y la probabilidad de errores.
#### Solución
- El objetivo principal del patrón Alta Cohesión es diseñar clases o módulos de tal manera que sus responsabilidades estén estrechamente relacionadas y enfocadas. Esto promueve la claridad, la mantenibilidad y la reutilización del código.
#### Aplicaciones

El patrón Alta Cohesión se utiliza en diversos sistemas de software, especialmente en aquellos que requieren una clara asignación de responsabilidades y un enfoque modular. Ejemplos incluyen sistemas empresariales, aplicaciones de gestión, y cualquier sistema donde sea necesario mantener las responsabilidades de una clase o módulo bien definidas.
## Estructura

#### Representación
``` mermaid
classDiagram 
	class GestorTareas 
	GestorTareas : +agregarTarea(String tarea) 
	GestorTareas : +eliminarTarea(String tarea) 
	GestorTareas : +listarTareas()
```

#### Participantes
- **Componente**: Una clase o módulo con responsabilidades estrechamente relacionadas.

#### Principios de Diseño asociados

1. **Single Responsibility Principle ([[Única Responsabilidad]])**: Una clase debe tener una sola razón para cambiar, es decir, debe tener solo una responsabilidad.
2. **[[Encapsular la variabilidad]]**: Encapsular los aspectos que varían en un diseño ayuda a minimizar el impacto de los cambios.
3. **[[Una y solo una regla]]**: Este principio sugiere que cada regla o responsabilidad debe estar en un solo lugar.
4. **[[Modularidad, cohesión y acoplamiento]]**: La alta cohesión está directamente relacionada con la modularidad y el bajo acoplamiento, ya que promueve la separación clara de responsabilidades y la independencia entre módulos.
#### Consecuencias
#### Ventajas
- **Claridad**: Las responsabilidades de una clase o módulo están bien definidas y fáciles de entender.
- **Mantenibilidad**: Cambios en una parte del sistema tienen menos impacto en otras partes.
- **Reutilización**: Los componentes cohesivos pueden ser reutilizados en diferentes contextos.

#### Desventajas
- Puede requerir un diseño más cuidadoso y una mayor inversión inicial.

#### Patrones Relacionados
- **Patrón de Diseño [[Singleton]]**: Para asegurar que una clase tenga una única instancia.
- **Patrón de Diseño [[Factory Method]]**: Para la creación de objetos.
- **Patrón de Diseño [[Observer]]**: Para notificar cambios a otros objetos.

#### Código de ejemplo

``` java
public class GestorTareas{
	public void agregarTarea(String tarea){
		// Agregar Tarea
	}

	public void eliminarTarea(String tarea){
		// Eliminar Tarea
	}

	public void listarTareas(){
		// Listar tareas
	}
}
```