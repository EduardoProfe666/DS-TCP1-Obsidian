## Descripción

- La funcionalidad del sistema se organiza en servicios y cada servicio lo entrega un servidor independiente. 
- El estilo al que pertenece es [[Llamada y Retorno]]
- Los clientes son usuarios de dichos servicios y para utilizarlos ingresan a los servidores.
- Un sistema que sigue el patrón cliente-servidor se organiza como un conjunto de servicios y servidores asociados, y de clientes que acceden y usan los servicios. Los principales componentes de este modelo son:
	1. **Un conjunto de servidores que ofrecen servicios a otros componentes.** Ejemplos de éstos incluyen servidores de impresión; servidores de archivo que brindan servicios de administración de archivos, y un servidor compilador, que proporciona servicios de compilación de lenguaje de programación.
	2. **Un conjunto de clientes que solicitan los servicios que ofrecen los servidores.** Habrá usualmente varias instancias de un programa cliente que se ejecuten de manera concurrente en diferentes computadoras.
	3. **Una red que permite a los clientes acceder a dichos servicios**. La mayoría de los sistemas cliente-servidor se implementan como sistemas distribuidos, conectados mediante protocolos de Internet.

	![[Pasted image 20240722215108.png]]
## ¿Cuándo se usa?

- Se usa cuando, desde varias ubicaciones, se tiene que ingresar a los datos en una base de datos compartida. Como los servidores se pueden replicar, también se usan cuando la carga de un sistema es variable.
## ¿Cómo se representa?

![[Pasted image 20240722215810.png]]