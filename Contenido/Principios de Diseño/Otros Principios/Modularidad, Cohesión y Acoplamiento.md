## Descripción
#### Modularidad

- La modularidad es un principio de diseño que busca dividir un sistema en componentes o módulos independientes, cada uno de los cuales puede ser desarrollado, probado, mantenido y modificado de manera aislada. Esto facilita la gestión del código, la reutilización y la escalabilidad del sistema.

- Es la partición lógica del diseño de software que permite al software complejo ser manejable para propósitos de implementación y mantenimiento.

- Es el atributo individual del software que permite a un programa ser intelectualmente manejable.

- Es la propiedad que tiene un sistema que ha sido descompuesto en un conjunto de módulos cohesivos y débilmente acoplados.
- 
Un módulo es cualquier parte o subsistema de un sistema mayor.

- Componente bien definido de un sistema.
- Autónomo, auto-contenido, cohesión lógica.

Un sistema es modular si está compuesto de módulos bien definidos, conceptualmente simples e independientes, que interactúan a través de interfaces bien definidas.

Los sistemas modulares son deseables por las siguientes razones:

- Son fáciles de entender y explicar porque se puede estudiar cada módulo por separado y tienen bien definidas las interdependencias.

- Más fáciles de documentar.

- Más fáciles de programar por grupos independientes.

- Más fáciles de mantener.

Reglas de evaluación de modularidad:

- Correspondencia directa entre estructura de la solución y la estructura del dominio del problema modelado.

- Pocas interfaces, cada componente debe comunicarse con el menor número posible de componentes.

- Interfaces pequeñas.

- Interfaces claras.

- Ocultación de información.
#### Cohesión

La cohesión se refiere a cuán relacionadas o enfocadas están las responsabilidades de un módulo. Un módulo con alta cohesión tiene todas sus funciones y datos estrechamente relacionados y trabajan juntos para cumplir una única tarea bien definida. Esto hace que el módulo sea más fácil de entender, mantener y modificar.

La cohesión es la medida de la relación funcional de los elementos de un módulo.

Es una indicación cualitativa del grado que tiene un módulo para centrase en una sola cosa.

Es la organización de los elementos de forma que los que tengan mayor relación para realizar una tarea, pertenezcan al mismo módulo y los elementos no relacionados se encuentren en módulos separados.

Un subsistema o módulo tiene un alto grado de cohesión si mantiene unidas cosas que están relacionadas entre ellas, y mantiene fuera al resto.

#### Acoplamiento

El acoplamiento se refiere a cuán dependientes o interconectados están los módulos entre sí. Un bajo acoplamiento implica que los cambios en un módulo tienen poco o ningún impacto en otros módulos. Esto facilita la modificación y prueba de módulos individuales sin afectar al sistema en su conjunto.

El acoplamiento es una medida de la interconexión entre los módulos de una estructura de software.

El acoplamiento depende de la complejidad de la interconexión entre los módulos, el punto donde  se realiza una entrada o referencia a un módulo y los datos que se pasan  a través de la interfaz.

Un acoplamiento bajo indica un sistema bien dividido y puede lograrse mediante la reducción de relaciones innecesarias.

Una conectividad sencilla entre módulos da como resultado:

•Un software más fácil de entender.

•Un software menos propenso al efecto “ola” (errores en un lugar se propagan a otros).

•Un bajo acoplamiento significa que un cambio en un componente no implicará un cambio en otro.

La meta es un software con alta cohesión y bajo acoplamiento.
## Ejemplo

```java
class Usuario {
    private String nombre;
    private String email;

    public Usuario(String nombre, String email) {
        this.nombre = nombre;
        this.email = email;
    }

    public String getNombre() {
        return nombre;
    }

    public String getEmail() {
        return email;
    }
}

// Clase para manejar operaciones de autenticación
class Autenticacion {
    private Usuario usuario;

    public Autenticacion(Usuario usuario) {
        this.usuario = usuario;
    }

    public boolean autenticar(String password) {
        // Lógica de autenticación ficticia
        return password.equals("1234");
    }
}

// Clase para manejar operaciones de correo
class Correo {
    private Usuario usuario;

    public Correo(Usuario usuario) {
        this.usuario = usuario;
    }

    public void enviarCorreo(String mensaje) {
        System.out.println("Enviando correo a " + usuario.getEmail() + ": " + mensaje);
    }
}

// Clase principal para ejecutar el ejemplo
public class Main {
    public static void main(String[] args) {
        Usuario usuario = new Usuario("Juan", "juan@example.com");
        Autenticacion autenticacion = new Autenticacion(usuario);
        Correo correo = new Correo(usuario);

        if (autenticacion.autenticar("1234")) {
            correo.enviarCorreo("Bienvenido a nuestro sistema!");
        } else {
            System.out.println("Autenticación fallida");
        }
    }
}
```

### Explicación del Ejemplo

1. **Modularidad**: El sistema está dividido en tres clases: `Usuario`, `Autenticacion` y `Correo`. Cada clase tiene una responsabilidad específica y puede ser desarrollada y probada de manera independiente.

2. **Cohesión**: Cada clase tiene alta cohesión, ya que todas las funciones y datos dentro de cada clase están estrechamente relacionados. Por ejemplo, la clase `Usuario` se encarga de manejar datos de usuario, la clase `Autenticacion` se encarga de la autenticación, y la clase `Correo` se encarga de enviar correos.

3. **Acoplamiento**: Las clases están débilmente acopladas. Por ejemplo, las clases `Autenticacion` y `Correo` dependen de la clase `Usuario`, pero no dependen una de la otra. Esto permite que los cambios en una clase no afecten a las otras, siempre y cuando la interfaz de la clase `Usuario` no cambie.