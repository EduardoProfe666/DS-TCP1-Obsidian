## Descripción
- Se le conoce también por `Decorador`  y `Envoltorio`.
- Es un patrón `estructural`
- En Refactoring Guru está [aquí](./RefactoringGuru/Decorator.mhtml)

## Propósito

**Decorator** es un patrón de diseño estructural que te permite añadir funcionalidades a objetos colocando estos objetos dentro de objetos encapsuladores especiales que contienen estas funcionalidades.
## ¿Cuándo aplicarlo?

- Utiliza el patrón Decorator cuando necesites asignar funcionalidades adicionales a objetos durante el tiempo de ejecución sin descomponer el código que utiliza esos objetos.
- El patrón Decorator te permite estructurar tu lógica de negocio en capas, crear un decorador para cada capa y componer objetos con varias combinaciones de esta lógica, durante el tiempo de ejecución. El código cliente puede tratar a todos estos objetos de la misma forma, ya que todos siguen una interfaz común.
- Utiliza el patrón cuando resulte extraño o no sea posible extender el comportamiento de un objeto utilizando la herencia.
- Muchos lenguajes de programación cuentan con la palabra clave `final` que puede utilizarse para evitar que una clase siga extendiéndose. Para una clase final, la única forma de reutilizar el comportamiento existente será envolver la clase con tu propio wrapper, utilizando el patrón Decorator.
## Representación

![[Pasted image 20240723194424.png]]
1. El **Componente** declara la interfaz común tanto para wrappers como para objetos envueltos.
2. **Componente Concreto** es una clase de objetos envueltos. Define el comportamiento básico, que los decoradores pueden alterar.
3. La clase **Decoradora Base** tiene un campo para referenciar un objeto envuelto. El tipo del campo debe declararse como la interfaz del componente para que pueda contener tanto los componentes concretos como los decoradores. La clase decoradora base delega todas las operaciones al objeto envuelto.
4. Los **Decoradores Concretos** definen funcionalidades adicionales que se pueden añadir dinámicamente a los componentes. Los decoradores concretos sobrescriben métodos de la clase decoradora base y ejecutan su comportamiento, ya sea antes o después de invocar al método padre.
5. El **Cliente** puede envolver componentes en varias capas de decoradores, siempre y cuando trabajen con todos los objetos a través de la interfaz del componente.
## Participantes

- **Component**: Define la interfaz para los objetos que pueden tener responsabilidades adicionales agregadas dinámicamente.
- **ConcreteComponent**: Define un objeto al que se le pueden agregar responsabilidades adicionales.
- **Decorator**: Mantiene una referencia al objeto Component y define una interfaz que sigue la interfaz de Component.
- **ConcreteDecorator**: Agrega responsabilidades adicionales al Component.
## Principios de diseño relacionados

- _Principio de responsabilidad única_. Puedes dividir una clase monolítica que implementa muchas variantes posibles de comportamiento, en varias clases más pequeñas.

## Ventajas

- Puedes extender el comportamiento de un objeto sin crear una nueva subclase.
-  Puedes añadir o eliminar responsabilidades de un objeto durante el tiempo de ejecución.
-  Puedes combinar varios comportamientos envolviendo un objeto con varios decoradores.
-  _Principio de responsabilidad única_. Puedes dividir una clase monolítica que implementa muchas variantes posibles de comportamiento, en varias clases más pequeñas.
## Desventajas

