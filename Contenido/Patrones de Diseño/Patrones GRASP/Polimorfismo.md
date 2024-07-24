## Descripción
- Otros nombres por los que se le conoce es `Polymorphism`
-   El patrón de diseño "Polimorfismo" es un principio de diseño orientado a objetos que permite que diferentes objetos respondan de manera diferente a la misma solicitud. Esto se logra mediante la implementación de interfaces o clases base con métodos que pueden ser sobrescritos por clases derivadas.

#### Problema
El problema que resuelve el patrón Polimorfismo es la necesidad de flexibilidad y extensibilidad en un sistema. Sin polimorfismo, cada vez que se necesita un comportamiento diferente para una operación, se tendría que escribir código específico para manejar cada caso, lo que resultaría en un código duplicado y difícil de mantener. El polimorfismo permite que diferentes objetos respondan de manera diferente a la misma solicitud, lo que facilita la adición de nuevos comportamientos sin modificar el código existente.

#### Solución
El objetivo principal del patrón Polimorfismo es permitir que objetos de diferentes clases puedan ser tratados de manera uniforme a través de una interfaz común. Esto promueve la flexibilidad, la extensibilidad y la reutilización del código.

#### Aplicaciones
El patrón Polimorfismo se utiliza en diversos sistemas de software, especialmente en aquellos que requieren una clara separación de responsabilidades y una fácil extensibilidad. Ejemplos incluyen sistemas empresariales, aplicaciones de gráficos, y cualquier sistema donde sea necesario tratar objetos de diferentes clases de manera uniforme.

## Estructura

#### Representación
``` mermaid
classDiagram
	class Circulo{
		+dibujar()
	}
	class Rectangulo{
		+dibujar()
	}
	class Figura{
		<<interface>>
		+dibujar()
	}

	Circulo ..> Figura
	Rectangulo ..> Figura
```
#### Participantes
- **Interfaz**: La interfaz o clase abstracta que define la operación.
- **ClaseA**: Una clase que implementa la interfaz y proporciona una implementación específica de la operación.
- **ClaseB**: Otra clase que implementa la interfaz y proporciona una implementación específica de la operación.
#### Principios de Diseño asociados
1. **Open/Close Principle ([[Open Close]])**: El patrón Polimorfismo facilita la extensión del sistema sin modificar el código existente. Por ejemplo, se pueden agregar nuevas clases que implementen una interfaz sin cambiar el código que utiliza esa interfaz.
2. **Liskov Substitution Principle ([[Sustitución de Liskov]])**: El patrón Polimorfismo promueve la sustitución de objetos de una jerarquía de clases sin alterar la corrección del programa. Esto ayuda a cumplir con el principio de que los objetos de una clase derivada deben poder ser utilizados en lugar de los objetos de la clase base sin problemas.
3. **Dependency Inversion Principle ([[Inversión de Dependencia]])**: El patrón Polimorfismo promueve la inversión de dependencias al depender de abstracciones (interfaces) en lugar de implementaciones concretas. Esto facilita la flexibilidad y la modularidad del sistema.
4. **Modularidad, cohesión y acoplamiento**: El patrón Polimorfismo promueve la modularidad al permitir que diferentes objetos implementen una interfaz, lo que reduce el acoplamiento entre componentes.
#### Consecuencias
#### Ventajas
- **Flexibilidad**: Permite tratar objetos de diferentes clases de manera uniforme.
- **Extensibilidad**: Facilita la adición de nuevas clases que implementen la interfaz.
- **Reutilización**: Los objetos pueden ser reutilizados en diferentes contextos.
#### Desventajas
- Puede introducir una capa adicional de complejidad si no se gestiona adecuadamente.
#### Patrones Relacionados
- **Patrón de Diseño [[Factory]]**: Para la creación de objetos.
- **Patrón de Diseño [[Strategy]]**: Para encapsular algoritmos y permitir su intercambio.
- **Patrón de Diseño Observer**: Para notificar cambios a otros objetos.
#### Código de ejemplo
``` java
public interface Figura{
	void dibujar();
}

public class Circulo implements Figura{
	@Override
	public void dibujar(){
		// Dibujar un circulo
	}
}

public class Rectangulo implements Figura{
	@Override
	public void dibujar(){
		// Dibujar un rectangulo
	}
}
```