## Descripción
- Se le conoce también por `Método Plantilla`.
- Es un patrón `de comportamiento`
- En Refactoring Guru está [aquí](./RefactoringGuru/Template-Method.mhtml)

## Propósito

**Template Method** es un patrón de diseño de comportamiento que define el esqueleto de un algoritmo en la superclase pero permite que las subclases sobrescriban pasos del algoritmo sin cambiar su estructura.
## ¿Cuándo aplicarlo?

- Utiliza el patrón Template Method cuando quieras permitir a tus clientes que extiendan únicamente pasos particulares de un algoritmo, pero no todo el algoritmo o su estructura.
- El patrón Template Method te permite convertir un algoritmo monolítico en una serie de pasos individuales que se pueden extender fácilmente con subclases, manteniendo intacta la estructura definida en una superclase.
- Utiliza el patrón cuando tengas muchas clases que contengan algoritmos casi idénticos, pero con algunas diferencias mínimas. Como resultado, puede que tengas que modificar todas las clases cuando el algoritmo cambie.
- Cuando conviertes un algoritmo así en un método plantilla, también puedes elevar los pasos con implementaciones similares a una superclase, eliminando la duplicación del código. El código que varía entre subclases puede permanecer en las subclases.
## Representación

![[Pasted image 20240723184653.png]]
1. La **Clase Abstracta** declara métodos que actúan como pasos de un algoritmo, así como el propio método plantilla que invoca estos métodos en un orden específico. Los pasos pueden declararse `abstractos` o contar con una implementación por defecto.
2. 1. Las **Clases Concretas** pueden sobrescribir todos los pasos, pero no el propio método plantilla.
## Participantes

1. **AbstractClass:** Define métodos abstractos que las subclases deben implementar y proporciona una implementación del Template Method que utiliza esos métodos abstractos.
2. **ConcreteClass:** Implementa los métodos abstractos definidos en `AbstractClass`.
## Principios de diseño relacionados

1. **Principio de Responsabilidad Única ([[Única Responsabilidad]])**: El patrón Template Method promueve el SRP al asignar la responsabilidad de implementar pasos específicos de un algoritmo a subclases separadas. Esto ayuda a mantener las clases enfocadas en una sola responsabilidad, lo que facilita la mantenibilidad y la reutilización del código.
2. **Inversión de Dependencias ([[Inversión de Dependencias]])**: El patrón Template Method puede ser visto como una aplicación del DIP, ya que el cliente que necesita utilizar el algoritmo depende de una abstracción (la clase abstracta que define el Template Method) en lugar de una implementación concreta. Esto permite que el cliente sea independiente de cómo se implementan los pasos específicos del algoritmo.

## Ventajas

- Puedes permitir a los clientes que sobrescriban tan solo ciertas partes de un algoritmo grande, para que les afecten menos los cambios que tienen lugar en otras partes del algoritmo.
-  Puedes colocar el código duplicado dentro de una superclase.
## Desventajas
-  Algunos clientes pueden verse limitados por el esqueleto proporcionado de un algoritmo.
-  Puede que violes el _principio de sustitución de Liskov_ suprimiendo una implementación por defecto de un paso a través de una subclase.
-  Los métodos plantilla tienden a ser más difíciles de mantener cuantos más pasos tengan.

## Código
``` pascal
// La clase abstracta define un método plantilla que contiene un
// esqueleto de algún algoritmo compuesto por llamadas,
// normalmente a operaciones primitivas abstractas. Las
// subclases concretas implementan estas operaciones, pero dejan
// el propio método plantilla intacto.
class GameAI is
    // El método plantilla define el esqueleto de un algoritmo.
    method turn() is
        collectResources()
        buildStructures()
        buildUnits()
        attack()

    // Algunos de los pasos se pueden implementar directamente
    // en una clase base.
    method collectResources() is
        foreach (s in this.builtStructures) do
            s.collect()

    // Y algunos de ellos pueden definirse como abstractos.
    abstract method buildStructures()
    abstract method buildUnits()

    // Una clase puede tener varios métodos plantilla.
    method attack() is
        enemy = closestEnemy()
        if (enemy == null)
            sendScouts(map.center)
        else
            sendWarriors(enemy.position)

    abstract method sendScouts(position)
    abstract method sendWarriors(position)

// Las clases concretas tienen que implementar todas las
// operaciones abstractas de la clase base, pero no deben
// sobrescribir el propio método plantilla.
class OrcsAI extends GameAI is
    method buildStructures() is
        if (there are some resources) then
            // Construye granjas, después cuarteles y después
            // fortaleza.

    method buildUnits() is
        if (there are plenty of resources) then
            if (there are no scouts)
                // Crea peón y añádelo al grupo de exploradores.
            else
                // Crea soldado, añádelo al grupo de guerreros.

    // ...

    method sendScouts(position) is
        if (scouts.length > 0) then
            // Envía exploradores a posición.

    method sendWarriors(position) is
        if (warriors.length > 5) then
            // Envía guerreros a posición.

// Las subclases también pueden sobrescribir algunas operaciones
// con una implementación por defecto.
class MonstersAI extends GameAI is
    method collectResources() is
        // Los monstruos no recopilan recursos.

    method buildStructures() is
        // Los monstruos no construyen estructuras.

    method buildUnits() is
        // Los monstruos no construyen unidades.
```