- Resulta difícil eliminar un wrapper específico de la pila de wrappers.
-  Es difícil implementar un decorador de tal forma que su comportamiento no dependa del orden en la pila de decoradores.
-  El código de configuración inicial de las capas pueden tener un aspecto desagradable.
## Código
``` pascal
// La interfaz de componente define operaciones que los
// decoradores pueden alterar.
interface DataSource is
    method writeData(data)
    method readData():data

// Los componentes concretos proporcionan implementaciones por
// defecto para las operaciones. En un programa puede haber
// muchas variaciones de estas clases.
class FileDataSource implements DataSource is
    constructor FileDataSource(filename) { ... }

    method writeData(data) is
        // Escribe datos en el archivo.

    method readData():data is
        // Lee datos del archivo.

// La clase decoradora base sigue la misma interfaz que los
// demás componentes. El principal propósito de esta clase es
// definir la interfaz de encapsulación para todos los
// decoradores concretos. La implementación por defecto del
// código de encapsulación puede incluir un campo para almacenar
// un componente envuelto y los medios para inicializarlo.
class DataSourceDecorator implements DataSource is
    protected field wrappee: DataSource

    constructor DataSourceDecorator(source: DataSource) is
        wrappee = source

    // La decoradora base simplemente delega todo el trabajo al
    // componente envuelto. En los decoradores concretos se
    // pueden añadir comportamientos adicionales.
    method writeData(data) is
        wrappee.writeData(data)

    // Los decoradores concretos pueden invocar la
    // implementación padre de la operación en lugar de invocar
    // directamente al objeto envuelto. Esta solución simplifica
    // la extensión de las clases decoradoras.
    method readData():data is
        return wrappee.readData()

// Los decoradores concretos deben invocar métodos en el objeto
// envuelto, pero pueden añadir algo de su parte al resultado.
// Los decoradores pueden ejecutar el comportamiento añadido
// antes o después de la llamada a un objeto envuelto.
class EncryptionDecorator extends DataSourceDecorator is
    method writeData(data) is
        // 1. Encripta los datos pasados.
        // 2. Pasa los datos encriptados al método writeData
        // (escribirDatos) del objeto envuelto.

    method readData():data is
        // 1. Obtiene datos del método readData (leerDatos) del
        // objeto envuelto.
        // 2. Intenta descifrarlo si está encriptado.
        // 3. Devuelve el resultado.

// Puedes envolver objetos en varias capas de decoradores.
class CompressionDecorator extends DataSourceDecorator is
    method writeData(data) is
        // 1. Comprime los datos pasados.
        // 2. Pasa los datos comprimidos al método writeData del
        // objeto envuelto.

    method readData():data is
        // 1. Obtiene datos del método readData del objeto
        // envuelto.
        // 2. Intenta descomprimirlo si está comprimido.
        // 3. Devuelve el resultado.

// Opción 1. Un ejemplo sencillo del montaje de un decorador.
class Application is
    method dumbUsageExample() is
        source = new FileDataSource("somefile.dat")
        source.writeData(salaryRecords)
        // El archivo objetivo se ha escrito con datos sin
        // formato.

        source = new CompressionDecorator(source)
        source.writeData(salaryRecords)
        // El archivo objetivo se ha escrito con datos
        // comprimidos.

        source = new EncryptionDecorator(source)
        // La variable fuente ahora contiene esto:
        // Cifrado > Compresión > FileDataSource
        source.writeData(salaryRecords)
        // El archivo se ha escrito con datos comprimidos y
        // encriptados.

// Opción 2. El código cliente que utiliza una fuente externa de
// datos. Los objetos SalaryManager no conocen ni se preocupan
// por las especificaciones del almacenamiento de datos.
// Trabajan con una fuente de datos preconfigurada recibida del
// configurador de la aplicación.
class SalaryManager is
    field source: DataSource

    constructor SalaryManager(source: DataSource) { ... }

    method load() is
        return source.readData()

    method save() is
        source.writeData(salaryRecords)
    // ...Otros métodos útiles...

// La aplicación puede montar distintas pilas de decoradores
// durante el tiempo de ejecución, dependiendo de la
// configuración o el entorno.
class ApplicationConfigurator is
    method configurationExample() is
        source = new FileDataSource("salary.dat")
        if (enabledEncryption)
            source = new EncryptionDecorator(source)
        if (enabledCompression)
            source = new CompressionDecorator(source)

        logger = new SalaryManager(source)
        salary = logger.load()
    // ...
```