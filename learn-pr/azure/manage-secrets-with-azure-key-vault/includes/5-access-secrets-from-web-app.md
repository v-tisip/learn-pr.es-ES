Ahora que sabe que al habilitar MSI se crea una identidad para que la aplicación la use para fines de autenticación, crearemos una aplicación que use dicha identidad para acceder a los secretos en el almacén.

## <a name="reading-secrets-in-an-aspnet-core-app"></a>Lectura de secretos en una aplicación ASP.NET Core

La API de Azure Key Vault es una API de REST que controla toda la administración y el uso de las claves y los almacenes. Cada secreto de un almacén tiene una dirección URL exclusiva, y los valores de los secretos se recuperan con solicitudes GET HTTP.

La biblioteca cliente oficial de Key Vault para .NET Core es la clase `KeyVaultClient` en el paquete NuGet Microsoft.Azure.KeyVault. No necesita usarla directamente; sin embargo, &mdash; con el método `AddAzureKeyVault` de ASP.NET Core, puede cargar todos los secretos de un almacén en Configuration API durante el inicio. Esta técnica le permite acceder a todos los secretos por nombre usando el misma interfaz `IConfiguration` utilizada para el resto de la configuración. Las aplicaciones que usan `AddAzureKeyVault` requieren los permisos **Get** y **List** para el almacén.

> [!TIP]
> Independientemente del marco de trabajo o del idioma utilizados para compilar la aplicación, cargue los secretos en memoria una vez durante el inicio de la aplicación, a menos que tenga una razón concreta para no hacerlo. Leerlos directamente desde el almacén cada vez que los necesite es un proceso innecesariamente lento y caro.

`AddAzureKeyVault` solo requiere el nombre del almacén como entrada, que se obtendrá de la configuración de la aplicación local. También controla automáticamente la autenticación de MSI &mdash;; cuando se usa en una aplicación implementada en Azure App Service con MSI habilitado, detectará el servicio de token de MSI y lo usará para la autenticación. Es una buena elección para la mayoría de los escenarios e implementa todos los procedimientos recomendados; además, lo vamos a usar en el ejercicio de esta unidad.

## <a name="handling-secrets-in-an-app"></a>Administración de secretos en una aplicación

Una vez cargado un secreto en la aplicación, depende de la aplicación que su administración sea segura. En la aplicación compilada en este módulo, escribimos el valor del secreto en la respuesta del cliente y lo visualizamos en un explorador web para demostrar que se ha cargado correctamente. **Devolver el valor de un secreto al cliente *no* es algo que normalmente haga.** Por lo general, usará secretos para hacer cosas como inicializar las bibliotecas cliente para bases de datos o API remotas.

> [!IMPORTANT]
> Revise siempre cuidadosamente el código para asegurarse de que la aplicación no escribe nunca secretos en cualquier tipo de salida, incluidos los registros, el almacenamiento y las respuestas.

## <a name="exercise"></a>Ejercicio

Vamos a crear una API web de ASP.NET Core y a usar `AddAzureKeyVault` para cargar el secreto desde nuestro almacén.

### <a name="create-the-app"></a>Creación de la aplicación

En el terminal de Azure Cloud Shell, ejecute lo siguiente para crear una aplicación de API web de ASP.NET Core y abrirla en el editor.

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

Una vez cargada en el editor, ejecute los comandos siguientes en el shell para agregar el paquete NuGet que contiene `AddAzureKeyVault` y restaurar todas las dependencias de la aplicación.

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault
dotnet restore
```

### <a name="add-code-to-load-and-use-secrets"></a>Adición de código para cargar y usar secretos

Para demostrar el uso correcto de Key Vault, vamos a modificar nuestra aplicación para cargar los secretos desde el almacén durante el inicio. También vamos a agregar un nuevo controlador con un punto de conexión que obtiene nuestro secreto **SecretPassword** del almacén.

En primer lugar, el inicio de la aplicación: abra `Program.cs`, elimine el contenido y reemplácelo por el siguiente código:

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
> No olvide guardar los archivos con `Ctrl+S` cuando haya terminado de editarlos.

El único cambio del código de inicio es la adición de `ConfigureAppConfiguration`. Aquí es donde cargamos el nombre del almacén desde la configuración y llamamos a `AddAzureKeyVault` con él.

A continuación, el controlador: cree un archivo en la carpeta `Controllers` denominado `SecretTestController.cs` y pegue el código siguiente en él.

> [!NOTE]
> Para crear un archivo, use el comando `touch` en el shell. En este caso, utilice `touch Controllers/SecretTestController.cs`. Necesitará hacer clic en el botón Actualizar en el panel de archivos del editor para verlo allí.

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

Ejecute `dotnet build` en el shell para asegurarse de que todo se compila correctamente. La aplicación está lista para ejecutar &mdash;, ahora vamos a integrarla en Azure.