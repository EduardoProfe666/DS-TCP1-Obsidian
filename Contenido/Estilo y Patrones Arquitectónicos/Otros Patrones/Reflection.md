### Descripción
El patrón Reflection, también conocido como "introspección" o "metaprogramación", permite a un programa acceder y modificar su propia estructura y comportamiento en tiempo de ejecución. Esto proporciona un nivel de flexibilidad y extensibilidad que no es posible con enfoques de programación tradicionales.

En un sistema Reflection, el programa se trata a sí mismo como datos, lo que permite:

- **Inspeccionar la estructura del programa:** Obtener información sobre clases, objetos, métodos, propiedades y otros elementos del programa.
- **Modificar el comportamiento del programa:** Crear nuevos objetos, invocar métodos de forma dinámica, modificar valores de propiedades y alterar el flujo de ejecución del programa.

La implementación del patrón Reflection varía según el lenguaje de programación, pero generalmente se basa en mecanismos como la metaprogramación, la invocación dinámica y el acceso a metadatos.
### ¿Cuándo se usa?
El patrón Reflection se utiliza en diversas situaciones, como:

- **Sistemas con requisitos dinámicos:** Cuando las necesidades del sistema pueden cambiar en tiempo de ejecución, la Reflection permite adaptar el programa sin necesidad de recompilarlo.
- **Metaprogramación:** La Reflection permite crear herramientas y frameworks que pueden generar código, modificar comportamientos existentes o extender la funcionalidad del programa de forma dinámica.
- **Depuración y pruebas:** La Reflection facilita la inspección del estado interno del programa y la ejecución de pruebas unitarias de forma más efectiva.

### Ejemplos de Representación
- **Ejemplo 1**: En este ejemplo, el programa utiliza un reflector para obtener información sobre sus propias clases, métodos y propiedades. El reflector proporciona al programa acceso a metadatos sobre su estructura interna.
``` mermaid
sequenceDiagram
  participant Programa
  participant Reflector

  Programa->>Reflector: Obtener clases
  activate Reflector
  Reflector->>Programa: Lista de clases (Clase1, Clase2, ...)
  deactivate Reflector

  Programa->>Reflector: Obtener métodos de Clase1
  activate Reflector
  Reflector->>Programa: Lista de métodos (metodo1(), metodo2(), ...)
  deactivate Reflector

  Programa->>Reflector: Obtener propiedades de Clase2
  activate Reflector
  Reflector->>Programa: Lista de propiedades (propiedad1, propiedad2, ...)
  deactivate Reflector

```

### Ventajas
- **Flexibilidad:** Permite adaptar el programa a nuevas necesidades en tiempo de ejecución.
- **Extensibilidad:** Facilita la creación de frameworks, herramientas y metaprogramas.
- **Potencia:** Permite realizar tareas complejas que no son posibles con enfoques tradicionales.

### Desventajas
- **Complejidad:** Aumenta la complejidad del código y puede dificultar su comprensión y mantenimiento.
- **Rendimiento:** El acceso a metadatos y la modificación del programa en tiempo de ejecución pueden tener un impacto en el rendimiento.
- **Dependencia del lenguaje:** La implementación del patrón varía según el lenguaje de programación, lo que limita la portabilidad del código.

### Atributos Asociados
- Modificabilidad
### Atributos en conflicto
- Desempeño