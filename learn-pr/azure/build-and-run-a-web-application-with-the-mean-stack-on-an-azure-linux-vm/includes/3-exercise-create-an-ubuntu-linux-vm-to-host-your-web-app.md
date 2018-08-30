<span data-ttu-id="b7bf7-101">La pila MEAN de componentes requiere un servidor.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-101">The MEAN stack of components requires a server.</span></span> <span data-ttu-id="b7bf7-102">Podría ser una máquina Linux o una máquina virtual en ejecución en su propia sala de servidores, o bien se puede configurar en una máquina virtual basada en la nube.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-102">It could be a Linux machine or virtual machine running in your own server room, or it can be configured on a cloud-based virtual machine.</span></span> <span data-ttu-id="b7bf7-103">En este módulo configurará la pila para que se ejecute en una máquina virtual Ubuntu Linux que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-103">In this module, we will be setting up the stack to run on an Ubuntu Linux virtual machine running on Azure.</span></span>

<span data-ttu-id="b7bf7-104">En este ejercicio, creará una máquina virtual Ubuntu Linux hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-104">In this exercise, you will be creating a new Ubuntu Linux virtual machine hosted on Azure.</span></span> <span data-ttu-id="b7bf7-105">También puede instalar los componentes de la pila MEAN en una máquina virtual existente o en un equipo host físico.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-105">You could also install your MEAN stack components on an existing virtual machine or physical host machine.</span></span> <span data-ttu-id="b7bf7-106">Si crea una nueva con este ejercicio, se pueden unir todos los componentes en un grupo de recursos de Azure para facilitar la administración y la limpieza después de completar los ejercicios.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-106">By creating a new one with this exercise, you can tie together all the components into an Azure resource group for easier management and clean-up after you complete the exercises.</span></span>

<span data-ttu-id="b7bf7-107">Usaremos la línea de comandos de Cloud Shell integrada en Azure Portal para crear la máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-107">We will use the Cloud Shell command-line integrated into the Azure portal to create the Linux VM.</span></span>

## <a name="provision-an-ubuntu-linux-vm"></a><span data-ttu-id="b7bf7-108">Aprovisionamiento de una máquina virtual Ubuntu Linux</span><span class="sxs-lookup"><span data-stu-id="b7bf7-108">Provision an Ubuntu Linux VM</span></span>

