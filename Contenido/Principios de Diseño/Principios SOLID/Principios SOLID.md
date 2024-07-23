- ## Principios SOLID
	- ### [[Inversión de Dependencia]]
	- ### [[Open Close]]
	- ### [[Segregación de Interfaces]]
	- ### [[Sustitución de Liskov]]
	- ### [[Única Responsabilidad]]

### Ver principios SOLID en Conferencia 4 de [[Conferencias]]

**¿Qué son los principios SOLID?**
Los principios SOLID son un conjunto de cinco principios de diseño de software que fueron introducidos por Robert C. Martin (también conocido como Uncle Bob) y que ayudan a crear código más mantenible, flexible y fácil de entender. Estos principios son fundamentales en el desarrollo de software orientado a objetos y se utilizan para mejorar la calidad del código al facilitar su mantenimiento, extensión y refactorización. Aquí están los cinco principios SOLID:

1. **Single Responsibility Principle (SRP)**
   - *Principio de Responsabilidad Única*: Una clase debe tener una sola razón para cambiar, lo que significa que debe tener solo una responsabilidad. Esto ayuda a mantener las clases enfocadas y reduce su complejidad.

2. **Open/Closed Principle (OCP)**
   - *Principio Abierto/Cerrado*: Las entidades de software (clases, módulos, funciones, etc.) deben estar abiertas para la extensión pero cerradas para la modificación. Esto significa que se pueden agregar nuevas funcionalidades sin cambiar el código existente.

3. **Liskov Substitution Principle (LSP)**
   - *Principio de Sustitución de Liskov*: Las clases derivadas deben ser sustituibles por sus clases base. Esto asegura que los objetos de una clase derivada puedan ser utilizados en lugar de los objetos de la clase base sin alterar la corrección del programa.

4. **Interface Segregation Principle (ISP)**
   - *Principio de Segregación de la Interfaz*: Los clientes no deben ser forzados a depender de interfaces que no utilizan. En lugar de tener una interfaz grande y monolítica, es mejor tener varias interfaces más pequeñas y específicas.

5. **Dependency Inversion Principle (DIP)**
   - *Principio de Inversión de Dependencia*: Los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deben depender de abstracciones. Además, las abstracciones no deben depender de detalles; los detalles deben depender de abstracciones.

Estos principios ayudan a los desarrolladores a escribir código que es más fácil de mantener, testear y extender, y que se adapta mejor a los cambios en los requisitos del sistema.