<span data-ttu-id="c862c-101">Si es necesario, instale **Azure PowerShell** en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="c862c-101">In this exercise, you will install **Azure PowerShell** on your local machine.</span></span> <span data-ttu-id="c862c-102">Elija la sección adecuada para su sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c862c-102">Choose the appropriate section for your operating system.</span></span>

## <a name="linux-and-mac"></a><span data-ttu-id="c862c-103">Linux y Mac</span><span class="sxs-lookup"><span data-stu-id="c862c-103">Linux and Mac</span></span>
<span data-ttu-id="c862c-104">En Linux y macOS, el primer paso es instalar **PowerShell Core**.</span><span class="sxs-lookup"><span data-stu-id="c862c-104">On Linux and macOS, the first step is to install **PowerShell Core**.</span></span>

### <a name="linux"></a><span data-ttu-id="c862c-105">Linux</span><span class="sxs-lookup"><span data-stu-id="c862c-105">Linux</span></span>
<span data-ttu-id="c862c-106">Como se mencionó en la última unidad, la instalación de PowerShell para Linux implicará el uso de un administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c862c-106">As mentioned in the last unit, installing PowerShell for Linux will involve using a package manager.</span></span> <span data-ttu-id="c862c-107">Usaremos **Ubuntu 18.04** en nuestro ejemplo aquí, pero tenemos [instrucciones detalladas para otras versiones y distribuciones en nuestra documentación](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).</span><span class="sxs-lookup"><span data-stu-id="c862c-107">We will use **Ubuntu 18.04** for our example here, but we have [detailed instructions for other versions and distributions in our documentation](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).</span></span>

<span data-ttu-id="c862c-108">Instalará PowerShell Core en Ubuntu Linux mediante Advanced Packaging Tool (**apt**) y la línea de comandos de Bash.</span><span class="sxs-lookup"><span data-stu-id="c862c-108">You will install PowerShell Core on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span> 

1. <span data-ttu-id="c862c-109">Importe la clave de cifrado del repositorio de Ubuntu de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c862c-109">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="c862c-110">Esto permitirá que el administrador de paquetes compruebe que el paquete de PowerShell Core que se instala proviene de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c862c-110">This will allow the package manager to verify that the PowerShell Core package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. <span data-ttu-id="c862c-111">Registre el **repositorio de Microsoft Ubuntu** para que el administrador de paquetes pueda localizar el paquete de PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="c862c-111">Register the **Microsoft Ubuntu repository** so the package manager can locate the PowerShell Core package.</span></span>

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. <span data-ttu-id="c862c-112">Actualice la lista de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c862c-112">Update the list of packages.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="c862c-113">Instale PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="c862c-113">Install PowerShell Core.</span></span>

    ```bash
    sudo apt-get install -y powershell
    ```

1. <span data-ttu-id="c862c-114">Inicie PowerShell para verificar que está instalado correctamente.</span><span class="sxs-lookup"><span data-stu-id="c862c-114">Start PowerShell to verify that it installed successfully.</span></span>

    ```bash
    pwsh
    ```

### <a name="macos"></a><span data-ttu-id="c862c-115">macOS</span><span class="sxs-lookup"><span data-stu-id="c862c-115">macOS</span></span>
<span data-ttu-id="c862c-116">A continuación, instalará **PowerShell Core** en macOS con el administrador de paquetes de Homebrew.</span><span class="sxs-lookup"><span data-stu-id="c862c-116">Next, install **PowerShell Core** on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c862c-117">Si el comando **brew** no está disponible, es posible que deba instalar el administrador de paquetes de Homebrew.</span><span class="sxs-lookup"><span data-stu-id="c862c-117">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="c862c-118">Para más información, vea el [sitio web de Homebrew](https://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="c862c-118">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="c862c-119">Instale Homebrew-Cask para obtener más paquetes, incluido el paquete de PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="c862c-119">Install Homebrew-Cask to obtain more packages, including the PowerShell Core package:</span></span>

    ```bash
    brew tap caskroom/cask
    ```
1. <span data-ttu-id="c862c-120">Instale PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="c862c-120">Install PowerShell Core:</span></span>

    ```bash
    brew cask install powershell
    ```

1. <span data-ttu-id="c862c-121">Inicie PowerShell Core para verificar que está instalado correctamente:</span><span class="sxs-lookup"><span data-stu-id="c862c-121">Start PowerShell Core to verify that it installed successfully:</span></span>

    ```bash
    pwsh
    ```

## <a name="install-azure-powershell"></a><span data-ttu-id="c862c-122">Instalar Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="c862c-122">Install Azure PowerShell</span></span>
<span data-ttu-id="c862c-123">Después de instalar el producto **PowerShell** base, instale **Azure PowerShell** para agregar los comandos específicos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c862c-123">After installing the base **PowerShell** product, install **Azure PowerShell** to add the Azure-specific commands.</span></span>

