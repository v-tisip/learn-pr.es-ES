Una vez que tenemos una idea de cómo vamos a almacenar los datos en cuentas de almacenamiento, blobs y contenedores, podemos pensar en los recursos de Azure que es necesario crear para admitir la aplicación.

### <a name="storage-accounts"></a>Cuentas de almacenamiento

La creación de la cuenta de almacenamiento es una actividad administrativa que tiene lugar antes de implementar y ejecutar la aplicación. Las cuentas se crean normalmente mediante un script de implementación o de configuración del entorno, una plantilla de Azure Resource Manager, o un administrador las crea manualmente. Las aplicaciones que no son herramientas administrativas generalmente no tienen permisos para crear cuentas de almacenamiento.

### <a name="containers"></a>Contenedores

A diferencia de la creación de cuentas de almacenamiento, la creación de contenedores es una actividad ligera que tiene sentido realizarla desde dentro de una aplicación. No es raro que las aplicaciones creen y eliminen contenedores como parte de su trabajo.

En el caso de aplicaciones que se basan en un conjunto conocido de contenedores con nombres codificados de forma rígida o preconfigurados, la práctica habitual es permitir que la aplicación cree los contenedores que necesita al inicio o en el primer uso si todavía no existen. Al permitir que la aplicación cree contenedores en lugar de hacerlo como parte de la implementación de la aplicación se elimina la necesidad de que tanto la aplicación como el proceso de implementación conozcan los nombres de los contenedores que usa la aplicación.

## <a name="exercise"></a>Ejercicio

Vamos a completar una aplicación de ASP.NET Core sin terminar mediante la adición de código para usar Azure Blob Storage. Este ejercicio tiene que ver más con la exploración de la API de Blob Storage que con el diseño de una organización y el esquema de nomenclatura, pero esta es una introducción rápida de la aplicación y cómo almacena los datos:

**Captura de pantalla de lista de tareas de la aplicación, ya que no vamos a verla ejecutada hasta el final**

Nuestra aplicación funciona como una carpeta compartida que acepta cargas de archivos y permite que estén disponibles para su descarga. No se usa en su lugar una base de datos para organizar los blobs, se corrigen los nombres de los archivos cargados y se usan directamente como nombres de blob. Todos los archivos cargados se almacenan en un único contenedor.

El código con el que comenzaremos se compila y ejecuta, pero las partes responsables de almacenar y cargar los datos están vacías. Una vez completado el código, implementaremos la aplicación en Azure App Service y la probaremos.

Vamos a configurar la infraestructura de almacenamiento de nuestra aplicación.

### <a name="resource-group-and-storage-account"></a>Grupo de recursos y cuenta de almacenamiento
En primer lugar, crearemos un grupo de recursos que contenga todos los recursos de este ejercicio. Al final lo eliminaremos para limpiar todo lo que creemos. También vamos a crear la cuenta de almacenamiento que nuestra aplicación usará para almacenar los blobs.

Use el terminal de Azure Cloud Shell para crear el grupo de recursos y la cuenta de almacenamiento mediante la ejecución de los siguientes comandos de la CLI de Azure. Deberá proporcionar un nombre único para la cuenta de almacenamiento; anótelo para usarlo más tarde. La elección de `eastus` como ubicación es arbitraria.

```console
az group create --name blob-exercise-group --location eastus
az storage account create --name <your-unique-storage-account-name> --resource-group blob-exercise-group --location eastus --kind StorageV2
```

**La lista de tareas a continuación deberá ir en el módulo de Azure Storage**

> [!NOTE]
> ¿Por qué`--kind StorageV2`? Hay unos cuantas clases diferentes de cuentas de almacenamiento. En la mayoría de los escenarios, usará cuentas de almacenamiento de fin general v2 (se indica con `StorageV2`). El único motivo de que se deban especificar aquí las cuentas de almacenamiento v2 es que todavía son bastante nuevas y aún no son las predeterminadas en Azure Portal o la CLI de Azure.

### <a name="container"></a>Contenedor
La aplicación con la que vamos a trabajar en este módulo usa un único contenedor. Vamos a seguir el procedimiento recomendado de dejar que la aplicación cree el contenedor al inicio. Sin embargo, se puede hacer desde la CLI de Azure: ejecute `az storage container create -h` en el terminal de Cloud Shell si le gustaría ver la documentación.