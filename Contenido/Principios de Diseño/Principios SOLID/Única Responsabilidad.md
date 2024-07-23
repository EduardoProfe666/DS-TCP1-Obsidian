## Descripción

·      Una clase o función de una clase deben tener una única razón para cambiar.

·      Cuando tenemos una clase o una función, debemos analizar si existe más de una posible razón que puedan generar cambios a la misma, si es así, puede ser que esta se esté dedicando a más de un tipo de responsabilidad, con lo cual, será más probable que cambie a menudo, y será potencialmente menos reutilizable.
## Ejemplo

Consideremos una clase `Student` que inicialmente maneja tres responsabilidades diferentes: registrar estudiantes, calcular sus resultados y enviar correos electrónicos a los estudiantes. Esta clase viola el Principio de Responsabilidad Única ya que tiene múltiples responsabilidades. Para adherirse al SRP, deberíamos dividir esta clase en tres clases separadas, cada una manejando una sola responsabilidad. Al hacer esto, cada clase tiene ahora una única responsabilidad, lo que facilita su mantenimiento y modificación sin afectar otras partes del código.
