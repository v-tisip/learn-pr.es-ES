<span data-ttu-id="c7152-101">Ahora es el momento de ejecutar nuestra aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="c7152-101">Now it's time to run our app in Azure.</span></span> <span data-ttu-id="c7152-102">Necesitamos crear una aplicación de Azure App Service, configurarla con MSI y nuestra configuración del almacén e implementar nuestro código.</span><span class="sxs-lookup"><span data-stu-id="c7152-102">We need to create an Azure App Service app, set it up with MSI and our vault configuration, and deploy our code.</span></span>

## <a name="exercise"></a><span data-ttu-id="c7152-103">Ejercicio</span><span class="sxs-lookup"><span data-stu-id="c7152-103">Exercise</span></span>

### <a name="create-the-app-service-plan-and-app"></a><span data-ttu-id="c7152-104">Creación del plan y la aplicación de App Service</span><span class="sxs-lookup"><span data-stu-id="c7152-104">Create the App Service plan and app</span></span>

<span data-ttu-id="c7152-105">La creación de una aplicación de App Service es un proceso de dos pasos: primero se crea el *plan* y luego la *aplicación*.</span><span class="sxs-lookup"><span data-stu-id="c7152-105">Creating an App Service app is a two-step process: First create the *plan*, then the *app*.</span></span>

<span data-ttu-id="c7152-106">El nombre del *plan* solo necesita ser único dentro de su suscripción, por lo que puede usar el mismo nombre que hemos usado: **keyvault-exercise-plan**.</span><span class="sxs-lookup"><span data-stu-id="c7152-106">The *plan* name only needs to be unique within your subscription, so you can use the same name we've used: **keyvault-exercise-plan**.</span></span> <span data-ttu-id="c7152-107">Sin embargo, el nombre de la aplicación debe ser globalmente único, por lo que necesitará elegir el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="c7152-107">The app name needs to be globally unique, though, so you'll need to pick your own.</span></span>

<span data-ttu-id="c7152-108">En Azure Cloud Shell, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7152-108">In Azure Cloud Shell, run the following:</span></span>

```azurecli
az appservice plan create --name keyvault-exercise-plan --resource-group keyvault-exercise-group
az webapp create --name <your-unique-app-name> --plan keyvault-exercise-plan --resource-group keyvault-exercise-group
```

### <a name="add-configuration-to-the-app"></a><span data-ttu-id="c7152-109">Incorporación de la configuración a la aplicación</span><span class="sxs-lookup"><span data-stu-id="c7152-109">Add configuration to the app</span></span>

<span data-ttu-id="c7152-110">Para realizar la implementación en Azure, seguiremos el procedimiento recomendado de App Service de colocar la configuración en Configuración de la aplicación en lugar de un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="c7152-110">For deploying to Azure, we'll follow the App Service best practice of putting configuration in Application Settings instead of a configuration file.</span></span>

```azurecli
az webapp config appsettings set --name <your-unique-app-name> --resource-group keyvault-exercise-group --settings VaultName=<your-unique-vault-name>
```

### <a name="enable-msi"></a><span data-ttu-id="c7152-111">Habilitación de MSI</span><span class="sxs-lookup"><span data-stu-id="c7152-111">Enable MSI</span></span>

<span data-ttu-id="c7152-112">La habilitación de MSI es muy rápida:</span><span class="sxs-lookup"><span data-stu-id="c7152-112">Enabling MSI on an app is a one-liner:</span></span>

```azurecli
az webapp identity assign --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="c7152-113">En la salida JSON que da como resultado, copie el valor **principalId**.</span><span class="sxs-lookup"><span data-stu-id="c7152-113">From the JSON output that results, copy the **principalId** value.</span></span> <span data-ttu-id="c7152-114">PrincipalId es el identificador único de la nueva identidad de la aplicación en Azure Active Directory y vamos a usarla en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="c7152-114">PrincipalId is the unique ID of the app's new identity in Azure Active Directory, and we're going to use it in the next step.</span></span>

### <a name="grant-access-to-the-vault"></a><span data-ttu-id="c7152-115">Concesión de acceso al almacén</span><span class="sxs-lookup"><span data-stu-id="c7152-115">Grant access to the vault</span></span>

<span data-ttu-id="c7152-116">Ahora debe proporcionar permisos de identidad a la aplicación para obtener y mostrar los secretos del almacén del entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c7152-116">Now you need to give your app identity permissions to get and list secrets from your production-environment vault.</span></span> <span data-ttu-id="c7152-117">Use el valor **principalId** copiado en el paso anterior como el valor de **object-id** en el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="c7152-117">Use the **principalId** value you copied from the previous step as the value for **object-id** in the command below.</span></span>

```azurecli
az keyvault set-policy --name <your-unique-vault-name> --object-id <your-msi-principleid> --secret-permissions get list
```

### <a name="deploy-the-app-and-try-it-out"></a><span data-ttu-id="c7152-118">Implementación de la aplicación y prueba de la misma</span><span class="sxs-lookup"><span data-stu-id="c7152-118">Deploy the app and try it out</span></span>

<span data-ttu-id="c7152-119">¡Toda la configuración está establecida y lista para implementarse!</span><span class="sxs-lookup"><span data-stu-id="c7152-119">All your configuration is set and you're ready to deploy!</span></span> <span data-ttu-id="c7152-120">Los siguientes comandos se publicarán en el sitio en la carpeta `pub`, comprímala en `site.zip` e implementar el archivo zip en App Service.</span><span class="sxs-lookup"><span data-stu-id="c7152-120">The below commands will publish the site to the `pub` folder, zip it up into `site.zip`, and deploy the zip to App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="c7152-121">Deberá `cd` al directorio KeyVaultDemoApp si no lo ha hecho ya.</span><span class="sxs-lookup"><span data-stu-id="c7152-121">You'll need to `cd` back to the KeyVaultDemoApp directory if you haven't already.</span></span>

```console
dotnet publish -o pub
zip -j site.zip pub/*
az webapp deployment source config-zip --src site.zip --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="c7152-122">Una vez que obtenga un resultado que indica que el sitio se ha implementado, abra `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` en un explorador.</span><span class="sxs-lookup"><span data-stu-id="c7152-122">Once you get a result that indicates the site has deployed, open `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in a browser.</span></span> <span data-ttu-id="c7152-123">Debería ver el valor del secreto, **reindeer_flotilla**.</span><span class="sxs-lookup"><span data-stu-id="c7152-123">You should see the secret value, **reindeer_flotilla**.</span></span>

<span data-ttu-id="c7152-124">¡La aplicación está terminada e implementada!</span><span class="sxs-lookup"><span data-stu-id="c7152-124">Your app is finished and deployed!</span></span>