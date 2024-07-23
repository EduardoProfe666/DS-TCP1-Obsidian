## Descripción
#### Modularidad

La modularidad es un principio de diseño que busca dividir un sistema en componentes o módulos independientes, cada uno de los cuales puede ser desarrollado, probado, mantenido y modificado de manera aislada. Esto facilita la gestión del código, la reutilización y la escalabilidad del sistema.

#### Cohesión

La cohesión se refiere a cuán relacionadas o enfocadas están las responsabilidades de un módulo. Un módulo con alta cohesión tiene todas sus funciones y datos estrechamente relacionados y trabajan juntos para cumplir una única tarea bien definida. Esto hace que el módulo sea más fácil de entender, mantener y modificar.

#### Acoplamiento

El acoplamiento se refiere a cuán dependientes o interconectados están los módulos entre sí. Un bajo acoplamiento implica que los cambios en un módulo tienen poco o ningún impacto en otros módulos. Esto facilita la modificación y prueba de módulos individuales sin afectar al sistema en su conjunto.

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