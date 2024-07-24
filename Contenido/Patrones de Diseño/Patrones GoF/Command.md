## Descripción
- Se le conoce también por `Comando`, `Action`, `Transaction`  y `Orden`.
- Es un patrón `de comportamiento`
- En Refactoring Guru está [aquí](./RefactoringGuru/Command.mhtml)

## Propósito

**Command** es un patrón de diseño de comportamiento que convierte una solicitud en un objeto independiente que contiene toda la información sobre la solicitud. Esta transformación te permite parametrizar los métodos con diferentes solicitudes, retrasar o poner en cola la ejecución de una solicitud y soportar operaciones que no se pueden realizar.

El objetivo principal del patrón Command es encapsular una solicitud en un objeto, permitiendo así que los clientes puedan parametrizar diferentes solicitudes, encolar solicitudes, registrarlas y soportar operaciones que pueden ser deshechas. Surgió como una solución para desacoplar el objeto que invoca la operación del que sabe cómo realizarla.

## ¿Cuándo aplicarlo?

- Utiliza el patrón Command cuando quieras parametrizar objetos con operaciones.

 - El patrón Command puede convertir una llamada a un método específico en un objeto autónomo. Este cambio abre la puerta a muchos usos interesantes: puedes pasar comandos como argumentos de método, almacenarlos dentro de otros objetos, cambiar comandos vinculados durante el tiempo de ejecución, etc.

- Aquí tienes un ejemplo: estás desarrollando un componente GUI, como un menú contextual, y quieres que los usuarios puedan configurar opciones del menú que activen operaciones cuando un usuario final haga clic sobre ellos.

 - Utiliza el patrón Command cuando quieras poner operaciones en cola, programar su ejecución, o ejecutarlas de forma remota.

 - Como pasa con cualquier otro objeto, un comando se pueden serializar, lo cual implica convertirlo en una cadena que pueda escribirse fácilmente a un archivo o una base de datos. Más tarde, la cadena puede restaurarse como el objeto de comando inicial. De este modo, puedes retardar y programar la ejecución del comando. ¡Pero aún hay más! Del mismo modo, puedes poner comandos en cola, así como registrarlos o enviarlos por la red.

 - Utiliza el patrón Command cuando quieras implementar operaciones reversibles.

 - Aunque hay muchas formas de implementar deshacer/rehacer, el patrón Command es quizá la más popular de todas.

- Para poder revertir operaciones, debes implementar el historial de las operaciones realizadas. El historial de comando es una pila que contiene todos los objetos de comando ejecutados junto a copias de seguridad relacionadas del estado de la aplicación.

- Este método tiene dos desventajas. Primero, no es tan fácil guardar el estado de una aplicación, porque parte de ella puede ser privada. Este problema puede mitigarse con el patrón Memento.

- Segundo, las copias de seguridad de estado pueden consumir mucha memoria RAM. Por lo tanto, en ocasiones puedes recurrir a una implementación alternativa: en lugar de restaurar el estado pasado, el comando realiza la operación inversa, aunque ésta también tiene un precio, ya que puede resultar difícil o incluso imposible de implementar.
## Representación

![[Pasted image 20240723193913.png]]
1. La clase **Emisora** (o _invocadora_) es responsable de inicializar las solicitudes. Esta clase debe tener un campo para almacenar una referencia a un objeto de comando. El emisor activa este comando en lugar de enviar la solicitud directamente al receptor. Ten en cuenta que el emisor no es responsable de crear el objeto de comando. Normalmente, obtiene un comando precreado de parte del cliente a través del constructor.
2. La interfaz **Comando** normalmente declara un único método para ejecutar el comando.
3. Los **Comandos Concretos** implementan varios tipos de solicitudes. Un comando concreto no se supone que tenga que realizar el trabajo por su cuenta, sino pasar la llamada a uno de los objetos de la lógica de negocio. Sin embargo, para lograr simplificar el código, estas clases se pueden fusionar. Los parámetros necesarios para ejecutar un método en un objeto receptor pueden declararse como campos en el comando concreto. Puedes hacer inmutables los objetos de comando permitiendo la inicialización de estos campos únicamente a través del constructor.
4. La clase **Receptora** contiene cierta lógica de negocio. Casi cualquier objeto puede actuar como receptor. La mayoría de los comandos solo gestiona los detalles sobre cómo se pasa una solicitud al receptor, mientras que el propio receptor hace el trabajo real.
5. El **Cliente** crea y configura los objetos de comando concretos. El cliente debe pasar todos los parámetros de la solicitud, incluyendo una instancia del receptor, dentro del constructor del comando. Después de eso, el comando resultante puede asociarse con uno o varios emisores.
## Participantes

1.     **Command:** Define una interfaz para ejecutar una operación.

2.     **ConcreteCommand:** Define una vinculación entre un objeto `Receiver` y una acción. Implementa `execute` llamando a la acción apropiada en el `Receiver`.

