## Descripción

- Este principio reconoce la separación de la interfaz abstracta de su implementación concreta.
- Parte de  la observación de que mientras las interfaces tienden a permanecer estables, las implementaciones pueden variar mucho, aparecer nuevas, modificarse formas existentes para ganar en una cualidad u otra como puede ser consumo de memoria o tiempo de respuesta.
## Ejemplo

Supongamos que estás desarrollando una aplicación que necesita enviar mensajes a través de diferentes medios, como correo electrónico y SMS. En lugar de codificar la lógica de envío de mensajes directamente en tu sistema, puedes definir una interfaz `MessageSender` que abstraiga esta funcionalidad:
``` java
interface MessageSender{
	void sendMessage(String message);
}
```

Luego, puedes crear implementaciones específicas para cada medio de comunicación:
``` java
class EmailSender implements MessageSender{
	@Override
	public void sendMessage(String message){
		// Lógica para enviar un correo electrónico
	}
}

class SMSSender implements MessageSender{
	@Override
	public void sendMessage(String message){
		// Lógica para enviar un SMS
	}
}
```

En tu sistema, en lugar de depender directamente de `EmailSender` o `SMSSender`, dependes de la interfaz `MessageSender`. Esto te permite cambiar fácilmente entre diferentes métodos de envío de mensajes o incluso agregar nuevos métodos en el futuro sin tener que modificar el código que utiliza `MessageSender`.
Por ejemplo, si tienes una clase `NotificationService` que necesita enviar mensajes:
``` java
class NotificationService {
	private MessageSender messageSender;

	public NotificationService(MessageSender message){
		this.messageSender = messagesender;
	}

	public void notify(String message){
		messageSender.sendMessage(message);
	}
}
```

Instanciar `NotificationService`, puedes pasarle cualquier objeto que implemente `MessageSender`, lo que te da la flexibilidad de cambiar entre diferentes formas de envío de mensajes simplemente cambiando la implementación pasada al constructor, sin necesidad de modificar el código de `NotificationService`.