# Fundamentos de Analítica de Datos en AWS

**Análisis** es una detallada evaluación de algo para poder comprender su naturaleza o determinar sus características esenciales. La **analítica de datos** es el proceso de compilar, procesar y analizar datos para poderla utilizar para toma de decisiones.

*Analítica es el análisis sistemático de datos. La analítica de datos es el proceso analítico aplicado.*

*Datos estructurados* están organizados y almacenados en forma de valores agrupados en filas y columnas en una tabla. Ejemplo, una agenda telefónica.
*Datos semi estructurados* usualmente almacenados en una pareja índice - valor, que son agrupados en elementos dentro de un archivo. Ejemplo, una lista de música, por género y artista.
*Datos no estructurados* no tienen una forma consistente, algunas solo contienen metadatos y algunos tiene datos semi-estructurados. Ejemplo, buzón de correo, galería de fotos.
*Metadata* información básica que describe a un objeto.

## Componentes de una solución para analítica de datos

### Consumo o ingesta de datos crudos 
Los datos a obtener pueden ser de diferentes tipos, estructurados, semiestructurados, no estructurados, se pueden originar de sistemas de la organización, del internet o de dispositivos directamente. Algunos se consumirán en bloques y otros en vivo.

### Almacenamiento
Una buena solución de análisis proveerá un almacenamiento seguro, escalable y durable, para cada uno de los tipos de datos que describimos en el consumo de datos. Los almacenes de datos o datawarehouses son eficientes para almacenar datos estructurados de tipo analítico, las bases de datos pueden almacenar datos estructurados y semiestructurados mientras los lagos de datos pueden almacenar todos los tipos de datos mencionados anteriormente.

### Proceso y análisis
Primero los datos se procesarán, transformándoles para que puedan ser consumidos por el solicitante. En este procesamiento se analizarán los datos (ordenamiento, agrupaciones, uniones y aplicar lógico del negocio para producir conjuntos de datos con sentido para la organización). El paso final de este proceso es almacenarlo o cargarlo en una ubicación específica para realizar la analítica.

### Consumo y visualización
Hay dos grandes formas de consumir los datos, por consulta directa o por medio de herramientas de inteligencia de negocio. Las consultas directas sirven para análisis rápidas, generalmente están a cargo de un analista de datos. Las herramientas de inteligencia de negocio permiten producir reportes y tableros de control para ayudar a los consumidores a explorar los datos y a tomar decisiones.

