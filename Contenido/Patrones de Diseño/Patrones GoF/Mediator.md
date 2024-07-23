## Descripción
- Se le conoce también por `Mediador`, `Intermediary`, `Controller`.
- Es un patrón `de comportamiento`
- En Refactoring Guru está [aquí](./RefactoringGuru/Mediator.mhtml)

## Propósito
**Mediator** es un patrón de diseño de comportamiento que te permite reducir las dependencias caóticas entre objetos. El patrón restringe las comunicaciones directas entre los objetos, forzándolos a colaborar únicamente a través de un objeto mediador.

## ¿Cuándo aplicarlo?
- Utiliza el patrón Mediator cuando resulte difícil cambiar algunas de las clases porque están fuertemente acopladas a un puñado de otras clases.
 - El patrón te permite extraer todas las relaciones entre clases dentro de una clase separada, aislando cualquier cambio en un componente específico, del resto de los componentes.
 - Utiliza el patrón cuando no puedas reutilizar un componente en un programa diferente porque sea demasiado dependiente de otros componentes.
 - Una vez aplicado el patrón Mediator, los componentes individuales no conocen los otros componentes. Todavía pueden comunicarse entre sí, aunque indirectamente, a través del objeto mediador. Para reutilizar un componente en una aplicación diferente, debes darle una nueva clase mediadora.
 - Utiliza el patrón Mediator cuando te encuentres creando cientos de subclases de componente sólo para reutilizar un comportamiento básico en varios contextos.
 - Debido a que todas las relaciones entre componentes están contenidas dentro del mediador, resulta fácil definir formas totalmente nuevas de colaboración entre estos componentes introduciendo nuevas clases mediadoras, sin tener que cambiar los propios componentes.

## Representación

![[Pasted image 20240723160609.png]]

1. Los **Componentes** son varias clases que contienen cierta lógica de negocio. Cada componente tiene una referencia a una interfaz mediadora, declarada con su tipo. El componente no conoce la clase de la interfaz mediadora, por lo que puedes reutilizarlo en otros programas vinculándolo a una mediadora diferente.
2. La interfaz **Mediadora** declara métodos de comunicación con los componentes, que normalmente incluyen un único método de notificación. Los componentes pueden pasar cualquier contexto como argumentos de este método, incluyendo sus propios objetos, pero sólo de tal forma que no haya acoplamiento entre un componente receptor y la clase del emisor.
3. Los **Mediadores Concretos** encapsulan las relaciones entre varios componentes. Los mediadores concretos a menudo mantienen referencias a todos los componentes que gestionan y en ocasiones gestionan incluso su ciclo de vida.
4. Los componentes no deben conocer otros componentes. Si le sucede algo importante a un componente, o dentro de él, sólo debe notificar a la interfaz mediadora. Cuando la mediadora recibe la notificación, puede identificar fácilmente al emisor, lo cual puede ser suficiente para decidir qué componente debe activarse en respuesta. Desde la perspectiva de un componente, todo parece una caja negra. El emisor no sabe quién acabará gestionando su solicitud, y el receptor no sabe quién envió la solicitud.


## Participantes

1.     **Mediator:** Define una interfaz para comunicarse con los `Colleague` objetos.
2.     **ConcreteMediator:** Implementa el comportamiento cooperativo y coordina la comunicación entre los `Colleague` objetos.
3.     **Colleague:** Cada `Colleague` conoce a su `Mediator` y se comunica con él cuando necesita interactuar con otros `Colleague` objetos.
4.     **ConcreteColleague:** Implementa el comportamiento específico del `Colleague` y se comunica con otros `Colleague` a través de su `Mediator`.
## Principios de diseño relacionados

-  _Principio de responsabilidad única_ ([[Única Responsabilidad]]). Puedes extraer las comunicaciones entre varios componentes dentro de un único sitio, haciéndolo más fácil de comprender y mantener.
    
-  _Principio de abierto/cerrado_ ([[Open Close]]). Puedes introducir nuevos mediadores sin tener que cambiar los propios componentes.

## Ventajas
- Reduce el acoplamiento entre los objetos que interactúan.
- Facilita la modificación y extensión de las interacciones entre objetos.
- Centraliza el control de las interacciones, lo que puede simplificar la lógica del sistema.
- Puedes reducir el acoplamiento entre varios componentes de un programa.
- Puedes reutilizar componentes individuales con mayor facilidad.
## Desventajas

- Puede convertirse en un objeto God Object (objeto que sabe demasiado o hace demasiado), lo que puede dificultar su mantenimiento.
## Código
``` pascal
// La interfaz mediadora declara un método utilizado por los
// componentes para notificar al mediador sobre varios eventos.
// El mediador puede reaccionar a estos eventos y pasar la
// ejecución a otros componentes.
interface Mediator is
    method notify(sender: Component, event: string)

// La clase concreta mediadora. La red entrecruzada de
// conexiones entre componentes individuales se ha desenredado y
// se ha colocado dentro de la mediadora.
class AuthenticationDialog implements Mediator is
    private field title: string
    private field loginOrRegisterChkBx: Checkbox
    private field loginUsername, loginPassword: Textbox
    private field registrationUsername, registrationPassword,
                  registrationEmail: Textbox
    private field okBtn, cancelBtn: Button

    constructor AuthenticationDialog() is
        // Crea todos los objetos del componente y pasa el
        // mediador actual a sus constructores para establecer
        // vínculos.

    // Cuando sucede algo con un componente, notifica al
    // mediador, que al recibir la notificación, puede hacer
    // algo por su cuenta o pasar la solicitud a otro
    // componente.
    method notify(sender, event) is
        if (sender == loginOrRegisterChkBx and event == "check")
            if (loginOrRegisterChkBx.checked)
                title = "Log in"
                // 1. Muestra los componentes del formulario de
                // inicio de sesión.
                // 2. Esconde los componentes del formulario de
                // registro.
            else
                title = "Register"
                // 1. Muestra los componentes del formulario de
                // registro.
                // 2. Esconde los componentes del formulario de
                // inicio de sesión.

        if (sender == okBtn && event == "click")
            if (loginOrRegister.checked)
                // Intenta encontrar un usuario utilizando las
                // credenciales de inicio de sesión.
                if (!found)
                    // Muestra un mensaje de error sobre el
                    // campo de inicio de sesión.
            else
                // 1. Crea una cuenta de usuario utilizando
                // información de los campos de registro.
                // 2. Ingresa a ese usuario.
                // ...

// Los componentes se comunican con un mediador utilizando la
// interfaz mediadora. Gracias a ello, puedes utilizar los
// mismos componentes en otros contextos vinculándolos con
// diferentes objetos mediadores.
class Component is
    field dialog: Mediator

    constructor Component(dialog) is
        this.dialog = dialog

    method click() is
        dialog.notify(this, "click")

    method keypress() is
        dialog.notify(this, "keypress")

// Los componentes concretos no hablan entre sí. Sólo tienen un
// canal de comunicación, que es el envío de notificaciones al
// mediador.
class Button extends Component is
    // ...

class Textbox extends Component is
    // ...

class Checkbox extends Component is
    method check() is
        dialog.notify(this, "check")
    // ...
```