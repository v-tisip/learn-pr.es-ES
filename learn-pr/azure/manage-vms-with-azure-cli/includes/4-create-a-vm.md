<span data-ttu-id="24b07-101">La CLI de Azure incluye el comando `vm` para trabajar con máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="24b07-101">The Azure CLI includes the `vm` command to work with virtual machines in Azure.</span></span> <span data-ttu-id="24b07-102">Podemos proporcionar varios subcomandos para realizar tareas específicas.</span><span class="sxs-lookup"><span data-stu-id="24b07-102">We can supply several subcommands to do specific tasks.</span></span> <span data-ttu-id="24b07-103">Los más comunes incluyen:</span><span class="sxs-lookup"><span data-stu-id="24b07-103">The most common include:</span></span>

| <span data-ttu-id="24b07-104">Subcomando</span><span class="sxs-lookup"><span data-stu-id="24b07-104">Sub-command</span></span> | <span data-ttu-id="24b07-105">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="24b07-105">Description</span></span> |
|-------------|-------------|
| `create`    | <span data-ttu-id="24b07-106">Creación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="24b07-106">Create a new virtual machine</span></span> |
| `deallocate` | <span data-ttu-id="24b07-107">Desasignación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="24b07-107">Deallocate a virtual machine</span></span> |
| `delete` | <span data-ttu-id="24b07-108">Eliminación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="24b07-108">Delete a virtual machine</span></span> |
| `list` | <span data-ttu-id="24b07-109">Lista de las máquinas virtuales creadas en su suscripción</span><span class="sxs-lookup"><span data-stu-id="24b07-109">List the created virtual machines in your subscription</span></span> |
| `open-port` | <span data-ttu-id="24b07-110">Apertura de un puerto de red específico para el tráfico entrante</span><span class="sxs-lookup"><span data-stu-id="24b07-110">Open a specific network port for inbound traffic</span></span> |
| `restart` | <span data-ttu-id="24b07-111">Reinicio de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="24b07-111">Restart a virtual machine</span></span> |
| `show` | <span data-ttu-id="24b07-112">Obtención de los detalles de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="24b07-112">Get the details for a virtual machine</span></span> |
| `start` | <span data-ttu-id="24b07-113">Inicio de una máquina virtual detenida</span><span class="sxs-lookup"><span data-stu-id="24b07-113">Start a stopped virtual machine</span></span> |
| `stop` | <span data-ttu-id="24b07-114">Detención de una máquina virtual en ejecución</span><span class="sxs-lookup"><span data-stu-id="24b07-114">Stop a running virtual machine</span></span> |
| `update` | <span data-ttu-id="24b07-115">Actualización de una propiedad de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="24b07-115">Update a property of a virtual machine</span></span> |

