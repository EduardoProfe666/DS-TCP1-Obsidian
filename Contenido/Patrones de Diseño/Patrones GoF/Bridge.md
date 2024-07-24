## Descripción
- Se le conoce también por `Puente`.
- Es un patrón `estructural`
- En Refactoring Guru está [aquí](./RefactoringGuru/Bridge.mhtml)

## Propósito

**Bridge** es un patrón de diseño estructural que te permite dividir una clase grande, o un grupo de clases estrechamente relacionadas, en dos jerarquías separadas (abstracción e implementación) que pueden desarrollarse independientemente la una de la otra.

El objetivo principal del patrón Bridge es desacoplar la abstracción de su implementación para que ambas puedan variar independientemente. Esto permite que la abstracción y la implementación puedan evolucionar de manera separada, facilitando la extensibilidad y reduciendo la complejidad del sistema.

## ¿Cuándo aplicarlo?

- Utiliza el patrón Bridge cuando quieras dividir y organizar una clase monolítica que tenga muchas variantes de una sola funcionalidad (por ejemplo, si la clase puede trabajar con diversos servidores de bases de datos).

 - Conforme más crece una clase, más difícil resulta entender cómo funciona y más tiempo se tarda en realizar un cambio. Cambiar una de las variaciones de funcionalidad puede exigir realizar muchos cambios a toda la clase, lo que a menudo provoca que se cometan errores o no se aborden algunos de los efectos colaterales críticos.

- El patrón Bridge te permite dividir la clase monolítica en varias jerarquías de clase. Después, puedes cambiar las clases de cada jerarquía independientemente de las clases de las otras. Esta solución simplifica el mantenimiento del código y minimiza el riesgo de descomponer el código existente.

 - Utiliza el patrón cuando necesites extender una clase en varias dimensiones ortogonales (independientes).

 - El patrón Bridge sugiere que extraigas una jerarquía de clase separada para cada una de las dimensiones. La clase original delega el trabajo relacionado a los objetos pertenecientes a dichas jerarquías, en lugar de hacerlo todo por su cuenta.

 - Utiliza el patrón Bridge cuando necesites poder cambiar implementaciones durante el tiempo de ejecución.

 - Aunque es opcional, el patrón Bridge te permite sustituir el objeto de implementación dentro de la abstracción. Es tan sencillo como asignar un nuevo valor a un campo.

- _Por cierto, este último punto es la razón principal por la que tanta gente confunde el patrón Bridge con el patrón Strategy. Recuerda que un patrón es algo más que un cierto modo de estructurar tus clases. También puede comunicar intención y el tipo de problema que se está abordando._
## Representación

![[Pasted image 20240723195126.png]]

1. La **Abstracción** ofrece lógica de control de alto nivel. Depende de que el objeto de la implementación haga el trabajo de bajo nivel.
2. La **Implementación** declara la interfaz común a todas las implementaciones concretas. Una abstracción sólo se puede comunicar con un objeto de implementación a través de los métodos que se declaren aquí. La abstracción puede enumerar los mismos métodos que la implementación, pero normalmente la abstracción declara funcionalidades complejas que dependen de una amplia variedad de operaciones primitivas declaradas por la implementación.
3. Las **Implementaciones Concretas** contienen código específico de plataforma.
4. Las **Abstracciones Refinadas** proporcionan variantes de lógica de control. Como sus padres, trabajan con distintas implementaciones a través de la interfaz general de implementación.
5. Normalmente, el **Cliente** sólo está interesado en trabajar con la abstracción. No obstante, el cliente tiene que vincular el objeto de la abstracción con uno de los objetos de la implementación.
## Participantes

- **Abstraction**: Define la interfaz de la abstracción y mantiene una referencia a la implementación.
- **RefinedAbstraction**: Extiende la interfaz definida por Abstraction.
- **Implementor**: Define la interfaz para la implementación. Esta interfaz no necesita coincidir exactamente con la interfaz de Abstraction.
- **ConcreteImplementor**: Implementa la interfaz de Implementor y define la implementación concreta.
## Principios de diseño relacionados

- _Principio de abierto/cerrado_. Puedes introducir nuevas abstracciones e implementaciones independientes entre sí.
-  _Principio de responsabilidad única_. Puedes centrarte en la lógica de alto nivel en la abstracción y en detalles de la plataforma en la implementación.

## Ventajas

- Puedes crear clases y aplicaciones independientes de plataforma.
- El código cliente funciona con abstracciones de alto nivel. No está expuesto a los detalles de la plataforma.
- Permite que la abstracción y la implementación evolucionen independientemente.
- Facilita la extensibilidad al permitir la adición de nuevas abstracciones y/o implementaciones.
- Mejora la organización del código al separar la interfaz de la implementación.
## Desventajas

 - Puede ser que el código se complique si aplicas el patrón a una clase muy cohesionada.
 - Puede introducir una capa adicional de abstracción, lo que puede complicar el diseño.
 - Puede ser menos eficiente que una solución específica, debido a las llamadas adicionales a través del puente.
## Código
``` pascal
// La "abstracción" define la interfaz para la parte de
// "control" de las dos jerarquías de clase. Mantiene una
// referencia a un objeto de la jerarquía de "implementación" y
// delega todo el trabajo real a este objeto.
class RemoteControl is
    protected field device: Device
    constructor RemoteControl(device: Device) is
        this.device = device
    method togglePower() is
        if (device.isEnabled()) then
            device.disable()
        else
            device.enable()
    method volumeDown() is
        device.setVolume(device.getVolume() - 10)
    method volumeUp() is
        device.setVolume(device.getVolume() + 10)
    method channelDown() is
        device.setChannel(device.getChannel() - 1)
    method channelUp() is
        device.setChannel(device.getChannel() + 1)

// Puedes extender clases de la jerarquía de abstracción
// independientemente de las clases de dispositivo.
class AdvancedRemoteControl extends RemoteControl is
    method mute() is
        device.setVolume(0)

// La interfaz de "implementación" declara métodos comunes a
// todas las clases concretas de implementación. No tiene por
// qué coincidir con la interfaz de la abstracción. De hecho,
// las dos interfaces pueden ser completamente diferentes.
// Normalmente, la interfaz de implementación únicamente
// proporciona operaciones primitivas, mientras que la
// abstracción define operaciones de más alto nivel con base en
// las primitivas.
interface Device is
    method isEnabled()
    method enable()
    method disable()
    method getVolume()
    method setVolume(percent)
    method getChannel()
    method setChannel(channel)

// Todos los dispositivos siguen la misma interfaz.
class Tv implements Device is
    // ...

class Radio implements Device is
    // ...

// En algún lugar del código cliente.
tv = new Tv()
remote = new RemoteControl(tv)
remote.togglePower()

radio = new Radio()
remote = new AdvancedRemoteControl(radio)
```