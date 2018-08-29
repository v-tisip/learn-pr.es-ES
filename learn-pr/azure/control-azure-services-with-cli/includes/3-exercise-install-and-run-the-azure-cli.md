
<span data-ttu-id="1b445-101">En este ejercicio, instalará la CLI de Azure en el equipo local y luego ejecutará un comando simple para comprobar la instalación.</span><span class="sxs-lookup"><span data-stu-id="1b445-101">In this exercise, you will install the Azure CLI on your local machine, and then run a simple command to verify your installation.</span></span> 

## <a name="installing-the-azure-cli"></a><span data-ttu-id="1b445-102">Instalación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1b445-102">Installing the Azure CLI</span></span>
<span data-ttu-id="1b445-103">El método que se usa para instalar la CLI de Azure depende del sistema operativo del equipo.</span><span class="sxs-lookup"><span data-stu-id="1b445-103">The method you use for installing the Azure CLI depends on the operating system of your computer.</span></span> <span data-ttu-id="1b445-104">Elija los pasos correspondientes a su sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="1b445-104">Please choose the steps for your operating system.</span></span>

### <a name="linux"></a><span data-ttu-id="1b445-105">Linux</span><span class="sxs-lookup"><span data-stu-id="1b445-105">Linux</span></span>
<span data-ttu-id="1b445-106">Aquí utilizará Advanced Packaging Tool (**apt**) y la línea de comandos de Bash para instalar la CLI de Azure en Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="1b445-106">Here you will install the Azure CLI on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span>

> [!NOTE]
> <span data-ttu-id="1b445-107">Los comandos mostrados a continuación son para Ubuntu versión 18.04.</span><span class="sxs-lookup"><span data-stu-id="1b445-107">The commands listed below are for Ubuntu version 18.04.</span></span> <span data-ttu-id="1b445-108">Si usa otra versión de Ubuntu, debe agregar un repositorio distinto.</span><span class="sxs-lookup"><span data-stu-id="1b445-108">If you are using a different version of Ubuntu, you must add a different repository.</span></span> <span data-ttu-id="1b445-109">Para más información, vea [Instalación de la CLI de Azure 2.0 con apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).</span><span class="sxs-lookup"><span data-stu-id="1b445-109">For details see [Install the Azure CLI 2.0 with apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).</span></span>

1. <span data-ttu-id="1b445-110">Modifique la lista de orígenes para que el repositorio de Microsoft quede registrado y el administrador de paquetes pueda localizar el paquete de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b445-110">Modify your sources list so that the Microsoft repository is registered, and the package manager can locate the Azure CLI package.</span></span>

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```
1. <span data-ttu-id="1b445-111">Importe la clave de cifrado del repositorio de Ubuntu de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1b445-111">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="1b445-112">Esto permitirá que el administrador de paquetes compruebe que el paquete de la CLI Azure que se instala proviene de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1b445-112">This will allow the package manager to verify that the Azure CLI package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. <span data-ttu-id="1b445-113">Instale la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b445-113">Install the Azure CLI.</span></span>

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

### <a name="macos"></a><span data-ttu-id="1b445-114">macOS</span><span class="sxs-lookup"><span data-stu-id="1b445-114">macOS</span></span>
<span data-ttu-id="1b445-115">Aquí instalará la CLI de Azure en macOS con el administrador de paquetes de Homebrew.</span><span class="sxs-lookup"><span data-stu-id="1b445-115">Here you will install the Azure CLI on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b445-116">Si el comando **brew** no está disponible, es posible que deba instalar el administrador de paquetes de Homebrew.</span><span class="sxs-lookup"><span data-stu-id="1b445-116">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="1b445-117">Para más información, vea el [sitio web de Homebrew](https://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="1b445-117">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="1b445-118">Actualice el repositorio de brew para asegurarse de que obtiene el paquete más reciente de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b445-118">Update your brew repository to make sure you get the latest Azure CLI package.</span></span>

    ```bash
    brew update
    ```
1. <span data-ttu-id="1b445-119">Instale la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b445-119">Install the Azure CLI.</span></span>

    ```bash
    brew install azure-cli
    ```

### <a name="windows"></a><span data-ttu-id="1b445-120">Windows</span><span class="sxs-lookup"><span data-stu-id="1b445-120">Windows</span></span>
<span data-ttu-id="1b445-121">Aquí instalará la CLI de Azure en Windows con el instalador MSI.</span><span class="sxs-lookup"><span data-stu-id="1b445-121">Here you will install the Azure CLI on Windows using the MSI installer.</span></span>

1. <span data-ttu-id="1b445-122">Vaya a [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows) y, en el cuadro de diálogo de seguridad del explorador, haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="1b445-122">Go to [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows), and in the browser security dialog box, click **Run**.</span></span>
1. <span data-ttu-id="1b445-123">En el instalador, acepte los términos de licencia y haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="1b445-123">In the installer, accept the license terms, and then click **Install**.</span></span>
1. <span data-ttu-id="1b445-124">En el cuadro de diálogo **Control de cuentas de usuario**, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="1b445-124">In the **User Account Control** dialog, select **Yes**.</span></span>

## <a name="running-the-azure-cli"></a><span data-ttu-id="1b445-125">Ejecución de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1b445-125">Running the Azure CLI</span></span>
<span data-ttu-id="1b445-126">Puede ejecutar la CLI de Azure abriendo un shell de bash (Linux y macOS) o desde el símbolo del sistema o PowerShell (Windows).</span><span class="sxs-lookup"><span data-stu-id="1b445-126">You run the Azure CLI by opening a bash shell (Linux and macOS), or from the command prompt or PowerShell (Windows).</span></span>

1. <span data-ttu-id="1b445-127">Inicie la CLI de Azure y compruebe la instalación ejecutando la comprobación de versión.</span><span class="sxs-lookup"><span data-stu-id="1b445-127">Start the Azure CLI and verify your installation by running the version check.</span></span>

    ```bash
    az --version
    ```

> [!NOTE]
> <span data-ttu-id="1b445-128">En Windows, la ejecución de la CLI de Azure en PowerShell tiene algunas ventajas con respecto a la ejecución de la CLI de Azure desde el símbolo del sistema; por ejemplo, PowerShell ofrece más características de finalización de pestañas que las disponibles desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="1b445-128">In Windows, running the Azure CLI from PowerShell has some advantages over running the Azure CLI from the command prompt; for example, PowerShell provides additional tab completion features over those available from the command prompt.</span></span> 

## <a name="summary"></a><span data-ttu-id="1b445-129">Resumen</span><span class="sxs-lookup"><span data-stu-id="1b445-129">Summary</span></span>
<span data-ttu-id="1b445-130">Configure las máquinas locales para administrar recursos de Azure con la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b445-130">You set up your local machines to administer Azure resources with the Azure CLI.</span></span> <span data-ttu-id="1b445-131">Ahora puede usar la CLI de Azure localmente para especificar comandos o ejecutar scripts.</span><span class="sxs-lookup"><span data-stu-id="1b445-131">You can now use the Azure CLI locally to enter commands or execute scripts.</span></span> <span data-ttu-id="1b445-132">La CLI de Azure reenviará los comandos a los centros de datos de Azure, en donde se ejecutarán dentro de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b445-132">The Azure CLI will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>
