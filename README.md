¿Qué hace exactamente el bloque let...in en lenguaje M? ¿Por qué cada paso puede referenciar al anterior?

El bloque let...in define la estructura secuencial y de evaluación en M. La sección "let" es donde se declaran las variables o pasos de transformación sobre los datos. La sección "in" especifica la variable final que será devuelta como resultado de la consulta para ingresar al modelo de datos. Cada paso puede referenciar al anterior porque en M los datos se procesan como un flujo en cadena inmutable; cada función recibe como primer parámetro el identificador del paso previo, generando una secuencia de dependencias ordenada y trazable.

¿Por qué M es Case Sensitive y qué consecuencia práctica tiene? Dá un ejemplo de un error que esto puede causar.

El lenguaje M es Case Sensitive porque el motor de evaluación de Power Query distingue estrictamente entre letras mayúsculas y minúsculas en palabras clave, funciones, nombres de variables y encabezados de columna. La consecuencia práctica es que invocar una función o campo con variaciones en las mayúsculas o minúsculas impedirá que el motor lo reconozca. Por ejemplo, escribir "table.selectrows" en lugar de "Table.SelectRows" genera un error de sintaxis del tipo Expression.Error indicando que la función no fue reconocida. Del mismo modo, hacer referencia al campo "[Categoria]" con mayúscula inicial fallará si en la tabla original está definido como "[categoria]".

¿Cuál es la diferencia entre usar Text.Trim y Text.Clean en M?

La función Text.Trim se utiliza exclusivamente para remover los espacios en blanco visibles ubicados al inicio y al final de una cadena de texto, sin modificar los espacios intermedios. Por otro lado, la función Text.Clean se utiliza para eliminar caracteres invisibles no imprimibles o de control (como saltos de línea, tabulaciones o retornos de carro) habituales en archivos exportados desde sistemas legacy.

¿Por qué filtraste los registros "PRUEBA" después de estandarizar la categoría y no antes?

Filtrar los registros de prueba después de estandarizar la columna con Text.Proper es un paso crítico debido a que M es Case Sensitive. Si se hubiera aplicado el filtro excluyendo la palabra "Prueba" antes de estandarizar, los registros ingresados como "PRUEBA", "prueba" o variantes mixtas no habrían sido detectados y habrían permanecido en el dataset. Al ejecutar primero Text.Proper, todas las variaciones del texto se unificaron automáticamente al formato Title Case ("Prueba"), permitiendo filtrarlas y eliminarlas con total seguridad en un solo paso.
