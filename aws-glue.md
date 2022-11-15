#AWS Glue

Es un servicio de AWS que permite conexión a *multiples fuentes de datos* (bases de datos relacionales, aplicaciones web, buckets de S3, etc), es un *servicio sin servidores* lo cual permite que se pague solamente por los recursos que se consuman, sin cargos fijos.

*Permite simplificar la orquestación de nuestros ETL*, podemos diseñar, ejecutar y visualizar el estado y bitácora de cada tarea y flujo. 

*Simplifica el desarrollo* podemos hacer nuestros jobs o tareas de forma visual, en scripts o en modo notebook.

Soporta lenguajes Python, Spark y Scala.

## Principales componentes de AWS Glue

### Crawler
Son herramientas que ayudan a descubrir el esquema de una base de datos, este se encarga de registrar las tablas, organizaciones lógicas y las va a registrar en el data catalog. Trabaja tanto en buckets de S3 como en bases de datos.

### Data Catalog
Es un catálogo de datos, donde se almacena metadatos, contiene la estructura de nuestros datos, propiedades, características. Facilita la interacción con otros servicios de AWS, como Athena, Sagemaker y Quicksight.

### Connections
Las conecciones permiten a Glue poder acceder a las diferentes fuentes de datos, encriptando credenciales y nombre de los servidores.

![Arquitectura de AWS Glue para ejemplo](https://github.com/macomeza/dataScience/blob/main/AWSGlueArquitecturaEjemplo.jpg)
