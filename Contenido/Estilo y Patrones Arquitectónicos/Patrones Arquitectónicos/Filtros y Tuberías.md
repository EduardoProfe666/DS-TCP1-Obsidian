## Descripción

- El estilo al que pertenece es [[Flujo de Datos]]
- Provee la estructura y los mecanismos para los sistemas que deben procesar flujos de datos. Cada etapa del procesamiento es encapsulada en un filtro. 
- Los datos se transmiten a través de tubos entre filtros adyacentes. 
- Se pueden obtener familias de sistemas relacionados recombinando, eliminando y agregando filtros.
- Se basa en un patrón de tuberías y filtros (componentes con interfaces) que consta de un conjunto de componentes denominados “filtros” conectados entre si por “tuberías” que trasmiten los datos desde un componente a otro.
- Los filtros trabajan de manera independiente de los componentes que se encuentran antes o después. Las entradas y salidas tienen formatos específicos.
- El procesamiento de datos en un sistema se organiza de forma que cada componente de procesamiento (filtro) sea discreto y realice un tipo de transformación de datos. Los datos fluyen (como en una tubería) de un componente a otro para su procesamiento.
- Es simple de entender e implementar.
- Es posible implementar procesos complejos con editores gráficos de líneas de tuberías o con comandos de línea.
- Fuerza un procesamiento secuencial.
- Es fácil de envolver (wrap) en una transacción atómica.
- Los filtros se pueden empaquetar, y hacer paralelos o distribuidos
- Una desventaja adicional referida en la literatura sobre estilos concierne a que eventualmente pueden llegar a requerirse buffers de tamaño indefinido, por ejemplo en las tuberías de clasificación de datos.
- No aconsejado para cuando se necesita interactividad
- Problemas de performance ya que los datos se transmiten en forma completa entre filtros


	![[Pasted image 20240722220128.png]]


## ¿Cuándo se usa?

Se suele usar en aplicaciones de procesamiento de datos (tanto basada en lotes batch como en transacciones), donde las entradas se procesan en etapas separadas para generar salidas relacionadas. También se usa cuando:

- Se puede especificar la secuencia de un número conocido de pasos.
- No se requiere esperar la respuesta asincrónica de cada paso.
- Se busca que todos los componentes situados corriente abajo sean capaces de inspeccionar y actuar sobre los datos que vienen de arriba (pero no viceversa)

## ¿Cuándo NO se usa?

- Situaciones interactivas cuando se requieren actualizaciones incrementales de la representación en pantalla.
- La independencia de los filtros implica que es muy posible la duplicación de funciones de preparación que son efectuadas por otros filtros (por ejemplo, el control de corrección de un objeto de fecha).
- Se presentan construcciones condicionales, bucles y otras lógicas de control de flujo.

## ¿Cómo se representa?

#### Ejemplo de Conferencia

	![[Pasted image 20240722220304.png]]

#### Ejemplo mio

	![[Pasted image 20240722220319.png]]