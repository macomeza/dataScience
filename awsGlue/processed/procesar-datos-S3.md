# Crear una tabla procesada en Glue

En esta publicación aprenderemos una forma para generar un archivo procesado a partir de datos crudos, para así poder consultarlos desde Athena y también desde QuickSight.

Paso 1, crearemos un crawler para que obtenga la estructura de nuestros archivos. Esto lo haremos desde Glue Studio. Luego le daremos clic a Crawlers y luego al botón Create crawler.

![Crear un crawler](https://github.com/macomeza/dataScience/blob/main/awsGlue/processed/01-creandoCrawler.png)

Paso 2, le daremos un nombre y descripción, luego le daremos clic en next.

![Nombrando al Crawler](https://github.com/macomeza/dataScience/blob/main/awsGlue/processed/02-nombrandoCrawler.png)

Paso 3, en el origen de datos le daremos clic en add a data source, seleccionaremos S3 y luego el directorio que contiene los archivos que nos interesan, es importante terminar la carpeta con la /.

![Añadir una fuente de datos](https://github.com/macomeza/dataScience/blob/main/awsGlue/processed/03-a%C3%B1adirFuenteDatos.png)

Buscamos la carpeta dentro del bucket

![Buscar la carpeta](https://github.com/macomeza/dataScience/blob/main/awsGlue/processed/04-buscar.png)

Seleccionamos la carpeta que deseamos

![Seleccionar la carpeta](https://github.com/macomeza/dataScience/blob/main/awsGlue/processed/05-seleccionarCarpeta.png)

Añadimos la diagonal a la ruta

![Añadir la diagonal](https://github.com/macomeza/dataScience/blob/main/awsGlue/processed/06-a%C3%B1adirDiagonal.png)

Paso 4, seleccionaremos el rol que tiene acceso a Glue.

Paso 5, seleccionaremos la base de datos destino, luego le pondremos un prefijo y le daremos clic en next.

Paso 6, le damos clic en guardar y luego lo pondremos a ejecutar.

Listo, solo es de esperar a que concluya la corrida, nos habrá añadido la tabla a la base de datos, esta contendrá la estructura (schema) y podemos previsualizar los datos desde Athena.

Posteriormente, podemos ingresar a QuickSight, crear un dataset cuyo origen es Athena y seleccionamos las tablas que nos interesan para crear nuestro tablero de control.

Espero sea de gran utilidad, hasta la próxima.
