El siguiente es un flujo de trabajo típico para aplicaciones que usan Azure Blob Storage:

1. **Recuperar la configuración**: al inicio, cargue la configuración, como la cadena de conexión con la clave de cuenta. Esto es necesario para autenticar las llamadas API.
1. **Inicializar el cliente**: use la cadena de conexión para inicializar la biblioteca de cliente de Azure Storage. Esta acción crea los objetos que usará la aplicación para trabajar con la API de Blob Storage.
1. **Usar**: realice llamadas API con la biblioteca de cliente para trabajar con contenedores y blobs.

## <a name="configure-your-connection-string"></a>Configuración de una cadena de conexión

Antes de escribir ningún código, necesitará la cadena de conexión de la cuenta de almacenamiento que usará. 

La cadena de conexión incluye la clave de la cuenta. La clave de la cuenta se considera un secreto y se debe almacenar de forma segura. Almacenaremos la cadena de conexión en una configuración de aplicación de App Service. Una configuración de aplicación es un lugar seguro para los secretos de la aplicación, pero no admite el desarrollo local y no es una solución de extremo a extremo sólida.

> [!WARNING]
> **No coloque las claves de la cuenta de almacenamiento en archivos de configuración desprotegidos.** Las claves de la cuenta de almacenamiento permiten acceso completo a la cuenta de almacenamiento. La pérdida de una clave puede provocar daños irrecuperables y grandes facturas. Consulte la sección Recursos adicionales al final de este módulo como guía de almacenamiento y asesoramiento sobre cómo recuperarse de una clave perdida.

## <a name="initialize-the-blob-storage-object-model"></a>Inicialización del modelo de objetos de Blob Storage

En el SDK de Azure Storage para .NET Core, el patrón estándar para usar Blob Storage consta de los pasos siguientes:

1. Llame a `CloudStorageAccount.Parse` (o `TryParse`) con la cadena de conexión para obtener `CloudStorageAccount`.
1. Llame a `CreateCloudBlobClient` en `CloudStorageAccount` para obtener `CloudBlobClient`.
1. Llame a `GetContainerReference` en `CloudBlobClient` para obtener `CloudBlobContainer`.
1. Use métodos en el contenedor para obtener una lista de blobs y obtener referencias a blobs individuales para cargar y descargar datos.

En el código, los pasos del 1 al 3 tienen el aspecto siguiente:

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); // or TryParse()
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
```

Ninguna parte de este código de inicialización realiza llamadas a través de la red. Esto significa que las excepciones que proceden de información incorrecta no se producirán hasta más tarde; por ejemplo, la llamada a `GetContainerReference` se realizará correctamente tanto si el contenedor existe realmente en la cuenta como si no.

## <a name="create-containers-at-startup"></a>Creación de contenedores al inicio

Es habitual que las aplicaciones creen los contenedores necesarios en el código, incluso cuando sabemos cuáles serán esos contenedores por adelantado. Llamar a `CreateIfNotExistsAsync` en `CloudBlobContainer` es la mejor manera de hacerlo, y la usaremos para crear cada contenedor que sabemos que será necesario antes de usarlo.

`CreateIfNotExistsAsync` *realiza* una llamada de red a Azure Storage. Un procedimiento recomendado es llamar a una vez al inicio y no cada vez que accedemos a un contenedor.

## <a name="exercise"></a>Ejercicio

### <a name="clone-and-explore-the-unfinished-app"></a>Clonación y exploración de la aplicación sin terminar

Primero, vamos a clonar la aplicación de inicio desde GitHub. En el terminal de Cloud Shell, ejecute el siguiente comando para obtener una copia del código fuente y abrirla en el editor:

```console
git clone TODO
cd TODO
code .
```

Abra el archivo `Controllers/FilesController.cs`.

Este controlador implementa una API con tres acciones:

* **Indexar** (GET /api/Files) devuelve una lista de direcciones URL, una para cada archivo que se ha cargado. El front-end de la aplicación llama a este método para crear una lista de hipervínculos a los archivos cargados.
* **Cargar** (POST /api/Files) recibe un archivo cargado y lo guarda.
* **Descargar** (GET /api/Files/{file-name}) descarga un archivo individual por su nombre.

Cada método usa una instancia de `IStorage` denominada `storage` para realizar su trabajo. Hay una implementación incompleta de `IStorage` en `Models/BlobStorage.cs`.

### <a name="add-the-nuget-package"></a>Incorporación del paquete NuGet

En primer lugar, agregue una referencia al SDK de Azure Storage. En el terminal, ejecute lo siguiente:

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

De esta forma se garantiza que usamos la versión más reciente de la biblioteca de cliente de almacenamiento de blobs.

### <a name="configure"></a>Configuración

Nuestra aplicación de inicio ya incluye la estructura de configuración que necesitamos. El parámetro de constructor `IOptions<AzureStorageConfig>` en `BlobStorage` tiene dos propiedades: la cadena de conexión de la cuenta de almacenamiento y el nombre del contenedor en el que nuestra aplicación almacenará los blobs. No hay código en el método `ConfigureServices` de `Startup.cs` que carguelos valores de configuración cuando se inicia la aplicación.

En este ejercicio, ejecutará la aplicación en Azure App Service, por lo que agregaremos más adelante los valores de configuración a la configuración de aplicación de App Service. Por ahora, no es necesario realizar ningún trabajo relacionado con la configuración.

### <a name="initialize"></a>Initialize

Abra `BlobStorage.cs`.

Busque el método `Initialize`. Nuestra aplicación llamará a este método cuando se use por primera vez. Si tiene curiosidad, puede examinar `ConfigureServices` en `Startup.cs` para ver cómo hacerlo. 

`Initialize` es donde queremos crear nuestro contenedor si aún no existe. Rellene `Initialize` con el código siguiente y guarde su trabajo:

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```