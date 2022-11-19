#AWS Glue

Es un servicio de AWS que permite conexión a *multiples fuentes de datos* (bases de datos relacionales, aplicaciones web, buckets de S3, etc), es un *servicio sin servidores* lo cual permite que se pague solamente por los recursos que se consuman, sin cargos fijos.

*Permite simplificar la orquestación de nuestros ETL*, podemos diseñar, ejecutar y visualizar el estado y bitácora de cada tarea y flujo. 

*Simplifica el desarrollo* podemos hacer nuestros jobs o tareas de forma visual, en scripts o en modo notebook.

Soporta lenguajes Python, Spark y Scala.

## Principales componentes de AWS Glue

### Crawler
Este es un componente que ayuda a descubrir el esquema de una base de datos, este se encarga de registrar las tablas, organizaciones lógicas y las va a registrar en el data catalog. Trabaja tanto en buckets de S3 como en bases de datos.

### Data Catalog
Es un catálogo de datos, donde se almacenan metadatos, contiene la estructura de nuestros datos, propiedades, características. Facilita la interacción con otros servicios de AWS, como Athena, Sagemaker y Quicksight. Se define el nombre de una base de datos y luego se le añaden tablas utilizando el Crawler.

### Connections
Las conecciones permiten a Glue poder acceder a las diferentes fuentes de datos, encriptando credenciales y nombre de los servidores.

En algunos casos es necesario crear un conector, este permite utilizar un driver actualizado y soportado por el motor de base de datos de nuestro interes, a partir de dicho conector personalizado se puede crear una conexión, en donde se puede establecer los parámetros de conexión, soporta la utilización de AWS Secret para que la información no sea visible.

## Arquitectura de ejemplo

![Arquitectura de AWS Glue](https://github.com/macomeza/dataScience/blob/main/awsGlue/AWSGlueArquitectura.jpg)

Dado que en nuestro ejemplo usaremos una base de datos SQL Server que se encuentra físicamente en el Ingenio pero que está conectada con Amazon a través de una VPC (segmento de red que enlaza una VPN desde AWS hacia el centro de cómputo) definiremos una conexión personalizada, esto requiere la creación de un conector que hace referencia al driver más reciente para conectar a MSSQL Server, el cual se descarga desde Microsoft y se sube a una carpeta dentro de un bucket en el que tengamos acceso, la buena práctica recomienda nombrar a la subcarpeta connectors para poderle identificar fácilmente.

En el momento de publicar este artículo, el link de descarga del driver fue el [siguiente](https://go.microsoft.com/fwlink/?linkid=2202911)

![Jar de driver para conectar a un servidor MS SQL Server](https://github.com/macomeza/dataScience/blob/main/awsGlue/01-descargar-driver-MSSQL.jpg)

Luego crearemos un conector personalizado, haciendo clic en "Connectors" dentro de AWS Glue Studio y luego en "Create custom connector".

![Creando un conector personalizado](https://github.com/macomeza/dataScience/blob/main/awsGlue/02-crear-conector-personalizado.jpg)

El cual definiremos con las siguientes características:

![Características de nuestro conector](https://github.com/macomeza/dataScience/blob/main/awsGlue/03-conector_mssql_vpc.jpg)


## Requisitos

- Es necesario tener acceso a un bucket, es una buena práctica usar una carpeta para los datos crudos que lo indique explicitamente, en nuestro ejemplo se indica mediante el término *raw* y también se completa el nombre de la carpeta con la región que estamos utilizando, esto es útil para acceso desde otros servicios.
- También es necesario tener creada o definir la base de datos en AWS Glue para generar las tablas que descubra el Crawler.



