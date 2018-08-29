<span data-ttu-id="74b88-101">En este módulo, protegió la configuración del secreto de una aplicación en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="74b88-101">In this module, you secured an app's secret configuration in Azure Key Vault.</span></span> <span data-ttu-id="74b88-102">El código de nuestra aplicación se autentica en el almacén con Managed Service Identity y carga automáticamente los secretos del almacén en el sistema de configuración de ASP.NET Core en el inicio.</span><span class="sxs-lookup"><span data-stu-id="74b88-102">Our app code authenticates to the vault with Managed Service Identity and automatically loads the secrets from the vault into ASP.NET Core's configuration system at startup.</span></span>

## <a name="cleanup"></a><span data-ttu-id="74b88-103">Limpieza</span><span class="sxs-lookup"><span data-stu-id="74b88-103">Cleanup</span></span>

<span data-ttu-id="74b88-104">Para limpiar la suscripción de Azure, ejecute el siguiente código en Azure Cloud Shell para eliminar el grupo de recursos que contiene todos los recursos que hemos creado en este módulo.</span><span class="sxs-lookup"><span data-stu-id="74b88-104">To clean up your Azure subscription, run the following in the Azure Cloud Shell to delete the resource group containing all the resources we created in this module.</span></span>

```console
az group delete --name keyvault-exercise-group
```

<span data-ttu-id="74b88-105">Para limpiar el almacenamiento de Cloud Shell, elimine el directorio `KeyVaultDemoApp`.</span><span class="sxs-lookup"><span data-stu-id="74b88-105">To clean up your Cloud Shell storage, delete the `KeyVaultDemoApp` directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74b88-106">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="74b88-106">Next steps</span></span>

<span data-ttu-id="74b88-107">Si se tratase de una aplicación real, ¿qué vendría a continuación?</span><span class="sxs-lookup"><span data-stu-id="74b88-107">If this was a real app, what would come next?</span></span>

* <span data-ttu-id="74b88-108">Colocar todos los secretos de aplicación en los almacenes.</span><span class="sxs-lookup"><span data-stu-id="74b88-108">Put all your app secrets in your vaults!</span></span> <span data-ttu-id="74b88-109">Ya no hay ninguna razón para tenerlos en archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="74b88-109">There's no longer any reason to have them in configuration files.</span></span>
* <span data-ttu-id="74b88-110">Seguir desarrollando la aplicación.</span><span class="sxs-lookup"><span data-stu-id="74b88-110">Continue to develop the application.</span></span> <span data-ttu-id="74b88-111">El entorno de producción está completamente configurado, por lo que no tendrá que repetir la instalación en las implementaciones futuras.</span><span class="sxs-lookup"><span data-stu-id="74b88-111">Your production environment is all set up, so for future deployments to it you don't need to repeat all the setup.</span></span>
* <span data-ttu-id="74b88-112">Para admitir el desarrollo, cree un almacén de entorno de desarrollo que contenga secretos con los mismos nombres pero distintos valores.</span><span class="sxs-lookup"><span data-stu-id="74b88-112">To support development, create a development-environment vault that contains secrets with the same names but different values.</span></span> <span data-ttu-id="74b88-113">Conceda permisos al equipo de desarrollo y configure el nombre del almacén en el archivo de configuración del entorno de desarrollo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="74b88-113">Grant permissions to the development team and configure the vault name in the app's development-environment configuration file.</span></span> <span data-ttu-id="74b88-114">Cuando los desarrolladores ejecutan la aplicación localmente, `AddAzureKeyVault` detectará automáticamente las instalaciones locales de Visual Studio y la CLI de Azure y usará las credenciales de Azure configuradas en esas aplicaciones para iniciar sesión y acceder al almacén.</span><span class="sxs-lookup"><span data-stu-id="74b88-114">When developers run the app locally, `AddAzureKeyVault` will automatically detect local installations of Visual Studio and the Azure CLI and use Azure credentials configured in those applications to sign in and access the vault.</span></span>
* <span data-ttu-id="74b88-115">Cree entornos adicionales con fines tales como pruebas de aceptación de usuario.</span><span class="sxs-lookup"><span data-stu-id="74b88-115">Create additional environments for purposes like user acceptance testing.</span></span>
* <span data-ttu-id="74b88-116">Reparta los almacenes entre distintas suscripciones y/o grupos de recursos para aislarlos.</span><span class="sxs-lookup"><span data-stu-id="74b88-116">Separate vaults across different subscriptions and/or resource groups to isolate them.</span></span>
* <span data-ttu-id="74b88-117">Conceda acceso a otros almacenes de entorno a las personas adecuadas.</span><span class="sxs-lookup"><span data-stu-id="74b88-117">Grant access to other environment vaults to the appropriate people.</span></span>

## <a name="further-reading"></a><span data-ttu-id="74b88-118">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="74b88-118">Further reading</span></span>

* [<span data-ttu-id="74b88-119">Documentación de Key Vault</span><span class="sxs-lookup"><span data-stu-id="74b88-119">Key Vault documentation</span></span>](https://docs.microsoft.com/azure/key-vault/)
* <span data-ttu-id="74b88-120">[More about AddAzureKeyVault and its advanced options](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x) (Más información sobre AddAzureKeyVault y sus opciones avanzadas)</span><span class="sxs-lookup"><span data-stu-id="74b88-120">[More about AddAzureKeyVault and its advanced options](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x)</span></span>
* <span data-ttu-id="74b88-121">[En este tutorial](https://docs.microsoft.com/azure/key-vault/key-vault-use-from-web-application) se explica cómo usar `KeyVaultClient`, incluida su autenticación manual en Azure Active Directory con un secreto de cliente en lugar de MSI.</span><span class="sxs-lookup"><span data-stu-id="74b88-121">[This tutorial](https://docs.microsoft.com/azure/key-vault/key-vault-use-from-web-application) walks through using `KeyVaultClient`, including manually authenticating it to Azure Active Directory using a client secret instead of MSI.</span></span>
* <span data-ttu-id="74b88-122">[MSI token service documentation](https://docs.microsoft.com/azure/app-service/app-service-managed-service-identity#using-the-rest-protocol) (Documentación del servicio de token de MSI), para implementar el flujo de trabajo de autenticación personalmente</span><span class="sxs-lookup"><span data-stu-id="74b88-122">[MSI token service documentation](https://docs.microsoft.com/azure/app-service/app-service-managed-service-identity#using-the-rest-protocol), for implementing the authentication workflow yourself</span></span>