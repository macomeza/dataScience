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

A continuación te invito a conocer para cada "V" una mejor descripción y los servicios que pone AWS para cada desafío.
- [Volumen](https://github.com/macomeza/dataScience/blob/main/volumen.md#volumen)
- [Velocidad](https://github.com/macomeza/dataScience/blob/main/velocidad.md#velocidad)
- [Variedad - (en proceso)](https://github.com/macomeza/dataScience/blob/main/variedad.md#variedad)

