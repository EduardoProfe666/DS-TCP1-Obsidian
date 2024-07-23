## Descripción

- Puede tener otros nombres como `Controlador` y `Controller`
- El patrón de diseño "Controlador" (Controller) es un patrón de diseño de arquitectura de software que se utiliza para manejar las interacciones entre diferentes componentes de un sistema. El Controlador actúa como un intermediario que recibe las solicitudes del usuario o de otros componentes y las dirige al componente adecuado para su procesamiento.

#### Problema

El problema que resuelve el patrón Controlador es la separación de preocupaciones y la gestión de la lógica de control en un sistema. Sin un Controlador, las interacciones entre los componentes podrían ser confusas y difíciles de mantener, ya que cada componente podría intentar manejar directamente las solicitudes de otros componentes. El Controlador centraliza esta lógica, lo que facilita la gestión y el mantenimiento del sistema.
#### Solución

- El objetivo principal del patrón Controlador es asignar la responsabilidad de manejar eventos y coordinar operaciones a una clase que actúa como intermediario entre la interfaz de usuario y el resto del sistema. Esto promueve la separación de preocupaciones, facilitando así el mantenimiento y la evolución del sistema.
#### Aplicaciones

El patrón Controlador se utiliza en diversos sistemas de software, especialmente en aplicaciones que siguen la arquitectura Model-View-Controller (MVC). Ejemplos incluyen aplicaciones web, aplicaciones de escritorio, y cualquier sistema donde sea necesario separar la lógica de negocio de la interfaz de usuario.
## Estructura

#### Representación
``` mermaid
classDiagram 
	class Controlador
	class Modelo
	class Vista

	Controlador: +Controlador(Modelo, Vista)
	Controlador: +manejarEvento()
	Modelo: +realizarOperacion()
	Vista: +actualizar()

	Controlador o-- Modelo
	Controlador o-- Vista
```

#### Participantes
- **Controlador**: La clase que tiene la responsabilidad de manejar eventos y coordinar operaciones.
#### Principios de Diseño asociados
1. **Open/Close Principle ([[Open Close]])**: El Controlador facilita la extensión del sistema sin modificar el código existente. Por ejemplo, se pueden agregar nuevos tipos de solicitudes o nuevos componentes sin cambiar el Controlador, siempre y cuando se sigan las interfaces definidas.
2. **Dependency Inversion Principle ([[Inversión de Dependencia]])**: El Controlador promueve la inversión de dependencias al depender de abstracciones (interfaces) en lugar de implementaciones concretas. Esto facilita la flexibilidad y la modularidad del sistema.
3. **[[Encapsular la variabilidad]]**: El Controlador encapsula la lógica de control, lo que ayuda a minimizar el impacto de los cambios en el sistema.
4. **[[Favorecer composición antes que herencia]]**: El Controlador se compone de diferentes componentes que manejan las solicitudes, lo que promueve la composición sobre la herencia.
5. **[[Hollywood]]**: "No nos llames, nosotros te llamaremos". El Controlador promueve la inversión de control al manejar las solicitudes y dirigirlas al componente adecuado, en lugar de permitir que los componentes se llamen directamente entre sí.
6. **[[Modularidad, cohesión y acoplamiento]]**: El Controlador promueve la modularidad al centralizar la lógica de control y reducir el acoplamiento entre componentes.

#### Consecuencias
#### Ventajas
- **Separación de preocupaciones**: La lógica de negocio está separada de la interfaz de usuario.
- **Reutilización**: El controlador puede ser reutilizado en diferentes contextos.
- **Mantenimiento y evolución facilitados**: Cambios en la lógica de negocio tienen menos impacto en la interfaz de usuario y viceversa.
#### Desventajas
- Puede llevar a la creación de controladores grandes y complejos si no se gestiona adecuadamente.
#### Patrones Relacionados
- **Patrón de Diseño [[MVC]] (Model-View-Controller)**: Para separar la lógica de negocio, la interfaz de usuario y el control de flujo.
- **Patrón de Diseño [[Observer]]**: Para notificar cambios a otros objetos.
- **Patrón de Diseño [[Command]]**: Para encapsular solicitudes como objetos.
#### Código de ejemplo
``` java
public class Controlador{
	private Modelo modelo;
	private Vista vista;

	public Controlador(Modelo modelo, Vista vista){
		this.modelo = modelo;
		this.vista = vista;
	}

	public void manejarEvento(){
		// Logica para manejar el evento
		modelo.realizarOperacion();
		vista.actualizar();
	}
}

public class Modelo{
	public void realizarOperacion() {
		// Realizar Operacion
	}
}

public class Vista{
	public void actualizar(){
		// Actualizar
	}
}

```