## Descripción
- Se le conoce también por `Peso ligero`  y `Cache`.
- Es un patrón `estructural`
- En Refactoring Guru está [aquí](./RefactoringGuru/Flyweight.mhtml)

## Propósito
**Flyweight** es un patrón de diseño estructural que te permite mantener más objetos dentro de la cantidad disponible de RAM compartiendo las partes comunes del estado entre varios objetos en lugar de mantener toda la información en cada objeto.

## ¿Cuándo aplicarlo?

1. Divide los campos de una clase que se convertirá en flyweight en dos partes:
    - el estado intrínseco: los campos que contienen información invariable duplicada a través de varios objetos
    - el estado extrínseco: los campos que contienen información contextual única de cada objeto
2. Deja los campos que representan el estado intrínseco en la clase, pero asegúrate de que sean inmutables. Deben llevar sus valores iniciales únicamente dentro del constructor.
3. Repasa los métodos que utilizan campos del estado extrínseco. Para cada campo utilizado en el método, introduce un nuevo parámetro y utilízalo en lugar del campo.
4. Opcionalmente, crea una clase fábrica para gestionar el grupo de objetos flyweight, buscando uno existente antes de crear uno nuevo. Una vez que la fábrica esté en su sitio, los clientes sólo deberán solicitar objetos flyweight a través de ella. Deberán describir el flyweight deseado pasando su estado intrínseco a la fábrica.
5. El cliente deberá almacenar o calcular valores del estado extrínseco (contexto) para poder invocar métodos de objetos flyweight. Por comodidad, el estado extrínseco puede moverse a una clase contexto separada junto con el campo referenciador del flyweight.
## Representación

![[Pasted image 20240723191219.png]]

1. El patrón Flyweight es simplemente una optimización. Antes de aplicarlo, asegúrate de que tu programa tenga un problema de consumo de RAM provocado por tener una gran cantidad de objetos similares en la memoria al mismo tiempo. Asegúrate de que este problema no se pueda solucionar de otra forma sensata.
2. La clase **Flyweight** contiene la parte del estado del objeto original que pueden compartir varios objetos. El mismo objeto flyweight puede utilizarse en muchos contextos diferentes. El estado almacenado dentro de un objeto flyweight se denomina _intrínseco_, mientras que al que se pasa a sus métodos se le llama _extrínseco_.
3. La clase **Contexto** contiene el estado extrínseco, único en todos los objetos originales. Cuando un contexto se empareja con uno de los objetos flyweight, representa el estado completo del objeto original.
4. Normalmente, el comportamiento del objeto original permanece en la clase flyweight. En este caso, quien invoque un método del objeto flyweight debe también pasar las partes adecuadas del estado extrínseco dentro de los parámetros del método. Por otra parte, el comportamiento se puede mover a la clase de contexto, que utilizará el objeto flyweight vinculado como mero objeto de datos.
5. El **Cliente** calcula o almacena el estado extrínseco de los objetos flyweight. Desde la perspectiva del cliente, un flyweight es un objeto plantilla que puede configurarse durante el tiempo de ejecución pasando información contextual dentro de los parámetros de sus métodos.
6. La **Fábrica flyweight** gestiona un grupo de objetos flyweight existentes. Con la fábrica, los clientes no crean objetos flyweight directamente. En lugar de eso, invocan a la fábrica, pasándole partes del estado intrínseco del objeto flyweight deseado. La fábrica revisa objetos flyweight creados previamente y devuelve uno existente que coincida con los criterios de búsqueda, o bien crea uno nuevo si no encuentra nada.
## Participantes

- **Flyweight**: Define una interfaz a través de la cual los flyweights pueden recibir y actuar sobre el estado intrínseco.
- **ConcreteFlyweight**: Implementa la interfaz Flyweight y almacena el estado intrínseco.
- **UnsharedConcreteFlyweight**: No todos los Flyweight necesitan ser compartidos.
- **FlyweightFactory**: Crea y gestiona los objetos Flyweight. Asegura que los flyweights sean compartidos adecuadamente.
- **Client**: Mantiene referencias a los flyweights y calcula o almacena el estado extrínseco.
## Principios de diseño relacionados

