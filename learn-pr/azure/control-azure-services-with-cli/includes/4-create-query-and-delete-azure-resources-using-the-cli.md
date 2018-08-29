## <a name="motivation"></a><span data-ttu-id="d01bc-101">Motivación</span><span class="sxs-lookup"><span data-stu-id="d01bc-101">Motivation</span></span>
<span data-ttu-id="d01bc-102">La CLI de Azure le permite escribir comandos y ejecutarlos de inmediato.</span><span class="sxs-lookup"><span data-stu-id="d01bc-102">The Azure CLI lets you write commands and execute them immediately.</span></span> <span data-ttu-id="d01bc-103">Recuerde que es el objetivo general en el ejemplo de desarrollo de software es implementar nuevas compilaciones de una aplicación web para realizar pruebas.</span><span class="sxs-lookup"><span data-stu-id="d01bc-103">Recall that the overall goal in the software development example is to deploy new builds of a web app for testing.</span></span> <span data-ttu-id="d01bc-104">El primer paso es crear un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d01bc-104">The first step is to create a resource group.</span></span> <span data-ttu-id="d01bc-105">Recuerde que el objetivo aquí es crear estos recursos mediante una instalación local de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d01bc-105">Remember that the goal here is to create these resources using a local installation of the Azure CLI.</span></span> 

<span data-ttu-id="d01bc-106">Esta unidad muestra cómo usar la CLI de Azure para iniciar sesión su suscripción de Azure y crear un nuevo recurso.</span><span class="sxs-lookup"><span data-stu-id="d01bc-106">This unit shows you how to use the Azure CLI to sign in to your Azure subscription and create a new resource.</span></span>

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a><span data-ttu-id="d01bc-107">¿Qué recursos de Azure se pueden administrar mediante la CLI de Azure?</span><span class="sxs-lookup"><span data-stu-id="d01bc-107">What Azure resources can be managed using the Azure CLI?</span></span>
<span data-ttu-id="d01bc-108">La CLI de Azure le permite controlar casi todos los aspectos de cualquier recurso de Azure.</span><span class="sxs-lookup"><span data-stu-id="d01bc-108">The Azure CLI lets you control nearly every aspect of every Azure resource.</span></span> <span data-ttu-id="d01bc-109">Puede trabajar con grupos de recursos, almacenamiento, máquinas virtuales, Azure Active Directory (Azure AD), contenedores, aprendizaje automático, etc.</span><span class="sxs-lookup"><span data-stu-id="d01bc-109">You can work with resource groups, storage, virtual machines, Azure Active Directory (Azure AD), containers, machine learning, and so on.</span></span>

<span data-ttu-id="d01bc-110">Los comandos de la CLI se estructuran en grupos y subgrupos.</span><span class="sxs-lookup"><span data-stu-id="d01bc-110">Commands in the CLI are structured in groups and subgroups.</span></span> <span data-ttu-id="d01bc-111">Cada grupo representa un servicio suministrado por Azure y los subgrupos dividen comandos para estos servicios en agrupaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="d01bc-111">Each group represents a service provided by Azure, and the subgroups divide commands for these services into logical groupings.</span></span> <span data-ttu-id="d01bc-112">Por ejemplo, el grupo de **almacenamiento** contiene subgrupos como **cuenta**, **blob**, **almacenamiento** y **cola**.</span><span class="sxs-lookup"><span data-stu-id="d01bc-112">For example, the **storage** group contains subgroups including **account**, **blob**, **storage**, and **queue**.</span></span>

<span data-ttu-id="d01bc-113">Así pues, ¿cómo puede encontrar los comandos específicos que necesita?</span><span class="sxs-lookup"><span data-stu-id="d01bc-113">So, how do you find the particular commands you need?</span></span> <span data-ttu-id="d01bc-114">Una manera es usar **az find**.</span><span class="sxs-lookup"><span data-stu-id="d01bc-114">One way is to use **az find**.</span></span> <span data-ttu-id="d01bc-115">Por ejemplo, si desea buscar los comandos que pueden ayudarle a administrar un **blob** de almacenamiento, usaría el comando de buscar siguiente:</span><span class="sxs-lookup"><span data-stu-id="d01bc-115">For example, if you want to find commands that might help you manage a storage **blob**, you'd use the following find command:</span></span>

```bash
az find -q blob
```

<span data-ttu-id="d01bc-116">Si ya conoce el nombre del comando que desea, el argumento **--help** para ese comando podría resultar más útil.</span><span class="sxs-lookup"><span data-stu-id="d01bc-116">If you already know the name of the command you want, the **--help** argument for that command may be more useful.</span></span> <span data-ttu-id="d01bc-117">Se obtiene información detallada sobre el comando y, para un grupo de comandos, una lista de los subcomandos disponibles.</span><span class="sxs-lookup"><span data-stu-id="d01bc-117">You get detailed information on the command, and for a command group, a list of the available subcommands.</span></span> <span data-ttu-id="d01bc-118">Por lo tanto, en nuestro ejemplo de almacenamiento, mostramos cómo puede obtener una lista de los comandos y subgrupos para administrar el almacenamiento de blobs:</span><span class="sxs-lookup"><span data-stu-id="d01bc-118">So, with our storage example, here's how you can get a list of the subgroups and commands for managing blob storage:</span></span>

