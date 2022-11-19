#AWS Glue

Es un servicio de AWS que permite conexión a *múltiples fuentes de datos* (bases de datos relacionales, aplicaciones web, buckets de S3, etc), es un *servicio sin servidores* lo cual permite que se pague solamente por los recursos que se consuman, sin cargos fijos.

*Permite simplificar la orquestación de nuestros ETL*, podemos diseñar, ejecutar y visualizar el estado y bitácora de cada tarea y flujo. 

*Simplifica el desarrollo* podemos hacer nuestros jobs o tareas de forma visual, en scripts o en modo notebook.

Soporta lenguajes Python, Spark y Scala.

## Principales componentes de AWS Glue

### Crawler
Este es un componente que ayuda a descubrir el esquema de una base de datos, este se encarga de registrar las tablas, organizaciones lógicas y las va a registrar en el data catalog. Trabaja tanto en buckets de S3 como en bases de datos.

### Data Catalog
Es un catálogo de datos, donde se almacenan metadatos, contiene la estructura de nuestros datos, propiedades, características. Facilita la interacción con otros servicios de AWS, como Athena, Sagemaker y Quicksight. Se define el nombre de una base de datos y luego se le añaden tablas utilizando el Crawler.

### Connections
Las conexiones permiten a Glue poder acceder a las diferentes fuentes de datos, encriptando credenciales y nombre de los servidores.

En algunos casos es necesario crear un conector, este permite utilizar un driver actualizado y soportado por el motor de base de datos de nuestro interés, a partir de dicho conector personalizado se puede crear una conexión, en donde se puede establecer los parámetros de conexión, soporta la utilización de AWS Secret para que la información no sea visible.

## Arquitectura de ejemplo

