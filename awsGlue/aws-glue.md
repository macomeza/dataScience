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

## Arquitectura de ejemplo

![Arquitectura de AWS Glue para ejemplo](https://github.com/macomeza/dataScience/blob/main/awsGlue/AWSGlueArquitecturaEjemplo.jpg)

Se usarán como fuente de datos, un bucket de S3. Cada una tendrá un servicio de Crawler que identificarán los datos en ambas fuentes.

Si hubieramos tenido una fuente de datos que fuera una base de datos relacionalpara conectar el Crawler hacia la base de datos RDS se necesita configurar una conexión. La salida de los Crawlers será generar el AWS Glue Data Catalog, para poder consumir estos datos posteriormente.

A nuestro S3, cargaremos como ejemplo el [SaaS-Sales.csv](https://github.com/macomeza/dataScience/blob/main/awsGlue/SaaS-Sales.csv).

## Requisitos

- Es necesario tener acceso a un bucket, es una buena práctica usar una carpeta para los datos crudos que lo indique explicitamente, en nuestro ejemplo se indica mediante el término *raw* y también se completa el nombre de la carpeta con la región que estamos utilizando, esto es útil para acceso desde otros servicios.
- También es necesario tener creada o definir la base de datos en AWS Glue para generar las tablas que descubra el Crawler.


Al tener cargado el archivo, cambiaremos de servicio en la conola a AWS Glue. Luego seleccionaremos Tables, luego daremos un clic en *Add tables using crawler*, le daremos un nombre a nuestro Crawler, le nombraremos s3-spc-fabrica-raw, dado que va a leer toda la carpeta de nuestro bucket.

![Crear crawler](https://github.com/macomeza/dataScience/blob/main/awsGlue/01-crawler.jpg)

Luego vamos a añadirle una fuente de datos.

![Añadir fuente de datos](https://github.com/macomeza/dataScience/blob/main/awsGlue/02-crawler.jpg)

De las diferentes fuentes de datos, vamos a seleccionar que el tipo es S3 y luego seleccionaremos el folder de nuestro bucket que contiene la data cruda.

![Seleccionar fuente de datos](https://github.com/macomeza/dataScience/blob/main/awsGlue/02-1-crawler.jpg)



