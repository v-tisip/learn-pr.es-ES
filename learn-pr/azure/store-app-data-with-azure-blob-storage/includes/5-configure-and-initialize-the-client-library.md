<span data-ttu-id="87867-101">El siguiente es un flujo de trabajo típico para aplicaciones que usan Azure Blob Storage:</span><span class="sxs-lookup"><span data-stu-id="87867-101">The following is the typical workflow for apps that use Azure Blob storage:</span></span>

1. <span data-ttu-id="87867-102">**Recuperar la configuración**: al inicio, cargue la configuración, como la cadena de conexión con la clave de cuenta.</span><span class="sxs-lookup"><span data-stu-id="87867-102">**Retrieve configuration**: At startup, load the configuration, such as the connection string with the account key.</span></span> <span data-ttu-id="87867-103">Esto es necesario para autenticar las llamadas API.</span><span class="sxs-lookup"><span data-stu-id="87867-103">This is needed to authenticate API calls.</span></span>
1. <span data-ttu-id="87867-104">**Inicializar el cliente**: use la cadena de conexión para inicializar la biblioteca de cliente de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="87867-104">**Initialize client**: Use the connection string to initialize the Azure Storage client library.</span></span> <span data-ttu-id="87867-105">Esta acción crea los objetos que usará la aplicación para trabajar con la API de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="87867-105">This creates the objects the app will use to work with the Blob storage API.</span></span>
1. <span data-ttu-id="87867-106">**Usar**: realice llamadas API con la biblioteca de cliente para trabajar con contenedores y blobs.</span><span class="sxs-lookup"><span data-stu-id="87867-106">**Use**: Make API calls with the client library to operate on containers and blobs.</span></span>

## <a name="configure-your-connection-string"></a><span data-ttu-id="87867-107">Configuración de una cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="87867-107">Configure your connection string</span></span>

<span data-ttu-id="87867-108">Antes de escribir ningún código, necesitará la cadena de conexión de la cuenta de almacenamiento que usará.</span><span class="sxs-lookup"><span data-stu-id="87867-108">Before writing any code, you'll need the connection string for the storage account you will use.</span></span> 

<span data-ttu-id="87867-109">La cadena de conexión incluye la clave de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="87867-109">The connection string includes your account key.</span></span> <span data-ttu-id="87867-110">La clave de la cuenta se considera un secreto y se debe almacenar de forma segura.</span><span class="sxs-lookup"><span data-stu-id="87867-110">The account key is considered a secret and should be stored securely.</span></span> <span data-ttu-id="87867-111">Almacenaremos la cadena de conexión en una configuración de aplicación de App Service.</span><span class="sxs-lookup"><span data-stu-id="87867-111">We will store the connection string in an App Service application setting.</span></span> <span data-ttu-id="87867-112">Una configuración de aplicación es un lugar seguro para los secretos de la aplicación, pero no admite el desarrollo local y no es una solución de extremo a extremo sólida.</span><span class="sxs-lookup"><span data-stu-id="87867-112">An application setting is a secure place for application secrets, but it does not support local development and is not a robust, end-to-end solution on its own.</span></span>

> [!WARNING]
> <span data-ttu-id="87867-113">**No coloque las claves de la cuenta de almacenamiento en archivos de configuración desprotegidos.**</span><span class="sxs-lookup"><span data-stu-id="87867-113">**Do not place storage account keys in code or in unprotected configuration files.**</span></span> <span data-ttu-id="87867-114">Las claves de la cuenta de almacenamiento permiten acceso completo a la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="87867-114">Storage account keys enable full access to your storage account.</span></span> <span data-ttu-id="87867-115">La pérdida de una clave puede provocar daños irrecuperables y grandes facturas.</span><span class="sxs-lookup"><span data-stu-id="87867-115">Leaking a key can result in unrecoverable damage and large bills.</span></span> <span data-ttu-id="87867-116">Consulte la sección Recursos adicionales al final de este módulo como guía de almacenamiento y asesoramiento sobre cómo recuperarse de una clave perdida.</span><span class="sxs-lookup"><span data-stu-id="87867-116">See the Additional Resources section at the end of this module for storage guidance and advice about how to recover from a leaked key.</span></span>