### <a name="windows"></a><span data-ttu-id="c862c-124">Windows</span><span class="sxs-lookup"><span data-stu-id="c862c-124">Windows</span></span>
<span data-ttu-id="c862c-125">Instale Azure PowerShell en Windows mediante el comando `Install-Module` de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c862c-125">Install Azure PowerShell on Windows using the `Install-Module` PowerShell command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c862c-126">Necesita PowerShell versión 5.0 o posterior para instalar Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c862c-126">You must have PowerShell version 5.0 or higher to install Azure PowerShell.</span></span> <span data-ttu-id="c862c-127">Para comprobar la versión de PowerShell, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c862c-127">To check your version of PowerShell, use the following command:</span></span> 
>
> `$PSVersionTable.PSVersion` 
>
><span data-ttu-id="c862c-128">Si el número de versión es inferior a 5.0, siga las instrucciones para [actualizar la versión de Windows PowerShell existente](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="c862c-128">If the version number is lower than 5.0, follow the instructions for [upgrading existing Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).</span></span>

1. <span data-ttu-id="c862c-129">Abra el menú **Inicio** y escriba **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c862c-129">Open the **Start** menu and type **Windows PowerShell**.</span></span>
2. <span data-ttu-id="c862c-130">Haga clic con el botón derecho en el icono **Windows PowerShell** y seleccione **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="c862c-130">Right-click the **Windows PowerShell** icon and select **Run as administrator**.</span></span>
3. <span data-ttu-id="c862c-131">En el cuadro de diálogo **Control de cuentas de usuario**, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="c862c-131">In the **User Account Control** dialog, select **Yes**.</span></span>
4. <span data-ttu-id="c862c-132">Escriba el siguiente comando y presione Entrar:</span><span class="sxs-lookup"><span data-stu-id="c862c-132">Type the following command, and then press Enter:</span></span>

    ```powershell
    Install-Module -Name AzureRM
    ```
5. <span data-ttu-id="c862c-133">Si se le pregunta si confía en los módulos de PSGallery, responda **Sí** o **Sí a todo**.</span><span class="sxs-lookup"><span data-stu-id="c862c-133">If you are asked whether you trust modules from PSGallery, answer **Yes** or **Yes to All**.</span></span>

> [!NOTE]
> <span data-ttu-id="c862c-134">Si recibe un mensaje de error que indica que ya está instalada una versión del módulo de Azure Powershell, puede actualizar a la versión _más reciente_ emitiendo el comando:</span><span class="sxs-lookup"><span data-stu-id="c862c-134">If you get an error message indicating that a version of the Azure Powershell module is already installed, you can update to the _latest_ version by issuing the command:</span></span>
> 
> `Update-Module -Name AzureRM`
> 
> <span data-ttu-id="c862c-135">Al igual que con el comando `Install-Module`, responda **Sí** o **Sí a todo** cuando se le pregunte si confía en el módulo.</span><span class="sxs-lookup"><span data-stu-id="c862c-135">As with the `Install-Module` command, answer **Yes** or **Yes to All** when prompted to trust the module.</span></span>

### <a name="linux-or-macos"></a><span data-ttu-id="c862c-136">Linux o macOS</span><span class="sxs-lookup"><span data-stu-id="c862c-136">Linux or macOS</span></span>
<span data-ttu-id="c862c-137">Usamos el mismo proceso básico para instalar Azure PowerShell en Linux o macOS.</span><span class="sxs-lookup"><span data-stu-id="c862c-137">We use the same basic process to install the Azure PowerShell on either Linux or macOS.</span></span> <span data-ttu-id="c862c-138">El procedimiento es el mismo para ambos sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="c862c-138">The procedure is the same for both operating systems.</span></span> <span data-ttu-id="c862c-139">La diferencia radica en la obtención de una sesión de PowerShell Core con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="c862c-139">The difference is in getting an elevated PowerShell Core session.</span></span>

1. <span data-ttu-id="c862c-140">En un terminal, escriba el siguiente comando para iniciar PowerShell Core con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="c862c-140">In a terminal, type the following command to launch PowerShell Core with elevated privileges.</span></span>

    ```bash
    sudo pwsh
    ```

1. <span data-ttu-id="c862c-141">Ejecute el siguiente comando en el símbolo del sistema de PowerShell Core para instalar Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c862c-141">Run the following command at the PowerShell Core prompt to install Azure PowerShell.</span></span>

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. <span data-ttu-id="c862c-142">Si se le pregunta si confía en los módulos de **PSGallery**, responda **Sí** o **Sí a todo**.</span><span class="sxs-lookup"><span data-stu-id="c862c-142">If you are asked whether you trust modules from **PSGallery**, answer **Yes** or **Yes to All**.</span></span>

## <a name="summary"></a><span data-ttu-id="c862c-143">Resumen</span><span class="sxs-lookup"><span data-stu-id="c862c-143">Summary</span></span>
<span data-ttu-id="c862c-144">Ha configurado las máquinas locales para administrar recursos de Azure con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c862c-144">You setup your local machine(s) to administer Azure resources with Azure PowerShell.</span></span> <span data-ttu-id="c862c-145">Ahora puede usar Azure PowerShell localmente para especificar comandos o ejecutar scripts.</span><span class="sxs-lookup"><span data-stu-id="c862c-145">You can now use Azure PowerShell locally to enter commands or execute scripts.</span></span> <span data-ttu-id="c862c-146">Azure PowerShell reenviará los comandos a los centros de datos de Azure, en donde se ejecutarán dentro de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c862c-146">Azure PowerShell will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>