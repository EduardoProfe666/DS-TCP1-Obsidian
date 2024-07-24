## Descripción
- Se le conoce también por `Intérprete`.
- Es un patrón `de comportamiento`

## Propósito

El objetivo principal del patrón Interpreter es definir una gramática para un lenguaje y proporcionar un mecanismo para interpretar sentencias en ese lenguaje. Esto es útil para crear lenguajes específicos de dominio (DSL) y para implementar intérpretes de comandos o expresiones.

## ¿Cuándo aplicarlo?

El patrón Interpreter se utiliza en diversas aplicaciones, como:
- Compiladores y analizadores léxicos.
- Intérpretes de comandos en sistemas operativos.
- Procesadores de lenguaje natural.
- Herramientas de modelado y simulación
## Representación

![[Pasted image 20240723190027.png]]
## Participantes

1. **AbstractExpression**: Define una interfaz para todos los nodos de expresión.
2. **TerminalExpression**: Implementa una operación asociada con los símbolos terminales de la gramática.
3. **NonTerminalExpression**: Implementa una operación asociada con los símbolos no terminales de la gramática.
4. **Context**: Contiene información global para el intérprete.
5. **Client**: Construye el árbol de expresiones abstractas que representan la gramática definida por el patrón.
## Principios de diseño relacionados

1. **Principio de Responsabilidad Única ([[Única Responsabilidad]])**: El patrón Interpreter promueve el SRP al asignar la responsabilidad de interpretar una parte específica de la gramática a una clase separada. Esto ayuda a mantener las clases enfocadas en una sola responsabilidad, lo que facilita la mantenibilidad y la reutilización del código.
2. **Desacoplamiento ([[Modularidad, Cohesión y Acoplamiento]])**: El patrón Interpreter ayuda a desacoplar el cliente de las reglas gramaticales específicas que se están utilizando. Esto facilita la modificación de las reglas gramaticales sin afectar el código que depende de ellas.
3. **Principio de Abierto/Cerrado ([[Open Close]])**: El patrón Interpreter promueve el OCP al permitir que las clases sean extendidas para soportar nuevas reglas gramaticales sin modificar el código existente. Esto se logra mediante la introducción de nuevas clases que implementan las reglas gramaticales.

## Ventajas

1. **Flexibilidad**: El patrón Interpreter permite definir y modificar gramáticas de manera flexible. Esto es especialmente útil para lenguajes específicos de dominio (DSL) que pueden evolucionar con el tiempo.
2. **Extensibilidad**: Es fácil agregar nuevos tipos de expresiones al sistema sin afectar las existentes. Esto facilita la extensión de la gramática y las funcionalidades del lenguaje.
3. **Mantenibilidad**: La estructura modular del patrón facilita el mantenimiento del código. Cada expresión es una clase independiente, lo que hace que el código sea más fácil de entender y mantener.
4. **Reutilización**: Las expresiones pueden ser reutilizadas en diferentes contextos, lo que reduce la redundancia y mejora la eficiencia del código.
5. **Separación de Responsabilidades**: El patrón promueve la separación de responsabilidades al mantener la lógica de interpretación separada de la lógica de negocio, lo que mejora la claridad y la organización del código.
## Desventajas

1. **Complejidad**: Para gramáticas muy grandes o complejas, el patrón Interpreter puede introducir una complejidad significativa. El mantenimiento y la comprensión del código pueden volverse desafiantes.
2. **Rendimiento**: La interpretación de expresiones puede ser menos eficiente que otras formas de procesamiento, especialmente si se realizan muchas operaciones de interpretación en un bucle o en un contexto de alto rendimiento.
3. **Escalabilidad**: A medida que la gramática se vuelve más compleja, el número de clases y objetos involucrados puede aumentar, lo que puede afectar la escalabilidad del sistema.
4. **Dificultad en la Depuración**: Debido a la naturaleza modular del patrón, depurar el código puede ser más difícil, especialmente cuando se trata de errores en la interpretación de expresiones complejas.
5. **Curva de Aprendizaje**: Para desarrolladores que no están familiarizados con el patrón Interpreter, puede haber una curva de aprendizaje significativa para entender y aplicar correctamente el patrón en un proyecto.
## Código
``` java
// AbstractExpression
interface Expresion{
	int interpret(Context context);
}

// TerminalExpression
class NumberExpression implements Expression {
	private int number;

	public NumberExpression(int number){
		this.number = number;
	}

	@Override
	public int interpret(Context context){
		return number;
	}
}

// NonTerminalExpression
class AddExpression implements Expression {
	private Expression leftExpression;
	private Expression rightExpression;

	public AddExpression(Expression leftExpression, Expression rightExpression){
		this.leftExpression = leftExpression;
		this.rightExpression = rightExpression;
	}

	@Override
	public int interpret(Context context){
		return leftExpression.interpret(context) + rightExpression(context);
	}
}

class Context{
	// Puede contener informacion global si es necesario
}

// Client
class InterpreterExample{
	public static void main(String[] args){
		Context context = new Context();

		// Construir el arbol de expresiones
		Expression expression = new AddExpression(
			new NumberExpression(10),
			new NumberExpression(20)
		);

		// Interpretar la expresion
		int result = expression.interpret(context);
		System.out.println("Resultado: " + result); // Resultado: 30	
	}
}
	
```