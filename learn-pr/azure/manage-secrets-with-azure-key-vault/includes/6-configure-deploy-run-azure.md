Ahora es el momento de ejecutar nuestra aplicación en Azure. Necesitamos crear una aplicación de Azure App Service, configurarla con MSI y nuestra configuración del almacén e implementar nuestro código.

## <a name="exercise"></a>Ejercicio

### <a name="create-the-app-service-plan-and-app"></a>Creación del plan y la aplicación de App Service

La creación de una aplicación de App Service es un proceso de dos pasos: primero se crea el *plan* y luego la *aplicación*.

El nombre del *plan* solo necesita ser único dentro de su suscripción, por lo que puede usar el mismo nombre que hemos usado: **keyvault-exercise-plan**. Sin embargo, el nombre de la aplicación debe ser globalmente único, por lo que necesitará elegir el suyo propio.

En Azure Cloud Shell, ejecute lo siguiente:

```azurecli
az appservice plan create --name keyvault-exercise-plan --resource-group keyvault-exercise-group
az webapp create --name <your-unique-app-name> --plan keyvault-exercise-plan --resource-group keyvault-exercise-group
```

### <a name="add-configuration-to-the-app"></a>Incorporación de la configuración a la aplicación

Para realizar la implementación en Azure, seguiremos el procedimiento recomendado de App Service de colocar la configuración en Configuración de la aplicación en lugar de un archivo de configuración.

```azurecli
az webapp config appsettings set --name <your-unique-app-name> --resource-group keyvault-exercise-group --settings VaultName=<your-unique-vault-name>
```

### <a name="enable-msi"></a>Habilitación de MSI

La habilitación de MSI es muy rápida:

```azurecli
az webapp identity assign --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

En la salida JSON que da como resultado, copie el valor **principalId**. PrincipalId es el identificador único de la nueva identidad de la aplicación en Azure Active Directory y vamos a usarla en el paso siguiente.

### <a name="grant-access-to-the-vault"></a>Concesión de acceso al almacén

Ahora debe proporcionar permisos de identidad a la aplicación para obtener y mostrar los secretos del almacén del entorno de producción. Use el valor **principalId** copiado en el paso anterior como el valor de **object-id** en el siguiente comando.

```azurecli
az keyvault set-policy --name <your-unique-vault-name> --object-id <your-msi-principleid> --secret-permissions get list
```

### <a name="deploy-the-app-and-try-it-out"></a>Implementación de la aplicación y prueba de la misma

¡Toda la configuración está establecida y lista para implementarse! Los siguientes comandos se publicarán en el sitio en la carpeta `pub`, comprímala en `site.zip` e implementar el archivo zip en App Service.

> [!NOTE]
> Deberá `cd` al directorio KeyVaultDemoApp si no lo ha hecho ya.

```console
dotnet publish -o pub
zip -j site.zip pub/*
az webapp deployment source config-zip --src site.zip --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

Una vez que obtenga un resultado que indica que el sitio se ha implementado, abra `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` en un explorador. Debería ver el valor del secreto, **reindeer_flotilla**.

¡La aplicación está terminada e implementada!