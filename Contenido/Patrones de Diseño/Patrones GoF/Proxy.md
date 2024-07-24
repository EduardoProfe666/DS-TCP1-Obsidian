## Descripción
- Se le conoce también por `Surrogado`.
- Es un patrón `estructural`
- En Refactoring Guru está [aquí](./RefactoringGuru/Proxy.mhtml)

## Propósito

El objetivo principal del patrón Proxy es proporcionar un intermediario para otro objeto con el fin de controlar el acceso a ese objeto. Esto permite realizar acciones adicionales antes o después de que la solicitud llegue al objeto real.
**Proxy** es un patrón de diseño estructural que te permite proporcionar un sustituto o marcador de posición para otro objeto. Un proxy controla el acceso al objeto original, permitiéndote hacer algo antes o después de que la solicitud llegue al objeto original.
## ¿Cuándo aplicarlo?

- Inicialización diferida (proxy virtual). Es cuando tienes un objeto de servicio muy pesado que utiliza muchos recursos del sistema al estar siempre funcionando, aunque solo lo necesites de vez en cuando.
- En lugar de crear el objeto cuando se lanza la aplicación, puedes retrasar la inicialización del objeto a un momento en que sea realmente necesario.
- Control de acceso (proxy de protección). Es cuando quieres que únicamente clientes específicos sean capaces de utilizar el objeto de servicio, por ejemplo, cuando tus objetos son partes fundamentales de un sistema operativo y los clientes son varias aplicaciones lanzadas (incluyendo maliciosas).
- El proxy puede pasar la solicitud al objeto de servicio tan sólo si las credenciales del cliente cumplen ciertos criterios.
- Ejecución local de un servicio remoto (proxy remoto). Es cuando el objeto de servicio se ubica en un servidor remoto.
- En este caso, el proxy pasa la solicitud del cliente por la red, gestionando todos los detalles desagradables de trabajar con la red.
- Solicitudes de registro (proxy de registro). Es cuando quieres mantener un historial de solicitudes al objeto de servicio.
- El proxy puede registrar cada solicitud antes de pasarla al servicio.
- Resultados de solicitudes en caché (proxy de caché). Es cuando necesitas guardar en caché resultados de solicitudes de clientes y gestionar el ciclo de vida de ese caché, especialmente si los resultados son muchos.
- El proxy puede implementar el caché para solicitudes recurrentes que siempre dan los mismos resultados. El proxy puede utilizar los parámetros de las solicitudes como claves de caché.
- Referencia inteligente. Es cuando debes ser capaz de desechar un objeto pesado una vez que no haya clientes que lo utilicen.
- El proxy puede rastrear los clientes que obtuvieron una referencia del objeto de servicio o sus resultados. De vez en cuando, el proxy puede recorrer los clientes y comprobar si siguen activos. Si la lista del cliente se vacía, el proxy puede desechar el objeto de servicio y liberar los recursos subyacentes del sistema.
- El proxy también puede rastrear si el cliente ha modificado el objeto de servicio. Después, los objetos sin cambios pueden ser reutilizados por otros clientes.

## Representación

![[Pasted image 20240723181913.png]]
1. La **Interfaz de Servicio** declara la interfaz del Servicio. El proxy debe seguir esta interfaz para poder camuflarse como objeto de servicio.
2. **Servicio** es una clase que proporciona una lógica de negocio útil.
3. La clase **Proxy** tiene un campo de referencia que apunta a un objeto de servicio. Cuando el proxy finaliza su procesamiento (por ejemplo, inicialización diferida, registro, control de acceso, almacenamiento en caché, etc.), pasa la solicitud al objeto de servicio. Normalmente los proxies gestionan el ciclo de vida completo de sus objetos de servicio.
4. El **Cliente** debe funcionar con servicios y proxies a través de la misma interfaz. De este modo puedes pasar un proxy a cualquier código que espere un objeto de servicio.
## Participantes

- **Subject**: Define la interfaz común para RealSubject y Proxy, de modo que un Proxy puede ser utilizado en cualquier lugar donde se espera un RealSubject.
- **RealSubject**: Define el objeto real que el Proxy representa.
- **Proxy**: Mantiene una referencia que permite al Proxy acceder al RealSubject. Proporciona una interfaz idéntica a la de RealSubject y puede ser responsable de crear y eliminar RealSubject.

