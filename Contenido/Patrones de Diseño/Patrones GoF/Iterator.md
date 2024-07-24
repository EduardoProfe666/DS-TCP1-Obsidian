## Descripción
- Se le conoce también por `Iterador`.
- Es un patrón `de comportamiento`
- En Refactoring Guru está [aquí](./RefactoringGuru/Iterator.mhtml)

## Propósito

**Iterator** es un patrón de diseño de comportamiento que te permite recorrer elementos de una colección sin exponer su representación subyacente (lista, pila, árbol, etc.).

El objetivo principal del patrón Iterator es proporcionar una forma uniforme de acceder a los elementos de una colección sin exponer su estructura interna. Surgió como una solución para abstraer el proceso de iteración sobre una colección, permitiendo así que diferentes tipos de colecciones puedan ser iterados de manera consistente.
## ¿Cuándo aplicarlo?
-  Utiliza el patrón Iterator cuando tu colección tenga una estructura de datos compleja a nivel interno, pero quieras ocultar su complejidad a los clientes (ya sea por conveniencia o por razones de seguridad).
- El iterador encapsula los detalles del trabajo con una estructura de datos compleja, proporcionando al cliente varios métodos simples para acceder a los elementos de la colección. Esta solución, además de ser muy conveniente para el cliente, también protege la colección frente a acciones descuidadas o maliciosas que el cliente podría realizar si trabajara con la colección directamente.
- Utiliza el patrón para reducir la duplicación en el código de recorrido a lo largo de tu aplicación.
- El código de los algoritmos de iteración no triviales tiende a ser muy voluminoso. Cuando se coloca dentro de la lógica de negocio de una aplicación, puede nublar la responsabilidad del código original y hacerlo más difícil de mantener. Mover el código de recorrido a iteradores designados puede ayudarte a hacer el código de la aplicación más breve y limpio.
- Utiliza el patrón Iterator cuando quieras que tu código pueda recorrer distintas estructuras de datos, o cuando los tipos de estas estructuras no se conozcan de antemano.
- El patrón proporciona un par de interfaces genéricas para colecciones e iteradores. Teniendo en cuenta que ahora tu código utiliza estas interfaces, seguirá funcionando si le pasas varios tipos de colecciones e iteradores que implementen esas interfaces.

## Representación

![[Pasted image 20240723155832.png]]

1. La interfaz **Iteradora** declara las operaciones necesarias para recorrer una colección: extraer el siguiente elemento, recuperar la posición actual, reiniciar la iteración, etc.
2. Los **Iteradores Concretos** implementan algoritmos específicos para recorrer una colección. El objeto iterador debe controlar el progreso del recorrido por su cuenta. Esto permite a varios iteradores recorrer la misma colección con independencia entre sí.
3. La interfaz **Colección** declara uno o varios métodos para obtener iteradores compatibles con la colección. Observa que el tipo de retorno de los métodos debe declararse como la interfaz iteradora de forma que las colecciones concretas puedan devolver varios tipos de iteradores.
4. Las **Colecciones Concretas** devuelven nuevas instancias de una clase iteradora concreta particular cada vez que el cliente solicita una. Puede que te estés preguntando: ¿dónde está el resto del código de la colección? No te preocupes, debe estar en la misma clase. Lo que pasa es que estos detalles no son fundamentales para el patrón en sí, por eso los omitimos.
5. El **Cliente** debe funcionar con colecciones e iteradores a través de sus interfaces. De este modo, el cliente no se acopla a clases concretas, permitiéndote utilizar varias colecciones e iteradores con el mismo código cliente. Normalmente, los clientes no crean iteradores por su cuenta, en lugar de eso, los obtienen de las colecciones. Sin embargo, en algunos casos, el cliente puede crear uno directamente, como cuando define su propio iterador especial.
## Participantes
1. **Iterator:** Define una interfaz para acceder y recorrer elementos.
2. **ConcreteIterator:** Implementa la interfaz `Iterator` y mantiene la posición actual en la iteración.
3. **Aggregate:** Define una interfaz para crear un objeto `Iterator`.
4. **ConcreteAggregate:** Implementa la interfaz `Aggregate` y devuelve una instancia de `ConcreteIterator` que puede iterar sobre su colección.

## Principios de diseño relacionados

- _Principio de responsabilidad única_ ([[Única Responsabilidad]]). Puedes limpiar el código cliente y las colecciones extrayendo algoritmos de recorrido voluminosos y colocándolos en clases independientes.
-  _Principio de abierto/cerrado_ ([[Open Close]]). Puedes implementar nuevos tipos de colecciones e iteradores y pasarlos al código existente sin descomponer nada.

