## Veracidad

> Cuando tienes datos que no están bajo control, que vienen de diferentes sistemas y no puedes seleccionar los datos asegurando la calidad, tienes un problema de veracidad.

*Selección* es la acción o el proceso de seleccionar, organizar y cuidar los elementos de una colección.
*Integridad de los datos* es el mantenimiento y la garantía de la exactitud y la coherencia de los datos durante todo su ciclo de vida.
*Veracidad de los datos* es el grado de exactitud, precisión y fiabilidad de estos.

Secciones
- [El problema de la veracidad](#el-problema-de-la-veracidad)
- [¿Qué es la integridad de los datos?](#qu%C3%A9-es-la-integridad-de-los-datos)
- [Identificación de problemas de integridad de datos](#identificaci%C3%B3n-de-problemas-de-integridad-de-datos)
  - [Conocer si su aspecto es limpio](#conocer-si-su-aspecto-es-limpio)
  - [Conocer de dónde proceden los errores](#conocer-de-d%C3%B3nde-proceden-los-errores)
  - [Conocer el aspecto de los cambios aceptables](#conocer-el-aspecto-de-los-cambios-aceptables)
  - [Conocer si los datos originales tienen valor](#conocer-si-los-datos-originales-tienen-valor)
- [Esquemas de base de datos](#esquemas-de-base-de-datos)
  - [Esquema de datos](#esquema-de-datos)
  - [Esquema de información](#esquema-de-informaci%C3%B3n)
- [Coherencia de la base de datos](#coherencia-de-la-base-de-datos)
  - [Conformidad con ACID](#conformidad-con-acid)
  - [Conformidad con BASE](#conformidad-con-base)
  - [ACID vs BASE](#acid-vs-base)
- [ETL](#etl)
  - [Extracción de datos](#extracci%C3%B3n-de-datos)
  - [Transformación de datos](#transformaci%C3%B3n-de-datos)
  - [Carga de datos](#carga-de-datos)
  - [Servicios de AWS en el proceso ETL](#servicios-de-aws-en-el-proceso-etl)
    - [EMR vs. Glue](#emr-vs-glue)

### El problema de la veracidad
Los datos cambian con el tiempo. A medida que se transfieren de un proceso a otro, y a través de sistemas, hay probabilidad que la integridad de los datos se vea afectada de manera negativa. Hay que asegurarse de mantener un alto nivel de certeza que los datos que se analizan sean fiables.

### ¿Qué es la integridad de los datos?
Se refiere a asegurar que los datos sean fiables. Para asegurar la integridad es necesario asegurar cada paso del ciclo de vida de datos.

- *Creación* - se debe asegurar la exactitud desde la creación, para ello se requiere cierta confianza en los sistemas que recopilan datos, para ello se realizarán auditorias regulares, para asegurar que generan datos o archivos válidos y que los cambios no afectarán negativamente a la integridad del sistema. 
- *Adición* - los datos no siempre están añadidos, pero muchas veces para la analítica se requiere que las métricas estén bien definidas y se asegure la integridad de los datos agrupados.
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

- Orígenes internos o externos - es poco probable influir en los datos originados externamente, sin embargo, podemos recomendar mejores para los datos generados internamente.

Algunos procedimientos para identificar problemas de integridad de los datos son los siguientes
#### Conocer si su aspecto es limpio
Se debe establecer qué aspecto tienen los datos limpios, algunos consideran que los datos deben estar en su formato sin procesar, pero con reglas de negocio aplicadas. Otros opinan que los datos deben estar normalizados, agrupados. Se debe establecer el criterio para la organización.

#### Conocer de dónde proceden los errores
Al identificar un error, se debe hacer su seguimiento para identificar el origen. Ayudará a reducir futuros errores, también hará más eficiente la operación de los ETL.

#### Conocer el aspecto de los cambios aceptables
Son pequeños detalles que pueden marcar la diferencia, como consolidar estados de un registro, cómo poner un cero en una columna vacía.

#### Conocer si los datos originales tienen valor
Algunas veces los datos originales pierden su valor tras ser transformados, sin embargo, en datos regulados o muy volátiles se deben conservar en el destino.

### Esquemas de base de datos
Las bases de datos relacionales se basan en esquemas para organizar el contenido de estas y permite aplicar la integridad referencial y de dominio. 

#### Esquema de datos
Es el conjunto de metadatos usados por la base de datos para organizar los objetos y aplicar las restricciones de integridad. Una base de datos puede tener uno o varios esquemas.

Hay 2 tipos de esquemas:
- Lógicos - se centran en las restricciones que se aplican dentro de la base de datos, incluye la organización de tablas, vistas y comprobaciones de integridad. También puede proporcionar la integridad mediante restricciones sobre valores permitidos. Enumera las restricciones, las relaciones y las propiedades de las tablas y las vistas en una base de datos.
- Físicos - se centran en el almacenamiento real de los datos en disco o en el repositorio en la nube, se incluyen detalles sobre los archivos, índices, tablas con particiones, clústeres, etc. Permiten hacer estimaciones de espacio de almacenamiento, crecimiento potencial del sistema y hasta para la recuperación de desastres.

#### Esquema de información
Es una base de datos de metadatos que contienen información sobre todos los objetos de la base de datos, su finalidad es definir lo que son todos los objetos de la base de datos y registrar la información vital sobre ellos, como el nombre y tamaño de una tabla, sus índices y las restricciones sobre los datos de cada tabla, configuración de seguridad de los usuarios, recursos de datos externos y configuración de administración.

### Coherencia de la base de datos
Los dos métodos que implementan las bases de datos para mantener la veracidad de los datos almacenados son ACID y BASE.
- ACID: Atomicity (atomicidad), Consistency (coherencia), Isolation (aislamiento), Durability (durabilidad). Es un método para mantener la coherencia y la integridad en una base de datos estructurada.
- Atomicidad - o funciona o falla completamente.
- Coherencia - todas las transacciones proporcionan datos válidos.
- Aislamiento - una transacción no interfiera con otra transacción simultánea.
- Durabilidad - una vez hechos los cambios, estos se mantendrán.

- BASE: viene de Basically Available (disponibilidad básica) Soft state (estado temporal) Eventually consistent (coherencia final). Es un método para mantener la coherencia y la integridad en una base de datos estructurada o semiestructurada.
- Disponibilidad básica - permite que una instancia reciba una solicitud de cambio y lo haga inmediatamente. El sistema garantiza una respuesta para cada solicitud. Sin embargo, es posible que la respuesta sea un error o datos obsoletos por un cambio no replicado en todos los nodos.
- Estado temporal - se permite coherencia parcial entre las instancias distribuidas. También llamado *estado modificable*.
- Consistencia eventual - los datos son coherentes con el tiempo, el cambio terminará efectuándose en todas las copias, sin embargo, estarán disponibles aunque no se haya propagado el cambio.

#### Conformidad con ACID
Una transacción es una secuencia de instrucciones ejecutadas conjuntamente. El objetivo es devolver la versión más reciente de todos los datos y garantizar que los datos introducidos en el sistema cumplan con las reglas y restricciones en todo momento.

#### Conformidad con BASE
Soporta la integridad en bases de datos no relacionales, NoSQL. La principal preocupación de estas bases de datos es la disponibilidad de los datos frente a la coherencia de estos, los cambios en los datos están disponibles de inmediato en la instancia en que se han efectuado, sin embargo, la replicación puede tomar cierto tiempo en replicarse en las demás instancias.

#### ACID vs. BASE
| ACID | BASE |
|------|------|
| Coherencia fuerte | Coherencia débil. Los datos obsoletos son correctos. |
| El aislamiento es clave | La disponibilidad es clave |
| Centrado en los resultados confirmados | Resultados del mejor esfuerzo |
| Disponibilidad conservadora (pesimista) | Disponibilidad agresiva (optimista)|

#### DynamoDB implementa ACID
Se implementa la conformidad ACID en una o varias tablas de una sola cuenta y por una región de AWS.

### ETL
Extraer, transformar y cargar, es el proceso de recopilar datos de orígenes de datos sin procesar y transformarlos en un tipo común, luego se cargan a una ubicación final permitiendo la analítica e inspección de datos. 

#### Extracción de datos
Es probablemente la fase más importante, seguramente tendremos varias ubicaciones y varios tipos, registros de transacciones, bases de datos de productos, orígenes de datos públicos o flujos de aplicaciones.

- Se debe identificar dónde están los datos de origen (internos o externos)
- Se debe planificar cuándo se llevará a cabo la extracción.
- Planificar dónde se almacenarán los datos durante el proceso, conocida como ubicación de almacenamiento provisional.
- Con qué frecuencia debe repetirse la extracción.

#### Transformación de datos
Es convertir los datos a un formato uniforme que se pueda consultar. La limpieza de datos también se lleva a cabo en esta etapa. También se realizarán sustituciones de valores, en base a reglas de negocio.

#### Carga de datos
Elegir la ubicación para guardar los datos transformados. Puede ser una base de datos, un almacén de datos o un lago de datos.

#### Servicios de AWS en el proceso ETL
- Orígenes de datos en las instalaciones y en la nube - S3 para datos basados en archivos, RDS para datos transaccionales, Redshift para datos analíticos, DynamoDB para datos no relacionales.
- Actualizaciones de transmisiones o por lotes - la ingesta de datos se puede hacer con Kinesis si son datos tipo transmisión o para lotes se puede utilizar EMR o Glue.
- Lago de datos operativo - S3
- Almacenamiento de datos - se puede usar Redshift para almacenes de datos y mercados de datos.
- Informes y paneles - Quicksight permite hacer informes, Athena permite hacer consultas a la medida.
- Generación de informes - Elasticseach, Kibana nos dan la flexibilidad y capacidad de obtener información de conjuntos de datos más grandes.

##### EMR vs Glue
EMR es una plataforma robusta de recopilación y procesamiento de datos, si requiere conocimiento técnico y práctico. Permite crear una canalización más personalizada, los costes de infraestructura pueden ser inferiores respecto a Glue.

Glue es una herramienta ETL administrada, sin servidor, más simplificada que EMR. Es recomendado para tareas simples. Se puede utilizar como almacén de metadatos par los datos transformados mediante el catálogo.