![Arquitectura de AWS Glue](https://github.com/macomeza/dataScience/blob/main/awsGlue/AWSGlueArquitectura.jpg)

Dado que en nuestro ejemplo usaremos una base de datos SQL Server que se encuentra físicamente en el Ingenio pero que está conectada con Amazon a través de una VPC (segmento de red que enlaza una VPN desde AWS hacia el centro de cómputo) definiremos una conexión personalizada, esto requiere la creación de un conector que hace referencia al driver más reciente para conectar a MSSQL Server, el cual se descarga desde Microsoft y se sube a una carpeta dentro de un bucket en el que tengamos acceso, la buena práctica recomienda nombrar a la subcarpeta connectors para poderle identificar fácilmente. 

Más adelante haremos un nuevo ejemplo en el cual nos conectaremos a una base de datos RDS MariaDB y en ese ejemplo si ejecutaremos el Crawler y luego el job sobre las tablas descubiertas.

En el momento de publicar este artículo, el link de descarga del driver fue el [siguiente](https://go.microsoft.com/fwlink/?linkid=2202911)

![Jar de driver para conectar a un servidor MS SQL Server](https://github.com/macomeza/dataScience/blob/main/awsGlue/01-descargar-driver-MSSQL.jpg)

Luego crearemos un conector personalizado, haciendo clic en "Connectors" dentro de AWS Glue Studio y luego en "Create custom connector".

![Creando un conector personalizado](https://github.com/macomeza/dataScience/blob/main/awsGlue/02-crear-conector-personalizado.png)

El cual definiremos con las siguientes características:

![Características de nuestro conector](https://github.com/macomeza/dataScience/blob/main/awsGlue/03-conector_mssql_vpc.png)

Luego seleccionaremos el conector recién creado

![Seleccionar conector](https://github.com/macomeza/dataScience/blob/main/awsGlue/04-seleccionar-conector.png)

Luego le daremos clic en crear conexión

![Crear conexión](https://github.com/macomeza/dataScience/blob/main/awsGlue/05-crear-conexi%C3%B3n.png)

Le daremos un nombre a la conexión, una descripción y luego seleccionaremos el tipo de credenciales, seleccionando default de la lista, luego usaremos el secreto que tenga la IP, puerto, nombre de usuario de conexión, contraseña y nombre de la base de datos. 

![Características de la conexión](https://github.com/macomeza/dataScience/blob/main/awsGlue/06-creando-la-conexi%C3%B3n.png)

Luego definiremos la VPC, subnet y security groups, en este ejemplo usamos los que permiten conectar al segmento de red de ILU.

![Opciones de red](https://github.com/macomeza/dataScience/blob/main/awsGlue/07-definiendo-opciones-red.png)

Crearemos un job para obtener los datos desde SQL Server, usaremos como fuente el conector personalizado y como destino S3. Haremos un job para cada tabla que deseamos importar hacia S3.

![Creando un job](https://github.com/macomeza/dataScience/blob/main/awsGlue/08-creando-job-etl.png)

Seleccionamos la conexión y luego podemos seleccionar una tabla o indicar un query de SQL.

![Seleccionando conexión e indicando tabla](https://github.com/macomeza/dataScience/blob/main/awsGlue/09-seleccionamos-conexi%C3%B3n-indicamos-nombre-tabla.png)

Iremos a la pestaña de data preview, le daremos clic en previsualizar, esto nos permitirá obtener los primeros registros de la tabla, permite validar que nuestro query o tabla sean válidos y nos devuelve la estructura que se convertirá en nuestra metadata. Luego le daremos clic en el botón de previsualización para poder seleccionar todos los campos.

![Previsualizar datos y estructura](https://github.com/macomeza/dataScience/blob/main/awsGlue/10-previsualizar-datos-para-obtener-esquema.png)

Seleccionaremos todos los campos, para poder obtener la estructura completa.

![Seleccionar todos los campos](https://github.com/macomeza/dataScience/blob/main/awsGlue/11-seleccionar-todos-los-campos.png)

Vamos a la pestaña de output schema y le daremos clic al botón de use datapreview schema.

![Usaremos esquema](https://github.com/macomeza/dataScience/blob/main/awsGlue/12-usar-estructura.png)

Es posible que algún tipo de dato este en null o sea incorrecto, si fuera el caso, debemos editar el esquema. Al finalizar la edición, le daremos clic en Apply.

![Previsualizando estructura](https://github.com/macomeza/dataScience/blob/main/awsGlue/10-previsualizar-datos-para-obtener-esquema.png)

Validaremos una vez más el mapeo, si necesitamos cambiar algún tipo de dato o el nombre de las columnas, podemos hacerlo acá.

![Validar mapeo](https://github.com/macomeza/dataScience/blob/main/awsGlue/14-validar-mapeo.png)

Seleccionaremos el nodo de salida a S3, establecemos el formato, tipo de compresión, destino en S3, base de datos en cuyo catálogo pondremos la tabla, nombre de la tabla, seguidamente seleccionaremos la opción de Create a tanle in the Data Catalog (2a opción).

![Salida a S3](https://github.com/macomeza/dataScience/blob/main/awsGlue/15-configar-salida-datos-s3.png)

Finalmente, le daremos clic a job details, le daremos un nombre al job, seleccionaremos el rol de IAM para ejecutar el mismo, se recomienda bajar el número de workers e incluso dejar que se escalen automáticamente y deshabilitaremos el job bookmark.

![Bautizando el job](https://github.com/macomeza/dataScience/blob/main/awsGlue/16-bautizar-job.png)

Luego a ejecutar el job, esperar un par de minutos en lo que se importan los datos. Para darle seguimiento al job, podemos ir al Monitoring en donde cambiará el estado a starting, running, luego a succeeded o failed. Si nos da un error, podemos consultar la bitácora en CloudWatch.

Si todo salió bien, podemos ir a Athena, escoger la base de datos, luego seleccionar una de nuestras tablas con datos, le damos clic en los 3 puntitos y luego preview table, nos mostrará los primeros 10 registros de la tabla. A partir de este momento, ya podemos hacer consultas avanzadas con nuestro lago de datos y podemos crear tableros de control o cualquier tipo de visualización con servicios con QuickSight.

![Ver datos en Athena](https://github.com/macomeza/dataScience/blob/main/awsGlue/17-previsualizar-datos-athena.png)

Felicidades, ya podemos usar AWS para crear un lago de datos.

## Requisitos

- Es necesario tener acceso a un bucket, es una buena práctica usar una carpeta para los datos crudos que lo indique explícitamente, en nuestro ejemplo se indica mediante el término *raw* y también se completa el nombre de la carpeta con la región que estamos utilizando, esto es útil para acceso desde otros servicios.
- También es necesario tener creada o definir la base de datos en AWS Glue para generar las tablas que descubra el Crawler.
