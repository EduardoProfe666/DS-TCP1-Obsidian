## Descripción

•       Al diseñar piezas de alto nivel que interactuarán con piezas de más bajo nivel, se debe evitar las llamadas de estas últimas a las primeras, las piezas de más alto nivel deben mantenerse como coordinadoras, y no viceversa.

•       La programación de una aplicación en la que se adicionan plugins debe seguir ese principio, el plugin no debe interactuar con su contenedor, sino al revés.

El principio de Hollywood, también conocido como el principio de "No nos llame, nosotros le llamaremos", es un concepto en el diseño de software que se relaciona estrechamente con el principio de inversión de control (IoC) y el principio de inversión de dependencias (uno de los cinco principios SOLID). Este principio sugiere que las clases de alto nivel no deberían depender directamente de las clases de bajo nivel, sino que deberían ser las clases de alto nivel las que determinen cuándo y cómo se invocan las clases de bajo nivel. Esto se logra a menudo a través de la inyección de dependencias, donde las dependencias necesarias son suministradas a una clase desde fuera, en lugar de que la clase las busque activamente.

El principio de Hollywood promueve un diseño de software donde las decisiones sobre qué componentes interactúan y cómo se realizan estas interacciones son tomadas por componentes de alto nivel o frameworks, en lugar de por los componentes individuales de bajo nivel. Esto ayuda a mantener un bajo acoplamiento entre componentes, facilita la reutilización de código y mejora la flexibilidad y la escalabilidad del sistema.
## Ejemplo

Consideremos un sistema simple de registro de usuarios donde necesitamos enviar un correo electrónico de confirmación después de que un usuario se registra. Sin aplicar el principio de Hollywood, podríamos tener una clase `UserRegistration` que depende directamente de una clase `EmailSender` para enviar el correo electrónico:

``` java
class EmailSender {
	void sendConfirmationEmail(User user) {
		// Lógica para enviar correo electrónico de confirmación
	}
}

class UserRegistration {
	private EmailSender emailSender;

	UserRegistration(EmailSender emailSender){
		this.emailSender = emailSender;
	}

	void register(User user) {
		// Lógica de registro
		emailSender.sendConfirmationEmail(user);
	}
}
```

Este diseño viola el principio de Hollywood porque `UserRegistration` está activamente buscando y utilizando `EmailSender`.

Para adherirse al principio de Hollywood, podríamos refactorizar el código para que `UserRegistration` no dependa directamente de `EmailSender`, sino que reciba una referencia a un servicio de envío de correos electrónicos a través de la inyección de dependencias:
``` java
interface EmailService {
	void sendConfirmationEmail(User user);
}
class EmailSender implements EmailService {
	@Override
	void sendConfirmationEmail(User user) {
		// Lógica para enviar correo electrónico de confirmación
	}
}

class UserRegistration {
	private EmailService emailService;

	UserRegistration(EmailService emailService){
		this.emailService = emailService;
	}

	void register(User user) {
		// Lógica de registro
		emailService.sendConfirmationEmail(user);
	}
}
```

En este diseño, `UserRegistration` no sabe nada sobre `EmailSender`; solo sabe que necesita un `EmailService` para enviar correos electrónicos. La decisión de qué implementación específica de `EmailService` usar se toma en algún punto de alto nivel en la aplicación, posiblemente en el momento de la configuración del sistema, y se inyecta en `UserRegistration` a través del constructor. Esto permite cambiar fácilmente la implementación de `EmailService` sin modificar `UserRegistration`, siguiendo el principio de Hollywood.