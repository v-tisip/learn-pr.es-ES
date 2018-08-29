Trabajar con un blob individual en el SDK de Azure Storage para .NET Core requiere un *referencia de blob* &mdash; una instancia de un objeto `ICloudBlob`.

Para obtener un `ICloudBlob`, solicítelo con el nombre del blob o selecciónelo en una lista de blobs del contenedor. Ambos requieren un `CloudBlobContainer`, que ya vimos cómo obtener en la última unidad.

## <a name="getting-blobs-by-name"></a>Obtención de blobs por nombre

Llame a uno de los métodos `GetXXXReference` en un `CloudBlobContainer` para obtener un `ICloudBlob` por nombre. Si conoce el tipo del blob que está recuperando, prefiera usar uno de los métodos más específicos (`GetBlockBlobReference`, `GetAppendBlobReference` o `GetPageBlobReference`).

Ninguno de estos métodos hace una llamada de red ni confirma si el blob existe realmente o no. Un método independiente, `GetBlobReferenceFromServerAsync`, llama a la API Blob Storage y se generará una excepción si el blob ya no existe.

## <a name="listing-blobs-in-a-container"></a>Enumeración de blobs en un contenedor

Puede obtener una lista de los blobs en un contenedor con el método `ListBlobsSegmentedAsync` de `CloudBlobContainer`. *Segmented* se refiere a las páginas independientes de los resultados devueltos &mdash; nunca se garantiza que una sola llamada a `ListBlobsSegmentedAsync` devuelva todos los resultado en una sola página. Es posible que sea necesario llamarlo varias veces con el token `ContinuationToken` que devuelve para avanzar por las páginas. Esto hace que el código para enumerar los blobs sea un poco más complejo que el código para cargar o descargar, pero hay un patrón estándar que puede usar para obtener cada blob de un contenedor:

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

Esto llamará varias veces a `ListBlobsSegmentedAsync` hasta que `continuationToken` sea `null`, que señala el final de los resultados.

### <a name="processing-list-results"></a>Procesamiento de los resultados de lista

El objeto que recuperará de `ListBlobsSegmentedAsync` contiene una propiedad `Results` de tipo `IEnumerable<IListBlobItem>`. `IListBlobItem` contiene un puñado de propiedades sobre la dirección URL y el contenedor del blob, pero no métodos de carga ni descarga. Esto es porque algunos de los objetos de resultado pueden ser objetos `CloudBlobDirectory` que representan los directorios virtuales en lugar de los blobs individuales.

Si solo está interesado en blobs individuales, puede usar el método `OfType<>` para filtrar los resultados. Estos son algunos ejemplos:

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

Usar `OfType<>` requerirá una referencia a al espacio de nombres `System.Linq` (`using System.Linq;`).

## <a name="exercise"></a>Ejercicio

Una de las características de nuestra aplicación requiere obtener una lista de blobs de la API. Vamos a usar el patrón mostrado anteriormente para enumerar todos los blobs del contenedor. A medida que procesamos la lista, obtenemos el nombre de cada blob.

Abra `BlobStorage.cs` en el editor y rellene `GetNames` con el código siguiente:

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

`FilesController` procesa los nombres que devuelve este método para convertirlos en direcciones URL. Cuando se devuelven al cliente, se representan como hipervínculos en la página.