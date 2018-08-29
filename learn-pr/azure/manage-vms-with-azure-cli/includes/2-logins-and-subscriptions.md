<span data-ttu-id="2a44b-101">Antes de empezar, vamos a revisar la sintaxis de la herramienta CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a44b-101">Before we start, let's review the syntax for the Azure CLI tool.</span></span> <span data-ttu-id="2a44b-102">Si ha tomado los **servicios de Azure de control con el módulo de la CLI de Azure**, sabrá que los comandos de la CLI de Azure adoptan la forma de:</span><span class="sxs-lookup"><span data-stu-id="2a44b-102">If you've taken the **Control Azure services with the Azure CLI** module, then you know that Azure CLI commands take the form of:</span></span>

```azurecli
az [command] [subcommand] [--parameter --parameter]
```

<span data-ttu-id="2a44b-103">`[command]` identifica un área específica de Azure que desea controlar.</span><span class="sxs-lookup"><span data-stu-id="2a44b-103">The `[command]` identifies the specific area of Azure you want to control.</span></span> <span data-ttu-id="2a44b-104">Por ejemplo, puede administrar la información de suscripción con el comando `account` o bases de datos SQL con el comando `sql`.</span><span class="sxs-lookup"><span data-stu-id="2a44b-104">For example, you can manage subscription information with the `account` command, or SQL databases with the `sql` command.</span></span> <span data-ttu-id="2a44b-105">`[subcommand]` y `[--parameters]` después dependen del comando con el que está trabajando.</span><span class="sxs-lookup"><span data-stu-id="2a44b-105">The `[subcommand]` and `[--parameters]` are then dependent upon the command you're working with.</span></span> 

<span data-ttu-id="2a44b-106">Puede ver una lista de parámetros, subcomandos y parámetros escribiendo un comando parcial.</span><span class="sxs-lookup"><span data-stu-id="2a44b-106">You can view a list of commands, subcommands, and parameters by typing in a partial command.</span></span> <span data-ttu-id="2a44b-107">Por ejemplo, si escribe `az` en la línea de comandos le proporcionará la pantalla de ayuda de nivel superior, mientras que si escribe `az vm` le proporcionará todos los subcomandos para máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="2a44b-107">For example, typing `az` at the command line will give you the top-level help screen, and typing `az vm` will give you all the subcommands for virtual machines.</span></span> <span data-ttu-id="2a44b-108">Este enfoque puede ser una excelente manera de explorar la herramienta CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a44b-108">This approach can be a great way to explore the Azure CLI tool.</span></span>

> [!NOTE]
> <span data-ttu-id="2a44b-109">Vamos a usar Azure Cloud Shell hospedado en explorador para que funcione con la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a44b-109">We will be using browser-hosted Azure Cloud Shell to work with the Azure CLI.</span></span> <span data-ttu-id="2a44b-110">Si prefiere trabajar desde el equipo local, todos los comandos que trataremos también se pueden ejecutar desde la línea de comandos [instalando la CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="2a44b-110">If you prefer to work from your local machine, all of the commands we cover can also be executed from the command line by [installing the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="2a44b-111">Inicio de sesión en Azure</span><span class="sxs-lookup"><span data-stu-id="2a44b-111">Log in to Azure</span></span>

<span data-ttu-id="2a44b-112">Lo primero que hará cuando se trabaje con la CLI de Azure es iniciar sesión en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a44b-112">The first thing you'll do when working with the Azure CLI is to log in to your Azure account.</span></span> <span data-ttu-id="2a44b-113">Esto se hace en el comando `login`.</span><span class="sxs-lookup"><span data-stu-id="2a44b-113">This is done with the `login` command.</span></span> <span data-ttu-id="2a44b-114">Si usa Cloud Shell, habrá un botón para iniciar sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="2a44b-114">If you're using Cloud Shell, there will be a button to sign in to Azure.</span></span>

```azurecli
az login
```

<span data-ttu-id="2a44b-115">Este comando iniciará una ventana de explorador y le permitirá seleccionar la cuenta de Microsoft que desea usar.</span><span class="sxs-lookup"><span data-stu-id="2a44b-115">This command will launch a browser window and allow you to select the Microsoft account you want to use.</span></span>

## <a name="working-with-subscriptions"></a><span data-ttu-id="2a44b-116">Trabajo con suscripciones</span><span class="sxs-lookup"><span data-stu-id="2a44b-116">Working with subscriptions</span></span>

<span data-ttu-id="2a44b-117">En este módulo, vamos a trabajar en una suscripción temporal creada como un área de juegos, pero normalmente usará una suscripción de su propia cuenta.</span><span class="sxs-lookup"><span data-stu-id="2a44b-117">In this module, we will work in a temporary subscription created as a playground, but you will normally use a subscription from your own account.</span></span> <span data-ttu-id="2a44b-118">Si tiene más de una suscripción, puede obtener una lista claramente formateada de las suscripciones mediante la instrucción `az account list --output table`.</span><span class="sxs-lookup"><span data-stu-id="2a44b-118">If you have more than one subscription, you can get a clearly formatted list of subscriptions using the `az account list --output table` statement.</span></span>

```
Name                                  CloudName    SubscriptionId                        State    IsDefault
------------------------------------  -----------  ------------------------------------  -------  -----------
Contoso Legacy Resources              AzureCloud   abc13b0c-d2c4-64b2-9ac5-2f4cb819b752  Enabled  True
Visual Studio Enterprise              AzureCloud   233aebce-23c2-4572-c056-c029449e93ed  Enabled  False
```

<span data-ttu-id="2a44b-119">Tenga en cuenta que el comando también identifica la suscripción _predeterminada_ donde se aplicarán todos los comandos.</span><span class="sxs-lookup"><span data-stu-id="2a44b-119">Notice that the command also identifies the _default_ subscription where all your commands will apply.</span></span> <span data-ttu-id="2a44b-120">Si prefiere trabajar en una suscripción diferente, puede usar el comando `az account set --subscription "[name]"`.</span><span class="sxs-lookup"><span data-stu-id="2a44b-120">If you would prefer to work in a different subscription, you can use the `az account set --subscription "[name]"` command.</span></span> <span data-ttu-id="2a44b-121">Por ejemplo, podríamos establecer nuestra suscripción actual para que sea `Visual Studio Enterprise` en la lista anterior mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="2a44b-121">For example, we could set our current subscription to be `Visual Studio Enterprise` from the above list through the following command:</span></span>

```azurecli
az account set --subscription "Visual Studio Enterprise"
```