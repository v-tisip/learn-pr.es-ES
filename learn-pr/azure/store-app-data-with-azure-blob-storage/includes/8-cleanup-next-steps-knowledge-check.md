En este módulo, aprendió a usar Azure Blob Storage para almacenar datos de aplicación web. Hemos hablado de sugerencias para crear una estrategia para usar Blob Storage en una aplicación web y de cómo usar el SDK de Azure Storage para .NET Core para escribir y leer en blobs. La aplicación que hemos realizado acepta archivos cargados de usuarios, los almacena en Blob Storage y permite que estén disponibles para su descarga.

## <a name="cleanup"></a>Limpieza

Para limpiar la suscripción de Azure, ejecute el siguiente código en Azure Cloud Shell para eliminar el grupo de recursos que contiene todos los recursos que hemos creado en este módulo.

```console
az group delete --name blob-exercise-group
```

Para limpiar el almacenamiento de Cloud Shell, elimine el directorio `TODO` con `rm -rf TODO`.

## <a name="additional-resources"></a>Recursos adicionales

**¿Vínculos entre conjuntos de documentos de lista de tareas?**

* **Almacenamiento seguro de las claves de la cuenta de almacenamiento**: la solución completa más sólida para almacenar valores de configuración secretos es Azure Key Vault. Para información sobre cómo usar Key Vault en una aplicación ASP.NET Core, consulte [aquí](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x). Como alternativa, puede almacenar de forma segura cadenas de conexión en la configuración de la aplicación de App Service y usar la [herramienta ASP.NET Core Secret Manager](https://docs.microsoft.com/aspnet/core/security/app-secrets?view=aspnetcore-2.1&tabs=windows) para admitir entornos de desarrollo.
* [Cargar archivos grandes con streaming en ASP.NET Core](https://docs.microsoft.com/aspnet/core/mvc/models/file-uploads?view=aspnetcore-2.1#uploading-large-files-with-streaming)
* [Simultaneidad de blobs: condiciones de acceso y concesiones de blobs](https://azure.microsoft.com/blog/managing-concurrency-in-microsoft-azure-storage-2/)
* [Concesión de acceso limitado al objeto de Azure Storage con firmas de acceso compartido](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1)
* [Indexación de Blob Storage con Azure Search](https://docs.microsoft.com/azure/search/search-howto-indexing-azure-blob-storage)
* [Restricciones de nombre de contenedor y blob](https://docs.microsoft.com/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata#resource-names)