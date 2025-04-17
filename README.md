# Documentación del Proceso de Despliegue de Angular en Azure Static Web Apps

## 1. Creación del Proyecto Angular

* **Instalar Angular CLI (si aún no lo tienes instalado):**
    ```bash
    npm install -g @angular/cli
    ```
    Este comando instala la interfaz de línea de comandos de Angular de forma global en tu sistema, lo que te permite crear, construir y servir aplicaciones Angular.

* **Crear un nuevo proyecto Angular:**
    ```bash
    ng new mi-proyecto-angular
    ```
    Reemplaza `mi-proyecto-angular` con el nombre que quieras darle a tu proyecto. Este comando creará una nueva carpeta con la estructura básica de un proyecto Angular y te preguntará si quieres configurar el enrutamiento y qué tipo de hojas de estilo quieres usar.

* **Navegar a la carpeta del proyecto:**
    ```bash
    cd mi-proyecto-angular
    ```
    Este comando te mueve al directorio raíz de tu proyecto Angular recién creado.

* **Generar la carpeta `dist` (construcción para producción):**
    ```bash
    ng build --prod
    ```
    Este comando construye tu aplicación Angular en modo de producción. Los archivos optimizados para el despliegue se generarán dentro de la carpeta `dist/mi-proyecto-angular`.

## 2. Iniciar Sesión en Azure

