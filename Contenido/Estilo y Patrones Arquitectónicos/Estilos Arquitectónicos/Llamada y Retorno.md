### Descripción
- El sistema se constituye de un programa principal que tiene el control del sistema y varios subprogramas que se comunican con éste mediante el uso de llamadas
- Organizados jerárquicamente cada capa le presta servicios a la capa superior y es cliente de la capa inferior y en su misma capa.
- Descomposición de la estructura de un programa en principal y subprogramas donde el programa “principal” llama a un  número de componentes del programa, que pueden a su vez llamar a otros. Los componentes puede estar distribuidos en una red.
- Esta familia de estilos enfatiza la modificabilidad y la escalabilidad. 
- Son los estilos más generalizados en sistemas en gran escala. Miembros de la familia son las arquitecturas de programa principal y subrutina, los sistemas basados en llamadas a procedimientos remotos, los sistemas orientados a objeto y los sistemas jerárquicos en capas.

	![[Llamada y Retorno.png]]

### Patrones Asociados
- [[MVC]]
- [[N-Capas]]
- [[Cliente-Servidor]]
- [[Arquitectura Basada en Componentes]]

### Atributos Asociados
- Modificabilidad
- Escalabilidad 
- Desempeño
### Atributos en Conflicto
- Mantenibilidad
- Desempeño