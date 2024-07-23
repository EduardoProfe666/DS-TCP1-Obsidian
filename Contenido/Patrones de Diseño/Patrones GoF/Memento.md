## Descripción
- Se le conoce también por `Recuerdo`  y `Instantanea`.
- Es un patrón `de comportamiento`
- En Refactoring Guru está [aquí](./RefactoringGuru/Memento.mhtml)

## Propósito
**Memento** es un patrón de diseño de comportamiento que te permite guardar y restaurar el estado previo de un objeto sin revelar los detalles de su implementación.
El objetivo principal del patrón Memento es permitir la recuperación de un estado anterior de un objeto. Surgió como una solución para implementar operaciones de "deshacer" en sistemas, permitiendo que un objeto pueda volver a un estado anterior sin violar su encapsulación.

## ¿Cuándo aplicarlo?
- Utiliza el patrón Memento cuando quieras producir instantáneas del estado del objeto para poder restaurar un estado previo del objeto.
- El patrón Memento te permite realizar copias completas del estado de un objeto, incluyendo campos privados, y almacenarlos independientemente del objeto. Aunque la mayoría de la gente recuerda este patrón gracias al caso de la función Deshacer, también es indispensable a la hora de tratar con transacciones (por ejemplo, si debes volver atrás sobre un error en una operación).
- Utiliza el patrón cuando el acceso directo a los campos, consultores o modificadores del objeto viole su encapsulación.
- El Memento hace al propio objeto responsable de la creación de una instantánea de su estado. Ningún otro objeto puede leer la instantánea, lo que hace que los datos del estado del objeto original queden seguros.

## Representación

![[Pasted image 20240723174537.png]]
1. La clase **Originadora** puede producir instantáneas de su propio estado, así como restaurar su estado a partir de instantáneas cuando lo necesita.
2. El **Memento** es un objeto de valor que actúa como instantánea del estado del originador. Es práctica común hacer el memento inmutable y pasarle los datos solo una vez, a través del constructor.
3. La **Cuidadora** sabe no solo “cuándo” y “por qué” capturar el estado de la originadora, sino también cuándo debe restaurarse el estado. Una cuidadora puede rastrear el historial de la originadora almacenando una pila de mementos. Cuando la originadora deba retroceder en el historial, la cuidadora extraerá el memento de más arriba de la pila y lo pasará al método de restauración de la originadora.
4. En esta implementación, la clase memento se anida dentro de la originadora. Esto permite a la originadora acceder a los campos y métodos de la clase memento, aunque se declaren privados. Por otro lado, la cuidadora tiene un acceso muy limitado a los campos y métodos de la clase memento, lo que le permite almacenar mementos en una pila pero no alterar su estado.

## Participantes

- **Command:** Puede usarse junto con Memento para implementar operaciones que puedan ser deshechas.
- **Iterator:** Puede usarse para recorrer la historia de los `Memento`.
## Principios de diseño relacionados

1. **Principio de Responsabilidad Única ([[Única Responsabilidad]])**: El patrón Memento promueve el SRP al asignar la responsabilidad de guardar y restaurar el estado de un objeto a una clase separada (el Memento). Esto ayuda a mantener las clases enfocadas en una sola responsabilidad, lo que facilita la mantenibilidad y la reutilización del código.
2. **Inversión de Dependencias ([[Inversión de Dependencias]])**: El patrón Memento puede ser visto como una aplicación del DIP, ya que el objeto original (Originator) depende de una abstracción (el Memento) en lugar de una implementación concreta. Esto permite que el Originator sea independiente de cómo se almacena y gestiona el estado.
3. **Principio de Abierto/Cerrado ([[Open Close]])** : Aunque el patrón Memento no se centra directamente en el OCP, su uso puede promover este principio al permitir que las clases sean extendidas para soportar nuevas formas de gestión de estados sin modificar el código existente.

## Ventajas
- Preserva la encapsulación al evitar que otros objetos accedan directamente al estado interno del `Originator`.
- Facilita la implementación de operaciones de "deshacer" y "rehacer".
- Puedes producir instantáneas del estado del objeto sin violar su encapsulación.
- Puedes simplificar el código de la originadora permitiendo que la cuidadora mantenga el historial del estado de la originadora.

## Desventajas
- Puede consumir mucha memoria si se almacenan muchos estados en los `Memento`.
- Requiere una gestión cuidadosa de los `Memento` para evitar fugas de memoria.
- La aplicación puede consumir mucha memoria RAM si los clientes crean mementos muy a menudo.
-  Las cuidadoras deben rastrear el ciclo de vida de la originadora para poder destruir mementos obsoletos.
-  La mayoría de los lenguajes de programación dinámicos, como PHP, Python y JavaScript, no pueden garantizar que el estado dentro del memento se mantenga intacto.
## Código
``` pascal
// El originador contiene información importante que puede
// cambiar con el paso del tiempo. También define un método para
// guardar su estado dentro de un memento, y otro método para
// restaurar el estado a partir de él.
class Editor is
    private field text, curX, curY, selectionWidth

    method setText(text) is
        this.text = text

    method setCursor(x, y) is
        this.curX = x
        this.curY = y

    method setSelectionWidth(width) is
        this.selectionWidth = width

    // Guarda el estado actual dentro de un memento.
    method createSnapshot():Snapshot is
        // El memento es un objeto inmutable; ese es el motivo
        // por el que el originador pasa su estado a los
        // parámetros de su constructor.
        return new Snapshot(this, text, curX, curY, selectionWidth)

// La clase memento almacena el estado pasado del editor.
class Snapshot is
    private field editor: Editor
    private field text, curX, curY, selectionWidth

    constructor Snapshot(editor, text, curX, curY, selectionWidth) is
        this.editor = editor
        this.text = text
        this.curX = x
        this.curY = y
        this.selectionWidth = selectionWidth

    // En cierto punto, puede restaurarse un estado previo del
    // editor utilizando un objeto memento.
    method restore() is
        editor.setText(text)
        editor.setCursor(curX, curY)
        editor.setSelectionWidth(selectionWidth)

// Un objeto de comando puede actuar como cuidador. En este
// caso, el comando obtiene un memento justo antes de cambiar el
// estado del originador. Cuando se solicita deshacer, restaura
// el estado del originador a partir del memento.
class Command is
    private field backup: Snapshot

    method makeBackup() is
        backup = editor.createSnapshot()

    method undo() is
        if (backup != null)
            backup.restore()
    // ...
```