1. <span data-ttu-id="b7bf7-109">Vaya a [Azure Portal](https://portal.azure.com?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="b7bf7-109">Go to the [Azure Portal](https://portal.azure.com?azure-portal=true).</span></span>
1. <span data-ttu-id="b7bf7-110">Abra Cloud Shell desde el icono `>_` en la barra de herramientas de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-110">Open the Cloud Shell from the `>_` icon in the Azure portal toolbar.</span></span>
1. <span data-ttu-id="b7bf7-111">En Cloud Shell, ejecute el comando para crear un grupo de recursos de Azure, que se incluirá en nuestra máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-111">Within the Cloud Shell, execute the command to create an Azure resource group, which will include our VM.</span></span> <span data-ttu-id="b7bf7-112">Sustituya el nombre del grupo de recursos propio por `<resource-group-name>` y la ubicación de Azure deseada por `<resource-group-location>` (`westus`, por ejemplo).</span><span class="sxs-lookup"><span data-stu-id="b7bf7-112">Substitute your own resource group name for `<resource-group-name>` and your desired Azure location for `<resource-group-location>` (`westus`, for example).</span></span>

    ```bash
    az group create --name <resource-group-name> --location <resource-group-location>
    ```

    <span data-ttu-id="b7bf7-113">Recuerde el nombre del grupo de recursos porque lo usará en otros comandos.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-113">Remember your resource group name as we will use it in other commands.</span></span>

1. <span data-ttu-id="b7bf7-114">En Cloud Shell, ejecute el siguiente comando para crear una nueva máquina virtual Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-114">In the Cloud Shell, run the following command to create a new Ubuntu Linux VM.</span></span> <span data-ttu-id="b7bf7-115">Sustituya el nombre del grupo de recursos propio por `<resource-group-name>` y el nombre de usuario administrador y la contraseña que prefiera por `<vm-admin-username>` y `<vm-admin-password>`.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-115">Substitute your own resource group name for `<resource-group-name>` and your preferred admin username and password for `<vm-admin-username>` and `<vm-admin-password>`.</span></span>

    ```bash
    az vm create \
        --resource-group <resource-group-name> \
        --name MeanDemo \
        --image UbuntuLTS \
        --admin-username <vm-admin-username> \
        --admin-password <vm-admin-password> \
        --generate-ssh-keys
    ```

    <span data-ttu-id="b7bf7-116">Anote el nombre de usuario administrador y la contraseña para que pueda conectarse a esta máquina virtual más adelante.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-116">Take note of your admin username and password to allow you to connect to this VM later.</span></span>

    <span data-ttu-id="b7bf7-117">Este comando tarda unos 2 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-117">This command takes about 2 minutes to complete.</span></span> <span data-ttu-id="b7bf7-118">Cuando el comando finalice, la salida resultante será similar a esta.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-118">When the command finishes, the resulting output will look similar to this.</span></span>

    ```json
    {
        "fqdns": "",
        "id": "...",
        "location": "<location you chose for the resource group>",
        "macAddress": "00-0D-3A-3A-54-EC",
        "powerState": "VM running",
        "privateIpAddress": "10.0.0.4",
        "publicIpAddress": "<the public IP address of the newly created machine>",
        "resourceGroup": "<name you chose for thr resource group>",
        "zones": ""
    }
    ```

    <span data-ttu-id="b7bf7-119">También deseará guardar la dirección IP pública de la máquina virtual recién creada con el fin de conectarse a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-119">You will also want to save the public IP address of the newly created VM in order to connect to the VM.</span></span>

1. <span data-ttu-id="b7bf7-120">Intente conectarse a la máquina virtual nueva.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-120">Try connecting to your new VM.</span></span>

    <span data-ttu-id="b7bf7-121">Abra un símbolo del sistema o una ventana de terminal y ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-121">Open a command prompt/terminal window and run the following command.</span></span> <span data-ttu-id="b7bf7-122">Sustituya el nombre de usuario administrador y la dirección IP pública de la máquina virtual mencionados por los marcadores de posición `<vm-admin-username>` y `<vm-public-ip>`.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-122">Substitute your admin username and your VM's public IP address from above for the `<vm-admin-username>` and `<vm-public-ip>` placeholders.</span></span>

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

    <span data-ttu-id="b7bf7-123">La primera vez que se conecte a la máquina, se le preguntará si confía en la máquina remota.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-123">The first time you connect to the machine, you'll be asked if you trust the remote machine.</span></span> <span data-ttu-id="b7bf7-124">Si responde `yes`, la huella digital de la clave ECDSA de la máquina se guardará localmente para que las conexiones subsiguientes sean de confianza.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-124">By answering `yes`, the machine's ECDSA key fingerprint will be saved locally so subsequent connections will be trusted.</span></span>

    <span data-ttu-id="b7bf7-125">Si todo se ve bien, escriba `exit` para cerrar la sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-125">If everything looks fine, type `exit` to close the SSH session.</span></span>

1. <span data-ttu-id="b7bf7-126">Abra el puerto 80 para permitir el tráfico HTTP entrante a la aplicación web nueva que creará.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-126">Open port 80 to allow incoming HTTP traffic to your new web application you will create.</span></span>

    <span data-ttu-id="b7bf7-127">Vuelva a Cloud Shell en Azure Portal y emita el siguiente comando, usando el nombre original del grupo de recursos para `<resource-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-127">Go back to the Cloud Shell on the Azure portal and issue the following command, using your original resource group name for `<resource-group-name>`.</span></span>

    ``` bash
    az vm open-port --port 80 --resource-group <resource-group-name> --name MeanDemo
    ```

    <span data-ttu-id="b7bf7-128">Con esto se abrirá el puerto HTTP de la máquina virtual que se denominó "MeanDemo" cuando se creó.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-128">This will open up the HTTP port on your VM that was named "MeanDemo" when it was created.</span></span>

## <a name="summary"></a><span data-ttu-id="b7bf7-129">Resumen</span><span class="sxs-lookup"><span data-stu-id="b7bf7-129">Summary</span></span>

<span data-ttu-id="b7bf7-130">Con la nueva máquina virtual Ubuntu Linux lista para comenzar, ahora podemos conectarnos a ella para empezar la instalación de los distintos componentes de la pila MEAN.</span><span class="sxs-lookup"><span data-stu-id="b7bf7-130">With your new Ubuntu Linux VM ready to go, we can now connect to it to start installing the various components of the MEAN stack.</span></span>
