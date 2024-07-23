## Descripción

- El estilo al que pertenece es [[Flujo de Datos]]
- Organiza el sistema en capas con funcionalidad relacionada con cada capa. Una capa da servicios a la capa de encima, de modo que las capas de nivel inferior representan servicios núcleo que es probable se utilicen a lo largo de todo el sistema.
- El patrón arquitectónico de Capas ayuda a estructurar las aplicaciones que pueden ser descompuestas en grupos de subtareas en las que cada grupo de subtareas se encuentra a un nivel particular de abstracción.
- Se basa en una distribución jerárquica de los roles y las responsabilidades para proporcionar una división efectiva de los problemas a resolver.
- Los roles indican el tipo y la forma de la interacción con otras capas, y las responsabilidades la funcionalidad que implementan.
- 

	![[Pasted image 20240722221340.png]]

**Pasos para la implementación:**
1. Definir los niveles de abstracción para agrupar las tareas.
2. Determinar el número de capas.
3. Asignar tareas a las distintas capas.
4. Especificar los servicios de cada capa.
5. Refinar las capas iterando sobre los cuatro pasos anteriores, para reorganizar las tareas de modo que solo se invoque servicios de la capa inmediata inferior y que todo lo que está en una capa tenga el mismo nivel de abstracción.
6. Especificar la interfaz de cada capa.
7. Definir los patrones que se pueden usar para la estructura interna de cada capa.
8. Especificar la comunicación entre las capas.
9. Desacoplar las capas adyacentes para que las capas no sepan quién usa sus servicios.
10. Diseñar una estrategia de manejo de errores en la capa más baja posible.
## ¿Cuándo se usa?

- Al construirse nuevas facilidades encima de los sistemas existentes
- Cuando el desarrollo se dispersa a través de varios equipos de trabajo, y cada uno es responsable de una capa de funcionalidad
- Cuando exista un requerimiento para seguridad multinivel

## ¿Cómo se representa?

Existen 2 estrategias para la estratificación: Basado en Reutilización y Basado en Responsabilidad

#### Basado en Reutilización
- Es una manera de mostrar la aplicación cuando nuestro interés es ver la arquitectura como un todo y el lente por el que estamos mirando es la reutilización.
- Es un enfoque para la visualización, estructura lógica. no es la versión definitiva.
- La aplicación se muestra, en 4 capas, se logra ver la aplicación desplegada desde sus componentes más específicos hasta los más reutilizables del sistema operativo sobre el cual se despliega:
	1. **Capa Específica:** Muestra los elementos (paquetes o subsistemas) del sistema actual, que no son reutilizados, los mismos pueden ser de distintos niveles de responsabilidad, o sea de Presentación, Lógica de Negocio, Acceso a los Datos  o cualquier otra, simplemente tienen que cumplir con la cualidad de ser específicos, o sea ***no reutilizables.***
	2. **Capa General:** Muestra los elementos de cualquier nivel de responsabilidad (al igual que en la capa anterior) pero que son ***reutilizados***. Los elementos que se muestran en esta capa, forman parte también del sistema actual (al igual que los de la capa específica).
	3. **Capa Middleware o Intermedia:** Es empleada para mostrar los elementos, paquetes, subsistemas, que no son propios del sistema que se está desarrollando, sino de ***terceros***, es brindado por el entorno de desarrollo (.NET, PHP, C++, J2EE), o componentes descargados de Internet, o Sistemas Legados. ***Tecnologías****
	4. **Capa de Software del Sistema:**  ***Protocolos***, componentes y subsistemas que son  provistos por el propio ***sistema operativo.***

##### N-Capa de Eva
	![[N-Capa Reutilizacion Eva.png]]

##### N-Capa de Ejercicio Integrador
	![[NCapa Reutilizacion Ejercicio Integrador.png]]
	

##### N-Capa de Ejercicio Integrador
#### Basado en Responsabilidad

- Se sigue el principio de que las clases, subsistemas, paquetes que tenemos en nuestra aplicación, pueden ser ubicadas horizontalmente en un nivel específico de abstracción, junto a otras cuyas responsabilidades se encuentran al mismo nivel.
- La aplicación se muestra en 3 capas básicas:
	1. **Capa de Presentación:** Agrupan los elementos que tienen que ver con las interfaces de usuario que brinda el sistema, así como cierta lógica de la manipulación y generación de dichas interfaces de usuario, todo al nivel de cómo se ve o presenta la aplicación. En este nivel se ubican las clases Boundary, aunque no se excluyen derivaciones de parte de las responsabilidades que se podían asignar a las clases estereotipadas como Control.
	2. **Capa de Lógica del Negocio:** Agrupan clases, subsistemas y paquetes que contienen lógica del negocio en cuestión, implementan reglas del negocio, conocen  qué condiciones deben cumplirse para poder ejecutar cierta funcionalidad y qué elementos en la siguiente capa deben ser empleados para poder completar las peticiones del usuario. Este nivel se alimenta principalmente con las Clases Control.
	3. **Capa de Acceso a datos:** Se ubican las clases, subsistemas y paquetes que contienen la lógica para acceder al medio de almacenamiento persistente. Para cumplir con sus responsabilidades siempre emplean elementos tecnológicos brindados por el Entorno de Desarrollo, “Connection”, “Query”, “Command”, “DataSet” entre otros.  Este nivel se alimenta principalmente con las Clases “Entity”.

##### N-Capa de Ejemplo
	![[Pasted image 20240722222835.png]]