```bash
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a><span data-ttu-id="d01bc-119">Creación de un recurso de Azure</span><span class="sxs-lookup"><span data-stu-id="d01bc-119">How to create an Azure resource</span></span>
<span data-ttu-id="d01bc-120">La creación de un nuevo recurso de Azure normalmente consta de tres pasos: la conexión a su suscripción de Azure, la creación del recurso y la comprobación de que se creó correctamente (ver abajo).</span><span class="sxs-lookup"><span data-stu-id="d01bc-120">When creating a new Azure resource, there are typically three steps: connect to your Azure subscription, create the resource, and verify that creation was successful (see below).</span></span>

![Pasos para crear un recurso mediante la CLI de Azure](../media-drafts/4-create-resources-overview.png)

<span data-ttu-id="d01bc-122">Cada paso se corresponde con un comando de la CLI de Azure diferente.</span><span class="sxs-lookup"><span data-stu-id="d01bc-122">Each step corresponds to a different Azure CLI command.</span></span>

### <a name="connect"></a><span data-ttu-id="d01bc-123">Conectar</span><span class="sxs-lookup"><span data-stu-id="d01bc-123">Connect</span></span>
<span data-ttu-id="d01bc-124">Puesto que está trabajando con una instalación local de la CLI de Azure, tiene que autenticarse para poder ejecutar comandos de Azure usando para ello el comando **login** de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d01bc-124">Since you're working with a local install of the Azure CLI, you'll need to authenticate before you can execute Azure commands, by using the Azure CLI **login** command.</span></span> 

```bash
az login
```

<span data-ttu-id="d01bc-125">La CLI de Azure normalmente iniciará el explorador predeterminado para abrir la página de inicio de sesión de Azure.</span><span class="sxs-lookup"><span data-stu-id="d01bc-125">The Azure CLI will typically launch your default browser to open the Azure sign-in page.</span></span> <span data-ttu-id="d01bc-126">Si esto no funciona, siga las instrucciones de la línea de comandos y escriba un código de autorización en [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span><span class="sxs-lookup"><span data-stu-id="d01bc-126">If this doesn't work, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

<span data-ttu-id="d01bc-127">Una vez que la sesión se inicie correctamente, estará conectado a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d01bc-127">After a successful sign in, you'll be connected to your Azure subscription.</span></span> 

### <a name="create"></a><span data-ttu-id="d01bc-128">Crear</span><span class="sxs-lookup"><span data-stu-id="d01bc-128">Create</span></span>
<span data-ttu-id="d01bc-129">A menudo, deberá crear un nuevo grupo de recursos para crear un nuevo servicio de Azure, por lo que vamos a usar grupos de recursos como ejemplo de creación de recursos de Azure desde la CLI.</span><span class="sxs-lookup"><span data-stu-id="d01bc-129">You'll often need to create a new resource group before you create a new Azure service, so we'll use resource groups as an example to show how to create Azure resources from the CLI.</span></span>

<span data-ttu-id="d01bc-130">El comando **group create** de la CLI de Azure crea un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d01bc-130">The Azure CLI **group create** command creates a resource group.</span></span> <span data-ttu-id="d01bc-131">Debe especificar un nombre y una ubicación.</span><span class="sxs-lookup"><span data-stu-id="d01bc-131">You must specify a name and location.</span></span> <span data-ttu-id="d01bc-132">El nombre debe ser único dentro de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="d01bc-132">The name must be unique within your subscription.</span></span> <span data-ttu-id="d01bc-133">La ubicación determina dónde se almacenarán los metadatos para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d01bc-133">The location determines where the metadata for your resource group will be stored.</span></span> <span data-ttu-id="d01bc-134">Use cadenas como "Oeste de EE. UU.", "Europa del Norte" u "Oeste de la India" para especificar la ubicación; también puede utilizar los equivalentes de una sola palabra, como westus, northeurope o westindia.</span><span class="sxs-lookup"><span data-stu-id="d01bc-134">You use strings like "West US", "North Europe", or "West India" to specify the location; alternatively, you can use single word equivalents, such as westus, northeurope, or westindia.</span></span> <span data-ttu-id="d01bc-135">La sintaxis del núcleo es:</span><span class="sxs-lookup"><span data-stu-id="d01bc-135">The core syntax is:</span></span>

```bash
az group create --name <name> --location <location>
```

### <a name="verify"></a><span data-ttu-id="d01bc-136">Verify</span><span class="sxs-lookup"><span data-stu-id="d01bc-136">Verify</span></span>
<span data-ttu-id="d01bc-137">Para muchos recursos de Azure, la CLI de Azure proporciona un subcomando **list** que le permite ver los detalles de los recursos.</span><span class="sxs-lookup"><span data-stu-id="d01bc-137">For many Azure resources, the Azure CLI provides a **list** subcommand to view resource details.</span></span> <span data-ttu-id="d01bc-138">Por ejemplo, el comando **group list** de la CLI de Azure enumera los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d01bc-138">For example, the Azure CLI **group list** command lists your Azure resource groups.</span></span> <span data-ttu-id="d01bc-139">Esto resulta útil aquí para comprobar si la creación del grupo de recursos se completó correctamente:</span><span class="sxs-lookup"><span data-stu-id="d01bc-139">This is useful here to verify whether creation of the resource group was successful:</span></span>

```bash
az group list
```

<span data-ttu-id="d01bc-140">Para obtener una vista más concisa, puede aplicar al resultado el formato de una tabla sencilla:</span><span class="sxs-lookup"><span data-stu-id="d01bc-140">To get a more concise view, you can format the output as a simple table:</span></span>

```bash
az group list --output table
```