## <a name="initialize-the-blob-storage-object-model"></a><span data-ttu-id="87867-117">Inicialización del modelo de objetos de Blob Storage</span><span class="sxs-lookup"><span data-stu-id="87867-117">Initialize the Blob storage object model</span></span>

<span data-ttu-id="87867-118">En el SDK de Azure Storage para .NET Core, el patrón estándar para usar Blob Storage consta de los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="87867-118">In the Azure Storage SDK for .NET Core, the standard pattern for using Blob storage consists of the following steps:</span></span>

1. <span data-ttu-id="87867-119">Llame a `CloudStorageAccount.Parse` (o `TryParse`) con la cadena de conexión para obtener `CloudStorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="87867-119">Call `CloudStorageAccount.Parse` (or `TryParse`) with your connection string to get a `CloudStorageAccount`.</span></span>
1. <span data-ttu-id="87867-120">Llame a `CreateCloudBlobClient` en `CloudStorageAccount` para obtener `CloudBlobClient`.</span><span class="sxs-lookup"><span data-stu-id="87867-120">Call `CreateCloudBlobClient` on the `CloudStorageAccount` to get a `CloudBlobClient`.</span></span>
1. <span data-ttu-id="87867-121">Llame a `GetContainerReference` en `CloudBlobClient` para obtener `CloudBlobContainer`.</span><span class="sxs-lookup"><span data-stu-id="87867-121">Call `GetContainerReference` on the `CloudBlobClient` to get a `CloudBlobContainer`.</span></span>
1. <span data-ttu-id="87867-122">Use métodos en el contenedor para obtener una lista de blobs y obtener referencias a blobs individuales para cargar y descargar datos.</span><span class="sxs-lookup"><span data-stu-id="87867-122">Use methods on the container to get a list of blobs and/or get references to individual blobs to upload and download data.</span></span>

<span data-ttu-id="87867-123">En el código, los pasos del 1 al 3 tienen el aspecto siguiente:</span><span class="sxs-lookup"><span data-stu-id="87867-123">In code, steps 1&ndash;3 look like this:</span></span>

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); // or TryParse()
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
```

<span data-ttu-id="87867-124">Ninguna parte de este código de inicialización realiza llamadas a través de la red.</span><span class="sxs-lookup"><span data-stu-id="87867-124">None of this initialization code makes calls over the network.</span></span> <span data-ttu-id="87867-125">Esto significa que las excepciones que proceden de información incorrecta no se producirán hasta más tarde; por ejemplo, la llamada a `GetContainerReference` se realizará correctamente tanto si el contenedor existe realmente en la cuenta como si no.</span><span class="sxs-lookup"><span data-stu-id="87867-125">This means exceptions that occur from incorrect information won't be thrown until later; for example, the call to `GetContainerReference` will succeed whether or not the container actually exists in the account.</span></span>

## <a name="create-containers-at-startup"></a><span data-ttu-id="87867-126">Creación de contenedores al inicio</span><span class="sxs-lookup"><span data-stu-id="87867-126">Create containers at startup</span></span>

<span data-ttu-id="87867-127">Es habitual que las aplicaciones creen los contenedores necesarios en el código, incluso cuando sabemos cuáles serán esos contenedores por adelantado.</span><span class="sxs-lookup"><span data-stu-id="87867-127">Common practice is for applications to create needed containers in code, even when we know what those containers will be up-front.</span></span> <span data-ttu-id="87867-128">Llamar a `CreateIfNotExistsAsync` en `CloudBlobContainer` es la mejor manera de hacerlo, y la usaremos para crear cada contenedor que sabemos que será necesario antes de usarlo.</span><span class="sxs-lookup"><span data-stu-id="87867-128">Calling `CreateIfNotExistsAsync` on a `CloudBlobContainer` is the best way to do this, and we should use it to create each container we know we'll need before we use them.</span></span>

