Una vez que tenemos una referencia a un blob, podemos cargar y descargar datos. Los objetos `ICloudBlob` tienen métodos `Upload` y `Download` que admiten matrices de bytes, secuencias y archivos como orígenes y destinos. Determinados tipos tienen métodos adicionales para su comodidad &mdash; por ejemplo, `CloudBlockBlob` admite la carga y descarga de cadenas con `UploadTextAsync` y `DownloadTextAsync`.

## <a name="creating-new-blobs"></a>Creación de nuevos blobs

Para crear un nuevo blob, llame a uno de los métodos `Upload` en un blob que no existe. Esto hace dos cosas: crea el blob y carga los datos. 

## <a name="moving-data-to-and-from-blobs"></a>Traslado de datos hacia y desde blobs

El traslado de datos hacia y desde un blob es una operación de red que lleva tiempo. En el SDK de Azure Storage para .NET Core, todos los métodos que requieren la actividad de red devuelven `Task`, así que asegúrese de que los métodos de controlador son `async` según corresponda, y que está aplicando `await` a las llamadas al método y no `Wait` a estas.

Una recomendación habitual cuando se trabaja con objetos de datos grandes es usar secuencias en lugar de estructuras en memoria como cadenas o matrices de bytes. Así se evita el almacenamiento en búfer del contenido completo en la memoria antes de enviarlo al destino. ASP.NET Core admite la lectura y escritura de secuencias desde solicitudes y respuestas.

## <a name="concurrent-access"></a>simultáneo

Es posible que otros procesos puedan agregar, cambiar o eliminar los blobs a medida que los use la aplicación. Codifique siempre de forma defensiva y piense en los problemas que provoca la simultaneidad, como blobs que se eliminan justo cuando intenta descargar desde ellos, o blobs cuyo contenido cambia de manera inesperada. Consulte la sección Recursos adicionales al final de este módulo para obtener información sobre el uso de AccessConditions y las concesiones de blobs para administrar el acceso a blobs simultáneo.

## <a name="exercise"></a>Ejercicio

Vamos a finalizar la aplicación agregando código de carga y descarga, y luego lo implementaremos en Azure App Service para realizar pruebas.

### <a name="upload"></a>Cargar

Para cargar un blob, implementaremos el método `BlobStorage.Save` utilizando `GetBlockBlobReference` para obtener `CloudBlockBlob` desde el contenedor. `FilesController.Upload` pasa la secuencia de archivos a `Save`, de manera que podemos usar `UploadFromStreamAsync` para realizar la carga y disfrutar así de la máxima eficacia.

Abra `BlobStorage.cs` en el editor y rellene la implementación de `Save` con el código siguiente:

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
> El código de carga basado en secuencias que se muestra aquí es más eficaz que la lectura del archivo en una matriz de bytes antes de enviarlo a Azure Blob Storage. Sin embargo, la técnica `IFormFile` que usamos para obtener el archivo desde el cliente no es una verdadera implementación de transmisión de un extremo a otro, y solo es adecuada en caso de cargas de archivos pequeños. Vea la sección Recursos adicionales al final de este módulo para obtener información acerca de las cargas de archivos transmitidos por completo.

### <a name="download"></a>Descargar

`BlobStorage.Load` devuelve `Stream`, lo que significa que nuestro código no tiene que mover físicamente los bytes de Blob Storage en absoluto &mdash; necesitamos solo devolver una referencia a la secuencia de blobs. Podemos hacerlo con `OpenReadAsync`. ASP.NET Core controlará la lectura y cerrará la secuencia cuando compile la respuesta del cliente.

Rellene `Load` con este código:

```csharp
public Task<Stream> Load(string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.GetBlobReference(name).OpenReadAsync();
}
```

### <a name="deploy-and-run-in-azure"></a>Implementación y ejecución en Azure

Nuestra aplicación está terminada &mdash; vamos a implementarla y ver cómo funciona. Ejecute el siguiente código en el terminal de Azure Cloud Shell para crear nuestro código e implementarlo en una nueva instancia de App Service. También agregamos nuestra cadena de conexión de la cuenta de almacenamiento a la configuración.

```console

```

...

Cargue y descargue algunos archivos para probar la aplicación y, a continuación, ejecute lo siguiente en el shell para ver los blobs que se han cargado:

```console

```

**Imagen TODO del portal**