<span data-ttu-id="64fec-101">En este ejercicio, continuará con el ejemplo de una empresa que crea herramientas administrativas con Linux.</span><span class="sxs-lookup"><span data-stu-id="64fec-101">In this exercise, you will continue with the example of a company that makes Linux admin tools.</span></span> <span data-ttu-id="64fec-102">Recuerde que tiene previsto usar máquinas virtuales Linux para permitir que los clientes potenciales prueben el software.</span><span class="sxs-lookup"><span data-stu-id="64fec-102">Recall that you plan to use Linux VMs to let potential customers test your software.</span></span> <span data-ttu-id="64fec-103">Tiene un grupo de recursos listo y ahora es el momento de crear las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="64fec-103">You have a resource group ready and now it is time to create the VMs.</span></span>

<span data-ttu-id="64fec-104">Su empresa ha pagado por un stand en la gran feria de Linux.</span><span class="sxs-lookup"><span data-stu-id="64fec-104">Your company has paid for a booth at a big Linux trade show.</span></span> <span data-ttu-id="64fec-105">Planea habilitar un área de demostración que contiene tres terminales, cada una de ellas conectada a una máquina virtual Linux independiente.</span><span class="sxs-lookup"><span data-stu-id="64fec-105">You plan a demo area containing three terminals each connected to a separate Linux VM.</span></span> <span data-ttu-id="64fec-106">Al final de cada día, desea eliminar las máquinas virtuales y volver a crearlas, para empezar de cero cada mañana.</span><span class="sxs-lookup"><span data-stu-id="64fec-106">At the end of each day, you want to delete the VMs and recreate them, so they start fresh every morning.</span></span> <span data-ttu-id="64fec-107">Crear las máquinas virtuales manualmente después de trabajar cuando está cansado sería una tarea propensa a errores.</span><span class="sxs-lookup"><span data-stu-id="64fec-107">Creating the VMs manually after work when you are tired would be error prone.</span></span> <span data-ttu-id="64fec-108">Desea escribir un script de PowerShell para automatizar el proceso de creación de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="64fec-108">You want to write a PowerShell script to automate the VM creation process.</span></span>

## <a name="write-a-script-that-creates-virtual-machines"></a><span data-ttu-id="64fec-109">Escritura de un script que crea máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="64fec-109">Write a script that creates Virtual Machines</span></span>

<span data-ttu-id="64fec-110">Siga estos pasos para escribir el script:</span><span class="sxs-lookup"><span data-stu-id="64fec-110">Follow these steps to write the script:</span></span>

1. <span data-ttu-id="64fec-111">Cree un archivo de texto llamado **ConferenceDailyReset.ps1**.</span><span class="sxs-lookup"><span data-stu-id="64fec-111">Create a new text file named **ConferenceDailyReset.ps1**.</span></span>

2. <span data-ttu-id="64fec-112">Capture el parámetro en una variable:</span><span class="sxs-lookup"><span data-stu-id="64fec-112">Capture the parameter in a variable:</span></span>

    ```powershell
    param([string]$resourceGroup)
    ```

3. <span data-ttu-id="64fec-113">Autentíquese con sus credenciales en Azure:</span><span class="sxs-lookup"><span data-stu-id="64fec-113">Authenticate with Azure using your credentials:</span></span>

    ```powershell
    Connect-AzureRmAccount
    ```

4. <span data-ttu-id="64fec-114">Pida un nombre de usuario y una contraseña para la cuenta de administrador de la máquina virtual y capture el resultado en una variable:</span><span class="sxs-lookup"><span data-stu-id="64fec-114">Prompt for a username and password for the VM's admin account and capture the result in a variable:</span></span>

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

5. <span data-ttu-id="64fec-115">Cree un bucle que se ejecute tres veces:</span><span class="sxs-lookup"><span data-stu-id="64fec-115">Create a loop that executes three times:</span></span>

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

6. <span data-ttu-id="64fec-116">En el cuerpo del bucle, cree un nombre para cada máquina virtual y almacénelo en una variable:</span><span class="sxs-lookup"><span data-stu-id="64fec-116">In the loop body, create a name for each VM and store it in a variable:</span></span>

    ```powershell
    $vmName = "ConferenceDemo" + $i
    ```

7. <span data-ttu-id="64fec-117">A continuación, cree una máquina virtual con la variable `$vmName`:</span><span class="sxs-lookup"><span data-stu-id="64fec-117">Next, create a VM using the `$vmName` variable:</span></span>

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" 
   ```

8. <span data-ttu-id="64fec-118">Guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="64fec-118">Save the file.</span></span>

<span data-ttu-id="64fec-119">Este es el aspecto que debería tener el script completado:</span><span class="sxs-lookup"><span data-stu-id="64fec-119">The completed script should look like this:</span></span>

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

Connect-AzureRmAccount

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i

    New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a><span data-ttu-id="64fec-120">Ejecución del script</span><span class="sxs-lookup"><span data-stu-id="64fec-120">Execute the script</span></span>

<span data-ttu-id="64fec-121">Inicie PowerShell y cambie al directorio donde guardó el archivo de script.</span><span class="sxs-lookup"><span data-stu-id="64fec-121">Launch PowerShell and change to the directory where you saved the script file.</span></span> <span data-ttu-id="64fec-122">Para ejecutar el script, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="64fec-122">To run the script, execute the following command:</span></span>

```powershell
.\ConferenceDailyReset.ps1 TrialsResourceGroup
```

<span data-ttu-id="64fec-123">El script puede tardar unos minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="64fec-123">The script may take a few minutes to complete.</span></span> <span data-ttu-id="64fec-124">Cuando haya finalizado, compruebe que se ejecutó correctamente:</span><span class="sxs-lookup"><span data-stu-id="64fec-124">When it is finished, verify that it ran successfully:</span></span>

1. <span data-ttu-id="64fec-125">En un explorador, inicie sesión en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="64fec-125">In a browser, sign into the Azure portal.</span></span>
2. <span data-ttu-id="64fec-126">En el panel de navegación de la izquierda, haga clic en **Grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="64fec-126">In the navigation on the left, click **Resource Groups**.</span></span>
3. <span data-ttu-id="64fec-127">En la lista de grupos de recursos, haga clic en **TrialsResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="64fec-127">In the list of resource groups, click **TrialsResourceGroup**.</span></span> <span data-ttu-id="64fec-128">En la lista de recursos, debería ver las máquinas virtuales recién creadas y sus recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="64fec-128">In the list of resources, you should see the newly created VMs and their associated resources.</span></span>

## <a name="summary"></a><span data-ttu-id="64fec-129">Resumen</span><span class="sxs-lookup"><span data-stu-id="64fec-129">Summary</span></span>
<span data-ttu-id="64fec-130">Escribió un script que automatizó la creación de tres máquinas virtuales en el grupo de recursos indicado por un parámetro de script.</span><span class="sxs-lookup"><span data-stu-id="64fec-130">You wrote a script that automated the creation of three VMs in the resource group indicated by a script parameter.</span></span> <span data-ttu-id="64fec-131">El script es corto y sencillo pero automatiza un proceso que tardaría mucho tiempo en completar manualmente en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="64fec-131">The script is short and simple but automates a process that would take a long time to complete manually with the portal.</span></span>