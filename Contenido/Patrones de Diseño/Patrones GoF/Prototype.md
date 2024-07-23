## Descripción
- Se le conoce también por `Prototipo`  y `Clone`.
- Es un patrón `creacional/estructural/de comportamiento`
- En Refactoring Guru está [aquí](./RefactoringGuru/Prototype.mhtml)

## Propósito
**Prototype** es un patrón de diseño creacional que nos permite copiar objetos existentes sin que el código dependa de sus clases.
El objetivo principal del patrón Prototype es reducir los costos de creación de objetos permitiendo la clonación de objetos existentes. Esto permite crear nuevos objetos copiando o clonando un prototipo existente, lo que puede ser más eficiente que crear un nuevo objeto desde cero.

## ¿Cuándo aplicarlo?

- Utiliza el patrón Prototype cuando tu código no deba depender de las clases concretas de objetos que necesites copiar.
- Esto sucede a menudo cuando tu código funciona con objetos pasados por código de terceras personas a través de una interfaz. Las clases concretas de estos objetos son desconocidas y no podrías depender de ellas aunque quisieras.
- El patrón Prototype proporciona al código cliente una interfaz general para trabajar con todos los objetos que soportan la clonación. Esta interfaz hace que el código cliente sea independiente de las clases concretas de los objetos que clona.
- Utiliza el patrón cuando quieras reducir la cantidad de subclases que solo se diferencian en la forma en que inicializan sus respectivos objetos. Puede ser que alguien haya creado estas subclases para poder crear objetos con una configuración específica.
- El patrón Prototype te permite utilizar como prototipos un grupo de objetos prefabricados, configurados de maneras diferentes.
- En lugar de instanciar una subclase que coincida con una configuración, el cliente puede, sencillamente, buscar el prototipo adecuado y clonarlo.
## Representación

![[Pasted image 20240723180856.png]]

1. La interfaz **Prototipo** declara los métodos de clonación. En la mayoría de los casos, se trata de un único método `clonar`.
2. La clase **Prototipo Concreto** implementa el método de clonación. Además de copiar la información del objeto original al clon, este método también puede gestionar algunos casos extremos del proceso de clonación, como, por ejemplo, clonar objetos vinculados, deshacer dependencias recursivas, etc.
3. El **Cliente** puede producir una copia de cualquier objeto que siga la interfaz del prototipo.
## Participantes
- **Prototype**: Define una interfaz para clonarse a sí mismo.
- **ConcretePrototype**: Implementa la operación de clonación.
- **Client**: Crea nuevos objetos solicitando a un prototipo que se clone.

## Principios de diseño relacionados

1. **Principio de Responsabilidad Única ([[Única Responsabilidad]])**: El patrón Prototype promueve el SRP al asignar la responsabilidad de la creación de objetos a la propia clase que representa el objeto. Esto ayuda a mantener las clases enfocadas en una sola responsabilidad, lo que facilita la mantenibilidad y la reutilización del código.
2. **Desacoplamiento ([[Bajo Acoplamiento]])**: El patrón Prototype ayuda a desacoplar el proceso de creación de objetos del código que utiliza esos objetos. Esto facilita la modificación del proceso de creación sin afectar el código que depende de los objetos.
3. **Principio de Abierto/Cerrado ([[Open Close]])**: El patrón Prototype promueve el OCP al permitir que las clases sean extendidas para soportar nuevos tipos de objetos sin modificar el código existente. Esto se logra mediante la clonación de prototipos existentes.

## Ventajas

- Puedes clonar objetos sin acoplarlos a sus clases concretas.
- Puedes evitar un código de inicialización repetido clonando prototipos prefabricados.
- Puedes crear objetos complejos con más facilidad.
- Obtienes una alternativa a la herencia al tratar con preajustes de configuración para objetos complejos.
- Reduce la necesidad de crear subclases para tipos de objetos similares.
- Permite la creación de objetos complejos de manera más eficiente.
- Proporciona flexibilidad para agregar o eliminar productos en tiempo de ejecución.
## Desventajas

- Clonar objetos complejos con referencias circulares puede resultar complicado.
- La implementación de la clonación puede ser compleja, especialmente si los objetos contienen referencias circulares.
## Código
``` pascal
// Prototipo base.
abstract class Shape is
    field X: int
    field Y: int
    field color: string

    // Un constructor normal.
    constructor Shape() is
        // ...

    // El constructor prototipo. Un nuevo objeto se inicializa
    // con valores del objeto existente.
    constructor Shape(source: Shape) is
        this()
        this.X = source.X
        this.Y = source.Y
        this.color = source.color

    // La operación clonar devuelve una de las subclases de
    // Shape (Forma).
    abstract method clone():Shape

// Prototipo concreto. El método de clonación crea un nuevo
// objeto y lo pasa al constructor. Hasta que el constructor
// termina, tiene una referencia a un nuevo clon. De este modo
// nadie tiene acceso a un clon a medio terminar. Esto garantiza
// la consistencia del resultado de la clonación.
class Rectangle extends Shape is
    field width: int
    field height: int

    constructor Rectangle(source: Rectangle) is
        // Para copiar campos privados definidos en la clase
        // padre es necesaria una llamada a un constructor
        // padre.
        super(source)
        this.width = source.width
        this.height = source.height

    method clone():Shape is
        return new Rectangle(this)

class Circle extends Shape is
    field radius: int

    constructor Circle(source: Circle) is
        super(source)
        this.radius = source.radius

    method clone():Shape is
        return new Circle(this)

// En alguna parte del código cliente.
class Application is
    field shapes: array of Shape

    constructor Application() is
        Circle circle = new Circle()
        circle.X = 10
        circle.Y = 10
        circle.radius = 20
        shapes.add(circle)

        Circle anotherCircle = circle.clone()
        shapes.add(anotherCircle)
        // La variable `anotherCircle` (otroCírculo) contiene
        // una copia exacta del objeto `circle`.

        Rectangle rectangle = new Rectangle()
        rectangle.width = 10
        rectangle.height = 20
        shapes.add(rectangle)

    method businessLogic() is
        // Prototype es genial porque te permite producir una
        // copia de un objeto sin conocer nada de su tipo.
        Array shapesCopy = new Array of Shapes.

        // Por ejemplo, no conocemos los elementos exactos de la
        // matriz de formas. Lo único que sabemos es que son
        // todas formas. Pero, gracias al polimorfismo, cuando
        // invocamos el método `clonar` en una forma, el
        // programa comprueba su clase real y ejecuta el método
        // de clonación adecuado definido en dicha clase. Por
        // eso obtenemos los clones adecuados en lugar de un
        // grupo de simples objetos Shape.
        foreach (s in shapes) do
            shapesCopy.add(s.clone())

        // La matriz `shapesCopy` contiene copias exactas del
        // hijo de la matriz `shape`.
```