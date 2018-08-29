<span data-ttu-id="ddf9e-101">Una vez que tenemos una referencia a un blob, podemos cargar y descargar datos.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-101">Once we have a reference to a blob, we can upload and download data.</span></span> <span data-ttu-id="ddf9e-102">Los objetos `ICloudBlob` tienen métodos `Upload` y `Download` que admiten matrices de bytes, secuencias y archivos como orígenes y destinos.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-102">`ICloudBlob` objects have `Upload` and `Download` methods that support byte arrays, streams, and files as sources and targets.</span></span> <span data-ttu-id="ddf9e-103">Determinados tipos tienen métodos adicionales para su comodidad &mdash; por ejemplo, `CloudBlockBlob` admite la carga y descarga de cadenas con `UploadTextAsync` y `DownloadTextAsync`.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-103">Specific types have additional methods for convenience &mdash; for example, `CloudBlockBlob` supports uploading and downloading strings with `UploadTextAsync` and `DownloadTextAsync`.</span></span>

## <a name="creating-new-blobs"></a><span data-ttu-id="ddf9e-104">Creación de nuevos blobs</span><span class="sxs-lookup"><span data-stu-id="ddf9e-104">Creating new blobs</span></span>

<span data-ttu-id="ddf9e-105">Para crear un nuevo blob, llame a uno de los métodos `Upload` en un blob que no existe.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-105">To create a new blob, you call one of the `Upload` methods on a blob that doesn't exist.</span></span> <span data-ttu-id="ddf9e-106">Esto hace dos cosas: crea el blob y carga los datos.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-106">This does two things: creates the blob and uploads the data.</span></span> 

## <a name="moving-data-to-and-from-blobs"></a><span data-ttu-id="ddf9e-107">Traslado de datos hacia y desde blobs</span><span class="sxs-lookup"><span data-stu-id="ddf9e-107">Moving data to and from blobs</span></span>

<span data-ttu-id="ddf9e-108">El traslado de datos hacia y desde un blob es una operación de red que lleva tiempo.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-108">Moving data to and from a blob is a network operation that takes time.</span></span> <span data-ttu-id="ddf9e-109">En el SDK de Azure Storage para .NET Core, todos los métodos que requieren la actividad de red devuelven `Task`, así que asegúrese de que los métodos de controlador son `async` según corresponda, y que está aplicando `await` a las llamadas al método y no `Wait` a estas.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-109">In the Azure Storage SDK for .NET Core, all methods that require network activity return `Task`s, so make sure your controller methods are `async` as appropriate and that you are `await`ing method calls and not `Wait`ing on them.</span></span>

<span data-ttu-id="ddf9e-110">Una recomendación habitual cuando se trabaja con objetos de datos grandes es usar secuencias en lugar de estructuras en memoria como cadenas o matrices de bytes.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-110">A common recommendation when working with large data objects is to use streams instead of in-memory structures like byte arrays or strings.</span></span> <span data-ttu-id="ddf9e-111">Así se evita el almacenamiento en búfer del contenido completo en la memoria antes de enviarlo al destino.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-111">This avoids buffering the full content in memory before sending it to the target.</span></span> <span data-ttu-id="ddf9e-112">ASP.NET Core admite la lectura y escritura de secuencias desde solicitudes y respuestas.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-112">ASP.NET Core supports reading and writing streams from requests and responses.</span></span>

## <a name="concurrent-access"></a><span data-ttu-id="ddf9e-113">simultáneo</span><span class="sxs-lookup"><span data-stu-id="ddf9e-113">Concurrent access</span></span>

<span data-ttu-id="ddf9e-114">Es posible que otros procesos puedan agregar, cambiar o eliminar los blobs a medida que los use la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-114">It is possible that other processes may be adding, changing, or deleting blobs as your app is using them.</span></span> <span data-ttu-id="ddf9e-115">Codifique siempre de forma defensiva y piense en los problemas que provoca la simultaneidad, como blobs que se eliminan justo cuando intenta descargar desde ellos, o blobs cuyo contenido cambia de manera inesperada.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-115">Always code defensively and think about problems caused by concurrency, such as blobs that are deleted right as you try to download from them, or blobs whose contents change when you don't expect them to.</span></span> <span data-ttu-id="ddf9e-116">Consulte la sección Recursos adicionales al final de este módulo para obtener información sobre el uso de AccessConditions y las concesiones de blobs para administrar el acceso a blobs simultáneo.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-116">See the Additional Resources section at the end of this module for information about using AccessConditions and blob leases to manage concurrent blob access.</span></span>

## <a name="exercise"></a><span data-ttu-id="ddf9e-117">Ejercicio</span><span class="sxs-lookup"><span data-stu-id="ddf9e-117">Exercise</span></span>

<span data-ttu-id="ddf9e-118">Vamos a finalizar la aplicación agregando código de carga y descarga, y luego lo implementaremos en Azure App Service para realizar pruebas.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-118">Let's finish our app by adding upload and download code, then deploy it to Azure App Service for testing.</span></span>

### <a name="upload"></a><span data-ttu-id="ddf9e-119">Cargar</span><span class="sxs-lookup"><span data-stu-id="ddf9e-119">Upload</span></span>

