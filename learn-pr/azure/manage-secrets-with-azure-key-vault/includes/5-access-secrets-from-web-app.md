<span data-ttu-id="9f5c5-101">Ahora que sabe que al habilitar MSI se crea una identidad para que la aplicación la use para fines de autenticación, crearemos una aplicación que use dicha identidad para acceder a los secretos en el almacén.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-101">Now that you know how enabling MSI creates an identity for our app to use for authentication, we'll create an app that uses that identity to access secrets in the vault.</span></span>

## <a name="reading-secrets-in-an-aspnet-core-app"></a><span data-ttu-id="9f5c5-102">Lectura de secretos en una aplicación ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="9f5c5-102">Reading secrets in an ASP.NET Core app</span></span>

<span data-ttu-id="9f5c5-103">La API de Azure Key Vault es una API de REST que controla toda la administración y el uso de las claves y los almacenes.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-103">The Azure Key Vault API is a REST API that handles all management and usage of keys and vaults.</span></span> <span data-ttu-id="9f5c5-104">Cada secreto de un almacén tiene una dirección URL exclusiva, y los valores de los secretos se recuperan con solicitudes GET HTTP.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-104">Each secret in a vault has a unique URL, and secret values are retrieved with HTTP GET requests.</span></span>

<span data-ttu-id="9f5c5-105">La biblioteca cliente oficial de Key Vault para .NET Core es la clase `KeyVaultClient` en el paquete NuGet Microsoft.Azure.KeyVault.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-105">The official Key Vault client library for .NET Core is the `KeyVaultClient` class in the Microsoft.Azure.KeyVault NuGet package.</span></span> <span data-ttu-id="9f5c5-106">No necesita usarla directamente; sin embargo, &mdash; con el método `AddAzureKeyVault` de ASP.NET Core, puede cargar todos los secretos de un almacén en Configuration API durante el inicio.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-106">You don't need to use it directly, though &mdash; with ASP.NET Core's `AddAzureKeyVault` method, you can load all the secrets from a vault into the Configuration API at startup.</span></span> <span data-ttu-id="9f5c5-107">Esta técnica le permite acceder a todos los secretos por nombre usando el misma interfaz `IConfiguration` utilizada para el resto de la configuración.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-107">This technique enables you to access all of your secrets by name using the same `IConfiguration` interface you use for the rest of your configuration.</span></span> <span data-ttu-id="9f5c5-108">Las aplicaciones que usan `AddAzureKeyVault` requieren los permisos **Get** y **List** para el almacén.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-108">Apps that use `AddAzureKeyVault` require both **Get** and **List** permissions to the vault.</span></span>

> [!TIP]
> <span data-ttu-id="9f5c5-109">Independientemente del marco de trabajo o del idioma utilizados para compilar la aplicación, cargue los secretos en memoria una vez durante el inicio de la aplicación, a menos que tenga una razón concreta para no hacerlo.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-109">Regardless of the framework or language you use to build your app, load secrets into memory once at app startup unless you have a specific reason not to.</span></span> <span data-ttu-id="9f5c5-110">Leerlos directamente desde el almacén cada vez que los necesite es un proceso innecesariamente lento y caro.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-110">Reading them directly from the vault every time you need them is unnecessarily slow and expensive.</span></span>

<span data-ttu-id="9f5c5-111">`AddAzureKeyVault` solo requiere el nombre del almacén como entrada, que se obtendrá de la configuración de la aplicación local.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-111">`AddAzureKeyVault` only requires the vault name as an input, which we'll get from our local app configuration.</span></span> <span data-ttu-id="9f5c5-112">También controla automáticamente la autenticación de MSI &mdash;; cuando se usa en una aplicación implementada en Azure App Service con MSI habilitado, detectará el servicio de token de MSI y lo usará para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-112">It also automatically handles MSI authentication &mdash; when used in an app deployed to Azure App Service with MSI enabled, it will detect the MSI token service and use it to authenticate.</span></span> <span data-ttu-id="9f5c5-113">Es una buena elección para la mayoría de los escenarios e implementa todos los procedimientos recomendados; además, lo vamos a usar en el ejercicio de esta unidad.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-113">It's a good fit for most scenarios and implements all best practices, and we'll use it in this unit's exercise.</span></span>

