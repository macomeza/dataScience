# Fundamentos de Analítica de Datos en AWS

**Análisis** es una detallada evaluación de algo para poder comprender su naturaleza o determinar sus características esenciales. La **analítica de datos** es el proceso de compilar, procesar y analizar datos para poderla utilizar para toma de decisiones.

*Analítica es el análisis sistemático de datos. La analítica de datos es el proceso analítico aplicado.*

*Datos estructurados* están organizados y almacenados en forma de valores agrupados en filas y columnas en una tabla. Ejemplo, una agenda telefónica.
*Datos semi estructurados* usualmente almacenados en una pareja indice - valor, que son agrupados en elementos dentro de un archivo. Ejemplo, una lista de música, por genero y artista.
*Datos no estructurados* no tienen una forma consistente, algunas solo contienen metadatos y algunos tiene datos semi-estructurados. Ejemplo, buzón de correo, galeria de fotos.
*Metadata* información básica que describe a un objeto.

## Componentes de una solución para analítica de datos

### Consumo o ingesta de datos crudos 
Los datos a obtener pueden ser de diferentes tipos, estructurados, semiestructurados, no estructurados, se pueden originar de sistemas de la organización, del internet o de dispositivos directamente. Algunos se consumirán en bloques y otros en vivo.

### Almacenamiento
Una buena solución de análisis proveera un almacenamiento seguro, escalable y durable, para cada uno de los tipos de datos que describimos en el consumo de datos. Los almacenes de datos o datawarehouses son eficientes para almacenar datos estructurados de tipo analítico, las bases de datos pueden almacenar datos estructurados y semiestructurados mientras los lagos de datos pueden almacenar todos los tipos de datos mencionados anteriormente.

### Proceso y análisis
Primero los datos se procesarán, transformándoles para que puedan ser consumidos por el solicitante. En este procesamiento se analizarán los datos (ordenamiento, agrupaciones, uniones y aplicar lógico del negocio para producir conjuntos de datos con sentido para la organización). El paso final de este proceso es almacenarlo o cargarlo en una ubicación específica para realizar la analítica.

### Consumo y visualización
Hay dos grandes formas de consumir los datos, por consulta directa o por medio de herramientas de inteligencia de negocio. Las consultas directas sirven para análisis rápidas, generalmente están a cargo de un analista de datos. Las herramientas de inteligencia de negocio permiten producir reportes y tableros de control para ayudar a los consumidores a explorar los datos y a tomar decisiones.

