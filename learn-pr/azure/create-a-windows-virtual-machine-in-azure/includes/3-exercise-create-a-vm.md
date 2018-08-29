<span data-ttu-id="5db93-101">En este ejercicio, creará una máquina virtual Windows en Azure.</span><span class="sxs-lookup"><span data-stu-id="5db93-101">In this exercise, you'll create a Windows virtual machine in Azure.</span></span>

## <a name="motivation"></a><span data-ttu-id="5db93-102">Motivación</span><span class="sxs-lookup"><span data-stu-id="5db93-102">Motivation</span></span>

<span data-ttu-id="5db93-103">Consideremos un escenario alternativo para este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="5db93-103">Let's consider an alternate scenario for this exercise.</span></span> <span data-ttu-id="5db93-104">En este caso, su organización es una escuela que usa máquinas virtuales Windows para poner en marcha los entornos de prueba en los que los estudiantes instalan aplicaciones web, configuran dominios y exploran características y servicios de Windows sin que afecte a los equipos de la escuela.</span><span class="sxs-lookup"><span data-stu-id="5db93-104">Here, your organization is a school that uses Windows virtual machines to spin up test environments on which students install web apps, configure domains, and explore Windows services and features without affecting the school's computers.</span></span> <span data-ttu-id="5db93-105">Los profesores se conectan a estas máquinas virtuales mediante RDP y comprueban el progreso de los estudiantes.</span><span class="sxs-lookup"><span data-stu-id="5db93-105">Teachers connect to these VMs by using RDP and check on student progress.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="5db93-106">Creación de una máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="5db93-106">Create a Windows VM</span></span>

<span data-ttu-id="5db93-107">Para crear una máquina virtual Windows, complete los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="5db93-107">To create a Windows VM, complete the following steps:</span></span>

1. <span data-ttu-id="5db93-108">Inicie sesión en Azure a través de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5db93-108">Log onto Azure through the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="5db93-109">Haga clic en **Crear un recurso** en la esquina superior izquierda de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5db93-109">Click **Create a resource** in the upper left corner of the Azure portal.</span></span>

1. <span data-ttu-id="5db93-110">En la **barra de búsqueda**, escriba **Windows Server 2016 Datacenter** y después haga clic en el vínculo con el mismo título.</span><span class="sxs-lookup"><span data-stu-id="5db93-110">In the **search bar**, enter  **Windows Server 2016 Datacenter**  and then click on the link with the same title.</span></span>

### <a name="configure-the-vm-settings"></a><span data-ttu-id="5db93-111">Configuración de las opciones de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5db93-111">Configure the VM settings</span></span>

1. <span data-ttu-id="5db93-112">En **Aspectos básicos**, en el campo **Nombre**, escriba un nombre para la máquina virtual, por ejemplo, "StudentVM".</span><span class="sxs-lookup"><span data-stu-id="5db93-112">Under **Basics**, in the **Name** field, enter a name for your VM, such as "StudentVM."</span></span>

1. <span data-ttu-id="5db93-113">En el campo **Tipo de disco de máquina virtual**, haga clic en el menú desplegable para ver las opciones.</span><span class="sxs-lookup"><span data-stu-id="5db93-113">In the **VM Disk Type** field, click the drop-down menu to see the options.</span></span> <span data-ttu-id="5db93-114">Asegúrese de que está seleccionada la opción **SSD**.</span><span class="sxs-lookup"><span data-stu-id="5db93-114">Ensure that **SSD** is selected.</span></span>

1. <span data-ttu-id="5db93-115">En el campo **Nombre de usuario**, escriba un nombre de usuario adecuado para usarlo al iniciar sesión en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5db93-115">In the **Username** field, enter a suitable user name to use to sign in to the VM.</span></span>

1. <span data-ttu-id="5db93-116">En el campo **Contraseña**, escriba una contraseña que tenga al menos 12 caracteres de longitud.</span><span class="sxs-lookup"><span data-stu-id="5db93-116">In the **Password** field, enter a password that's at least 12 characters long.</span></span> <span data-ttu-id="5db93-117">También debe tener caracteres en mayúsculas y minúsculas, números y caracteres especiales.</span><span class="sxs-lookup"><span data-stu-id="5db93-117">It must also have upper and lowercase characters, numbers, and special characters.</span></span>

