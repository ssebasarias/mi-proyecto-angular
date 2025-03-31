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
