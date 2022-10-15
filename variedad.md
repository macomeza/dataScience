# Variedad
> Cuando la organización está *abrumada* por la gran cantidad de fuentes de datos que se deben analizar y no encuentra sistemas para llevar a cabo la analítica, tenemos un problema de variedad.

Se dice que hay tantos tipos de datos como personas. 
Secciones
- [Tipos de orígenes de datos](#tipos-de-or%C3%ADgenes-de-datos)
  - [Datos estructurados](#datos-estructurados)
  - [Datos semiestructurados](#datos-semiestructurados)
  - [Datos no estructurados](#datos-no-estructurados)
  - [Desafíos asociados](#desaf%C3%ADos-asociados-a-la-variedad)
- [Almacenes de datos estructurados](#almacenes-de-datos-estructurados)
  - [Datos de archivo plano](#datos-de-archivo-plano)
  - [Base de datos relacionales](#bases-de-datos-relacionales)
  - [Tipos de sistemas de información](#tipos-de-sistemas-de-informaci%C3%B3n)
    - [Bases de datos OLTP](#bases-de-datos-oltp)
    - [Bases de datos OLAP](#bases-de-datos-olap)
    - [Comparación de OLTP y OLAP](#comparaci%C3%B3n-de-oltp-y-olap)
  - [Indexación por filas y por columnas](#indexaci%C3%B3n-de-datos-por-filas-y-por-columnas)
  - [Amazon RDS](#amazon-rds)
  - [Amazon Redshift](#amazon-redshift)
  - [Ventajas y desventajas de las bases de datos relacionales](#ventajas-y-desventajas-de-las-bases-de-datos-relacionales)
- [Bases de datos no relacionales](#bases-de-datos-no-relacionales) 
  - [Cambios de esquema en bases de datos relacionales y no relacionales](#cambios-de-esquema-en-bases-de-datos-relacionales-y-no-relacionales)
  - [Tipos de bases de datos no relacionales](#tipos-de-bases-de-datos-no-relacionales) 
    - [Documentos](#documentos)
    - [Valor de clave](#valor-de-clave)
      - [Amazon DynamoDB](#amazon-dynamodb)
    - [Grafos](#grafos)
      - [Amazon Neptune](#amazon-neptune)
- [Ventajas y desventajas de las bases de datos no relacionales](#ventajas-y-desventajas-de-las-bases-de-datos-no-relacionales)
- [Comparación entre bases de datos relacionales y no relacionales](#comparaci%C3%B3n-entre-bases-de-datos-relacionales-y-no-relacionales)

## Tipos de orígenes de datos
> Los datos estructurados facilitan el análisis de datos, pero no son flexible. Los semiestructurados pueden necesitar preprocesamiento, pero son muy flexibles. Los no estructurados tienen todo lo que necesitamos, pero en medio de muchas cosas que no nos sirven.
> El 10% de los datos es estructurado, otro 10% es semiestructurado y 80% es no estructurado.

### Datos estructurados
Se almacenan en formato tabular, lo más común es almacenar dentro de un sistema de gestión de bases de datos. Tienen un esquema llamado modelo relacional que permite definir su estructura y los elementos que forman parte de cada tabla y se indica si tiene relación con otras tablas. Una tabla está formada de varias columnas y cada registro individual se almacena en filas. Permite realizar muchas operaciones de escritura y actualización de datos transaccionales. Permite muchas operaciones de lectura para bases de datos analíticas. Cuando se requiere realizar ajustes al esquema es complicado pues requiere actualizar todos los registros de una tabla.

### Datos semiestructurados
Se almacenan como elementos y atributos, en una base de datos no relacional, sin esquemas predefinidos y se puede almacenar en archivos. Cada archivo tiene su propio esquema o estructura, esto le permite ser altamente flexible. No se pueden unir archivos entre sí.

### Datos no estructurados
Se almacena en archivos, no tiene esquema predefinido, puede ser un archivo de cualquier tipo y cualquier contenido. Estos archivos siempre se deben preprocesar y se requiere de un servicio para añadir etiquetas a cada archivo o bien realizar un catálogo de datos.

## Desafíos asociados a la variedad
- Necesidad de combinar datos estructurados y semiestructurados.

## Almacenes de datos estructurados
### Datos de archivo plano
Son estructuras sencillas, muchas veces con extensión txt o csv, no parecen bases de datos pero tienen los requisitos básicos. A continuación, algunas características:
- Valores duplicados. 
- Valores ambiguos.
- Datos faltantes.
- No se pueden establecer relaciones entre archivos.

### Bases de datos relacionales
A partir de un proceso de normalización se toman archivos planos y se convierten en una base de datos relacional. Algunas ventajas de la normalización son reducir la redundancia, aumentar la fiabilidad y proporcionar más coherencia en los datos.

Cada entidad recibe el nombre de tabla y las escrituras o lecturas se hacen por medio del lenguaje SQL (lenguaje de consulta estructurado). Cada campo se guarda como columna, la cual es un atributo de una entidad. Un registro individual se guarda en filas dentro de cada tabla. Cada tabla incluye una clave primaria que brinda la garantía que cada fila será única.

Se pueden crear relaciones creando una clave externa o foránea, que relaciona una clave primaria con el de otra tabla.

Una base de datos relacional cumple con ACID (Atomicidad se ejecuta todo o ninguno, Consistencia solo se empieza lo que se puede acabar, Aislamiento una operación no puede afectar a otras y Durabilidad la operación persistirá). 

Una de las principales desventajas es que algunas consultas complejas se hacen lentas.

## Tipos de sistemas de información
Hay dos grandes tipos, uno orientado al almacenamiento de transacciones (OLTP) y otro para el proceso de análisis de estas (OLAP).

### Bases de datos OLTP
Las bases de datos operativas organizan los datos en tablas y están diseñadas para permitir escribir datos en simultáneo (insertar, actualizar o eliminar). Su eficiencia se mide en transacciones por segundo.

### Bases de datos OLAP
A menudo denominadas *almacenes de datos* o *datawarehouse* se organizan en tablas y están optimizadas para la consulta de datos. La eficiencia de este tipo de base de datos se mide en tiempo de respuesta de las consultas. Se generan a partir de otras bases de datos.

### Comparación de OLTP y OLAP
| Característica | OLTP | OLAP |
|----------------|------|------|
| Naturaleza | Transacciones constantes (consultas / actualizaciones) | Grandes actualizaciones periódicas, consultas complejas. |
| Ejemplos | Contabilidades, transacciones de una tienda | Informes, tableros de control. |
| Tipo | Datos operativos | Datos consolidados |
| Retención de datos | A corto plazo (2-6 meses) | A largo plazo (2-5 años) |
| Almacenamiento | GB | TB / PB |
| Usuarios | Muchas | Pocos |
| Protección | Protección de datos robusta y constante. Tolerancia a errores. | Protección periódica. |

### Indexación de datos por filas y por columnas
Para poder hacer consultas rápidamente necesitamos índices, controlan la forma en que los datos se escriben físicamente y los organizan en base a las claves definidas. Un índice bien definido permitirá que la consulta lea directamente los registros en caso contrario, se tendría que leer la tabla completamente.

En una base de datos operativa, generalmente se tiene un índice en las columnas de clave. Las consultas generalmente son de tipo búsqueda, devolviendo varias columnas para cada coincidencia con el criterio que se establezca. Este tipo de consultas requiere un índice por filas.

En una base de datos de análisis, comúnmente se hacen consultas añadidas, tomando un gran número de filas las cuales se reducen a un solo resultado de una o más columnas. En estas consultas un índice columnar es muy útil. Un índice columnar guarda un dato por cada dato diferente de la columna.

| Característica | Índices por filas | Índices columnares |
|----------------|-------------------|--------------------|
| Almacenamiento en disco | Fila a fila | Columna a columna |
| Lectura/escritura | Lo mejor en lecturas y escrituras aleatorias | Lo mejor en lecturas y escrituras secuenciales |
| Mejor escenario | Mostrar filas completas basados en una clave | Mostrar operaciones de valores de columnas |
| Implementación | Sistemas transaccionales | Procesamiento analítico |
| Compresión de datos | Baja a media | Alta |

### Amazon RDS
Es la base de datos relacional de Amazon (Relational Database Service) es compatible con MySQL, PostreSQL, MariaDB, Oracle, SQL Server y Amazon Aurora. Es una base de datos tipo OLTP, implementa indexación basada en filas. Facilita la configuración, funcionamiento y escalado. Automatiza la gestión, como el aprovisionamiento de hardware, configuración de la base de datos, parches y copias de seguridad.

### Amazon Redshift
Es un almacén de datos rápido y escalable, también permite analizar datos de un lago de datos. Puede ejecutar consultas desde lagos de datos en S3. Implementa indexación en columnas para máximo rendimiento de cargas de trabajo analíticas.

### Ventajas y desventajas de las bases de datos relacionales
La principal ventaja es que es una tecnología probada, ampliamente adoptada y comprendida. 

La principal desventaja es su escalabilidad y la rigidez de su esquema.

## Bases de datos no relacionales
Los datos semiestructurados y no estructurados se almacenan en bases de datos no relacionales o NoSQL. Para evitar confusiones, las bases de datos NoSQL son un poco más que solo SQL. 

### Cambios de esquema en bases de datos relacionales y no relacionales
- Esquemas de datos, una base de datos relacional almacena datos en forma de tablas que contienen filas, cada fila representa un tipo de registro único. Cada columna almacena atributos de dicho registro. En una base de datos no relacional se almacenan los datos en forma de archivos con grupos de información entre corchetes, cada grupo de información también representa un registro.
- Hacer un cambio en un esquema relacional, cuando se necesita una nueva columna, se debe permitir que acepte valores nulos, luego se tendrá que rellenar con un valor para cada registro existente.
- Hacer un cambio en un esquema no relacional, acá solo es necesario añadir los valores al registro de interés. Siendo esta una de las mayores ventajas de este tipo de bases de datos.

### Tipos de bases de datos no relacionales
#### Documentos
Almacena datos semiestructurados y no estructurados, se incluyen archivos tipo JSON, BSON, XML. Los archivos contienen datos como una serie de elementos, cada elemento es una instancia de un objeto. 

Ventajas:
- Flexibilidad.
- Fácil de escalar.
- No es necesario planificar el tipo de dato.

Debilidades:
- No cumple con ACID.
- No se puede consultar entre archivos.

#### Valor de clave
Almacenan datos no estructurados en forma de pares de valor y clave. Tienen una tabla única. Se almacenan en forma de objeto blob y no requieren un esquema definido.

Ventajas:
- Muy flexible.
- Gran variedad de tipos de datos.
- Vínculo directo entre clave y valores, lo cual no requiere indexación ni uniones.
- El contenido se puede copiar fácilmente a otros sistemas.

Debilidades:
- Imposible consultar valores individuales, porque son un bloque.
- Actualizar o editar el contenido es muy difícil.
- No es fácil modelar objetos en pares de valor y clave.

#### Amazon DynamoDB
Es una base de datos de valor de clave y de documentos que ofrece rendimiento de menos de 10 milisegundos. Es completamente administrada, incluyendo seguridad integrada, copias de seguridad y restauración, caché en memoria. Puede gestionar 10 billones de solicitudes por día y picos de 20 millones de solicitudes por segundo.
Funciona para aplicaciones móviles, web, juegos, publicidad, IoT y todo tipo de aplicaciones que requieran baja latencia.

#### Grafos
Se crean para almacenar cualquier tipo de datos, permiten navegar a través de las relaciones. Se consultan mediante un lenguaje específico asociado a la herramienta que software que se seleccione.
Los datos se almacenan como un nodo, las aristas almacenan información sobre las relaciones entre los nodos. Una arista tiene un nodo inicial, un nodo final, un tipo y una dirección, y una arista puede describir varias relaciones principal-secundario, acciones, propiedades, etc.

Ventajas:
- Recuperación sencilla y rápida de estructuras jerárquicas complejas.
- Es ideal para la minería de grandes datos en tiempo real.
- Se pueden identificar con rapidez puntos comunes entre nodos.
- Ideal para hacer recomendaciones y permitir consulta rápida de esas relaciones.

Debilidades:
- No se pueden almacenar datos transaccionales.
- Se requiere un lenguaje nuevo.
- Los análisis sobre los datos no son tan eficientes.

##### Amazon Neptune
Es un servicio de base de datos de grafos rápido, fiable y completamente administrado, para trabajar con conjuntos de datos altamente conectados. Tiene un motor de base de datos de grafos de alto rendimiento, creado para almacenar miles de millones de relaciones con una latencia de milisegundos.

### Ventajas y desventajas de las bases de datos no relacionales
Ofrecen un esquema dinámico, lo cual permite actualizar el esquema sin impactar al sistema. Se pueden escalar fácilmente en servidores básicos distribuidos. La distribución masiva tiene la desventaja que los datos no se actualizan de forma instantánea con cada cambio, se ponen al día en segundo plano. Sin embargo, es importante notar que DynamoDB si cumple con ACID.
Las bases de datos no relacionales no funcionan tan bien en aplicaciones que requieren latencia transaccional extremadamente baja y aún no son tan maduras como las relacionales.

### Comparación entre bases de datos relacionales y no relacionales
| Característica | Relacional | No relacional | Grafos |
|----------------|------------|---------------|--------|
| Representación | Múltiples tablas, cada una con columnas y filas. | Colección de documentos, tabla única con claves y valores. | Colección de nodos y relaciones. |
| Diseño de datos | Almacén de datos relacional o dimensional normalizado. | Desnormalizado, columna ancha o valor clave. | Relación de entidad desnormalizada. |
| Optimizado | Almacenamiento | Informática / Cálculo | Relaciones |
| Estilo de consulta | SQL | Muchos lenguajes (consulta objetos) | Muchos lenguajes (consulta de objetos) |
| Escalado | Vertical | Horizontal | Híbrido |
| Implementación | Sistemas empresariales OLTP, OLAP | web/móvil OLTP | web/móvil OLTP |