## Principios de diseño relacionados
 - _Principio de abierto/cerrado_ ([[Open Close]]). Puedes introducir nuevos proxies sin cambiar el servicio o los clientes.
 - **Inversión de Dependencias ([[Inversión de Dependencias]])**: El patrón Proxy puede ser visto como una aplicación del DIP, ya que el cliente que necesita acceder al objeto real depende de una abstracción (la interfaz común entre el Proxy y el objeto real) en lugar de una implementación concreta. Esto permite que el cliente sea independiente de cómo se gestiona el acceso al objeto.


## Ventajas
- Puedes controlar el objeto de servicio sin que los clientes lo sepan.
-  Puedes gestionar el ciclo de vida del objeto de servicio cuando a los clientes no les importa.
-  El proxy funciona incluso si el objeto de servicio no está listo o no está disponible.
-  _Principio de abierto/cerrado_. Puedes introducir nuevos proxies sin cambiar el servicio o los clientes.
- Permite controlar el ciclo de vida de los objetos reales.
- Puede realizar optimizaciones, como la carga diferida o el almacenamiento en caché.
- Puede añadir funcionalidades adicionales, como el control de acceso o el registro de solicitudes.

## Desventajas
- El código puede complicarse ya que debes introducir gran cantidad de clases nuevas.
-  La respuesta del servicio puede retrasarse.
- Puede introducir una capa adicional de abstracción, lo que puede complicar el diseño.
- Puede ser menos eficiente que una solución directa, debido a las llamadas adicionales a través del proxy.

## Código
``` pascal
// La interfaz de un servicio remoto.
interface ThirdPartyYouTubeLib is
    method listVideos()
    method getVideoInfo(id)
    method downloadVideo(id)

// La implementación concreta de un conector de servicio. Los
// métodos de esta clase pueden solicitar información a YouTube.
// La velocidad de la solicitud depende de la conexión a
// internet del usuario y de YouTube. La aplicación se
// ralentizará si se lanzan muchas solicitudes al mismo tiempo,
// incluso aunque todas soliciten la misma información.
class ThirdPartyYouTubeClass implements ThirdPartyYouTubeLib is
    method listVideos() is
        // Envía una solicitud API a YouTube.

    method getVideoInfo(id) is
        // Obtiene metadatos de algún video.

    method downloadVideo(id) is
        // Descarga un archivo de video de YouTube.

// Para ahorrar ancho de banda, podemos guardar en caché
// resultados de la solicitud durante algún tiempo, pero se
// puede colocar este código directamente dentro de la clase de
// servicio. Por ejemplo, puede haberse proporcionado como parte
// de la biblioteca de un tercero y/o definido como `final`. Por
// eso colocamos el código de almacenamiento en caché dentro de
// una nueva clase proxy que implementa la misma interfaz que la
// clase servicio. Delega al objeto de servicio únicamente
// cuando deben enviarse las solicitudes reales.
class CachedYouTubeClass implements ThirdPartyYouTubeLib is
    private field service: ThirdPartyYouTubeLib
    private field listCache, videoCache
    field needReset

    constructor CachedYouTubeClass(service: ThirdPartyYouTubeLib) is
        this.service = service

    method listVideos() is
        if (listCache == null || needReset)
            listCache = service.listVideos()
        return listCache

    method getVideoInfo(id) is
        if (videoCache == null || needReset)
            videoCache = service.getVideoInfo(id)
        return videoCache

    method downloadVideo(id) is
        if (!downloadExists(id) || needReset)
            service.downloadVideo(id)

// La clase GUI, que solía trabajar directamente con un objeto
// de servicio, permanece sin cambios siempre y cuando trabaje
// con el objeto de servicio a través de una interfaz. Podemos
// pasar sin riesgo un objeto proxy en lugar de un objeto de
// servicio real, ya que ambos implementan la misma interfaz.
class YouTubeManager is
    protected field service: ThirdPartyYouTubeLib

    constructor YouTubeManager(service: ThirdPartyYouTubeLib) is
        this.service = service

    method renderVideoPage(id) is
        info = service.getVideoInfo(id)
        // Representa la página del video.

    method renderListPanel() is
        list = service.listVideos()
        // Representa la lista de miniaturas de los videos.

    method reactOnUserInput() is
        renderVideoPage()
        renderListPanel()

// La aplicación puede configurar proxies sobre la marcha.
class Application is
    method init() is
        aYouTubeService = new ThirdPartyYouTubeClass()
        aYouTubeProxy = new CachedYouTubeClass(aYouTubeService)
        manager = new YouTubeManager(aYouTubeProxy)
        manager.reactOnUserInput()
```