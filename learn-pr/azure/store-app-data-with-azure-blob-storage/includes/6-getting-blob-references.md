<span data-ttu-id="97139-101">Trabajar con un blob individual en el SDK de Azure Storage para .NET Core requiere un *referencia de blob* &mdash; una instancia de un objeto `ICloudBlob`.</span><span class="sxs-lookup"><span data-stu-id="97139-101">Working with an individual blob in the Azure Storage SDK for .NET Core requires a *blob reference* &mdash; an instance of an `ICloudBlob` object.</span></span>

<span data-ttu-id="97139-102">Para obtener un `ICloudBlob`, solicítelo con el nombre del blob o selecciónelo en una lista de blobs del contenedor.</span><span class="sxs-lookup"><span data-stu-id="97139-102">You can get an `ICloudBlob` by requesting it with the blob's name or selecting it from a list of blobs in the container.</span></span> <span data-ttu-id="97139-103">Ambos requieren un `CloudBlobContainer`, que ya vimos cómo obtener en la última unidad.</span><span class="sxs-lookup"><span data-stu-id="97139-103">Both require a `CloudBlobContainer`, which we saw how to get in the last unit.</span></span>

## <a name="getting-blobs-by-name"></a><span data-ttu-id="97139-104">Obtención de blobs por nombre</span><span class="sxs-lookup"><span data-stu-id="97139-104">Getting blobs by name</span></span>

<span data-ttu-id="97139-105">Llame a uno de los métodos `GetXXXReference` en un `CloudBlobContainer` para obtener un `ICloudBlob` por nombre.</span><span class="sxs-lookup"><span data-stu-id="97139-105">Call one of the `GetXXXReference` methods on a `CloudBlobContainer` to get an `ICloudBlob` by name.</span></span> <span data-ttu-id="97139-106">Si conoce el tipo del blob que está recuperando, prefiera usar uno de los métodos más específicos (`GetBlockBlobReference`, `GetAppendBlobReference` o `GetPageBlobReference`).</span><span class="sxs-lookup"><span data-stu-id="97139-106">If you know the type of the blob you are retrieving, prefer using one of the more specific methods (`GetBlockBlobReference`, `GetAppendBlobReference`, or `GetPageBlobReference`).</span></span>

<span data-ttu-id="97139-107">Ninguno de estos métodos hace una llamada de red ni confirma si el blob existe realmente o no.</span><span class="sxs-lookup"><span data-stu-id="97139-107">None of these methods make a network call, nor do they confirm whether or not the blob actually exists.</span></span> <span data-ttu-id="97139-108">Un método independiente, `GetBlobReferenceFromServerAsync`, llama a la API Blob Storage y se generará una excepción si el blob ya no existe.</span><span class="sxs-lookup"><span data-stu-id="97139-108">A separate method, `GetBlobReferenceFromServerAsync`, does call the Blob storage API and will throw an exception if the blob doesn't already exist.</span></span>

## <a name="listing-blobs-in-a-container"></a><span data-ttu-id="97139-109">Enumeración de blobs en un contenedor</span><span class="sxs-lookup"><span data-stu-id="97139-109">Listing blobs in a container</span></span>

<span data-ttu-id="97139-110">Puede obtener una lista de los blobs en un contenedor con el método `ListBlobsSegmentedAsync` de `CloudBlobContainer`.</span><span class="sxs-lookup"><span data-stu-id="97139-110">You can get a list of the blobs in a container using `CloudBlobContainer`'s `ListBlobsSegmentedAsync` method.</span></span> <span data-ttu-id="97139-111">*Segmented* se refiere a las páginas independientes de los resultados devueltos &mdash; nunca se garantiza que una sola llamada a `ListBlobsSegmentedAsync` devuelva todos los resultado en una sola página.</span><span class="sxs-lookup"><span data-stu-id="97139-111">*Segmented* refers to the separate pages of results returned &mdash; a single call to `ListBlobsSegmentedAsync` is never guaranteed to return all the results in a single page.</span></span> <span data-ttu-id="97139-112">Es posible que sea necesario llamarlo varias veces con el token `ContinuationToken` que devuelve para avanzar por las páginas.</span><span class="sxs-lookup"><span data-stu-id="97139-112">We may need to call it repeatedly using the `ContinuationToken` it returns to work our way through the pages.</span></span> <span data-ttu-id="97139-113">Esto hace que el código para enumerar los blobs sea un poco más complejo que el código para cargar o descargar, pero hay un patrón estándar que puede usar para obtener cada blob de un contenedor:</span><span class="sxs-lookup"><span data-stu-id="97139-113">This makes the code for listing blobs a little more complex than the code for uploading or downloading, but there's a standard pattern you can use to get every blob in a container:</span></span>