<span data-ttu-id="ddf9e-120">Para cargar un blob, implementaremos el método `BlobStorage.Save` utilizando `GetBlockBlobReference` para obtener `CloudBlockBlob` desde el contenedor.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-120">To upload a blob, we'll implement the `BlobStorage.Save` method using `GetBlockBlobReference` to get a `CloudBlockBlob` from the container.</span></span> <span data-ttu-id="ddf9e-121">`FilesController.Upload` pasa la secuencia de archivos a `Save`, de manera que podemos usar `UploadFromStreamAsync` para realizar la carga y disfrutar así de la máxima eficacia.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-121">`FilesController.Upload` passes the file stream to `Save`, so we can use `UploadFromStreamAsync` to perform the upload for maximum efficiency.</span></span>

<span data-ttu-id="ddf9e-122">Abra `BlobStorage.cs` en el editor y rellene la implementación de `Save` con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="ddf9e-122">Open `BlobStorage.cs` in the editor and fill in the `Save` implementation with the following code:</span></span>

```csharp
public Task Save(Stream fileStream, string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    CloudBlockBlob blockBlob = container.GetBlockBlobReference(name);
    return blockBlob.UploadFromStreamAsync(fileStream);
}
```

> [!NOTE]
> <span data-ttu-id="ddf9e-123">El código de carga basado en secuencias que se muestra aquí es más eficaz que la lectura del archivo en una matriz de bytes antes de enviarlo a Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-123">The stream-based upload code shown here is more efficient than reading the file into a byte array before sending it to Azure Blob storage.</span></span> <span data-ttu-id="ddf9e-124">Sin embargo, la técnica `IFormFile` que usamos para obtener el archivo desde el cliente no es una verdadera implementación de transmisión de un extremo a otro, y solo es adecuada en caso de cargas de archivos pequeños.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-124">However, the `IFormFile` technique we use to get the file from the client is not a true end-to-end streaming implementation and is only appropriate for handling uploads of small files.</span></span> <span data-ttu-id="ddf9e-125">Vea la sección Recursos adicionales al final de este módulo para obtener información acerca de las cargas de archivos transmitidos por completo.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-125">See the Additional Resources section at the end of this module for information about fully streamed file uploads.</span></span>

### <a name="download"></a><span data-ttu-id="ddf9e-126">Descargar</span><span class="sxs-lookup"><span data-stu-id="ddf9e-126">Download</span></span>

<span data-ttu-id="ddf9e-127">`BlobStorage.Load` devuelve `Stream`, lo que significa que nuestro código no tiene que mover físicamente los bytes de Blob Storage en absoluto &mdash; necesitamos solo devolver una referencia a la secuencia de blobs.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-127">`BlobStorage.Load` returns a `Stream`, meaning that our code doesn't need to physically move the bytes from Blob storage at all &mdash; we just need to return a reference to the blob stream.</span></span> <span data-ttu-id="ddf9e-128">Podemos hacerlo con `OpenReadAsync`.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-128">We can do that with `OpenReadAsync`.</span></span> <span data-ttu-id="ddf9e-129">ASP.NET Core controlará la lectura y cerrará la secuencia cuando compile la respuesta del cliente.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-129">ASP.NET Core will handle reading and closing the stream when it builds the client response.</span></span>

<span data-ttu-id="ddf9e-130">Rellene `Load` con este código:</span><span class="sxs-lookup"><span data-stu-id="ddf9e-130">Fill in `Load` with this code:</span></span>

```csharp
public Task<Stream> Load(string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.GetBlobReference(name).OpenReadAsync();
}
```

### <a name="deploy-and-run-in-azure"></a><span data-ttu-id="ddf9e-131">Implementación y ejecución en Azure</span><span class="sxs-lookup"><span data-stu-id="ddf9e-131">Deploy and run in Azure</span></span>

<span data-ttu-id="ddf9e-132">Nuestra aplicación está terminada &mdash; vamos a implementarla y ver cómo funciona.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-132">Our app is finished &mdash; let's deploy it and see it work.</span></span> <span data-ttu-id="ddf9e-133">Ejecute el siguiente código en el terminal de Azure Cloud Shell para crear nuestro código e implementarlo en una nueva instancia de App Service.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-133">Run the following code in the Azure Cloud Shell terminal to build our code and deploy it to a new App Service instance.</span></span> <span data-ttu-id="ddf9e-134">También agregamos nuestra cadena de conexión de la cuenta de almacenamiento a la configuración.</span><span class="sxs-lookup"><span data-stu-id="ddf9e-134">We also add our storage account connection string to configuration.</span></span>

```console

```

<span data-ttu-id="ddf9e-135">...</span><span class="sxs-lookup"><span data-stu-id="ddf9e-135">...</span></span>

<span data-ttu-id="ddf9e-136">Cargue y descargue algunos archivos para probar la aplicación y, a continuación, ejecute lo siguiente en el shell para ver los blobs que se han cargado:</span><span class="sxs-lookup"><span data-stu-id="ddf9e-136">Upload and download some files to test the app, then run the following in the shell to see the blobs that have been uploaded:</span></span>

```console

```

<span data-ttu-id="ddf9e-137">**Imagen TODO del portal**</span><span class="sxs-lookup"><span data-stu-id="ddf9e-137">**TODO pic from portal**</span></span>