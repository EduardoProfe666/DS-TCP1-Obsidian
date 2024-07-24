## Descripción
- Se le conoce también por `Chain of Command`  y `Cadena de responsabilidad`.
- Es un patrón `de comportamiento`
- En Refactoring Guru está [aquí](./RefactoringGuru/Chain-of-Responsibility.mhtml)

## Propósito

**Chain of Responsibility** es un patrón de diseño de comportamiento que te permite pasar solicitudes a lo largo de una cadena de manejadores. Al recibir una solicitud, cada manejador decide si la procesa o si la pasa al siguiente manejador de la cadena.

El objetivo principal del patrón Chain of Responsibility es desacoplar a los emisores de las solicitudes de sus receptores, permitiendo que múltiples objetos tengan la oportunidad de manejar la solicitud. Surgió como una solución para manejar solicitudes de manera flexible y dinámica, evitando la necesidad de conocer de antemano qué objeto es responsable de manejar una solicitud específica.
## ¿Cuándo aplicarlo?

- Utiliza el patrón Chain of Responsibility cuando tu programa deba procesar distintos tipos de solicitudes de varias maneras, pero los tipos exactos de solicitudes y sus secuencias no se conozcan de antemano.

 - El patrón te permite encadenar varios manejadores y, al recibir una solicitud, “preguntar” a cada manejador si puede procesarla. De esta forma todos los manejadores tienen la oportunidad de procesar la solicitud.

 - Utiliza el patrón cuando sea fundamental ejecutar varios manejadores en un orden específico.

 - Ya que puedes vincular los manejadores de la cadena en cualquier orden, todas las solicitudes recorrerán la cadena exactamente como planees.

 - Utiliza el patrón Chain of Responsibility cuando el grupo de manejadores y su orden deban cambiar durante el tiempo de ejecución.

 - Si aportas modificadores (_setters_) para un campo de referencia dentro de las clases manejadoras, podrás insertar, eliminar o reordenar los manejadores dinámicamente.
## Representación

![[Pasted image 20240723194537.png]]

1. La clase **Manejadora** declara la interfaz común a todos los manejadores concretos. Normalmente contiene un único método para manejar solicitudes, pero en ocasiones también puede contar con otro método para establecer el siguiente manejador de la cadena.
2. La clase **Manejadora Base** es opcional y es donde puedes colocar el código boilerplate (segmentos de código que suelen no alterarse) común para todas las clases manejadoras. Normalmente, esta clase define un campo para almacenar una referencia al siguiente manejador. Los clientes pueden crear una cadena pasando un manejador al constructor o modificador (_setter_) del manejador previo. La clase también puede implementar el comportamiento de gestión por defecto: puede pasar la ejecución al siguiente manejador después de comprobar su existencia.
3. Los **Manejadores Concretos** contienen el código para procesar las solicitudes. Al recibir una solicitud, cada manejador debe decidir si procesarla y, además, si la pasa a lo largo de la cadena. Habitualmente los manejadores son autónomos e inmutables, y aceptan toda la información necesaria únicamente a través del constructor.
4. El **Cliente** puede componer cadenas una sola vez o componerlas dinámicamente, dependiendo de la lógica de la aplicación. Observa que se puede enviar una solicitud a cualquier manejador de la cadena; no tiene por qué ser al primero.
    
## Participantes

1.     **Handler:** Define una interfaz para manejar las solicitudes y opcionalmente implementa el siguiente enlace en la cadena.

2.     **ConcreteHandler:** Maneja las solicitudes para las que es responsable y tiene la opción de pasar la solicitud al siguiente manejador en la cadena.

3.     **Client:** Inicia la solicitud a un objeto ConcreteHandler en la cadena.
## Principios de diseño relacionados

- _Principio de responsabilidad única_. Puedes desacoplar las clases que invoquen operaciones de las que realicen operaciones.
-  _Principio de abierto/cerrado_. Puedes introducir nuevos manejadores en la aplicación sin descomponer el código cliente existente.

## Ventajas

-  Puedes controlar el orden de control de solicitudes.
-  Reduce el acoplamiento entre emisores y receptores de solicitudes.
- Promueve la flexibilidad y la reutilización de código.
- Permite agregar o cambiar responsabilidades a objetos individuales sin afectar a otros objetos.
## Desventajas

 - Algunas solicitudes pueden acabar sin ser gestionadas.
## Código
``` pascal
// La interfaz manejadora declara un método para ejecutar una
// solicitud.
interface ComponentWithContextualHelp is
    method showHelp()

// La clase base para componentes simples.
abstract class Component implements ComponentWithContextualHelp is
    field tooltipText: string

    // El contenedor del componente actúa como el siguiente
    // eslabón de la cadena de manejadores.
    protected field container: Container

    // El componente muestra una pista si tiene un texto de
    // ayuda asignado. De lo contrario, reenvía la llamada al
    // contenedor, si es que existe.
    method showHelp() is
        if (tooltipText != null)
            // Muestra la pista.
        else
            container.showHelp()

// Los contenedores pueden contener componentes simples y otros
// contenedores como hijos. Las relaciones de la cadena se
// establecen aquí. La clase hereda el comportamiento showHelp
// (mostrarAyuda) de su padre.
abstract class Container extends Component is
    protected field children: array of Component

    method add(child) is
        children.add(child)
        child.container = this

// Los componentes primitivos pueden estar bien con la
// implementación de la ayuda por defecto...
class Button extends Component is
    // ...

// Pero los componentes complejos pueden sobrescribir la
// implementación por defecto. Si no puede proporcionarse el
// texto de ayuda de una nueva forma, el componente siempre
// puede invocar la implementación base (véase la clase
// Componente).
class Panel extends Container is
    field modalHelpText: string

    method showHelp() is
        if (modalHelpText != null)
            // Muestra una ventana modal con el texto de ayuda.
        else
            super.showHelp()

// ...igual que arriba...
class Dialog extends Container is
    field wikiPageURL: string

    method showHelp() is
        if (wikiPageURL != null)
            // Abre la página de ayuda wiki.
        else
            super.showHelp()

// Código cliente.
class Application is
    // Cada aplicación configura la cadena de forma diferente.
    method createUI() is
        dialog = new Dialog("Budget Reports")
        dialog.wikiPageURL = "http://..."
        panel = new Panel(0, 0, 400, 800)
        panel.modalHelpText = "This panel does..."
        ok = new Button(250, 760, 50, 20, "OK")
        ok.tooltipText = "This is an OK button that..."
        cancel = new Button(320, 760, 50, 20, "Cancel")
        // ...
        panel.add(ok)
        panel.add(cancel)
        dialog.add(panel)

    // Imagina lo que pasa aquí.
    method onF1KeyPress() is
        component = this.getComponentAtMouseCoords()
        component.showHelp()
```