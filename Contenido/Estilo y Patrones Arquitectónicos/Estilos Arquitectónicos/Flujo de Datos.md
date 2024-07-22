### Descripción
- El dato ingresa en el sistema, y fluye entre los componentes, de uno en uno, hasta que se le asigne un destino final (salida o repositorio)
- Provee la estructura y los mecanismos para los sistemas que deben procesar flujos de datos. 
- Cada etapa del procesamiento es encapsulada en un filtro.
- Los datos se transmiten a través de tubos entre filtros adyacentes. 
- Se pueden obtener familias de sistemas relacionados recombinando, eliminando y agregando filtros.
- Se basa en un patrón de tuberías y filtros (componentes con interfaces) que consta de un conjunto de componentes denominados “filtros” conectados entre si por “tuberías” que trasmiten los datos desde un componente a otro.
- Los filtros trabajan de manera independiente de los componentes que se encuentran antes o después. Las entradas y salidas tienen formatos  específicos.

### Patrones Asociados
- [[Filtros y Tuberías]]

### Atributos Asociados
- Reusabilidad
- Modificabilidad
- Mantenibilidad

### Atributos en conflictos
- Desempeño