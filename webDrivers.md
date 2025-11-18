# ⚙️ Guía Definitiva: Configuración de WebDrivers para KNIME en Windows 64-bit (Chrome & Edge)

Una guía paso a paso para solucionar el error `"Unable to obtain driver for Edge/Chrome..."` y configurar un entorno de automatización web con KNIME en una instalación limpia de Windows.

## Un Problema Común: "Unable to obtain driver"

Si estás utilizando los nodos de automatización web de KNIME, el error `"Unable to obtain driver for Edge/Chrome..."` es común. Ocurre cuando KNIME no puede encontrar o ejecutar el controlador web (**WebDriver**) necesario para interactuar con tu navegador.

La solución se centra en tres pasos clave: **Coincidencia de Versiones**, **Descarga** y **Configuración del PATH** de Windows.

---

## 1. Coincidencia de Versiones: El Paso Crítico

El WebDriver que uses **debe coincidir** en los tres primeros segmentos con la versión de tu navegador.

### 1.1. Verificar la Versión de Tu Navegador

| Navegador | Dirección para verificar la versión |
| :--- | :--- |
| **Google Chrome** | Escribe `chrome://version` en la barra de direcciones. |
| **Microsoft Edge** | Escribe `edge://version` en la barra de direcciones. |

> **Ejemplo:** Si tu versión de Chrome es `129.0.6647.110`, necesitas un **ChromeDriver** que comience con `129.0.6647`.

---

## 2. Descarga de los WebDrivers

Una vez que tengas las versiones exactas, procede a descargar los ejecutables.

### 2.1. ChromeDriver (Para Google Chrome)

1.  **Visita el sitio oficial:** Busca y descarga el **ChromeDriver** oficial.
2.  **Busca la versión:** Localiza la versión del driver que **coincida** con los primeros tres números de la versión de tu Chrome.
3.  **Descarga y Descomprime:** Descarga el archivo ZIP para `win64` y extrae el ejecutable **`chromedriver.exe`**.

### 2.2. MSEdgeDriver (Para Microsoft Edge)

1.  **Visita el sitio oficial:** Busca y descarga el **MSEdgeDriver** (Microsoft Edge WebDriver) oficial.
2.  **Busca la versión:** Localiza el enlace que corresponda a los primeros tres números de tu versión de Edge.
3.  **Descarga y Descomprime:** Descarga el archivo ZIP para Windows y extrae el ejecutable **`msedgedriver.exe`**.

---

## 3. Configuración del PATH de Windows (Solución Global)

Configurar la variable de entorno **PATH** permite que KNIME encuentre los WebDrivers automáticamente desde cualquier lugar del sistema.

### 3.1. Crear y Organizar la Carpeta de Drivers

1.  Crea una carpeta dedicada para tus drivers.
    * **Ruta recomendada:** `C:\WebDrivers`
2.  Copia los archivos ejecutables que descargaste a esta nueva carpeta:
    * `C:\WebDrivers\chromedriver.exe`
    * `C:\WebDrivers\msedgedriver.exe`

### 3.2. Modificar la Variable de Entorno PATH

1.  Abre el menú de **Inicio** y busca **"Editar las variables de entorno del sistema"**.
2.  Haz clic en el botón **"Variables de entorno..."**.
3.  En la sección **"Variables del sistema"**, busca y selecciona la variable llamada **`Path`**.
4.
