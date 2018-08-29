
<span data-ttu-id="7eb11-101">En este ejercicio, usará la CLI de Azure en el equipo local para crear un grupo de recursos y después para implementar una aplicación web en este grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7eb11-101">In this exercise, you will use the Azure CLI on your local machine to create a resource group, and then to deploy a web app into this resource group.</span></span> 

### <a name="steps-to-create-a-resource-group"></a><span data-ttu-id="7eb11-102">Pasos para crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="7eb11-102">Steps to create a resource group</span></span>
1. <span data-ttu-id="7eb11-103">Abra un shell de Bash en Linux o macOS, o bien abra la ventana del símbolo del sistema o PowerShell si trabaja en Windows.</span><span class="sxs-lookup"><span data-stu-id="7eb11-103">Open a bash shell on Linux or macOS, or open the Command Prompt window or PowerShell if working from Windows.</span></span>

1. <span data-ttu-id="7eb11-104">Inicie la CLI de Azure y ejecute el comando de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="7eb11-104">Start the Azure CLI and run the login command.</span></span>

    ```bash
    az login
    ```
    <span data-ttu-id="7eb11-105">Si no aparece una página de inicio de sesión de Azure en el explorador web, siga las instrucciones de la línea de comandos y escriba un código de autorización en [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span><span class="sxs-lookup"><span data-stu-id="7eb11-105">If you do not get an Azure sign-in page in your web browser, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

1. <span data-ttu-id="7eb11-106">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7eb11-106">Create a resource group.</span></span>

    ```bash
    az group create --location westeurope --name popupResGroup
    ```

1. <span data-ttu-id="7eb11-107">Muestre todos sus grupos de recursos en una tabla para comprobar que el grupo de recursos se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="7eb11-107">Verify that the resource group was created successfully by listing all your resource groups in a table.</span></span>

    ```bash
    az group list --output table
    ```
1. <span data-ttu-id="7eb11-108">Si quiere, confirme que el recurso se ha creado en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7eb11-108">Optionally, confirm the resource was created in the Azure portal.</span></span> <span data-ttu-id="7eb11-109">Abra un explorador web, inicie sesión en el portal y vaya a la sección **Grupos de recursos** (ver a continuación).</span><span class="sxs-lookup"><span data-stu-id="7eb11-109">Open a web browser, sign in to the portal and navigate to the **Resource Groups** section (see below).</span></span> <span data-ttu-id="7eb11-110">El nuevo grupo de recursos debería mostrarse en la lista.</span><span class="sxs-lookup"><span data-stu-id="7eb11-110">The new resource group should be displayed in the list.</span></span>

![Uso del portal para enumerar los grupos de recursos](../media-drafts/5-listing-resource-groups.png)

### <a name="steps-to-create-a-service-plan"></a><span data-ttu-id="7eb11-112">Pasos para crear un plan de servicio</span><span class="sxs-lookup"><span data-stu-id="7eb11-112">Steps to create a service plan</span></span>
<span data-ttu-id="7eb11-113">Al ejecutar Web Apps, mediante Azure App Service, paga por los recursos de proceso de Azure que use la aplicación y esto depende del plan de App Service asociado con Web Apps.</span><span class="sxs-lookup"><span data-stu-id="7eb11-113">When you run Web Apps, using the Azure App Service, you pay for the Azure compute resources used by the app, and this depends on the App Service plan associated with your Web Apps.</span></span> <span data-ttu-id="7eb11-114">Los planes de servicio determinan la región que se usa para el centro de datos de la aplicación, el número de máquinas virtuales que se usan y el plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="7eb11-114">Service plans determine the region used for the app datacenter, number of VMs used, and pricing tier.</span></span>

1. <span data-ttu-id="7eb11-115">Cree un plan de App Service para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7eb11-115">Create an App Service plan to run your app.</span></span> <span data-ttu-id="7eb11-116">El nombre de la aplicación y el plan deben ser únicos, así que cambie la cadena "12345" por un número aleatorio.</span><span class="sxs-lookup"><span data-stu-id="7eb11-116">The name of the app and plan must be unique, so change the string "12345" to a random number.</span></span> <span data-ttu-id="7eb11-117">El siguiente comando no especifica un plan de tarifa ni detalles de la instancia de la máquina virtual, de modo que, de forma predeterminada, obtendrá un plan **Básico** con una instancia de máquina virtual **pequeña**.</span><span class="sxs-lookup"><span data-stu-id="7eb11-117">The following command does not specify a pricing tier or VM instance details, so by default, you'll get a **Basic** plan with 1 **Small** VM instance.</span></span>

    ```bash
    az appservice plan create --name popupapp12345 --resource-group popupResGroup --location westeurope
    ```

1. <span data-ttu-id="7eb11-118">Muestre todos sus planes en una tabla para comprobar que el plan de servicio se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="7eb11-118">Verify that the service plan was created successfully by listing all your plans in a table.</span></span>

    ```bash
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a><span data-ttu-id="7eb11-119">Pasos para crear una aplicación web</span><span class="sxs-lookup"><span data-stu-id="7eb11-119">Steps to create a web app</span></span>
<span data-ttu-id="7eb11-120">A continuación, creará la aplicación web en su plan de servicio.</span><span class="sxs-lookup"><span data-stu-id="7eb11-120">Next, you'll create the web app in your service plan.</span></span> <span data-ttu-id="7eb11-121">Puede implementar el código al mismo tiempo, pero, en nuestro ejemplo, lo haremos en pasos distintos.</span><span class="sxs-lookup"><span data-stu-id="7eb11-121">You can deploy the code at the same time, but for our example, we'll do this as separate steps.</span></span>

1. <span data-ttu-id="7eb11-122">Cree la aplicación web, sin olvidarse de cambiar la cadena "12345" por el mismo número aleatorio que ha usado antes.</span><span class="sxs-lookup"><span data-stu-id="7eb11-122">Create the web app, remembering to change the string "12345" to the same random number you used earlier.</span></span>
    ```bash
    az webapp create --name popupapp12345 --resource-group popupResGroup --plan popupapp12345
    ```

1. <span data-ttu-id="7eb11-123">Muestre todas las aplicaciones en una tabla para comprobar que la aplicación se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="7eb11-123">Verify that the app was created successfully by listing all your apps in a table.</span></span>

    ```bash
    az webapp list --output table
    ```

1. <span data-ttu-id="7eb11-124">Apunte el valor de **DefaultHostName**; lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="7eb11-124">Make a note of the **DefaultHostName**; you will need this later.</span></span>

### <a name="steps-to-deploy-code-from-github"></a><span data-ttu-id="7eb11-125">Pasos para implementar código desde GitHub</span><span class="sxs-lookup"><span data-stu-id="7eb11-125">Steps to deploy code from GitHub</span></span>
1. <span data-ttu-id="7eb11-126">El último paso consiste en implementar código desde un repositorio de GitHub en la aplicación web, recordando de nuevo cambiar la cadena "12345" por el mismo número aleatorio que ha usado antes.</span><span class="sxs-lookup"><span data-stu-id="7eb11-126">The final step is to deploy code from a GitHub repository to the web app, again remembering to change the string "12345" to the same random number you used earlier.</span></span>
    ```bash
    az webapp deployment source config --name popupapp12345 --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. <span data-ttu-id="7eb11-127">Copie la siguiente URL en un explorador para ver la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7eb11-127">Copy the following url into a browser to see the web app.</span></span>
<span data-ttu-id="7eb11-128">http://popupapp12345.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="7eb11-128">http://popupapp12345.azurewebsites.net</span></span>

1. <span data-ttu-id="7eb11-129">La página muestra “HelloWorld!”.</span><span class="sxs-lookup"><span data-stu-id="7eb11-129">The page displays "HelloWorld!"</span></span>

1. <span data-ttu-id="7eb11-130">Cierre la ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="7eb11-130">Close the browser window.</span></span>

## <a name="summary"></a><span data-ttu-id="7eb11-131">Resumen</span><span class="sxs-lookup"><span data-stu-id="7eb11-131">Summary</span></span>
<span data-ttu-id="7eb11-132">Este ejercicio ha mostrado un patrón típico de una sesión interactiva de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="7eb11-132">This exercise demonstrated a typical pattern for an interactive Azure CLI session.</span></span> <span data-ttu-id="7eb11-133">Primero ha usado un comando estándar para crear un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7eb11-133">You first used a standard command to create a new resource group.</span></span> <span data-ttu-id="7eb11-134">Después ha usado un conjunto de comandos para implementar un recurso (en este ejemplo, una aplicación web) en este grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7eb11-134">You then used a set of commands to deploy a resource (in this example, a web app) into this resource group.</span></span> <span data-ttu-id="7eb11-135">Este conjunto de comandos podría combinarse fácilmente en un script de shell y ejecutarse cada vez que necesite crear el mismo recurso.</span><span class="sxs-lookup"><span data-stu-id="7eb11-135">This set of commands could easily be combined into a shell script, and executed every time you need to create the same resource.</span></span>
