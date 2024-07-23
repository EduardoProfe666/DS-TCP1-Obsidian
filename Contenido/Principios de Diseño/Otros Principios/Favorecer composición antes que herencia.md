## Descripción

La composición permite una mayor flexibilidad ya que facilita la modificación y extensión del comportamiento de los objetos en tiempo de ejecución, simplemente cambiando las instancias de los objetos contenidos.

El principio de diseño de software "Favorecer la composición antes que la herencia" sugiere que es preferible construir relaciones entre objetos mediante la composición de objetos más pequeños con comportamientos específicos, en lugar de utilizar la herencia para extender funcionalidades de una clase base o padre. Este enfoque promueve un diseño más flexible y mantenible, permitiendo reutilizar y combinar comportamientos de manera más efectiva sin estar atado a una jerarquía rígida de clases.
## Ejemplo

Consideremos un ejemplo clásico de modelado de vehículos. Un enfoque basado en herencia podría verse así:

``` java
class Vehicle{
	void move(){
		// Lógica para mover el vehículo
	}
}

class Car extends Vehicle {
	// Car hereda de Vehicle
}

class Bicycle extends Vehicle {
	// Bicycle hereda de Vehicle
}
```

Este enfoque puede volverse complicado si necesitamos modelar vehículos que combinan características de diferentes tipos, como un coche híbrido que tiene partes de un automóvil y partes de una bicicleta.

Un enfoque basado en composición sería diferente:

``` java
interface Movable{
	void move(){}
}

class Engine implements Movable {
	@Override
	public void move() {
		// Lógica para mover usando un motor
	}
}

class Pedals implements Movable {
	@Override
	public void move() {
		// Lógica para mover usando pedales
	}
}

class HybridCar {
	private Movable engine;
	private Movable pedals;
	public HybridCar(Movable engine, Movable pedals) {
	this.engine = engine;
	this.pedals = pedals; 
	} 
	
	public void move() {
		// Puede elegir moverse usando el motor o los pedales
		engine.move();
		// o
		pedals.move();
	}
}
```
En este caso, `HybridCar` utiliza composición para incluir tanto un `Engine` como `Pedals`, ambos implementando la interfaz `Movable`. Esto le da a `HybridCar` la capacidad de moverse de múltiples maneras sin necesidad de heredar de múltiples clases, lo cual no es posible en lenguajes como Java que no soportan herencia múltiple. Además, este diseño es más flexible y fácil de modificar o extender, ya que puedes cambiar cómo se mueve el `HybridCar` simplemente pasando diferentes implementaciones de `Movable` al constructor.