## Descripción

•       Principio de subdivisión de Interfaces: Los clientes no deberían depender de interfaces que no emplean.

•       Las interfaces deberían ser tan pequeñas como sea posible, de modo que mantengan la cohesión de las funciones que declaran.

•       Si una misma interfaz es empleada por más de un tipo de cliente, y cada uno tiene sus necesidades separadas, posiblemente la solución será dividir esta interfaz “gruesa” en dos para hacer cada una de las nuevas interfaces ajustada a las necesidades de su cliente.

## Ejemplo

Imagina que tienes una interfaz `Printer` que define métodos para imprimir, escanear y faxear documentos:

``` java
interface Printer {
	void print(Document document);
	void scan(Document document);
	void fax(Document document);
}
```

Una clase `Photocopier` que implementa `Printer` solo necesita los métodos `print` y `scan`, pero no fax. Esto viola el ISP porque `Photocopier` está forzado a depender de un método (`fax`) que no utiliza.

Para adherirse al ISP, podríamos dividir la interfaz `Printer` en interfaces más específicas:

``` java
interface Printer {
	void print(Document document);
}
interface Scanner {
	void scan(Document document);
}
interface Fax {
	void fax(Document document);
}
```

Ahora, `Photocopier` solo necesita implementar `Printer` y `Scanner`, sin verse forzado a depender de `Fax`:

``` java
class Photocopier implements Printer, Scanner {
	@Override
	public void print(Document document){
		// Lógica para imprimir
	}
	@Override
	public void scan(Document document){
		// Lógica para escanear
	}
}
```