## Descripción

•       Al diseñar, se deben reconocer las partes que son variables, de aquellas que no varían, y separarse entre sí.

•       Las partes variables deben ser encapsuladas en piezas separadas de modo que las partes que no varían puedan estabilizarse rápidamente.

•       Esto favorece también los casos en que las partes variables, pueden incrementarse o cambiarse en el  tiempo.
## Ejemplo

Imagina que estás desarrollando un sistema de comercio electrónico que actualmente soporta pagos a través de tarjetas de crédito. Sabes que en el futuro podrías querer agregar más métodos de pago, como PayPal o transferencias bancarias.

En lugar de codificar la lógica de pago directamente en tu sistema, puedes encapsular la variabilidad creando una interfaz `PaymentMethod` y clases concretas para cada método de pago:

``` java
interface PaymentMethod {
	void pay(int amount);
}

class CreditCardPayment implements PaymentMethod {
	@Override
	public void pay(int amount) {
		// Lógica para pagar con tarjeta de crédito
	}
}

class PayPalPayment implements PaymentMethod {
	@Override
	public void pay(int amount) {
				// Lógica para pagar con PayPal
	}
}
```

De esta manera, cuando quieras agregar un nuevo método de pago, solo necesitas crear una nueva clase que implemente `PaymentMethod`, sin tener que modificar el código existente que utiliza este método de pago.