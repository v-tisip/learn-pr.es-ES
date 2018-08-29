<span data-ttu-id="85492-101">En este ejercicio, vamos a crear una función de Azure que muestra el nombre y el tamaño de un blob cuando se crea o actualiza.</span><span class="sxs-lookup"><span data-stu-id="85492-101">In this exercise, we're going to create an Azure function that displays the name and size of a blob when it's created or updated.</span></span> 

> [!NOTE]
> <span data-ttu-id="85492-102">Para completar este ejercicio, asegúrese de que ha iniciado sesión en [Azure Portal](https://portal.azure.com/) con una cuenta válida.</span><span class="sxs-lookup"><span data-stu-id="85492-102">To complete this exercise, make sure you're signed in to the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-a-blob-trigger"></a><span data-ttu-id="85492-103">Creación de un desencadenador de blobs</span><span class="sxs-lookup"><span data-stu-id="85492-103">Create a blob trigger</span></span>

<span data-ttu-id="85492-104">Nuevamente, vamos a seguir usando nuestra aplicación de Azure Functions existente y agregarle un desencadenador de blobs.</span><span class="sxs-lookup"><span data-stu-id="85492-104">Again, let's continue using our existing Azure Functions application and add a blob trigger.</span></span>

1. <span data-ttu-id="85492-105">Vaya a **Functions** y seleccione el icono de signo más (+).</span><span class="sxs-lookup"><span data-stu-id="85492-105">Point to **Functions** and select the plus (+) icon.</span></span>

    ![Selección de Functions y el signo más](../media/4-hover-function.png)

1. <span data-ttu-id="85492-107">Seleccione **Desencadenador de blobs**.</span><span class="sxs-lookup"><span data-stu-id="85492-107">Select **Blob trigger**.</span></span>

1. <span data-ttu-id="85492-108">Seleccione **C#** como lenguaje.</span><span class="sxs-lookup"><span data-stu-id="85492-108">Select **C#** as the language.</span></span> 

1. <span data-ttu-id="85492-109">Deje el **Nombre** establecido en el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="85492-109">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="85492-110">Deje la **Ruta** establecida en el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="85492-110">Leave the **Path** set to the default value.</span></span>

1. <span data-ttu-id="85492-111">Seleccione una cuenta de Azure Storage existente o seleccione **Crear** si desea que Azure cree una nueva cuenta en su lugar.</span><span class="sxs-lookup"><span data-stu-id="85492-111">Select an existing Azure Storage account, or select **Create** if you want Azure to create a new account for you.</span></span>

## <a name="download-storage-explorer"></a><span data-ttu-id="85492-112">Descarga del Explorador de Storage</span><span class="sxs-lookup"><span data-stu-id="85492-112">Download Storage explorer</span></span>

<span data-ttu-id="85492-113">Ahora que hemos creado un desencadenador de blobs, vamos a descargar el Explorador de Storage, que nos permitirá crear fácilmente un blob.</span><span class="sxs-lookup"><span data-stu-id="85492-113">Now that we've created a blob trigger, let's download Storage explorer, which will allow us to easily create a blob.</span></span>

- <span data-ttu-id="85492-114">Descargue el [Explorador de Storage](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="85492-114">Download [Storage explorer](http://storageexplorer.com).</span></span>

## <a name="connect-to-your-azure-storage-account"></a><span data-ttu-id="85492-115">Conexión a la cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="85492-115">Connect to your Azure Storage account</span></span>

<span data-ttu-id="85492-116">Ya tenemos descargado el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="85492-116">We now have Storage explorer downloaded.</span></span> <span data-ttu-id="85492-117">Vamos a iniciar sesión con las credenciales proporcionadas.</span><span class="sxs-lookup"><span data-stu-id="85492-117">Let's sign in using the credentials that were supplied.</span></span>

1. <span data-ttu-id="85492-118">En el Explorador de Storage, seleccione el icono de signo más (+) de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="85492-118">In Storage explorer, select the plus (+) icon on the left.</span></span>

1. <span data-ttu-id="85492-119">Seleccione **Usar un nombre y clave de la cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="85492-119">Select **Use a storage account name and key**.</span></span>

1. <span data-ttu-id="85492-120">Seleccione **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="85492-120">Select **Next**.</span></span>

1. <span data-ttu-id="85492-121">En Azure, en el desencadenador de blobs, seleccione **Integración**.</span><span class="sxs-lookup"><span data-stu-id="85492-121">In Azure, under your blob trigger, select **Integrate**.</span></span>

1. <span data-ttu-id="85492-122">Seleccione **Documentación** para expandir la vista.</span><span class="sxs-lookup"><span data-stu-id="85492-122">Select **Documentation** to expand the view.</span></span>

1. <span data-ttu-id="85492-123">Copie el **Nombre de cuenta** y la **Clave de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="85492-123">Copy the **Account Name** and **Account Key**.</span></span>

1. <span data-ttu-id="85492-124">De nuevo en el Explorador de Storage, pegue el **Nombre de cuenta** y la **Clave de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="85492-124">Back in Storage explorer, paste in the **Account Name** and **Account Key**.</span></span>

1. <span data-ttu-id="85492-125">Especifique un **Nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="85492-125">Enter a **Display name**.</span></span> <span data-ttu-id="85492-126">Este valor es el nombre de la conexión en el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="85492-126">This value is the name of the connection in Storage explorer.</span></span>

1. <span data-ttu-id="85492-127">Seleccione **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="85492-127">Select **Next**.</span></span>

1. <span data-ttu-id="85492-128">Seleccione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="85492-128">Select **Connect**.</span></span> 

## <a name="create-a-blob-container"></a><span data-ttu-id="85492-129">Creación de un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="85492-129">Create a blob container</span></span>

<span data-ttu-id="85492-130">No estamos conectados a nuestra cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="85492-130">We aren't connected to our Azure Storage account.</span></span> <span data-ttu-id="85492-131">Recuerde que el desencadenador de blobs está supervisando solo la ubicación que se describe en el campo **Ruta**.</span><span class="sxs-lookup"><span data-stu-id="85492-131">Remember that our blob trigger is monitoring only the location described in the **Path** field.</span></span> <span data-ttu-id="85492-132">De forma predeterminada, la ruta de acceso debe ser:</span><span class="sxs-lookup"><span data-stu-id="85492-132">By default, our path should be:</span></span>

> <span data-ttu-id="85492-133">samples-workitems/{name}</span><span class="sxs-lookup"><span data-stu-id="85492-133">samples-workitems/{name}</span></span>

<span data-ttu-id="85492-134">Es necesario crear un contenedor denominado **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="85492-134">We need to create a container called **samples-workitems**.</span></span>

1. <span data-ttu-id="85492-135">En el Explorador de Storage, expanda la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="85492-135">In Storage explorer, expand your storage account.</span></span> <span data-ttu-id="85492-136">El nombre debe ser el **Nombre para mostrar** que haya proporcionado durante el proceso de conexión.</span><span class="sxs-lookup"><span data-stu-id="85492-136">The name should be the **Display name** that you provided during the connection process.</span></span>

1. <span data-ttu-id="85492-137">Haga clic con el botón derecho en **Contenedores de blobs** y seleccione **Crear contenedor de blobs**.</span><span class="sxs-lookup"><span data-stu-id="85492-137">Right-click **Blob Containers** and select **Create blob container**.</span></span>

1. <span data-ttu-id="85492-138">Escriba **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="85492-138">Enter **samples-workitems**.</span></span>

## <a name="turn-on-your-blob-trigger"></a><span data-ttu-id="85492-139">Activación del desencadenador de blobs</span><span class="sxs-lookup"><span data-stu-id="85492-139">Turn on your blob trigger</span></span>

<span data-ttu-id="85492-140">Ahora que hemos creado nuestro contenedor para supervisar, vamos a ejecutar la función para que podamos ver la salida cuando se crea un blob.</span><span class="sxs-lookup"><span data-stu-id="85492-140">Now that we've created our container to monitor, let's run our function so we can see output when a blob is created.</span></span>

1. <span data-ttu-id="85492-141">Seleccione el desencadenador de blobs para abrir la pantalla del código.</span><span class="sxs-lookup"><span data-stu-id="85492-141">Select your blob trigger to open the code screen.</span></span>

1. <span data-ttu-id="85492-142">Seleccione **Run** (Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="85492-142">Select **Run**.</span></span>

## <a name="create-a-blob"></a><span data-ttu-id="85492-143">Creación de un blob</span><span class="sxs-lookup"><span data-stu-id="85492-143">Create a blob</span></span>

<span data-ttu-id="85492-144">El desencadenador de blobs ya está listo para escuchar la actividad.</span><span class="sxs-lookup"><span data-stu-id="85492-144">Our blob trigger is now up and listening for activity.</span></span> <span data-ttu-id="85492-145">Vamos a crear un blob para ver si se recibe un mensaje de registro.</span><span class="sxs-lookup"><span data-stu-id="85492-145">Let's create a blob to see if we get a log message.</span></span>

1. <span data-ttu-id="85492-146">En el Explorador de Storage, seleccione el contenedor **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="85492-146">In Storage explorer, select the **samples-workitems** container.</span></span>

1. <span data-ttu-id="85492-147">Seleccione **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="85492-147">Select **Upload**.</span></span> 

1. <span data-ttu-id="85492-148">Seleccione **Cargar archivos**.</span><span class="sxs-lookup"><span data-stu-id="85492-148">Select **Upload Files**.</span></span>

1. <span data-ttu-id="85492-149">Seleccione cualquier archivo de su equipo.</span><span class="sxs-lookup"><span data-stu-id="85492-149">Select any file from your computer.</span></span>

1. <span data-ttu-id="85492-150">Seleccione **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="85492-150">Select **Upload**.</span></span>

1. <span data-ttu-id="85492-151">Vuelva a Azure.</span><span class="sxs-lookup"><span data-stu-id="85492-151">Go back to Azure.</span></span> <span data-ttu-id="85492-152">Busque en los registros un mensaje que indique qué archivo se cargó.</span><span class="sxs-lookup"><span data-stu-id="85492-152">Check your logs for a message that displays what file was uploaded.</span></span>

## <a name="clean-up"></a><span data-ttu-id="85492-153">Limpieza</span><span class="sxs-lookup"><span data-stu-id="85492-153">Clean up</span></span>

<span data-ttu-id="85492-154">Para asegurarse de que no se le cobra por esta función, seleccione **Pausar** encima de la ventana de registro.</span><span class="sxs-lookup"><span data-stu-id="85492-154">To ensure that you aren't charged for this function, select **Pause** above the log window.</span></span>

![Pausar](../media/4-pause-timer.png)


