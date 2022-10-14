### Velocidad
> Cuándo las organizaciones necesitan rápido conocimiento desde los datos que están recolectando, pero los sistemas no pueden satisfacer la demanda, se presenta un problema de velocidad.

Secciones
- [Procesamiento de la información](#procesamiento-de-la-informaci%C3%B3n)
- [Aceleración de los datos](#aceleraci%C3%B3n-de-los-datos)
- [Diferencias en el procesamiento de lotes y de transmisiones](#diferencias-en-el-procesamiento-de-lotes-y-en-transmisi%C3%B3n)
- [Procesamiento de datos por lotes](#procesamiento-de-datos-por-lotes)
  - [Procesamiento de datos con Amazon EMR y Apache Hadoop](#procesamiento-de-lotes-de-datos-con-amazon-emr-y-apache-hadoop)
  - [Explorando Apache Hadoop](#explorando-apache-hadoop)
    - [Hadoop Common](#hadoop-common)
    - [HDFS](#hdfs-hadoop-distributed-file-system)
    - [YARN](#yarn)
    - [Hadoop MapReduce](#hadoop-mapreduce)
  - [Arquitectura para procesamiento de lotes](#arquitectura-para-procesamiento-de-lotes)
    - [S3](#s3)
    - [Lambda](#lambda)
    - [Amazon EMR](#amazon-emr---elastic-mapreduce)
    - [Glue](#aws-glue)
    - [Redshift](#amazon-redshift-1)
  - [Casos de uso](#casos-de-uso-para-procesamiento-de-lotes)
- [Procesamiento de datos en transmisiones](#procesamiento-de-datos-en-transmisi%C3%B3n)
  - [Procesamiento con Amazon Kinesis](#procesamiento-en-transmisi%C3%B3n-con-amazon-kinesis))
  - [Arquitectura para procesamiento combinado](#arquitectura-para-procesamiento-combinado) 
  - [Casos de uso](#casos-de-uso-de-flujo-de-datos-en-vivo)

#### Procesamiento de la información
Es la recolección y manipulación de los datos para producir información con sentido para la organización. Se divide en dos partes, la recolección y el procesamiento.

*Recolección* es obtener datos de diferentes fuentes y guardarlos en un destino común para su análisis.
*Procesamiento* es darle formato, organizar y hacerle filtros a los datos.

Hay dos tipos de procesamiento de datos
- Lotes - se recibirán datos en intervalos programados (diario, por hora, cada n minutos), tienden a ser predecibles pues se espera que el tiempo sea constante a través del tiempo (suponiendo similar volumen de datos en cada lote). 
- Periódico - pueden necesitarse también intervalos periódicos irregulares, esto es un poco más impredecible pues el volumen de datos puede cambiar muchísimo.
- En directo - casi en tiempo real, se transmite en lotes a intervalos muy pequeños, típicamente e procesan en los siguientes minutos de haberse obtenido. 
- En tiempo real - se recibe en intervalos aún más pequeños y se procesa en milisegundos.

Los datos primero se recolectan, tal cual, desde su origen, luego se procesan hasta convertirlos en conocimiento.

#### Aceleración de los datos
Otra característica clave de la velocidad es la *aceleración*, significa la tasa a la cual se consumirán las colecciones de datos, tasa de procesamiento y de análisis. La aceleración no es constante es variable. El sistema debe ser capaz de manejar eficientemente los picos y bajadas.

#### Diferencias en el procesamiento de lotes y en transmisión
| Atributo | Procesamiento de lotes | Procesamiento en transmisión |
|----------|------------------------|--------------------------|
| Alcance | Las consultas o procesamiento es sobre todo o casi todos los datos de un set de datos | Consultas o procesamiento de datos en una ventana de tiempo, o solo lo más reciente.|
| Tamaño | Lotes grandes de datos | Registros individuales o micro lotes de algunos pocos datos |
| Latencia | Minutos a horas | segundos o milisegundos |
| Análisis | Analíticas complejas | Funciones de respuesta simple, agrupados y métricas |

#### Procesamiento de datos por lotes
Se ha pensado algunas veces que procesamiento en lotes es un proceso lento. Pero no es el caso. El procesamiento de lotes debe ser rápido y efectivo al consumir un gran volumen de datos de una sola vez. Este es un desafío que no es tan crítico para el procesamiento en directo.

El procesamiento en lotes les brinda a las organizaciones la habilidad de poder navegar a más profundidad en los datos que han recolectado para producir analíticas complejas que no se pueden lograr con analíticas en vivo.

El procesamiento de datos es la ejecución de una serie de programas, o trabajos, en uno o más computadoras sin intervención manual. Los lotes se recolectan asíncronamente. El lote es enviado a un sistema de procesamiento cuando se cumplen ciertas condiciones, tales como una hora específica del día. Los resultados del trabajo de procesamiento se envían a una ubicación de almacenamiento que se puede consultar posteriormente.

#### Procesamiento de lotes de datos con Amazon EMR y Apache Hadoop

Amazon EMR es un servicio administrado para implementar cargas de trabajo con Apache Hadoop, también se pueden ejecutar otros marcos de trabajo distribuidos tales como Apache Spark, HBase, Presto y Flink en EMR. Además, podemos interactuar con otros almacenes de datos como S3 y DynamoDB.

Los libros de Amazon EMR permiten el desarrollo sin servidor y un ambiente colaborativo para consultas de una sola vez y análisis exploratorio. Podemos manipular los datos y generar gráficas usando la interfaz gráfica. Permite monitorear los trabajos y hasta ayudarnos a hacer trazabilidad del código.

##### Explorando Apache Hadoop
Es un sistema escalable de almacenamiento y procesamiento de lotes de datos. Usa servidores comunes y les brinda tolerancia a fallas a nivel de software. Hadoop complementa los sistemas existentes de datos al poder ingerir datos en simultaneo de gran volumen, estructurados o no, desde cualquier número de fuentes, lo cual permite un análisis más profundo que lo que un solo sistema puede brindar. Estos resultados se pueden entregar a cualquier sistema empresarial sin requerir de nuevo a Hadoop.

##### Hadoop Common
Es un conjunto de utilidades para Java que soportan los otros módulos de Hadoop. Estas libreras ayudan con la abstracción del sistema de archivos desde los componentes de procesamiento. Estos archivos de Java y sus scripts se requieren para iniciar Hadoop.

##### HDFS Hadoop Distributed File System
Es un sistema de archivos distribuido que almacena los datos en un ambiente de alta velocidad de nodos comunitarios. Esta arquitectura se asegura un ancho de banda muy alto para acceder a los datos de la aplicación.

##### YARN
Es el marco de trabajo de gestión de recursos responsable de calendarizar y ejecutar los trabajos de procesamiento.

##### Hadoop MapReduce
Es un sistema basado en YARN que permite el procesamiento en paralelo de grandes conjuntos de datos en el clúster.

#### Arquitectura para procesamiento de lotes
El procesamiento de lotes se puede llevar a cabo de diferentes formas en AWS.

##### S3
En un servicio de almacenamiento de objetos que ofrece gran escalabilidad, disponibilidad, seguridad y rendimiento.

##### Lambda
Nos permite ejecutar código sin provisionar servidores. Permite lanzar llamadas para operaciones de procesamiento.

##### Amazon EMR - Elastic MapReduce
Provee un marco de trabajo gestionado por Hadoop que simplifica, lo hace rápido y efectivo en costo el procesamiento de vastos volúmenes de datos, a través de instancias de EC2. Permite realizar operaciones de analítica de gran complejidad.

##### AWS Glue
Es un servicio totalmente administrado para extraer, transformar y cargar, que hace fácil la preparación y carga de datos para analítica.

##### Amazon Redshift
Es una base de datos tipo data warehouse que es rápida y escalable que hace simple y eficiente en costo el poder analizar los datos a través del almacén de datos y de lagos de datos. Permite guardar grandes cantidades de datos transaccionales para propósito de analíticas.

Una configuración típica de flujo de datos para un sistema de analítica de lotes básico es utilizar S3 para almacenar los datos, Lambda para realizar el ETL del archivo recién subido, EMR para el ETL agregado (la carga pesada, consolidación de información y carga en el motor), Redshift como almacen de datos para guardar los datos necesarios para la reporteria.

Podemos sustituir EMR por Glue, quien tiene la ventaja que es totalmente administrable, mientras que EMR requiere gestión y configuración de los componentes que requiere el servicio.

##### Casos de uso para procesamiento de lotes
- Analítica de bitácora.
- Vista unificada de datos a través de múltiples almacenamientos de datos.
- Análisis predictivo.
- Consultas directamente a S3 como lago de datos.

#### Procesamiento de datos en transmisión
Este tipo de procesamiento les permite a las organizaciones poder obtener conocimiento desde sus datos en segundos desde haber recolectado los datos.

Los datos son enviados constantemente hacia el servicio en directo desde un productor, el flujo se procesa a registros en el consumidor y finalmente se envían a almacenamiento.

#### Procesamiento en transmisión con Amazon Kinesis
Al procesar flujos en directo, se usan múltiples servicios, un servicio para ingerir los flujos constantes de datos, uno para procesar y analizar el flujo, otro para cargarlos en un almacenamiento de datos analíticos si fuera requerido. 
- Amazon Kinesis Data Firehose - permite capturar, transformar y cargar flujos de datos hacia almacenamientos de datos de AWS para poder llevar a cabo analítica muy próxima a tiempo real por medio de las herramientas de inteligencia de negocio existentes de la organización.
- Amazon Kinesis Data Streams - permite construir aplicaciones personalizadas en tiempo real que procesan los flujos de datos usando los marcos de trabajo populares para procesamiento de flujos.
- Amazon Kinesis Video Streams - hace más fácil asegurar los flujos de video desde dispositivos conectados a AWS para analítica, aprendizaje de máquina (ML) y otros tipos de procesamiento.
- Amazon Kinesis Data Analytics - es la forma más fácil de procesar flujos de datos en tiempo real con SQL o Java sin tener que aprender nuevos lenguajes de programación o marcos de trabajo para procesamiento.

#### Arquitectura para procesamiento combinado
- Kinesis Data Firehose captura transforma y carga en casi tiempo real.
- Kinesis Data Analytics procesa los flujos de datos en tiempo real con SQL o Java.
- S3 almacena los resultados para análisis más profundo.
- Athena es un servicio para consultas interactivas que hace fácil el analizar datos en S3 usando SQL estándar. Athena es sin servidor.
- Quicksight es una potente herramienta de inteligencia de negocios para entregar conocimiento a todos los interesados en la organización.
- Glue puede utilizarse para combinar los almacenes de datos en S3, uno que se procesó en tiempo real y otro que se procesó en lote y cuyo resultado se puede cargar de vuelta a otro bucket de S3.

##### Casos de uso de flujo de datos en vivo
- Aplicaciones de analítica de video.
- Evolucionar de lote a analítica en tiempo real.
- Análisis de datos originados en dispositivos de IoT.