<span data-ttu-id="87867-129">`CreateIfNotExistsAsync` *realiza* una llamada de red a Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="87867-129">`CreateIfNotExistsAsync` *does* make a network call to Azure Storage.</span></span> <span data-ttu-id="87867-130">Un procedimiento recomendado es llamar a una vez al inicio y no cada vez que accedemos a un contenedor.</span><span class="sxs-lookup"><span data-stu-id="87867-130">Best practice is to call it once at startup and not every time we access a container.</span></span>

## <a name="exercise"></a><span data-ttu-id="87867-131">Ejercicio</span><span class="sxs-lookup"><span data-stu-id="87867-131">Exercise</span></span>

### <a name="clone-and-explore-the-unfinished-app"></a><span data-ttu-id="87867-132">Clonación y exploración de la aplicación sin terminar</span><span class="sxs-lookup"><span data-stu-id="87867-132">Clone and explore the unfinished app</span></span>

<span data-ttu-id="87867-133">Primero, vamos a clonar la aplicación de inicio desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="87867-133">First, let's clone the starter app from GitHub.</span></span> <span data-ttu-id="87867-134">En el terminal de Cloud Shell, ejecute el siguiente comando para obtener una copia del código fuente y abrirla en el editor:</span><span class="sxs-lookup"><span data-stu-id="87867-134">In the Cloud Shell terminal, run the following command to get a copy of the source code and open it in the editor:</span></span>

```console
git clone TODO
cd TODO
code .
```

