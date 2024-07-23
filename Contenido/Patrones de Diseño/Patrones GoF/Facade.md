## Descripción
- Se le conoce también por `Fachada` 
- Es un patrón `estructural`
- En Refactoring Guru está [aquí](./RefactoringGuru/Facade.mhtml)

## Propósito

**Facade** es un patrón de diseño estructural que proporciona una interfaz simplificada a una biblioteca, un framework o cualquier otro grupo complejo de clases.
## ¿Cuándo aplicarlo?

1. Comprueba si es posible proporcionar una interfaz más simple que la que está proporcionando un subsistema existente. Estás bien encaminado si esta interfaz hace que el código cliente sea independiente de muchas de las clases del subsistema.
2. Declara e implementa esta interfaz en una nueva clase fachada. La fachada deberá redireccionar las llamadas desde el código cliente a los objetos adecuados del subsistema. La fachada deberá ser responsable de inicializar el subsistema y gestionar su ciclo de vida, a no ser que el código cliente ya lo haga.
3. Para aprovechar el patrón al máximo, haz que todo el código cliente se comunique con el subsistema únicamente a través de la fachada. Ahora el código cliente está protegido de cualquier cambio en el código del subsistema. Por ejemplo, cuando se actualice un subsistema a una nueva versión, sólo tendrás que modificar el código de la fachada.
4. Si la fachada se vuelve [demasiado grande](https://refactoring.guru/es/smells/large-class), piensa en extraer parte de su comportamiento y colocarlo dentro de una nueva clase fachada refinada.
## Representación

![[Pasted image 20240723193637.png]]
1. El patrón **Facade** proporciona un práctico acceso a una parte específica de la funcionalidad del subsistema. Sabe a dónde dirigir la petición del cliente y cómo operar todas las partes móviles.
2. Puede crearse una clase **Fachada Adicional** para evitar contaminar una única fachada con funciones no relacionadas que podrían convertirla en otra estructura compleja. Las fachadas adicionales pueden utilizarse por clientes y por otras fachadas.
3. El **Subsistema Complejo** consiste en decenas de objetos diversos. Para lograr que todos hagan algo significativo, debes profundizar en los detalles de implementación del subsistema, que pueden incluir inicializar objetos en el orden correcto y suministrarles datos en el formato adecuado. Las clases del subsistema no conocen la existencia de la fachada. Operan dentro del sistema y trabajan entre sí directamente.
4. El **Cliente** utiliza la fachada en lugar de invocar directamente los objetos del subsistema.
## Participantes

- **Facade**: Conoce qué clases del subsistema son responsables de una solicitud y delega las solicitudes del cliente a los objetos apropiados del subsistema.
- **Subsystem Classes**: Implementan la funcionalidad del subsistema y manejan el trabajo asignado por el objeto Facade. No tienen conocimiento del Facade y no mantienen referencias a él.
## Principios de diseño relacionados

1. **Principio de Responsabilidad Única ([[Única Responsabilidad]])**: El patrón Facade promueve el SRP al asignar la responsabilidad de proporcionar una interfaz simplificada a una clase separada. Esto ayuda a mantener las clases enfocadas en una sola responsabilidad, lo que facilita la mantenibilidad y la reutilización del código.
2. **Inversión de Dependencias ([[Inversión de Dependencias]])**: El patrón Facade puede ser visto como una aplicación del DIP, ya que el cliente que necesita utilizar el subsistema depende de una abstracción (la interfaz Facade) en lugar de una implementación concreta. Esto permite que el cliente sea independiente de cómo se implementa el subsistema.
3. **Principio de Abierto/Cerrado ([[Open Close]])**: El patrón Facade promueve el OCP al permitir que las clases sean extendidas para soportar nuevas funcionalidades sin modificar el código existente. Esto se logra mediante la introducción de nuevas clases que implementan la interfaz Facade.

## Ventajas

- Puedes aislar tu código de la complejidad de un subsistema.
- Proporciona una interfaz simplificada para un subsistema complejo, facilitando su uso.
- Promueve un acoplamiento débil entre el subsistema y los clientes.
- Puede servir como un punto de entrada para encapsular el subsistema y evitar la proliferación de dependencias.
## Desventajas

 - Una fachada puede convertirse en [un objeto todopoderoso](https://refactoring.guru/es/antipatterns/god-object) acoplado a todas las clases de una aplicación.
 - Puede ocultar la flexibilidad y la granularidad del subsistema, lo que puede dificultar la realización de operaciones específicas.
## Código
``` pascal
// Estas son algunas de las clases de un framework de conversión
// de video de un tercero. No controlamos ese código, por lo que
// no podemos simplificarlo.

class VideoFile
// ...

class OggCompressionCodec
// ...

class MPEG4CompressionCodec
// ...

class CodecFactory
// ...

class BitrateReader
// ...

class AudioMixer
// ...

// Creamos una clase fachada para esconder la complejidad del
// framework tras una interfaz simple. Es una solución de
// equilibrio entre funcionalidad y simplicidad.
class VideoConverter is
    method convert(filename, format):File is
        file = new VideoFile(filename)
        sourceCodec = (new CodecFactory).extract(file)
        if (format == "mp4")
            destinationCodec = new MPEG4CompressionCodec()
        else
            destinationCodec = new OggCompressionCodec()
        buffer = BitrateReader.read(filename, sourceCodec)
        result = BitrateReader.convert(buffer, destinationCodec)
        result = (new AudioMixer()).fix(result)
        return new File(result)

// Las clases Application no dependen de un millón de clases
// proporcionadas por el complejo framework. Además, si decides
// cambiar los frameworks, sólo tendrás de volver a escribir la
// clase fachada.
class Application is
    method main() is
        convertor = new VideoConverter()
        mp4 = convertor.convert("funny-cats-video.ogg", "mp4")
        mp4.save()
```