## Descripción

Este principio establece dos reglas fundamentales:

·       Las clases de alto nivel no deberían depender de las clases de bajo nivel. Ambas deberían depender de abstracciones.

·       Las abstracciones no deberían depender de los detalles. Los detalles deberían depender de las abstracciones.

El objetivo del Principio de Inversión de Dependencias es reducir el acoplamiento entre las clases de alto nivel (aquellas que contienen la lógica de negocio) y las clases de bajo nivel (aquellas que realizan tareas específicas, como acceso a datos), haciendo que ambas dependan de abstracciones en lugar de depender directamente unas de otras. Esto se logra a través del uso de interfaces o clases abstractas que definen las operaciones que las clases de bajo nivel deben implementar, permitiendo así que las clases de alto nivel interactúen con estas abstracciones en lugar de con las implementaciones concretas.
## Ejemplo

Supongamos que tenemos una aplicación que guarda información de personas en una base de datos MySQL. Tradicionalmente, podríamos tener una clase `ServicePerson` que crea una instancia de una clase `MySQL` para guardar la información:

``` java
class MySQL {
	void save (Person person) {
		// Lógica para guardar en MySQL
	}
}

class ServicePerson {
	private MySQL mysql;

	ServicePerson() {
		this.mysql = new MySQL();
	}

	void savePerson(Person person) {
		mysql.save(person);
	}
}
```

Este diseño viola el Principio de Inversión de Dependencias porque `ServicePerson` (una clase de alto nivel) depende directamente de `MySQL` (una clase de bajo nivel). Si decidimos cambiar el sistema de almacenamiento a otro diferente a MySQL, tendríamos que modificar `ServicePerson`.

Para adherirse al DIP, creamos una interfaz `IPersistence` que abstrae la operación de guardar:

``` java
interface IPersistence {
	void save(Person person);
}

class MySQL implements IPersistence {
	@Override
	public void save (Person person) {
		// Lógica para guardar en MySQL
	}
}

class ServicePerson {
	private IPersistence persistence;

	ServicePerson(IPersistence persistence) {
		this.persistence = persistence;
	}

	void savePerson(Person person) {
		persistence.save(person);
	}
}
```

Ahora, `ServicePerson` depende de la abstracción `IPersistence` en lugar de la implementación concreta `MySQL`. Esto permite cambiar fácilmente el mecanismo de persistencia sin modificar `ServicePerson`, simplemente pasando una implementación diferente de `IPersistence` al constructor de `ServicePerson`.