```csharp
BlobContinuationToken continuationToken = null;
BlobResultSegment resultSegment = null; 

do
{
    resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

    // Do work here on resultSegment.Results

    continuationToken = resultSegment.ContinuationToken;
} while (continuationToken != null);
```

<span data-ttu-id="97139-114">Esto llamará varias veces a `ListBlobsSegmentedAsync` hasta que `continuationToken` sea `null`, que señala el final de los resultados.</span><span class="sxs-lookup"><span data-stu-id="97139-114">This will call `ListBlobsSegmentedAsync` repeatedly until `continuationToken` is `null`, which signals the end of the results.</span></span>

### <a name="processing-list-results"></a><span data-ttu-id="97139-115">Procesamiento de los resultados de lista</span><span class="sxs-lookup"><span data-stu-id="97139-115">Processing list results</span></span>

<span data-ttu-id="97139-116">El objeto que recuperará de `ListBlobsSegmentedAsync` contiene una propiedad `Results` de tipo `IEnumerable<IListBlobItem>`.</span><span class="sxs-lookup"><span data-stu-id="97139-116">The object you'll get back from `ListBlobsSegmentedAsync` contains a `Results` property of type `IEnumerable<IListBlobItem>`.</span></span> <span data-ttu-id="97139-117">`IListBlobItem` contiene un puñado de propiedades sobre la dirección URL y el contenedor del blob, pero no métodos de carga ni descarga.</span><span class="sxs-lookup"><span data-stu-id="97139-117">`IListBlobItem`s contain a handful of properties about the blob's container and URL, but no upload or download methods.</span></span> <span data-ttu-id="97139-118">Esto es porque algunos de los objetos de resultado pueden ser objetos `CloudBlobDirectory` que representan los directorios virtuales en lugar de los blobs individuales.</span><span class="sxs-lookup"><span data-stu-id="97139-118">This is because some of the result objects may be `CloudBlobDirectory` objects that represent virtual directories rather than individual blobs.</span></span>

<span data-ttu-id="97139-119">Si solo está interesado en blobs individuales, puede usar el método `OfType<>` para filtrar los resultados.</span><span class="sxs-lookup"><span data-stu-id="97139-119">If you are only interested in individual blobs, you can use the `OfType<>` method to filter the results.</span></span> <span data-ttu-id="97139-120">Estos son algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="97139-120">Here are a few examples:</span></span>

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

<span data-ttu-id="97139-121">Usar `OfType<>` requerirá una referencia a al espacio de nombres `System.Linq` (`using System.Linq;`).</span><span class="sxs-lookup"><span data-stu-id="97139-121">Using `OfType<>` will require a reference to the `System.Linq` namespace (`using System.Linq;`).</span></span>

## <a name="exercise"></a><span data-ttu-id="97139-122">Ejercicio</span><span class="sxs-lookup"><span data-stu-id="97139-122">Exercise</span></span>

<span data-ttu-id="97139-123">Una de las características de nuestra aplicación requiere obtener una lista de blobs de la API.</span><span class="sxs-lookup"><span data-stu-id="97139-123">One of the features in our app requires getting a list of blobs from the API.</span></span> <span data-ttu-id="97139-124">Vamos a usar el patrón mostrado anteriormente para enumerar todos los blobs del contenedor.</span><span class="sxs-lookup"><span data-stu-id="97139-124">We'll use the pattern shown above to list all the blobs in our container.</span></span> <span data-ttu-id="97139-125">A medida que procesamos la lista, obtenemos el nombre de cada blob.</span><span class="sxs-lookup"><span data-stu-id="97139-125">As we process the list, we get the name of each blob.</span></span>

<span data-ttu-id="97139-126">Abra `BlobStorage.cs` en el editor y rellene `GetNames` con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="97139-126">Open `BlobStorage.cs` in the editor and fill in `GetNames` with the following code:</span></span>

```csharp
public async Task<IEnumerable<string>> GetNames()
{
    List<string> names = new List<string>();

    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);

    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    do
    {
        resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

        // Get the name of each blob.
        names.AddRange(resultSegment.Results.OfType<ICloudBlob>().Select(b => b.Name));

        continuationToken = resultSegment.ContinuationToken;
    } while (continuationToken != null);

    return names;
}
```

<span data-ttu-id="97139-127">`FilesController` procesa los nombres que devuelve este método para convertirlos en direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="97139-127">The names returned by this method are processed by `FilesController` to turn them into URLs.</span></span> <span data-ttu-id="97139-128">Cuando se devuelven al cliente, se representan como hipervínculos en la página.</span><span class="sxs-lookup"><span data-stu-id="97139-128">When they are returned to the client, they are rendered as hyperlinks on the page.</span></span>