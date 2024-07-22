### Descripción
El patrón **Representation Abstraction Control (RAC)**, también conocido como "Separación de Representación, Abstracción y Control", es un patrón de arquitectura de software que promueve la modularidad y la separación de responsabilidades en el desarrollo de aplicaciones. Este patrón divide el desarrollo de software en tres capas independientes:

**1. Capa de Representación:**

- Se encarga de la representación de los datos en un formato específico, como texto, gráficos o audio.
- Maneja la serialización y deserialización de datos.
- No contiene lógica de negocios ni reglas de validación.

**2. Capa de Abstracción:**

- Define una abstracción de los datos, independientemente de su representación.
- Proporciona una interfaz para acceder y manipular los datos de forma independiente de su formato de representación.
- Implementa la lógica de negocios y las reglas de validación.

**3. Capa de Control:**

- Controla el flujo de la aplicación y la interacción entre las capas de representación y abstracción.
- Implementa la lógica de presentación y la interacción con el usuario.
- No contiene código de representación o de abstracción de datos.
### ¿Cuándo se usa?
El patrón RAC se utiliza en diversas situaciones, como:

- **Aplicaciones con múltiples representaciones de datos:** Cuando la misma información necesita ser representada en diferentes formatos, como texto, gráficos o audio.
- **Aplicaciones con reglas de negocio complejas:** Cuando la lógica de negocios es compleja y necesita ser separada de la representación y el control de los datos.
- **Aplicaciones con requisitos de pruebas amplios:** Cuando se requiere realizar pruebas unitarias y de integración de forma efectiva.

### Ejemplos de Representación
- **Ejemplo 1:** En este ejemplo, un usuario solicita datos al controlador. El controlador recupera los datos de la capa de abstracción de datos, los formatea a texto utilizando la capa de representación de texto y los muestra al usuario.
``` mermaid
sequenceDiagram
  participant Usuario
  participant Controlador
  participant AbstraccionDatos
  participant RepresentacionTexto

  Usuario->>Controlador: Solicitar datos
  activate Controlador
  Controlador->>AbstraccionDatos: Obtener datos
  activate AbstraccionDatos
  AbstraccionDatos->>Controlador: Datos sin formato
  Controlador->>RepresentacionTexto: Formatear datos a texto
  activate RepresentacionTexto
  RepresentacionTexto->>Controlador: Datos formateados en texto
  Controlador->>Usuario: Mostrar datos en texto
  deactivate RepresentacionTexto
  deactivate AbstraccionDatos
  deactivate Controlador

```

- **Ejemplo 2:** En este ejemplo, el diagrama de clases muestra las relaciones entre las clases del patrón RAC. El usuario interactúa con el controlador, que delega la recuperación de datos a la capa de abstracción de datos y el formateo a la capa de representación de texto.
``` mermaid
classDiagram
  class Usuario {
    - solicitarDatos(): void
    - mostrarDatos(datos: String): void
  }

  class Controlador {
    - solicitarDatos(): String
    - mostrarDatos(datos: String): void
  }

  class AbstraccionDatos {
    - obtenerDatos(): Datos
  }

  class RepresentacionTexto {
    - formatearDatosATexto(datos: Datos): String
  }

  Usuario -->Controlador: solicitarDatos, mostrarDatos
  Controlador -->AbstraccionDatos: obtenerDatos
  Controlador -->RepresentacionTexto: formatearDatosATexto

```
### Ventajas
- **Modularidad:** Promueve la modularidad del código, facilitando el desarrollo, mantenimiento y reutilización de componentes.
- **Separación de responsabilidades:** Separa las responsabilidades de representación, abstracción y control, mejorando la claridad y la mantenibilidad del código.
- **Testability:** Facilita la realización de pruebas unitarias y de integración al aislar las capas.
- **Reutilización:** Permite la reutilización de componentes en diferentes aplicaciones.

### Desventajas
- **Complejidad:** Aumenta la complejidad del diseño de la arquitectura.
- **Overhead:** Puede introducir un ligero overhead de rendimiento debido a la comunicación entre las capas.
- **Curva de aprendizaje:** Requiere una comprensión más profunda de los principios de diseño de software.

### Atributos Asociados
- Modificabilidad
- Escalabilidad
- Integrabilidad

### Atributos en conflicto
- Desempeño 
- Mantenibilidad