## Los 5 desafíos del análisis de datos 
Te recomiendo mi publicación en medium sobre el desafío de las 5Vs [ir a 5 desafíos de la analítica de datos.](https://medium.com/@macomeza/5-desafios-de-la-an%C3%A1litica-de-datos-950906b0fa42)
- [Volumen](#volumen)
- [Velocidad](#velocidad)
- [Variedad](#variedad)

### Volumen
> Cuando los negocios tienen más datos que los que pueden procesar y analizar, tienen un problema de volumen.

Secciones relacionadas a Volumen
- [S3](#Amazon-S3)
- [Lago de datos](#lago-de-datos)
  - [Qué datos podemos guardar en un lago de datos](#qu%C3%A9-datos-podemos-guardar-en-un-lago-de-datos)
  - [Beneficios de los lagos de datos](#beneficios-de-los-lagos-de-datos)
  - [Amazon EMR y Lagos de Datos](#amazon-emr-y-lagos-de-datos)
  - [Preparación de un Lago de Datos](#preparaci%C3%B3n-de-un-lago-de-datos)
  - [AWS Lake Formation](#aws-lake-formation)
  - [¿Cuál es mejor un Data Warehouse o un Data Lake?](#cu%C3%A1l-es-mejor-un-data-warehouse-o-un-data-lake)
  - [Amazon Redshift](#amazon-redshift)
  - [Características de un Data Warehouse y un Data Lake](#caracter%C3%ADsticas-de-un-data-warehouse-y-un-data-lake)
  - [Apache Hadoop](#apache-hadoop)

#### Amazon S3
Mientras más cerca estén los datos de tu sistema de procesamiento, mejor rendimiento tendrá el procesamiento. S3 significa Amazon Simple Storage Service (Servicio de Almacenamiento Simple) permite almacenar todos los datos semi estructurados y no estructurados.

En S3 los archivos se guardan como objetos dentro de folders llamados cubetas (buckets). Un *objeto* está compuesto del archivo y la metadata del mismo. Los buckets son los contenedores lógicos para los objetos, se puede controlar el acceso a cada bucket, incluyendo permiso de creación, eliminación, visualizar. Siempre se incluye una bitácora de acceso a cada bucket y sus objetos.

Cada vez que se carga un objeto a un bucket en S3, se crea una clave única para el objeto, incluye un identificador de la versión del objeto.

#### Lago de Datos
Un lago de datos es un repositorio centralizado que nos permite almacenar datos del tipo estructurado, semi estructurado y no estructurado a cualquier escala.

Almacenar los archivos de una organización conlleva los siguientes desafíos, en que carpeta debería almacenarlo, usar prefijos o sufijos para identificar versiones, se divide por tema específico o departamento. A partir de lo anteriormente descrito y la necesidad de organizar mejor la información de cada vez mayor volumen se dio el surgimiento de los lagos de datos.

El lago de datos nos permite comprender que información es la que tenemos almacenada a través de catálogos e indexación de la información.

- Es un repositorio centralizado.
- Almacena datos estructurados.
- Almacena datos semi estructurados y no estructurados.

[DataLakes](https://aws.amazon.com/es/big-data/datalakes-and-analytics/)

##### ¿Qué datos podemos guardar en un lago de datos?
- Se puede alimentar de información proveniente de sistemas y servidores propios de la organización, los soporta en su formato original. No requiere crear estructuras de datos, esquemas y transformaciones previas.
- Datos relacionales, datos de las aplicaciones del negocio, aplicaciones móviles, dispositivos conectados a internet y redes sociales.
- Obtener datos en vivo, en tiempo real.
- Aprendizaje de máquina, se pueden generar conocimientos, incluyendo reportería sobre datos históricos o construcción de modelos para pronóstico u optimización.
- Analítica de datos, dar acceso a la organización a procesar y a los datos ya procesados.

##### Beneficios de los lagos de datos
- Fuente única de la verdad - para lograrlo se debe organizar adecuadamente y estructurar los datos que ingresarán al lago.
- Guardar cualquier tipo de datos, sin importar la estructura - guardar archivos relevantes, se deben establecer políticas de retención para que los datos se mantengan al día.
- Puede ser analizada utilizando inteligencia artificial y aprendizaje de máquina - podemos ir más allá de las capacidades humanas de analítica y encontrar conocimientos significativos.
- Es una solución eficiente en costo.
- Implementa cumplimiento y seguridad lideres en la industria.
- Ofrece la ventaja de obtener datos de varias formas.
- Categorizar y gestionar los datos. Podemos usar AWS Glue para entender la estructura de los datos de nuestro lago de datos, prepararla y cargarla a almacenamiento de dato, una vez Glue ha catalogado los datos, se puede buscar inmediatamente.
- Permite convertir nuestros datos a conocimientos significativos.

#### Amazon EMR y Lagos de Datos
Las organizaciones pueden ubicar los datos en un Lago de Datos y usar su propio marco de trabajo distribuido para el procesamiento de estos, tales como Apache Hadoop y Spark son soportados.

#### Preparación de un Lago de Datos
> Los científicos de datos invierten el 60% de su tiempo limpiando y organizando datos y el 19% recolectando conjuntos de datos.

La preparación de los datos requiere bastante esfuerzo, no hay atajos o respuestas fáciles respecto a cómo realizar la limpieza, transformación y recolección de datos para el Lago de Datos. Sin embargo, hay servicios que nos pueden ayudar a automatizar muchos de estos procesos que consumen bastante tiempo.

#### AWS Lake Formation
> AWS Lake Formation es un servicio que facilita la configuración de un lago de datos seguro en cuestión de días. Un lago de datos es un repositorio centralizado, seleccionado y seguro que almacena todos sus datos, tanto en su forma original como preparados para análisis. Un lago de datos le permite desglosar los silos de datos y combinar diferentes tipos de análisis para obtener información y tomar mejores decisiones empresariales.

- Organizar y curar datos.
- Asegurar el acceso a los datos a través del Lago de Datos.
- Orquestar las tareas de transformación con otros servicios de AWS.

[AWS Lake Formation](https://aws.amazon.com/es/lake-formation)

#### Cuál es mejor un Data Warehouse o un Data Lake
Son diferentes soluciones para diferentes problemas.

Data warehouse - Almacén de Datos
: Es un repositorio central da datos estructurados de varios orígenes de datos. Estos datos son transformados, agrupados y preparados para reportes y análisis del negocio.

Los datos fluyen desde los sistemas transaccionales, bases de datos relacionales y otras fuentes. Pueden incluir datos semi estructurados y no estructurados. Estas fuentes deben ser transformadas a datos estructurados antes de poderse almacenar.

Los datos se guardan en el Data Warehouse usando un esquema, el cual define cómo los datos se guardarán en tablas, columnas y filas. El esquema fuerza algunas restricciones en los datos para asegurar su integridad. El proceso de transformación también requiere algunos pasos para que los datos se ajusten al esquema. Después del primer consumo de datos, el proceso puede continuar regularmente.

Los analistas de negocio, científicos de datos y los tomadores de decisiones acceden los datos a través de herramienta de inteligencia de negocio, clientes SQL y otras aplicaciones de analítica. 

Data marts
: Es un conjunto de datos de un Data Warehouse. Se enfoca en un tema específico o en un área funcional de la organización.

#### Amazon Redshift

Es el Data Warehouse de Amazon, es un producto diseñado para ser 10x más rápido que un Data Warehouse tradicional, más fácil de implementar y gestionar, seguro y escalable rápidamente para satisfacer las necesidades.

#### Características de un Data Warehouse y un Data Lake
| Característica | Data Warehouse | Data Lake |
| -------------- | -------------- | ----------|
| Datos | Relacionales desde sistemas transaccionales, bases de datos, aplicaciones del negocio | No-relacionales y relacionales originadas en dispositivos IoT, sitios web, aplicaciones móviles, redes sociales, aplicaciones corporativas.
| Esquema | Diseñado previo a la implementación | Escrito en el momento del análisis
| Precio / rendimiento | Consultas más rápidas resulta en un costo mayor de almacenamiento | Consulta de resultados se vuelven más rápidos utilizando un almacenamiento de menor costo.
| Calidad de los datos | Datos altamente depurados que sirven como fuente central de la verdad | Cualquier dato, el cual pudo o no ser depurado. (data cruda)
| Usuarios | Analista de negocio | Científicos de datos, desarrolladores de datos y analistas de negocio (usando datos curados).
| Analítica | Reportería en lote, Inteligencia de Negocio y Visualizaciones | Aprendizaje de Máquina, analítica predictiva, descubrimiento de datos y perfilamiento.

#### Apache Hadoop
Utiliza una arquitectura de procesamiento distribuida, en la cual una tarea se realiza por varios servidores. Cada pieza del trabajo es distribuida a un clúster de servidores y se puede ejecutar y volver a ejecutar en cualquiera de los servidores. Usan frecuentemente el HDFS (sistema de archivos distribuido de Hadoop, en español), para almacenar los datos localmente para su procesamiento. Luego los resultados se reducen a un solo conjunto de datos. Un nodo, que fue designado como el principal, controla la distribución de tareas y puede manejar fallas automáticamente.

Para implementar Hadoop en AWS se recomienda utilizar EMR. El cual permite que escojamos dos sistemas de archivos (un conjunto de reglas para gobernar cómo se guardan los archivos).
- HDFS el nativo, el cual crea una copia temporal de los datos y luego la procesa y almacena en S3.
- EMRFS la versión adaptada, la cual no necesita una copia temporal ahorrando segundos valiosos.

### Velocidad
> Cuando las organizaciones necesitan rápido conocimiento desde los datos que están recolectando, pero los sistemas no pueden satisfacer la demanda, se presenta un problema de velocidad.

Secciones
- [Procesamiento de la información](#procesamiento-de-la-informaci%C3%B3n)
- [Aceleración de los datos](#aceleraci%C3%B3n-de-los-datos)
- [Diferencias en el procesamiento de lotes y de transmisiones](#diferencias-en-el-procesamiento-de-lotes-y-de-transmisiones)
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
- [Procesamiento de datos en transmisiones](#procesamiento-de-datos-en-tra)
  - [Procesamiento con Amazon Kinesis](#procesamiento-en-directo-con-amazon-kinesis)
  - [Arquitectura para procesamiento de flujos](#arquitectura-para-procesamiento-de-flujos) 
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

#### Arquitectura para procesamiento de flujos
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

### Variedad
> Cuando la organización está *abrumada* por la gran cantidad de fuentes de datos que se deben analizar y no encuentran sistemas para llevar a cabo la analítica, tenemos un problema de variedad.
