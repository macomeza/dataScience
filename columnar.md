# ¿Qué es el formato columnar?

En ciencia de datos se busca dar respuestas a consultas de los tomadores de decisiones y analistas, lo cual demanda preparación de datos, las principales actividades son limpieza de datos, darles forma y mezclarlos.

Otro factor que hace diferencia en cuanto a rendimiento y costo es la forma de almacenar la información.

## Filas vs columnas

Los datos tradicionalmente se guardan en filas, tal como los archivos CSV, este formato está optimizado para escritura. 

La otra opción es guardarlos por columnas, esto tiene la ventaja que podemos escanear solo los campos de nuestro intereses, ahorrando lectura de disco, ahorrando tamaño escaneado y tiempo. Los archivos OCR y Parquet son ejemplos de este tipo.

## Diferencia en tiempo y costo

El formato columnar también permite compresión, hay varios formatos, algunos orientados a reducir al máximo posible el almacenamiento, otros orientados a lectura rápida. El tipo de compresión balanceado se llama Snappy, es muy eficiente para ahorrar espacio y para lectura.

## Qué debo hacer para aprovechar el formato parquet

Si tenemos un datalake en AWS S3 en formato de filas, podemos correr un crawler que capturará la estructura del archivo y creará un esquema de tabla (metadata), a la vez hará posible poder hacer consultas desde Athena (cómo si fuera nuestro cliente para ejecutar consultas). En Athena podemos crear una tabla tipo columnar con la siguiente instrucción:

CREATE TABLE <nombre tabla parquet<
WITH (
      format = 'Parquet',
      write_compression = 'SNAPPY')
AS SELECT *
FROM <tabla origen almacenada en filas>;
  
Así de fácil, podremos ahorrar tiempo, almacenamiento y costo.
  
Espero haya sido de utilidad, hasta la próxima.
