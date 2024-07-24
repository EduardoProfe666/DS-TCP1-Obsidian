## Descripción
- Puede tener otros nombres como `Controlador` y `Controller`
- El patrón de diseño "Creador" (Creator) es un patrón de diseño de comportamiento que se utiliza para delegar la responsabilidad de la creación de objetos a una clase específica. Este patrón se centra en quién debe ser el responsable de crear instancias de una clase determinada.
#### Problema
- ¿Quién debería ser el  responsable de crear una nueva instancia de una nueva clase?
- El problema que resuelve el patrón Creador es la delegación adecuada de la responsabilidad de la creación de objetos. En un sistema complejo, la creación de objetos puede ser una tarea complicada y puede requerir conocimiento específico o dependencias adicionales. El patrón Creador ayuda a centralizar esta responsabilidad en una clase adecuada, lo que facilita la gestión y el mantenimiento del sistema.

#### Solución
El objetivo principal del patrón Creador es asignar la responsabilidad de la creación de objetos a la clase que tiene la información necesaria para hacerlo de manera eficiente y coherente. Esto promueve la cohesión y reduce el acoplamiento, facilitando así el mantenimiento y la evolución del sistema.

Asignarle a la clase B la responsabilidad de crear una instancia de la clase A en uno de los casos siguientes:
- B agrega los objetos de A
- B contiene los objetos de A
- B registra las instancias de los objetos de A
- B utiliza específicamente los objetos de A
- B utiliza los datos de inicialización que serán trasmitidos a A cuando este objeto sea creado
#### Aplicaciones
El patrón Creador se utiliza en diversos sistemas de software, especialmente en aquellos que requieren una clara asignación de responsabilidades de creación de objetos. Ejemplos incluyen sistemas empresariales, aplicaciones de gestión, y cualquier sistema donde la creación de objetos esté estrechamente relacionada con la lógica de negocio.

## Estructura

#### Representación
``` mermaid
classDiagram
	class Creador
	class Objeto

	Creador: +crearObjeto() Objeto
	Objeto: +operacion()
	Objeto --> Creador
```

#### Participantes
- **Creador**: La clase que tiene la responsabilidad de crear instancias de otra clase.
#### Principios de Diseño asociados
1. **Single Responsibility Principle ([[Única Responsabilidad]])**: El patrón Creador promueve la separación de responsabilidades al delegar la creación de objetos a una clase específica, lo que ayuda a cumplir con el principio de que una clase debe tener una sola razón para cambiar.
2. **Open/Close Principle ([[Open Close]])**: El patrón Creador facilita la extensión del sistema sin modificar el código existente. Por ejemplo, se pueden agregar nuevos tipos de objetos sin cambiar las clases que los utilizan, siempre y cuando se sigan las interfaces definidas.
3. **[[Encapsular la variabilidad]]**: El patrón Creador encapsula la lógica de creación de objetos, lo que ayuda a minimizar el impacto de los cambios en el sistema.
4. **[[Modularidad, cohesión y acoplamiento]]**: El patrón Creador promueve la modularidad al centralizar la lógica de creación de objetos y reducir el acoplamiento entre componentes.
#### Consecuencias
#### Ventajas
- **Cohesión alta**: Las clases tienen responsabilidades claras y bien definidas.
- **Acoplamiento bajo**: Reduce la dependencia entre clases.
- **Mantenimiento y evolución facilitados**: Cambios en la creación de objetos tienen menos impacto en otras partes del sistema.
#### Desventajas
- Puede llevar a la creación de muchas clases pequeñas, lo que puede complicar la estructura del sistema si no se gestiona adecuadamente.
#### Patrones Relacionados
- **Patrón de Diseño [[Singleton]]**: Para asegurar que una clase tenga una única instancia.
- **Patrón de Diseño [[Factory Method]]**: Para la creación de objetos mediante un método de fábrica.
- **Patrón de Diseño [[Abstract Factory]]**: Para la creación de familias de objetos relacionados.
#### Código de ejemplo
``` java
public class Creador{
	public Objeto crearObjeto(){
		return new Objeto();
	}
}

public class Objeto{
	public void operacion(){
		// Realizar Operacion
	}
}
```