<span data-ttu-id="87867-135">Abra el archivo `Controllers/FilesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="87867-135">Open the file `Controllers/FilesController.cs`.</span></span>

<span data-ttu-id="87867-136">Este controlador implementa una API con tres acciones:</span><span class="sxs-lookup"><span data-stu-id="87867-136">This controller implements an API with three actions:</span></span>

* <span data-ttu-id="87867-137">**Indexar** (GET /api/Files) devuelve una lista de direcciones URL, una para cada archivo que se ha cargado.</span><span class="sxs-lookup"><span data-stu-id="87867-137">**Index** (GET /api/Files) returns a list of URLs, one for each file that's been uploaded.</span></span> <span data-ttu-id="87867-138">El front-end de la aplicación llama a este método para crear una lista de hipervínculos a los archivos cargados.</span><span class="sxs-lookup"><span data-stu-id="87867-138">The app front end calls this method to build a list of hyperlinks to the uploaded files.</span></span>
* <span data-ttu-id="87867-139">**Cargar** (POST /api/Files) recibe un archivo cargado y lo guarda.</span><span class="sxs-lookup"><span data-stu-id="87867-139">**Upload** (POST /api/Files) receives an uploaded file and saves it.</span></span>
* <span data-ttu-id="87867-140">**Descargar** (GET /api/Files/{file-name}) descarga un archivo individual por su nombre.</span><span class="sxs-lookup"><span data-stu-id="87867-140">**Download** (GET /api/Files/{file-name}) downloads an individual file by its name.</span></span>

<span data-ttu-id="87867-141">Cada método usa una instancia de `IStorage` denominada `storage` para realizar su trabajo.</span><span class="sxs-lookup"><span data-stu-id="87867-141">Each method uses an `IStorage` instance called `storage` to do its work.</span></span> <span data-ttu-id="87867-142">Hay una implementación incompleta de `IStorage` en `Models/BlobStorage.cs`.</span><span class="sxs-lookup"><span data-stu-id="87867-142">There is an incomplete implementation of `IStorage` in  `Models/BlobStorage.cs`.</span></span>

### <a name="add-the-nuget-package"></a><span data-ttu-id="87867-143">Incorporación del paquete NuGet</span><span class="sxs-lookup"><span data-stu-id="87867-143">Add the NuGet package</span></span>

<span data-ttu-id="87867-144">En primer lugar, agregue una referencia al SDK de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="87867-144">First, add a reference to the Azure Storage SDK.</span></span> <span data-ttu-id="87867-145">En el terminal, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="87867-145">In the terminal, run the following:</span></span>

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

<span data-ttu-id="87867-146">De esta forma se garantiza que usamos la versión más reciente de la biblioteca de cliente de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="87867-146">This will make sure we're using the newest version of the Blob storage client library.</span></span>

### <a name="configure"></a><span data-ttu-id="87867-147">Configuración</span><span class="sxs-lookup"><span data-stu-id="87867-147">Configure</span></span>

<span data-ttu-id="87867-148">Nuestra aplicación de inicio ya incluye la estructura de configuración que necesitamos.</span><span class="sxs-lookup"><span data-stu-id="87867-148">Our starter app already includes the configuration plumbing we need.</span></span> <span data-ttu-id="87867-149">El parámetro de constructor `IOptions<AzureStorageConfig>` en `BlobStorage` tiene dos propiedades: la cadena de conexión de la cuenta de almacenamiento y el nombre del contenedor en el que nuestra aplicación almacenará los blobs.</span><span class="sxs-lookup"><span data-stu-id="87867-149">The `IOptions<AzureStorageConfig>` constructor parameter in `BlobStorage` has two properties: the storage account connection string and the name of the container our app will store blobs in.</span></span> <span data-ttu-id="87867-150">No hay código en el método `ConfigureServices` de `Startup.cs` que carguelos valores de configuración cuando se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="87867-150">There is code in the `ConfigureServices` method of `Startup.cs` that loads the values from configuration when the app starts.</span></span>

<span data-ttu-id="87867-151">En este ejercicio, ejecutará la aplicación en Azure App Service, por lo que agregaremos más adelante los valores de configuración a la configuración de aplicación de App Service.</span><span class="sxs-lookup"><span data-stu-id="87867-151">In this exercise, we will run the app in Azure App Service, so we will add the configuration values to the App Service application settings later.</span></span> <span data-ttu-id="87867-152">Por ahora, no es necesario realizar ningún trabajo relacionado con la configuración.</span><span class="sxs-lookup"><span data-stu-id="87867-152">For now, we don't need to do any work related to configuration.</span></span>

### <a name="initialize"></a><span data-ttu-id="87867-153">Initialize</span><span class="sxs-lookup"><span data-stu-id="87867-153">Initialize</span></span>

<span data-ttu-id="87867-154">Abra `BlobStorage.cs`.</span><span class="sxs-lookup"><span data-stu-id="87867-154">Open `BlobStorage.cs`.</span></span>

<span data-ttu-id="87867-155">Busque el método `Initialize`.</span><span class="sxs-lookup"><span data-stu-id="87867-155">Location the `Initialize` method.</span></span> <span data-ttu-id="87867-156">Nuestra aplicación llamará a este método cuando se use por primera vez.</span><span class="sxs-lookup"><span data-stu-id="87867-156">Our app will call this method when it's first used.</span></span> <span data-ttu-id="87867-157">Si tiene curiosidad, puede examinar `ConfigureServices` en `Startup.cs` para ver cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="87867-157">If you're curious, you can look at `ConfigureServices` in `Startup.cs` to see how this is done.</span></span> 

<span data-ttu-id="87867-158">`Initialize` es donde queremos crear nuestro contenedor si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="87867-158">`Initialize` is where we want to create our container if it doesn't already exist.</span></span> <span data-ttu-id="87867-159">Rellene `Initialize` con el código siguiente y guarde su trabajo:</span><span class="sxs-lookup"><span data-stu-id="87867-159">Fill in `Initialize` with the following code and save your work:</span></span>

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```