> [!NOTE]
> <span data-ttu-id="24b07-116">Para una lista completa de comandos, puede comprobar la [documentación de referencia de la CLI de Azure](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="24b07-116">For a complete list of commands, you can check the [Azure CLI reference documentation](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).</span></span>

<span data-ttu-id="24b07-117">Comencemos con el primero: `az vm create`.</span><span class="sxs-lookup"><span data-stu-id="24b07-117">Let's start with the first one: `az vm create`.</span></span> <span data-ttu-id="24b07-118">Este comando se utiliza para crear una máquina virtual en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="24b07-118">This command is used to create a virtual machine in a resource group.</span></span> <span data-ttu-id="24b07-119">Hay varios parámetros que se pueden pasar para configurar todos los aspectos de la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="24b07-119">There are several parameters you can pass to configure all the aspects of the new VM.</span></span> <span data-ttu-id="24b07-120">Los tres parámetros que se deben proporcionar son:</span><span class="sxs-lookup"><span data-stu-id="24b07-120">The three parameters that must be supplied are:</span></span>

| <span data-ttu-id="24b07-121">Parámetro</span><span class="sxs-lookup"><span data-stu-id="24b07-121">Parameter</span></span> | <span data-ttu-id="24b07-122">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="24b07-122">Description</span></span> |
|-----------|-------------|
| `resource-group` | <span data-ttu-id="24b07-123">El grupo de recursos que poseerá la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="24b07-123">The resource group that will own the virtual machine</span></span> |
| `name` | <span data-ttu-id="24b07-124">El nombre de la máquina virtual; tiene que ser único dentro del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="24b07-124">The name of the virtual machine - must be unique within the resource group</span></span> |
| `image` | <span data-ttu-id="24b07-125">La imagen de sistema operativo que se va a usar para crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="24b07-125">The operating system image to use to create the VM</span></span> |

<span data-ttu-id="24b07-126">Además, resulta útil agregar la marca `--verbose` para ver el progreso mientras se crea la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="24b07-126">In addition, it's helpful to add the `--verbose` flag to see progress while the VM is being created.</span></span> 

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="24b07-127">Creación de una máquina virtual con Linux</span><span class="sxs-lookup"><span data-stu-id="24b07-127">Create a Linux virtual machine</span></span>

<span data-ttu-id="24b07-128">Vamos a crear una máquina virtual con Linux.</span><span class="sxs-lookup"><span data-stu-id="24b07-128">Let's create a new Linux virtual machine.</span></span> <span data-ttu-id="24b07-129">Ejecute el comando siguiente en Azure Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="24b07-129">Execute the following command in Azure Cloud Shell:</span></span>

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --verbose 
```

<span data-ttu-id="24b07-130">Este comando creará una nueva máquina virtual con Linux **Debian** con el nombre `SampleVM`.</span><span class="sxs-lookup"><span data-stu-id="24b07-130">This command will create a new **Debian** Linux virtual machine with the name `SampleVM`.</span></span> <span data-ttu-id="24b07-131">Tenga en cuenta que la herramienta CLI de Azure se bloquea mientras se está creando la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="24b07-131">Notice that the Azure CLI tool is blocked while the VM is being created.</span></span> <span data-ttu-id="24b07-132">Si prefiere no esperar, puede usar la opción `--no-wait` para indicar a la herramienta CLI de Azure que vuelva de inmediato, por ejemplo, si está ejecutando el comando en un script.</span><span class="sxs-lookup"><span data-stu-id="24b07-132">If you would prefer not to wait, you can use the `--no-wait` option to tell the Azure CLI tool to return immediately, for example if you're executing the command in a script.</span></span> <span data-ttu-id="24b07-133">Más adelante, en el script, utilice el comando `azure vm wait --name [vm-name]` para esperar a que la máquina virtual termine de crearse.</span><span class="sxs-lookup"><span data-stu-id="24b07-133">Later in the script, use the `azure vm wait --name [vm-name]` command to wait for the VM to finish being created.</span></span>

<span data-ttu-id="24b07-134">Si observa las respuestas detalladas, también verá que el nombre `SampleVM` se usa para denominar varias dependencias de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="24b07-134">If you look at the verbose responses, you will also see that the `SampleVM` name is used to name various dependencies for the VM.</span></span>

```
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

<span data-ttu-id="24b07-135">Puede invalidar estos nombres de recurso generados automáticamente mediante los parámetros opcionales a `vm create`, como `--vnet-name` y `--public-ip-address-dns-name`.</span><span class="sxs-lookup"><span data-stu-id="24b07-135">You can override these auto-generated resource names using optional parameters to `vm create`, such as `--vnet-name` and `--public-ip-address-dns-name`.</span></span>

<span data-ttu-id="24b07-136">Tenga en cuenta que especificamos el nombre de cuenta de administrador a través de la marca `admin-username` para que sea "aldis".</span><span class="sxs-lookup"><span data-stu-id="24b07-136">Notice that we are specifying the admin account name through the `admin-username` flag to be "aldis".</span></span> <span data-ttu-id="24b07-137">Si omite esto, el comando `vm create` usará el _nombre de usuario actual_.</span><span class="sxs-lookup"><span data-stu-id="24b07-137">If you omit this, the `vm create` command will use your _current user name_.</span></span> <span data-ttu-id="24b07-138">Puesto que las reglas de los nombres de cuenta son diferentes para cada sistema operativo, es más seguro especificar un nombre concreto.</span><span class="sxs-lookup"><span data-stu-id="24b07-138">Since the rules for account names are different for each OS, it's safer to specify a specific name.</span></span> <span data-ttu-id="24b07-139">No se permiten nombres comunes como "raíz" y "admin" para la mayoría de las imágenes.</span><span class="sxs-lookup"><span data-stu-id="24b07-139">Common names such as "root" and "admin" are not allowed for most images.</span></span>

<span data-ttu-id="24b07-140">También usamos la marca `generate-ssh-keys`.</span><span class="sxs-lookup"><span data-stu-id="24b07-140">We are also using the `generate-ssh-keys` flag.</span></span> <span data-ttu-id="24b07-141">Este parámetro se usa para las distribuciones de Linux y crea un par de claves de seguridad, por lo que podemos usar la herramienta `ssh` para acceder a la máquina virtual de forma remota.</span><span class="sxs-lookup"><span data-stu-id="24b07-141">This parameter is used for Linux distributions and creates a pair of security keys so we can use the `ssh` tool to access the virtual machine remotely.</span></span> <span data-ttu-id="24b07-142">Los dos archivos se colocan en la carpeta `.ssh` en el equipo y en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="24b07-142">The two files are placed into the `.ssh` folder on your machine and in the VM.</span></span> <span data-ttu-id="24b07-143">Si ya tiene una clave SSH llamada `id_rsa` en la carpeta de destino, se utilizará en lugar de generar una nueva clave.</span><span class="sxs-lookup"><span data-stu-id="24b07-143">If you already have an SSH key named `id_rsa` in the target folder, then it will be used rather than having a new key generated.</span></span>

<span data-ttu-id="24b07-144">Una vez que haya terminado de crear la máquina virtual, obtendrá una respuesta JSON que incluye el estado actual de la máquina virtual y sus direcciones IP públicas y privadas asignadas por Azure:</span><span class="sxs-lookup"><span data-stu-id="24b07-144">Once it finishes creating the VM, you will get a JSON response which includes the current state of the virtual machine and its public and private IP addresses assigned by Azure:</span></span>

```json
{
  "fqdns": "",
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Compute/virtualMachines/SampleVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-1A-D9-74",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "168.61.54.62",
  "resourceGroup": "ExerciseResources",
  "zones": ""
}
```

