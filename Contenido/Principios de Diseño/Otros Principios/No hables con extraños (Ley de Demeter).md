## Descripción

Las piezas de código no deben revelar sus particularidades, y no deben interactuar con demasiadas otras “piezas”.

Dividir el código en “células” (clases, módulos, subsistemas) dependiendo de la complejidad, y mantener al mínimo posible las interacciones entre estas subdivisiones, de modo que, si una de ellas requiere ser sustituida o reparada, el número de afectaciones se mantenga bajo.

Las operaciones de una clase, solamente deberían efectuar llamadas a objetos que cumplan una de las 4 características siguientes:

1. **A  sí mismos.**
2. **A objetos pasados como argumento.**
3. **A objetos creados por ella.**
4. **A objetos con los cuales tiene relaciones directas.**

**Diseñar componentes tímidos (shy), que respetan la Ley de Demeter**, ayuda a obtener bajo acoplamiento.
## Ejemplo

Consideremos un sistema de gestión de empleados donde cada empleado tiene un jefe. Un enfoque que violaría la Ley de Demeter sería intentar obtener el nombre del jefe del jefe de un empleado, accediendo a propiedades anidadas de manera encadenada:

``` java
class Employee {
	private String name;
	private Employee manager;// Jefe del empleado
	public Employee(String name, Employee manager) {
		this.name = name;
		this.manager = manager;
	}
	
	public String getName() {
		return name;
	}

	public Employee getManager() {
		return manager;
	}
}

// Uso incorrecto que viola la Ley de Demeter
String bossName = employee.getManager().getManager().getName();
```

Este código viola la Ley de Demeter porque `Employee` está accediendo a la propiedad `Manager` de su `Manager`, lo cual es considerado hablar con un "extraño".

Para adherirse a la Ley de Demeter, podríamos refactorizar el código para que cada objeto solo interactúe con sus colaboradores directos. Una forma de hacerlo sería agregar un método en la clase `Employee` que encapsule la lógica de obtener el nombre del jefe del jefe:

``` java
class Employee {
	private String name;
	private Employee manager;// Jefe del empleado
	public Employee(String name, Employee manager) {
		this.name = name;
		this.manager = manager;
	}
	
	public String getName() {
		return name;
	}

	public Employee getManager() {
		return manager;
	}
	
	public String getBossName() {
		if (manager != null && manager.getManger() != null) {
			return manager.getManager().getName();
		}
		return "N/A";
	} 
}
// Uso correcto que respeta la Ley de Demeter
String bossName = employee.getBossName();
```
En este caso, `getBossName` encapsula la lógica de acceder al nombre del jefe del jefe, manteniendo la interacción dentro de los límites establecidos por la Ley de Demeter. Esto reduce el acoplamiento entre objetos y hace que el código sea más fácil de mantener y entender, ya que cada objeto solo interactúa con sus colaboradores directos.