* **Desde la Consola (Azure CLI):**
    * **Instalar Azure CLI (si no lo tienes instalado):** Sigue las instrucciones en la [documentación oficial de Microsoft](https://docs.microsoft.com/es-es/cli/azure/install-azure-cli).
    * **Iniciar sesión en Azure:**
        ```bash
        az login
        ```
        Este comando abrirá una ventana en tu navegador donde podrás ingresar tus credenciales de cuenta de Azure.

* **Desde la Extensión de Azure en VS Code:**
    1.  Abre **Visual Studio Code**.
    2.  En la barra de actividad (normalmente a la izquierda), haz clic en el icono de **Azure** (la "A" azul).
    3.  Si no has iniciado sesión, verás un botón que dice **"Sign in to Azure..."**. Haz clic en él y sigue las instrucciones para ingresar tus credenciales de cuenta de Azure.

## 3. Creación del Grupo de Recursos

* **Desde la Consola (Azure CLI):**
    ```bash
    az group create --name angular-group --location centralus
    ```
    * Reemplaza `angular-group` con el nombre que quieras darle a tu grupo de recursos.
    * Reemplaza `centralus` con la ubicación (región) donde quieres crear el grupo de recursos (por ejemplo, `eastus`, `westeurope`, etc.). Puedes ver la lista de ubicaciones disponibles con el comando `az account list-locations --output table`.

* **Desde el Azure Portal:**
    1.  Ve al [Azure Portal](https://portal.azure.com/).
    2.  Haz clic en **"Grupos de recursos"** en el menú de la izquierda.
    3.  Haz clic en el botón **"+ Crear"**.
    4.  Selecciona tu **Suscripción**.
    5.  Ingresa el **Nombre** que quieres darle al grupo de recursos (por ejemplo, `angular-group`).
    6.  Selecciona la **Región** donde quieres crear el grupo de recursos.
    7.  Haz clic en el botón **"Revisar + crear"** y luego en **"Crear"**.

## 4. Creación de la Azure Static Web App

* **Desde el Azure Portal:**
    1.  Ve al [Azure Portal](https://portal.azure.com/).
    2.  Haz clic en **"Crear un recurso"**.
    3.  Busca **"Static Web Apps"** y selecciona el resultado.
    4.  Haz clic en el botón **"Crear"**.
    5.  **Pestaña "Aspectos básicos":**
        * **Suscripción:** Selecciona tu suscripción de Azure (por ejemplo, "Azure for Students").
        * **Grupo de recursos:** Selecciona el grupo de recursos que creaste (por ejemplo, `angular-group`).
        * **Nombre:** Elige un nombre para tu Static Web App (por ejemplo, `mi-proyecto-angular-swa`).
        * **Región:** Selecciona una región.
        * **Plan:** Selecciona **"Gratis"**.
    6.  **Sección "Detalles de la implementación":**
        * **Origen de la implementación:** Selecciona **"GitHub"**.
        * Haz clic en **"Iniciar sesión con GitHub"** y autoriza tu cuenta si es necesario.
        * **Organización:** Selecciona tu nombre de usuario de GitHub.
        * **Repositorio:** Selecciona el repositorio de tu proyecto Angular (`mi-proyecto-angular`).
        * **Rama:** Selecciona la rama `main`.
    7.  **Sección "Detalles de la compilación":**
        * **Preajustes de compilación:** Selecciona **"Angular"**.
        * **Ubicación de la aplicación:** `/`
        * **Ubicación de la API:** (Déjalo en blanco si no tienes una API)
        * **Ubicación del artefacto de la aplicación:** `dist/mi-proyecto-angular/browser`
    8.  **Pestaña "Revisar + crear":** Revisa la configuración y haz clic en **"Crear"**.


# 🧠 Documentación del Proceso en Azure Machine Learning – Clasificación Automatizada

## 🔹 1. Creación del recurso de Azure Machine Learning

1. Ingresé al portal de [Azure](https://portal.azure.com).
2. Busqué **“Machine Learning”** y seleccioné la opción **"Crear"**.
3. Completé los campos básicos:
   - **Nombre del recurso**: _(Nombre personalizado)_
   - **Grupo de recursos**: _(Nombre del grupo existente o nuevo)_
   - **Tipo de plan**: _Gratis (Free Tier)_
   - Dejé el resto de opciones con su configuración predeterminada.
4. Una vez creado el recurso, ingresé a él y seleccioné **“Launch Studio”** para entrar a Azure ML Studio.

---

## 🔹 2. Creación del entorno de cómputo

1. Dentro de Azure ML Studio, fui a la sección **“Compute”**.
2. Seleccioné **"Compute Instances"** y creé una nueva con:
   - **Tipo de máquina**: _CPU (2 núcleos)_
   - **Plan de bajo costo**: _La opción más económica disponible_
   - Dejé la configuración predeterminada.
3. Esperé a que la instancia se activara correctamente (estado: *Running*).

---

## 🔹 3. Ejecución del entrenamiento automatizado (AutoML)

1. Fui al módulo de **"Automated ML"** y seleccioné **“New Automated ML run”**.
2. Asigné un **nombre al experimento**.
3. En la sección de datos:
   - Seleccioné **“+ Create dataset”**
   - Elegí la opción **“From local files”**
   - Subí un archivo CSV con datos de ejemplo proporcionados.
   - Dejé todas las configuraciones predeterminadas.
4. Seleccioné como columna objetivo la variable `target` ya que es una variable categórica (clasificación).
5. Elegí la tarea de **Clasificación**.
6. En la configuración de validación:
   - Dejé activado el método **automático** para separar los datos en entrenamiento y prueba.
7. En la sección de cómputo:
   - Seleccioné la **máquina virtual creada previamente** (Compute Instance).

---

## 🔹 4. Resultado del experimento

Una vez completado el entrenamiento, el sistema mostró el resumen del **mejor modelo encontrado**:

- **Algoritmo aplicado**:  
  `MaxAbsScaler + ExtremeRandomTrees`
  
- **Métrica principal (AUC ponderado)**:  
  `1.00000` (indica una excelente capacidad de clasificación)

- **Otros detalles:**
  - Muestreo: 100%
  - No se ha desplegado como API aún
  - Aún no se ha registrado oficialmente el modelo

---

## 🔹 5. Observaciones

- El proceso no arrojó errores y finalizó con éxito.
- El modelo mostró un rendimiento perfecto sobre los datos cargados.
- Todavía se puede:
  - Probar el modelo con nuevos datos
  - Desplegar el modelo como un servicio web (API)
  - Descargar el modelo o exportar el código generado automáticamente
