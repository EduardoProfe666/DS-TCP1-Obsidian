## Descripción

El Principio de Sustitución de Liskov asegura que una subclase pueda asumir el lugar de su superclase sin afectar la funcionalidad esperada del programa. Para cumplir con este principio, es necesario que:

- Los objetos de una superclase puedan ser reemplazados por objetos de una subclase sin afectar la corrección del programa.
- Las subclases deben ser substituibles por sus superclases sin alterar las propiedades deseables del programa (tales como la corrección).
## Ejemplo

Imagina que tienes una clase `Bird` (Ave) con un método `fly()` (volar). Si creas una subclase `Penguin` (Pingüino) que hereda de `Bird`, pero los pingüinos no pueden volar, esto violaría el Principio de Sustitución de Liskov porque no puedes reemplazar un objeto `Bird` con un objeto `Penguin` sin alterar la funcionalidad esperada del programa (en este caso, la capacidad de volar).

Para adherirse al LSP, podrías refactorizar tus clases para que la capacidad de volar no esté implícita en la superclase `Bird`. Una solución podría ser tener una interfaz `FlyingBird` (AveVoladora) que tenga el método `fly()`, y hacer que solo aquellas aves que pueden volar implementen esta interfaz. De esta manera, `Penguin` no implementaría `FlyingBird`, y el programa podría tratar adecuadamente con ambos tipos de aves sin violar el LSP