1. <span data-ttu-id="5db93-118">En **Grupo de recursos**, haga clic en **Crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="5db93-118">Under **Resource group**, click **Create new**.</span></span> <span data-ttu-id="5db93-119">Asigne al grupo de recursos un nombre, por ejemplo, "myTestRG".</span><span class="sxs-lookup"><span data-stu-id="5db93-119">Give the resource group a name, such as "myTestRG."</span></span>

1. <span data-ttu-id="5db93-120">Seleccione una ubicación adecuada para que se cree la máquina virtual y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5db93-120">Select a suitable location for the VM to be created, and then click **OK**.</span></span>

### <a name="select-the-vm-image-size-and-options"></a><span data-ttu-id="5db93-121">Selección de las opciones y el tamaño de la imagen de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5db93-121">Select the VM image size and options</span></span>

1. <span data-ttu-id="5db93-122">En la página **Elegir un tamaño**, haga clic en la imagen **B1s** y, después, en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="5db93-122">In the **Choose a size** page, click the **B1s** image, and then click **Select**.</span></span>

   > [!Note] 
   > <span data-ttu-id="5db93-123">La imagen B1 tiene solo 1 GB de RAM y dará lugar a errores de memoria la primera vez que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="5db93-123">The B1 image has only 1 GB of RAM and will result in memory errors when you first sign in.</span></span> <span data-ttu-id="5db93-124">En cambio, puede cambiar el tamaño de la imagen más adelante como parte de un laboratorio posterior.</span><span class="sxs-lookup"><span data-stu-id="5db93-124">However, you can resize the image later as part of a later lab.</span></span>

1. <span data-ttu-id="5db93-125">En la página **Configuración**, en **Seleccionar puertos de entrada públicos**, haga clic en **No hay puertos de entrada públicos**.</span><span class="sxs-lookup"><span data-stu-id="5db93-125">In the **Settings** page, under **Select Public Inbound Ports**, select **No public inbound ports**.</span></span> <span data-ttu-id="5db93-126">Configuraremos el acceso RDP más tarde.</span><span class="sxs-lookup"><span data-stu-id="5db93-126">We'll configure RDP access later.</span></span>

### <a name="finish-configuring-the-vm-and-create-the-image"></a><span data-ttu-id="5db93-127">Finalización de la configuración de la máquina virtual y creación de la imagen</span><span class="sxs-lookup"><span data-stu-id="5db93-127">Finish configuring the VM and create the image</span></span>

1. <span data-ttu-id="5db93-128">Desplácese hacia abajo y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5db93-128">Scroll to the bottom and click **OK**.</span></span>

1. <span data-ttu-id="5db93-129">En **Crear**, compruebe las opciones que ha configurado.</span><span class="sxs-lookup"><span data-stu-id="5db93-129">Under **Create**, check the settings that you configured.</span></span> <span data-ttu-id="5db93-130">En la parte inferior, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5db93-130">At the bottom, click **Create**.</span></span> <span data-ttu-id="5db93-131">El panel de Azure mostrará la máquina virtual que se va a implementar.</span><span class="sxs-lookup"><span data-stu-id="5db93-131">The Azure dashboard will show the VM that's being deployed.</span></span> <span data-ttu-id="5db93-132">Este proceso podría tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="5db93-132">This may take several minutes.</span></span>

## <a name="summary"></a><span data-ttu-id="5db93-133">Resumen</span><span class="sxs-lookup"><span data-stu-id="5db93-133">Summary</span></span>

<span data-ttu-id="5db93-134">Acaba de crear una máquina virtual de Windows Server que es adecuada para los requisitos de los estudiantes y a la que se puede acceder desde la red de la escuela.</span><span class="sxs-lookup"><span data-stu-id="5db93-134">You've now created a Windows Server virtual machine that's suitable for student requirements and accessible from the school network.</span></span> <span data-ttu-id="5db93-135">En la siguiente unidad, examinará cómo conectarse a esa máquina virtual mediante RDP y cómo administrarla.</span><span class="sxs-lookup"><span data-stu-id="5db93-135">In the next unit, you will look at how you connect to and manage that VM by using RDP.</span></span>