3.     **Client:** Crea un objeto `ConcreteCommand` y establece su `Receiver`.

4.     **Invoker:** Pide al `Command` que ejecute la solicitud.

5.     **Receiver:** Sabe cómo realizar las operaciones asociadas con la solicitud.
## Principios de diseño relacionados

- _Principio de responsabilidad única_. Puedes desacoplar las clases que invocan operaciones de las que realizan esas operaciones.
-  _Principio de abierto/cerrado_. Puedes introducir nuevos comandos en la aplicación sin descomponer el código cliente existente.

## Ventajas

- Desacopla el objeto que invoca la operación del que sabe cómo realizarla.
- Permite la creación de comandos complejos y compuestos.
- Soporta operaciones que pueden ser deshechas.
- Puedes implementar deshacer/rehacer.
- Puedes implementar la ejecución diferida de operaciones.
- Puedes ensamblar un grupo de comandos simples para crear uno complejo.

## Desventajas

- Puede llevar a un aumento en el número de clases y objetos en el sistema.
- El código puede complicarse, ya que estás introduciendo una nueva capa entre emisores y receptores.

## Código
``` pascal
// La clase base comando define la interfaz común a todos los
// comandos concretos.
abstract class Command is
    protected field app: Application
    protected field editor: Editor
    protected field backup: text

    constructor Command(app: Application, editor: Editor) is
        this.app = app
        this.editor = editor

    // Realiza una copia de seguridad del estado del editor.
    method saveBackup() is
        backup = editor.text

    // Restaura el estado del editor.
    method undo() is
        editor.text = backup

    // El método de ejecución se declara abstracto para forzar a
    // todos los comandos concretos a proporcionar sus propias
    // implementaciones. El método debe devolver verdadero o
    // falso dependiendo de si el comando cambia el estado del
    // editor.
    abstract method execute()

// Los comandos concretos van aquí.
class CopyCommand extends Command is
    // El comando copiar no se guarda en el historial ya que no
    // cambia el estado del editor.
    method execute() is
        app.clipboard = editor.getSelection()
        return false

class CutCommand extends Command is
    // El comando cortar no cambia el estado del editor, por lo
    // que debe guardarse en el historial. Y se guardará siempre
    // y cuando el método devuelva verdadero.
    method execute() is
        saveBackup()
        app.clipboard = editor.getSelection()
        editor.deleteSelection()
        return true

class PasteCommand extends Command is
    method execute() is
        saveBackup()
        editor.replaceSelection(app.clipboard)
        return true

// La operación deshacer también es un comando.
class UndoCommand extends Command is
    method execute() is
        app.undo()
        return false

// El historial global de comandos tan solo es una pila.
class CommandHistory is
    private field history: array of Command

    // El último dentro...
    method push(c: Command) is
        // Empuja el comando al final de la matriz del
        // historial.

    // ...el primero fuera.
    method pop():Command is
        // Obtiene el comando más reciente del historial.

// La clase editora tiene operaciones reales de edición de
// texto. Juega el papel de un receptor: todos los comandos
// acaban delegando la ejecución a los métodos del editor.
class Editor is
    field text: string

    method getSelection() is
        // Devuelve el texto seleccionado.

    method deleteSelection() is
        // Borra el texto seleccionado.

    method replaceSelection(text) is
        // Inserta los contenidos del portapapeles en la
        // posición actual.

// La clase Aplicación establece relaciones entre objetos. Actúa
// como un emisor: cuando algo debe hacerse, crea un objeto de
// comando y lo ejecuta.
class Application is
    field clipboard: string
    field editors: array of Editors
    field activeEditor: Editor
    field history: CommandHistory

    // El código que asigna comandos a objetos UI puede tener
    // este aspecto.
    method createUI() is
        // ...
        copy = function() { executeCommand(
            new CopyCommand(this, activeEditor)) }
        copyButton.setCommand(copy)
        shortcuts.onKeyPress("Ctrl+C", copy)

        cut = function() { executeCommand(
            new CutCommand(this, activeEditor)) }
        cutButton.setCommand(cut)
        shortcuts.onKeyPress("Ctrl+X", cut)

        paste = function() { executeCommand(
            new PasteCommand(this, activeEditor)) }
        pasteButton.setCommand(paste)
        shortcuts.onKeyPress("Ctrl+V", paste)

        undo = function() { executeCommand(
            new UndoCommand(this, activeEditor)) }
        undoButton.setCommand(undo)
        shortcuts.onKeyPress("Ctrl+Z", undo)

    // Ejecuta un comando y comprueba si debe añadirse al
    // historial.
    method executeCommand(command) is
        if (command.execute())
            history.push(command)

    // Toma el comando más reciente del historial y ejecuta su
    // método deshacer. Observa que no conocemos la clase de ese
    // comando. Pero no tenemos por qué, ya que el comando sabe
    // cómo deshacer su propia acción.
    method undo() is
        command = history.pop()
        if (command != null)
            command.undo()
```