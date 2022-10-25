## Veracidad

> Cuando tienes datos que no están bajo control, que vienen de diferentes sistemas y no puedes seleccionar los datos asegurando la calidad, tienes un problema de veracidad.

*Selección* es la acción o el proceso de seleccionar, organizar y cuidar los elementos de una colección.
*Integridad de los datos* es el mantenimiento y la garantía de la exactitud y la coherencia de los datos durante todo su ciclo de vida.
*Veracidad de los datos* es el grado de exactitud, precisión y fiabilidad de los mismos.

Secciones
- [El problema de la veracidad](#el-problema-de-la-veracidad)
- [¿Qué es la intgridad de los datos?](#qu%C3%A9-es-la-integridad-de-los-datos)
- [Identificación de problemas de integridad de datos](#identificaci%C3%B3n-de-problemas-de-integridad-de-datos)

### El problema de la veracidad
Los datos cambian con el tiempo. A medida que se transfieren de un proceso a otro, y a través de sistemas, hay probabilidad que la integridad de los datos se vea afectada de manera negativa. Hay que asegurarse de mantener un alto nivel de certeza que los datos que se analizan sean fiables.

### ¿Qué es la integridad de los datos?
Se refiere a asegurar que los datos sean fiables. Para asegurar la integridad es necesario asegurar cada paso del ciclo de vida de datos.

- *Creación* - se debe asegurar la exactitud desde la creación, para ello se requiere cierta confianza en los sistemas que recopilan datos, para ello se realizarán auditorias regulares, para asegurar qye generan datos o archivos válidos y que los cambios no afectarán negativamente a la integridad del sistema. 
- *Adición* - los datos no siempre están añadidos, pero muchas veces para la análitica se requiere que las métricas estén bien definidas y se asegure la integridad de los datos agrupados.
- *Almacenamiento* - esta fase es de las más estables, hay que asegurar que los datos sean actualizados solo por quienes estén autorizados y los datos que deben permanecer estables nunca cambien.
- *Acceso*- los datos están disponibles en modo lectura, estos datos se reflejarán en informes y tableros de control.
- *Uso compartido* - Dar acceso a través de distintas herramientas a los informes preparados, si los consumidores no ven las cifras que esperan cuestionarán la validez de los datos.
- *Archivado* - llega un momento donde los datos ya no tengan valor, se pueden eliminar o agrupar para guardar estadísticas.

La *limpieza de datos* es el proceso de detectar y corregir datos corruptos.
La *integridad referencial* es el proceso de garantizar que se aplican las restricciones de las relaciones de la tabla. Garantiza que ambos miembros de una relación permanezcan coherentes.
La *integridad del dominio* es el proceso de garantizar que los datos que se especifican en un campo coinciden con el tipo de datos definido para ese proceso.
La *integridad de la entidad* es el proceso de garantizar que los valores almacenados en un campo coinciden con las restricciones definidas para ese campo. Garantiza que los valores de un campo permanezcan coherentes.

### Identificación de problemas de integridad de datos
Para asegurar la integridad de los datos, buscaremos potenciales orígenes de problemas de integridad de los datos.

- Orígenes internos o externos - es poco probable influir en los datos originados externamente, sin embargo podemos recomendar mejores para los datos generados internamente.

Algunos procedimientos para identificar problemas de integridad de los datos son los siguientes
#### Conocer si su aspecto es limpio
Se debe establecer qué aspecto tienen los datos limpios, algunos consideran que los datos deben estar en su formato sin procesar pero con reglas de negocio aplicadas. Otros opinan que los datos deben estar normalizados, agrupados. Se debe establecer el criterio para la organización.

#### Conocer de dónde proceden los errores
Al identificar un error, se debe hacer su seguimiento para identificar el origen. Ayudará a reducir futuros errores, también hara más eficiente la operación de los ETL.

#### Conocer el aspecto de los cambios aceptables
Son pequeños detalles que pueden marcar la diferencia, como consolidar estados de un registro, cómo poner un cero en una columna vacía.

#### Conocer si los datos originales tienen valor
Algunas veces los datos originales pierden su valor tras ser transformados, sin embargo en datos regulados o muy volátiles se deben conservar en el destino.

### Esquemas de base de datos
Las bases de datos relacionales se basan en esquemas para organizar el contenido de las mismas y permite aplicar la integridad referencial y de dominio. 

#### Esquema de datos
Es el conjunto de metadatos usados por la base de datos para organizar los objetos y aplicar las restricciones de integridad. Una base de datos puede tener uno o varios esquemas.

Hay 2 tipos de esquemas:
- Lógicos - se centran en las restricciones que se aplican dentro de la base de datos, incluye la organización de tablas, vistas y comprobaciones de integridad. También puede proporcionar la integridad mediante restricciones sobre valores permitidos. Enumera las restricciones, las relaciones y las propiedades de las tablas y las vistas en una base de datos.
- Físicos - se centran en el almacenamiento real de los datos en disco o en el repositorio en la nube, se incluyen detalles sobre los archivos, índices, tablas con particiones, clústeres, etc. Permiten hacer estimacioens de espacio de almacenamiento, crecimiento potencial del sistema y hasta para la recuperación de desastres.

#### Esquema de información
Es una base de datos de metadatos que contienen información sobre todos los objetos de la base de datos, su finaildad es definir lo que son todos los objetos de la base de datos y registrar la información vital sobre ellos, como el nombre y tamaño de una tabla, sus índices y las restricciones sobre los datos de cada tabla, configuración de seguridad de los usuarios, recursos de datos externos y configuración de administración.