1. **Principio de Responsabilidad Única ([[Única Responsabilidad]])**: El patrón Flyweight promueve el SRP al asignar la responsabilidad de gestionar los estados intrínsecos y extrínsecos a clases separadas. Esto ayuda a mantener las clases enfocadas en una sola responsabilidad, lo que facilita la mantenibilidad y la reutilización del código.
2. **Inversión de Dependencias ([[Inversión de Dependencias]])**: El patrón Flyweight puede ser visto como una aplicación del DIP, ya que el cliente que necesita utilizar los objetos flyweight depende de una abstracción (la fábrica de flyweights) en lugar de una implementación concreta. Esto permite que el cliente sea independiente de cómo se gestionan los objetos flyweight.
3. **Principio de Abierto/Cerrado ([[Open Close]])**: El patrón Flyweight promueve el OCP al permitir que las clases sean extendidas para soportar nuevos objetos flyweight sin modificar el código existente. Esto se logra mediante la introducción de nuevas clases que implementan los estados intrínsecos y extrínsecos.

## Ventajas

-  Puedes ahorrar mucha RAM, siempre que tu programa tenga toneladas de objetos similares.
## Desventajas

- Puede que estés cambiando RAM por ciclos CPU cuando deba calcularse de nuevo parte de la información de contexto cada vez que alguien invoque un método flyweight.
-  El código se complica mucho. Los nuevos miembros del equipo siempre estarán preguntándose por qué el estado de una entidad se separó de tal manera.
## Código
``` pascal
// La clase flyweight contiene una parte del estado de un árbol.
// Estos campos almacenan valores que son únicos para cada árbol
// en particular. Por ejemplo, aquí no encontrarás las
// coordenadas del árbol. Pero la textura y los colores que
// comparten muchos árboles sí están aquí. Ya que esta cantidad
// de datos suele ser GRANDE, dedicarás mucha memoria a
// mantenerla en cada objeto árbol. En lugar de eso, podemos
// extraer la textura, el color y otros datos repetidos y
// colocarlos en un objeto independiente que muchos objetos
// individuales del árbol pueden referenciar.
class TreeType is
    field name
    field color
    field texture
    constructor TreeType(name, color, texture) { ... }
    method draw(canvas, x, y) is
        // 1. Crea un mapa de bits de un tipo, color y textura
        // concretos.
        // 2. Dibuja el mapa de bits en el lienzo con las
        // coordenadas X y Y.

// La fábrica flyweight decide si reutiliza el flyweight
// existente o si crea un nuevo objeto.
class TreeFactory is
    static field treeTypes: collection of tree types
    static method getTreeType(name, color, texture) is
        type = treeTypes.find(name, color, texture)
        if (type == null)
            type = new TreeType(name, color, texture)
            treeTypes.add(type)
        return type

// El objeto contextual contiene la parte extrínseca del estado
// del árbol. Una aplicación puede crear millones de ellas, ya
// que son muy pequeñas: dos coordenadas en números enteros y un
// campo de referencia.
class Tree is
    field x,y
    field type: TreeType
    constructor Tree(x, y, type) { ... }
    method draw(canvas) is
        type.draw(canvas, this.x, this.y)

// Las clases Tree y Forest son los clientes de flyweight.
// Puedes fusionarlas si no tienes la intención de desarrollar
// más la clase Tree.
class Forest is
    field trees: collection of Trees

    method plantTree(x, y, name, color, texture) is
        type = TreeFactory.getTreeType(name, color, texture)
        tree = new Tree(x, y, type)
        trees.add(tree)

    method draw(canvas) is
        foreach (tree in trees) do
            tree.draw(canvas)
```