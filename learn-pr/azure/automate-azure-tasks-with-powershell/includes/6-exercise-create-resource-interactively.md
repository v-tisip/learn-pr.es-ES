<span data-ttu-id="9d1c6-101">Imagine que trabaja en una empresa que crea un conjunto de herramientas de administración de Linux.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-101">Suppose you work at a company that makes a suite of Linux admin tools.</span></span> <span data-ttu-id="9d1c6-102">Su trabajo consiste en ayudar a posibles clientes a probar el software antes de comprarlo.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-102">Your job is to help potential customers try your software before they buy it.</span></span> <span data-ttu-id="9d1c6-103">Dado que el software hace cambios en el nivel de raíz del sistema operativo, decidió crear una máquina virtual Linux para cada cliente de prueba.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-103">Because the software makes root-level changes to the OS, you have decided to create a Linux VM for each trial customer.</span></span> <span data-ttu-id="9d1c6-104">Puede crear todas las máquinas virtuales que necesite y eliminarlas al final de la suscripción de prueba.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-104">You create the VMs as needed and delete them at the end of the trial subscription.</span></span> <span data-ttu-id="9d1c6-105">De este modo, cada cliente empieza con una versión limpia del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-105">This way, each customer starts with a clean version of the OS.</span></span> 

<span data-ttu-id="9d1c6-106">Para separar estas máquinas virtuales de las máquinas virtuales que la empresa usa para las pruebas internas, creará un grupo de recursos dedicado para alojarlas.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-106">To keep these VMs separate from the VMs your company uses for internal testing, you will create a dedicated resource group to house them.</span></span> <span data-ttu-id="9d1c6-107">Solo necesita un grupo de recursos, por lo que usar Azure PowerShell en modo interactivo es una opción razonable para esta tarea.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-107">You only need one resource group so using Azure PowerShell in interactive mode is a reasonable choice for this task.</span></span>

## <a name="steps-to-create-a-resource-group"></a><span data-ttu-id="9d1c6-108">Pasos para crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9d1c6-108">Steps to create a resource group</span></span>

1. <span data-ttu-id="9d1c6-109">Inicie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-109">Launch PowerShell.</span></span>

1. <span data-ttu-id="9d1c6-110">Importe el módulo en la sesión actual para que pueda acceder a los cmdlets de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-110">Import the module into the current session so you have access to the Azure cmdlets.</span></span>

   ```powershell
   Import-Module AzureRM
   ```

1. <span data-ttu-id="9d1c6-111">Conéctese a Azure mediante el comando que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-111">Connect to Azure using the command shown below.</span></span> <span data-ttu-id="9d1c6-112">Después de escribir el comando, autentíquese con sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-112">After entering the command, authenticate by providing your Azure credentials.</span></span>

   ```powershell
   Connect-AzureRmAccount
   ```

1. <span data-ttu-id="9d1c6-113">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-113">Create a resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name "TrialsResourceGroup" -Location "East US"
    ```

1. <span data-ttu-id="9d1c6-114">Compruebe que el grupo de recursos se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-114">Verify the resource group was created successfully.</span></span>

    ```powershell
    Get-AzureRmResource | Format-Table
    ```
<span data-ttu-id="9d1c6-115">Otra manera de comprobar si el grupo de recursos se creó correctamente es usar Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-115">Another way to check whether the resource group was created successfully is to use the Azure Portal.</span></span> <span data-ttu-id="9d1c6-116">Para hacerlo, inicie sesión en el portal y navegue a la sección **Grupos de recursos** (ver a continuación).</span><span class="sxs-lookup"><span data-stu-id="9d1c6-116">To do this, login to the Portal and navigate to the **Resource Groups** section (see below).</span></span> <span data-ttu-id="9d1c6-117">El nuevo grupo de recursos debería mostrarse en la lista.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-117">The new resource group should be displayed in the list.</span></span>

![Uso del portal para enumerar los grupos de recursos](../media-drafts/6-listing-resource-groups.png)

## <a name="summary"></a><span data-ttu-id="9d1c6-119">Resumen</span><span class="sxs-lookup"><span data-stu-id="9d1c6-119">Summary</span></span>
<span data-ttu-id="9d1c6-120">En este ejercicio se muestra un patrón común para una sesión interactiva de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-120">This exercise shows a common pattern for an interactive PowerShell session.</span></span> <span data-ttu-id="9d1c6-121">Usó un cmdlet estándar para importar el módulo AzureRM y después los cmdlets de Azure PowerShell para realizar una tarea específica.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-121">You used a standard cmdlet to import the AzureRM module and then the Azure PowerShell cmdlets to perform a specific task.</span></span> <span data-ttu-id="9d1c6-122">Ahora tiene un grupo de recursos en su suscripción y está listo para crear máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9d1c6-122">You now have a resource group in your subscription and are ready to create VMs.</span></span>