## <a name="handling-secrets-in-an-app"></a><span data-ttu-id="9f5c5-114">Administración de secretos en una aplicación</span><span class="sxs-lookup"><span data-stu-id="9f5c5-114">Handling secrets in an app</span></span>

<span data-ttu-id="9f5c5-115">Una vez cargado un secreto en la aplicación, depende de la aplicación que su administración sea segura.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-115">Once a secret is loaded into your app, it's up to your app to handle it securely.</span></span> <span data-ttu-id="9f5c5-116">En la aplicación compilada en este módulo, escribimos el valor del secreto en la respuesta del cliente y lo visualizamos en un explorador web para demostrar que se ha cargado correctamente.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-116">In the app we build in this module, we write our secret value out to the client response and view it in a web browser to demonstrate that it has been loaded successfully.</span></span> <span data-ttu-id="9f5c5-117">**Devolver el valor de un secreto al cliente *no* es algo que normalmente haga.**</span><span class="sxs-lookup"><span data-stu-id="9f5c5-117">**Returning a secret value to the client is *not* something you'd normally do!**</span></span> <span data-ttu-id="9f5c5-118">Por lo general, usará secretos para hacer cosas como inicializar las bibliotecas cliente para bases de datos o API remotas.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-118">Usually, you'll use secrets to do things like initialize client libraries for databases or remote APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f5c5-119">Revise siempre cuidadosamente el código para asegurarse de que la aplicación no escribe nunca secretos en cualquier tipo de salida, incluidos los registros, el almacenamiento y las respuestas.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-119">Always carefully review your code to ensure that your app never writes secrets to any kind of output, including logs, storage, and responses.</span></span>

## <a name="exercise"></a><span data-ttu-id="9f5c5-120">Ejercicio</span><span class="sxs-lookup"><span data-stu-id="9f5c5-120">Exercise</span></span>

<span data-ttu-id="9f5c5-121">Vamos a crear una API web de ASP.NET Core y a usar `AddAzureKeyVault` para cargar el secreto desde nuestro almacén.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-121">We'll create a new ASP.NET Core web API and use `AddAzureKeyVault` to load the secret from our vault.</span></span>

### <a name="create-the-app"></a><span data-ttu-id="9f5c5-122">Creación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="9f5c5-122">Create the app</span></span>

<span data-ttu-id="9f5c5-123">En el terminal de Azure Cloud Shell, ejecute lo siguiente para crear una aplicación de API web de ASP.NET Core y abrirla en el editor.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-123">In the Azure Cloud Shell terminal, run the following to create a new ASP.NET Core web API application and open it in the editor.</span></span>

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

<span data-ttu-id="9f5c5-124">Una vez cargada en el editor, ejecute los comandos siguientes en el shell para agregar el paquete NuGet que contiene `AddAzureKeyVault` y restaurar todas las dependencias de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-124">After the editor loads, run the following commands in the shell to add the NuGet package containing `AddAzureKeyVault` and restore all of the app's dependencies.</span></span>

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault
dotnet restore
```

### <a name="add-code-to-load-and-use-secrets"></a><span data-ttu-id="9f5c5-125">Adición de código para cargar y usar secretos</span><span class="sxs-lookup"><span data-stu-id="9f5c5-125">Add code to load and use secrets</span></span>

<span data-ttu-id="9f5c5-126">Para demostrar el uso correcto de Key Vault, vamos a modificar nuestra aplicación para cargar los secretos desde el almacén durante el inicio.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-126">To demonstrate good usage of Key Vault, we will modify our app to load secrets from the vault at startup.</span></span> <span data-ttu-id="9f5c5-127">También vamos a agregar un nuevo controlador con un punto de conexión que obtiene nuestro secreto **SecretPassword** del almacén.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-127">We'll also add a new controller with an endpoint that gets our **SecretPassword** secret from the vault.</span></span>

<span data-ttu-id="9f5c5-128">En primer lugar, el inicio de la aplicación: abra `Program.cs`, elimine el contenido y reemplácelo por el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="9f5c5-128">First, the app startup: Open `Program.cs`, delete the contents and replace them with the following code:</span></span>

```csharp
using Microsoft.AspNetCore;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;