## Ventajas
-  _Principio de responsabilidad única_. Puedes limpiar el código cliente y las colecciones extrayendo algoritmos de recorrido voluminosos y colocándolos en clases independientes.
-  _Principio de abierto/cerrado_. Puedes implementar nuevos tipos de colecciones e iteradores y pasarlos al código existente sin descomponer nada.
-  Puedes recorrer la misma colección en paralelo porque cada objeto iterador contiene su propio estado de iteración.
-  Por la misma razón, puedes retrasar una iteración y continuar cuando sea necesario.
- Proporciona una forma uniforme de iterar sobre diferentes tipos de colecciones.
- Desacopla el algoritmo de iteración de la colección, promoviendo la encapsulación.
- Permite la creación de iteradores personalizados para diferentes necesidades de iteración.

## Desventajas
- Aplicar el patrón puede resultar excesivo si tu aplicación funciona únicamente con colecciones sencillas.
-  Utilizar un iterador puede ser menos eficiente que recorrer directamente los elementos de algunas colecciones especializadas.
- Puede introducir una sobrecarga adicional en términos de complejidad y rendimiento si no se utiliza adecuadamente.

## Código
``` pascal
// La interfaz de colección debe declarar un método fábrica para
// producir iteradores. Puedes declarar varios métodos si hay
// distintos tipos de iteración disponibles en tu programa.
interface SocialNetwork is
    method createFriendsIterator(profileId):ProfileIterator
    method createCoworkersIterator(profileId):ProfileIterator

// Cada colección concreta está acoplada a un grupo de clases
// iteradoras concretas que devuelve, pero el cliente no lo
// está, ya que la firma de estos métodos devuelve interfaces
// iteradoras.
class Facebook implements SocialNetwork is
    // ... El grueso del código de la colección debe ir aquí ...
    // Código de creación del iterador.
    method createFriendsIterator(profileId) is
        return new FacebookIterator(this, profileId, "friends")
    method createCoworkersIterator(profileId) is
        return new FacebookIterator(this, profileId, "coworkers")

// La interfaz común a todos los iteradores.
interface ProfileIterator is
    method getNext():Profile
    method hasMore():bool

// La clase iteradora concreta.
class FacebookIterator implements ProfileIterator is
    // El iterador necesita una referencia a la colección que
    // recorre.
    private field facebook: Facebook
    private field profileId, type: string

    // Un objeto iterador recorre la colección
    // independientemente de otro iterador, por eso debe
    // almacenar el estado de iteración.
    private field currentPosition
    private field cache: array of Profile

    constructor FacebookIterator(facebook, profileId, type) is
        this.facebook = facebook
        this.profileId = profileId
        this.type = type

    private method lazyInit() is
        if (cache == null)
            cache = facebook.socialGraphRequest(profileId, type)

    // Cada clase iteradora concreta tiene su propia
    // implementación de la interfaz iteradora común.
    method getNext() is
        if (hasMore())
            result = cache[currentPosition]
            currentPosition++
            return result

    method hasMore() is
        lazyInit()
        return currentPosition < cache.length

// Aquí tienes otro truco útil: puedes pasar un iterador a una
// clase cliente en lugar de darle acceso a una colección
// completa. De esta forma, no expones la colección al cliente.
//
// Y hay otra ventaja: puedes cambiar la forma en la que el
// cliente trabaja con la colección durante el tiempo de
// ejecución pasándole un iterador diferente. Esto es posible
// porque el código cliente no está acoplado a clases iteradoras
// concretas.
class SocialSpammer is
    method send(iterator: ProfileIterator, message: string) is
        while (iterator.hasMore())
            profile = iterator.getNext()
            System.sendEmail(profile.getEmail(), message)

// La clase Aplicación configura colecciones e iteradores y
// después los pasa al código cliente.
class Application is
    field network: SocialNetwork
    field spammer: SocialSpammer

    method config() is
        if working with Facebook
            this.network = new Facebook()
        if working with LinkedIn
            this.network = new LinkedIn()
        this.spammer = new SocialSpammer()

    method sendSpamToFriends(profile) is
        iterator = network.createFriendsIterator(profile.getId())
        spammer.send(iterator, "Very important message")

    method sendSpamToCoworkers(profile) is
        iterator = network.createCoworkersIterator(profile.getId())
        spammer.send(iterator, "Very important message")
```