## Los 5 desafios del análisis de datos 
Te recomiendo mi publicación en medium sobre el desafio de las 5Vs [ir a 5 desafios de la analítica de datos.](https://medium.com/@macomeza/5-desafios-de-la-an%C3%A1litica-de-datos-950906b0fa42)

### Volumen
> Cuando los negocios tienen más datos que los que pueden procesar y analizar, tienen un problema de volumen.

#### Amazon S3
Mientras más cerca esten los datos de tu sistema de procesamiento, mejor rendimiento tendrá el procesamiento. S3 significa Amazon Simple Storage Service (Servicio de Almacenamiento Simple) permite almacenar todos los datos semi estructurados y no estructurados.

En S3 los archivos se guardan como objetos dentro de folders llamados cubetas (buckets). Un *objeto* está compuesto del archivo y la metadata del mismo. Los buckets son los contenedores lógicos para los objetos, se puede controlar el acceso a cada bucket, incluyendo permiso de creación, eliminación, visualizar. Siempre se incluye una bitácora de acceso a cada bucket y sus objetos.

Cada vez que se carga un objeto a un bucket en S3, se crea una clave única para el objeto, incluye un identificador de la versión del objeto.

#### Lago de Datos - Data Lake
Un lago de datos es un repositorio centalizado que nos permite almacenar datos del tipo estructurado, semi estructurado y no estrucutado a cualquier escala.

Almacenar los archivos de una organización conlleva los siguientes desafios, en que carpeta debería almacenarlo, usar prefijos o sufijos para identificar versiones, se divide por tema específico o departamento. A partir de lo anteriormente descrito y la necesidad de organizar mejor la información de cada vez mayor volumen se dio el surgimiento de los lagos de datos.

El lago de datos nos permite comprender que información es la que tenemos almacenada a través de catálogos e indexación de la información.

- Es un repositorio centralizado.
- Almacena datos estructurados.
- Almacena datos semi estructurados y no estructurados.

[DataLakes](https://aws.amazon.com/es/big-data/datalakes-and-analytics/)

##### ¿Qué datos podemos guardar de un lago de datos?
- Se puede alimentar de información proveniente de sistemas y servidores propios de la organización, los soporta en su formato original. No requiere crear estructuras de datos, esquemas y transformaciones previas.
- Datos relacionales, datos de las aplicaciones del negocio, aplicaciones móviles, dispositovos conectados a internet y redes sociales.
- Obtener datos en vivo, en tiempo real.
- Aprendizaje de máquina, se pueden generar conocimientos, incluyendo reportería sobre datos históricos o construcción de modelos para pronóstico u optimización.
- Analítica de datos, dar acceso a la organización a procesar y a los datos ya procesados.

##### Beneficios de los lagos de datos
- Fuente única de la verdad - para lograrlo se debe organizar adecuadamente y estructurar los datos que ingresarán al lago.
- Guardar cualquier tipo de datos, sin importar la estructura - guardar arhivos relevantes, se deben establecer políticas de retención para que los datos se mantengan al día.
- Puede ser analizada utilizando inteligencia artificial y aprendizaje de máquina - podemos ir más allá de las capacidades humanas de analítica y encontrar conocimientos significantivos.
- Es una solución eficiente en costo.
- Implementa cumplimiento y seguridad lideres en la industria.
- Ofrece la ventaja de obtener datos de varias formas.
- Categorizar y gestionar los datos. Podemos usar AWS Glue para entender la estructura de los datos de nuestro lago de datos, prepararla y cargarla a almacenamiento de dato, una vez Glue ha catalogado los datos, se puede buscar inmediatamente.
- Permite convertir nuestros datos a conocimientos significativos.

#### Amazon EMR y Lagos de Datos
Las organizaciones pueden ubicar los datos en un Lago de Datos y usar su propio marco de trabajo distribuido para el procesamiento de los mismos, tales como Apache Hadoop y Spark son soportados.

#### Preparación de un Lago de Datos
> Los científicos de datos invierten el 60% de su tiempo limpiando y organizando datos y el 19% recolentando conjuntos de datos.

La preparación de los datos requiere bastante esfuerzo, no hay atajos o respuestas fáciles respecto a cómo realizar la limpieza, transformación y recolección de datos para el Lago de Datos. Sin embargo, hay servicios que nos pueden ayudar a automatizar muchos de estos procesos que consumen bastante tiempo.

#### AWS Lake Formation
> AWS Lake Formation es un servicio que facilita la configuración de un lago de datos seguro en cuestión de días. Un lago de datos es un repositorio centralizado, seleccionado y seguro que almacena todos sus datos, tanto en su forma original como preparados para análisis. Un lago de datos le permite desglosar los silos de datos y combinar diferentes tipos de análisis para obtener información y tomar mejores decisiones empresariales.

- Organizar y curar datos.
- Asegurar el acceso a los datos a través del Lago de Datos.
- Orquestar las tareas de transformación con otros servicios de AWS.

[AWS Lake Formation](https://aws.amazon.com/es/lake-formation)

#### Cuál es mejor un Data Warehouse o un Data Lake
Son diferentes soluciones para diferentes problemas.

Data warehouse - Almacen de Datos
: Es un repositorio central da datos estructurados de varios origenes de datos. Estos datos son transformados, agrupados y preparados para reportes y análisis del negocio.

Los datos fluyen desde los sistemas transaccionales, bases de datos relacionales y otras fuentes. Pueden incluir datos semi estructurados y no estructurados. Estas fuentes deben ser transformadas a datos estructurados antes de poderse almacenar.

Los datos se guardan en el Data Warehouse usando un esquema, el cual define cómo los datos se guardarán en tablas, columnas y filas. El esquema fuerza algunas restricciones en los datos para asegurar su integridad. El proceso de transformación también requiere algunos pasos para que los datos se ajusten al esquema. Después del primer consumo de datos, el proceso puede continuar regularmente.

Los analistas de negocio, científicos de datos y los tomadores de decisiones acceden los datos a través de herramienta de inteligencia de negocio, clientes SQL y otras apliaciones de analítica. 

Data marts
: Es un conjunto de datos de un Data Warehouse. Se enfoca en un tema específico o en una área funcional de la organización.

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
Utiliza una arquitectura de procesamiento distribuida, en la cual una tarea se realiza por varios servidores. Cada pieza del trabajo es distribuida a un cluster de servidores y se puede ejecutar y volver a ejecutar en cualquiera de los servidores. Usan frecuentemente el HDFS (sistema de archivos distribuido de Hadoop, en español), para almacenar los datos localmente para su procesamiento. Luego los resultados se reducen a un solo conjunto de datos. Un nodo, que fue designado como el principal, controla la distribución de tareas y puede manejar fallas automáticamente.

Para implementar Hadoop en AWS se recomienda utilizar EMR. El cual permite que escojamos dos sistemas de archivos (un conjunto de reglas para gobernar cómo se guardan los archivos).
- HDFS el nativo, el cual crea una copia temporal de los datos y luego la procesa y almacena en S3.
- EMRFS la versión adaptada, la cual no necesita una copia temporal ahorrando segundos valiosos.

### Velocidad - procesamiento de datos
> Cuando las organizaciones necesitan rápido conocimiento desde los datos que están recolectando, per los sistemas no pueden satisfacer la demanda, se presenta un problema de velocidad.

#### Procesamiento de la información
Es la recolección y manipulación de los datos para producir información con sentido para la organización. Se divide en dos partes, la recolección y el procesamiento.

*Recolección* es obtener datos de diferentes fuentes y guardarlos en un destino común para su análisis.
*Procesamiento* es darle formato, organizar y hacerle filtros a los datos.

Hay dos tipos de procesamiento de datos
- Lotes, se recibirán datos en intervalos programados (diario, por hora, cada n minutos), tienden a ser predecibles pues se espera que el tiempo sea constante a través del tiempo (suponiendo similar volumen de datos en cada lote). Pueden necesitarse también intervalos periódicos irregulares, esto es un poco más impredecible pues el volumen de datos puede cambiar muchísimo.
- En directo - casi en tiempo real, se transmite en lotes a intervalos muy pequeños, tipicamente e procesan en los siguientes minutos de haberse obtenido. En tiempo real, se recibe en interavlos aún más pequeños y se procesa en milisegundos.