namespace KeyVaultDemoApp
{
    public class Program
    {
        public static void Main(string[] args)
        {
            CreateWebHostBuilder(args).Build().Run();
        }

        public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
            WebHost.CreateDefaultBuilder(args)
                .ConfigureAppConfiguration((context, config) =>
                {
                    // Build the current set of configuration to load values from
                    // JSON files and environment variables, including VaultName.
                    var builtConfig = config.Build();

                    // Use VaultName from the configuration to create the full vault URL.
                    var vaultUrl = $"https://{builtConfig["VaultName"]}.vault.azure.net/";

                    // Load all secrets from the vault into configuration. This will automatically
                    // authenticate to the vault using MSI. If MSI is not available, it will
                    // check if Visual Studio and/or the Azure CLI are installed locally and
                    // see if they are configured with credentials that can access the vault.
                    config.AddAzureKeyVault(vaultUrl);
                })
                .UseStartup<Startup>();
    }
}
```

> [!NOTE]
> <span data-ttu-id="9f5c5-129">No olvide guardar los archivos con `Ctrl+S` cuando haya terminado de editarlos.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-129">Make sure to save files with `Ctrl+S` when you're done editing them.</span></span>

<span data-ttu-id="9f5c5-130">El único cambio del código de inicio es la adición de `ConfigureAppConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-130">The only change from the starter code is the addition of `ConfigureAppConfiguration`.</span></span> <span data-ttu-id="9f5c5-131">Aquí es donde cargamos el nombre del almacén desde la configuración y llamamos a `AddAzureKeyVault` con él.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-131">This is where we load the vault name from configuration and call `AddAzureKeyVault` with it.</span></span>

<span data-ttu-id="9f5c5-132">A continuación, el controlador: cree un archivo en la carpeta `Controllers` denominado `SecretTestController.cs` y pegue el código siguiente en él.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-132">Next, the controller: Create a new file in the `Controllers` folder called `SecretTestController.cs` and paste the following code into it.</span></span>

> [!NOTE]
> <span data-ttu-id="9f5c5-133">Para crear un archivo, use el comando `touch` en el shell.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-133">To create a new file, use the `touch` command in the shell.</span></span> <span data-ttu-id="9f5c5-134">En este caso, utilice `touch Controllers/SecretTestController.cs`.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-134">In this case, use `touch Controllers/SecretTestController.cs`.</span></span> <span data-ttu-id="9f5c5-135">Necesitará hacer clic en el botón Actualizar en el panel de archivos del editor para verlo allí.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-135">You'll need to click the refresh button in the Files pane of the editor to see it there.</span></span>

```csharp
using System;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Configuration;

namespace KeyVaultDemoApp.Controllers
{
    [Route("api/[controller]")]
    public class SecretTestController : ControllerBase
    {
        private readonly IConfiguration _configuration;

        public SecretTestController(IConfiguration configuration)
        {
            _configuration = configuration;
        }

        [HttpGet]
        public IActionResult Get()
        {
            // Get the secret value from configuration. This can be done anywhere
            // we have access to IConfiguration. This does not call the Key Vault
            // API, because the secrets were loaded at startup.
            var secretName = "SecretPassword";
            var secretValue = _configuration[secretName];

            if (secretValue == null)
            {
                return StatusCode(
                    StatusCodes.Status500InternalServerError,
                    $"Error: No secret named {secretName} was found...");
            }
            else {
                return Content($"Secret value: {secretValue}" +
                    Environment.NewLine + Environment.NewLine +
                    "This is for testing only! Never output a secret " +
                    "to a response or anywhere else in a real app!");
            }
        }
    }
}
```

<span data-ttu-id="9f5c5-136">Ejecute `dotnet build` en el shell para asegurarse de que todo se compila correctamente.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-136">Run `dotnet build` in the shell to make sure everything compiles.</span></span> <span data-ttu-id="9f5c5-137">La aplicación está lista para ejecutar &mdash;, ahora vamos a integrarla en Azure.</span><span class="sxs-lookup"><span data-stu-id="9f5c5-137">The app is ready to run &mdash; now let's get it into Azure!</span></span>