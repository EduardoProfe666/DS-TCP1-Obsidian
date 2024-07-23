## Descripción

•       El diseño debe quedar abierto para extensiones y cerrado para modificaciones.

•       Identificar los cambios probables y dejar puntos de extensión necesarios abiertos, mientras deja cerrada la solución para las modificaciones más probables.

•      Esto se logra generalmente mediante el uso de abstracciones y polimorfismo, permitiendo que nuevas funcionalidades se añadan mediante la creación de nuevas clases que extienden o implementan las abstracciones existentes, en lugar de modificar las clases ya existentes.
## Ejemplo

Consideremos un sistema de cálculo de áreas para diferentes formas geométricas. Sin aplicar el OCP, podríamos tener una función que calcule el área basándose en el tipo de forma:

``` java
public class AreaCalculator {
	public double calculateArea(Object shape) {
		if(shape instanceof Circle) {
			Circle circle = (Circle) shape;
			return Math.PI * circle.radius * circle.radius;
		} else if (shape instanceof Rectangle) {
			Rectangle rectangle = (Rectangle) shape;
			return rectangle.width * rectangle.height;
		}
		// Agregar más formas aquí requeriría modificar este método.
		throw new UnsupportedOperationException("Shape not supported");
	} 
}
```

Este enfoque viola el Principio de Abierto/Cerrado porque cada vez que queremos agregar una nueva forma geométrica, necesitamos modificar el método `calculateArea`.

Para adherirse al OCP, podemos definir una interfaz `Shape` con un método `area()` y hacer que todas las formas geométricas implementen esta interfaz:

```java
public class Shape {
	double area();
}

public class Circle implements Shape {
	private double radius;

	public Circle(double radius) {
		this.radius = radius;
	}
	@Override
	public double area() {
		return Math.PI * radius * radius;
	}
}

public class Rectangle implements Shape {
	private double width;
	private double height;

	public Rectangle(double width, double height) {
		this.width = width;
		this.height = height;
	}
	@Override
	public double area() {
		return width * height;
	}
}

public class AreaCalculator {
	public double calculateArea(Shape shape) {
		return shape.area(); // No necesita modificarse para nuevas formas.
	}

}
```

Con este diseño, podemos agregar tantas formas geométricas como queramos sin necesidad de modificar el código existente del `AreaCalculator`, cumpliendo así con el Principio de Abierto/Cerrado.