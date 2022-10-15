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

Es un servicio para organizar y seleccionar los datos, proteger los datos del lago de datos y para coordinar las tareas de transformación con otros servicios de AWS.

[AWS Lake Formation](https://aws.amazon.com/es/lake-formation)

#### Cuál es mejor un Data Warehouse o un Data Lake
Son diferentes soluciones para diferentes problemas.

Data warehouse - Almacén de Datos
: Es un repositorio central da datos estructurados de varios orígenes de datos. Estos datos son transformados, agrupados y preparados para reportes y análisis del negocio.

Los datos fluyen desde los sistemas transaccionales, bases de datos relacionales y otras fuentes. Pueden incluir datos semi estructurados y no estructurados. Estas fuentes deben ser transformadas a datos estructurados antes de poderse almacenar.

Los datos se guardan en el Data Warehouse usando un esquema, el cual define cómo los datos se guardarán en tablas, columnas y filas. El esquema fuerza algunas restricciones en los datos para asegurar su integridad. El proceso de transformación también requiere algunos pasos para que los datos se ajusten al esquema. Después del primer consumo de datos, el proceso puede continuar regularmente.

Los analistas de negocio, científicos de datos y los tomadores de decisiones acceden los datos a través de herramienta de inteligencia de negocio, clientes SQL y otras aplicaciones de analítica. 

Los almacenes de datos proporcionan almacenamiento para conjuntos de datos muy estructurados que sirven como única fuente de verdad para las consultas analíticas.

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
