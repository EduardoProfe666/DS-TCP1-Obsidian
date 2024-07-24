## Descripción
- Se le conoce también por `Instancia Unica`.
- Es un patrón `creacional`
- En Refactoring Guru está [aquí](./RefactoringGuru/Singleton.mhtml)

## Propósito
**Singleton** es un patrón de diseño creacional que nos permite asegurarnos de que una clase tenga una única instancia, a la vez que proporciona un punto de acceso global a dicha instancia.
El objetivo principal del patrón Singleton es asegurar que una clase tenga una única instancia y proporcionar un punto de acceso global a esa instancia. Esto permite controlar el acceso a recursos compartidos, como bases de datos, archivos de configuración o registros de logs, de manera eficiente y segura.

## ¿Cuándo aplicarlo?

- Utiliza el patrón Singleton cuando una clase de tu programa tan solo deba tener una instancia disponible para todos los clientes; por ejemplo, un único objeto de base de datos compartido por distintas partes del programa.
 - El patrón Singleton deshabilita el resto de las maneras de crear objetos de una clase, excepto el método especial de creación. Este método crea un nuevo objeto, o bien devuelve uno existente si ya ha sido creado.
- Utiliza el patrón Singleton cuando necesites un control más estricto de las variables globales.
- Al contrario que las variables globales, el patrón Singleton garantiza que haya una única instancia de una clase. A excepción de la propia clase Singleton, nada puede sustituir la instancia en caché.
- Ten en cuenta que siempre podrás ajustar esta limitación y permitir la creación de cierto número de instancias Singleton. La única parte del código que requiere cambios es el cuerpo del método `getInstance`.
## Representación

![[Pasted image 20240723182845.png]]

1. La clase **Singleton** declara el método estático `obtenerInstancia` que devuelve la misma instancia de su propia clase. El constructor del Singleton debe ocultarse del código cliente. La llamada al método `obtenerInstancia` debe ser la única manera de obtener el objeto de Singleton.
## Participantes
- **Singleton**: Define una instancia estática que proporciona un punto de acceso global a esa instancia. También puede encargarse de crear su propia única instancia.

## Principios de diseño relacionados

1. **Principio de Abierto/Cerrado ([[Open Close]])**: El patrón Singleton puede promover el OCP al permitir que las clases sean extendidas para soportar nuevas funcionalidades sin modificar el código existente. Sin embargo, es importante tener cuidado con la implementación del Singleton para no violar el OCP al agregar nuevas responsabilidades a la clase Singleton.

## Ventajas
- Garantiza que una clase tenga una única instancia.
- Proporciona un punto de acceso global a esa instancia.
- Permite un control centralizado sobre el estado y el comportamiento de la instancia.
- Puedes tener la certeza de que una clase tiene una única instancia.
- Obtienes un punto de acceso global a dicha instancia.
- El objeto Singleton solo se inicializa cuando se requiere por primera vez.

## Desventajas
- Puede ocultar las dependencias entre clases, dificultando la comprensión y el mantenimiento del código.
- Puede llevar a problemas de concurrencia si no se implementa correctamente en entornos multi-hilo.
- Vulnera el _Principio de responsabilidad única_. El patrón resuelve dos problemas al mismo tiempo.
- El patrón Singleton puede enmascarar un mal diseño, por ejemplo, cuando los componentes del programa saben demasiado los unos sobre los otros

## Código
``` pascal
// La clase Base de datos define el método `obtenerInstancia`
// que permite a los clientes acceder a la misma instancia de
// una conexión de la base de datos a través del programa.
class Database is
    // El campo para almacenar la instancia singleton debe
    // declararse estático.
    private static field instance: Database

    // El constructor del singleton siempre debe ser privado
    // para evitar llamadas de construcción directas con el
    // operador `new`.
    private constructor Database() is
        // Algún código de inicialización, como la propia
        // conexión al servidor de una base de datos.
        // ...

    // El método estático que controla el acceso a la instancia
    // singleton.
    public static method getInstance() is
        if (Database.instance == null) then
            acquireThreadLock() and then
                // Garantiza que la instancia aún no se ha
                // inicializado por otro hilo mientras ésta ha
                // estado esperando el desbloqueo.
                if (Database.instance == null) then
                    Database.instance = new Database()
        return Database.instance

    // Por último, cualquier singleton debe definir cierta
    // lógica de negocio que pueda ejecutarse en su instancia.
    public method query(sql) is
        // Por ejemplo, todas las consultas a la base de datos
        // de una aplicación pasan por este método. Por lo
        // tanto, aquí puedes colocar lógica de regularización
        // (throttling) o de envío a la memoria caché.
        // ...

class Application is
    method main() is
        Database foo = Database.getInstance()
        foo.query("SELECT ...")
        // ...
        Database bar = Database.getInstance()
        bar.query("SELECT ...")
        // La variable `bar` contendrá el mismo objeto que la
        // variable `foo`.
```