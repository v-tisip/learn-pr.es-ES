<span data-ttu-id="763e0-101">En este ejercicio creará una nueva cuenta de almacenamiento en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="763e0-101">In this exercise, you will create a new Storage Account in your Azure subscription.</span></span> <span data-ttu-id="763e0-102">A continuación, usará Azure Cloud Shell para crear una nueva cola, agregarle un mensaje y, a continuación, leer ese mensaje y quitarlo de la cola.</span><span class="sxs-lookup"><span data-stu-id="763e0-102">You will then use the Azure Cloud Shell to create a new queue, add a message to it, and then read that message and remove it from the queue.</span></span>

<span data-ttu-id="763e0-103">Estas son las mismas acciones realizadas por los componentes de una aplicación distribuida.</span><span class="sxs-lookup"><span data-stu-id="763e0-103">These are the same actions taken by components in a distributed application.</span></span> <span data-ttu-id="763e0-104">Por ejemplo, una aplicación móvil puede agregar un mensaje a una cola, donde espera que un servicio web la recupere y procese.</span><span class="sxs-lookup"><span data-stu-id="763e0-104">For example, a mobile app may add a message to a queue, where it waits for a web service to retrieve it and process it.</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="763e0-105">Creación de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="763e0-105">Create a Storage Account</span></span>

<span data-ttu-id="763e0-106">Puesto que las colas de almacenamiento forman parte de las cuentas de almacenamiento de Azure de uso general,</span><span class="sxs-lookup"><span data-stu-id="763e0-106">Since Storage queues are part of Azure general purpose Storage accounts.</span></span> <span data-ttu-id="763e0-107">debe empezar creando una cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="763e0-107">You must start by creating a Storage account:</span></span>

1. <span data-ttu-id="763e0-108">En un explorador, vaya a [Azure Portal](http://portal.azure.com) e inicie sesión con sus credenciales normales.</span><span class="sxs-lookup"><span data-stu-id="763e0-108">In a browser, navigate to the [Azure Portal](http://portal.azure.com) and sign in with your normal credentials.</span></span>
1. <span data-ttu-id="763e0-109">En la esquina superior izquierda, haga clic en **Todos los servicios**.</span><span class="sxs-lookup"><span data-stu-id="763e0-109">In the top left, click **All services**.</span></span>
1. <span data-ttu-id="763e0-110">Desplácese hacia abajo hasta la sección **Almacenamiento** y haga clic en **Cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="763e0-110">Scroll down to the **Storage** section, and then click **Storage accounts**.</span></span>
1. <span data-ttu-id="763e0-111">En la esquina superior izquierda de la hoja **Cuentas de almacenamiento**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="763e0-111">At the top left of the **Storage accounts** blade, click **Add**.</span></span>

    ![Creación de una cuenta de almacenamiento](../images/5-create-a-storage-account-1.png)

1. <span data-ttu-id="763e0-113">En el cuadro de texto **Nombre**, escriba un nombre único para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="763e0-113">In the **Name** text box, type a unique name for the storage account.</span></span>
1. <span data-ttu-id="763e0-114">En **Modelo de implementación**, asegúrese de que **Resource Manager** está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="763e0-114">Under **Deployment model**, ensure that **Resource Manager** is selected.</span></span>
1. <span data-ttu-id="763e0-115">En la lista desplegable **Tipo de cuenta**seleccione **Almacenamiento (uso general v2)**.</span><span class="sxs-lookup"><span data-stu-id="763e0-115">In the **Account kind** drop-down list, select **Storage (general purpose v2)**.</span></span>
1. <span data-ttu-id="763e0-116">En la lista desplegable **Ubicación**, seleccione una región cercana.</span><span class="sxs-lookup"><span data-stu-id="763e0-116">In the **Location** drop-down list, select a region near you.</span></span>
1. <span data-ttu-id="763e0-117">En la lista desplegable **Replicación**, seleccione **Almacenamiento con redundancia local (LRS)**.</span><span class="sxs-lookup"><span data-stu-id="763e0-117">In the **Replication** drop-down list, select **Locally-redundant storage (LRS)**.</span></span>
1. <span data-ttu-id="763e0-118">En **Rendimiento**, seleccione **Estándar**.</span><span class="sxs-lookup"><span data-stu-id="763e0-118">Under **Performance**, select **Standard**.</span></span>
1. <span data-ttu-id="763e0-119">En **Nivel de acceso**, seleccione **Esporádico**.</span><span class="sxs-lookup"><span data-stu-id="763e0-119">Under **Access tier**, select **Cool**.</span></span>
1. <span data-ttu-id="763e0-120">En **Se requiere transferencia segura**, seleccione **Deshabilitado**.</span><span class="sxs-lookup"><span data-stu-id="763e0-120">Under **Secure transfer required** select, **Disabled**.</span></span>
1. <span data-ttu-id="763e0-121">En **Suscripción**, seleccione la suscripción.</span><span class="sxs-lookup"><span data-stu-id="763e0-121">Under **Subscription**, select your subscription.</span></span>

    ![Creación de una cuenta de almacenamiento](../images/5-create-a-storage-account-2.png)

1. <span data-ttu-id="763e0-123">En **Grupo de recursos** seleccione **Crear nuevo** y en el cuadro de texto, escriba **MusicSharingResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="763e0-123">Under **Resource group** select **Create new**, and then in the textbox type **MusicSharingResourceGroup**.</span></span>
1. <span data-ttu-id="763e0-124">En **Redes virtuales**, seleccione **Deshabilitadas** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="763e0-124">Under **Virtual networks** select **Disabled** and then click **Create**.</span></span>

    ![Creación de una cuenta de almacenamiento](../images/5-create-a-storage-account-3.png)

<span data-ttu-id="763e0-126">Azure crea la nueva cuenta de almacenamiento y el nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="763e0-126">Azure creates the new storage account and the new resource group.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="763e0-127">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="763e0-127">Create a Queue</span></span>

<span data-ttu-id="763e0-128">Ahora que se creó la cuenta de almacenamiento, puede agregarle una cola nueva.</span><span class="sxs-lookup"><span data-stu-id="763e0-128">Now that the Storage Account has been created, you can add a new queue to it.</span></span> <span data-ttu-id="763e0-129">Debe crear la cola mediante con los comandos de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="763e0-129">You must create the queue by using PowerShell commands:</span></span>

1. <span data-ttu-id="763e0-130">En la esquina superior derecha del portal, haga clic en el vínculo **Cloud Shell**.</span><span class="sxs-lookup"><span data-stu-id="763e0-130">In the top right of the portal, click the **Cloud Shell** link.</span></span>

    ![Inicio de Cloud Shell](../images/5-create-a-storage-queue-1.png)

1. <span data-ttu-id="763e0-132">En la pantalla de **bienvenida a Azure Cloud Shell**, haga clic en **PowerShell (Linux)**.</span><span class="sxs-lookup"><span data-stu-id="763e0-132">In the **Welcome to Azure Cloud Shell** screen, click **PowerShell (Linux)**.</span></span>
1. <span data-ttu-id="763e0-133">Si aparece la pantalla **You have no storage mounted** (No tiene montado ningún almacenamiento), haga clic en **Crear almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="763e0-133">If the **You have no storage mounted** screen appears, click **Create storage**.</span></span>
1. <span data-ttu-id="763e0-134">Cuando aparezca el símbolo del sistema `PS Azure`, para obtener la cuenta de almacenamiento, escriba este comando sustituyendo `<storageaccountname>` por el nombre único de la cuenta de almacenamiento y presione ENTRAR:</span><span class="sxs-lookup"><span data-stu-id="763e0-134">When the `PS Azure` prompt appears, to obtain the storage account, type the following command, substituting `<storageaccountname>` with the unique name of your storage account, and then press Enter:</span></span>

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

1. <span data-ttu-id="763e0-135">Para obtener el contexto de la cuenta de almacenamiento, escriba este comando y presione ENTRAR:</span><span class="sxs-lookup"><span data-stu-id="763e0-135">To obtain the context of the storage account, type the following command and then press Enter:</span></span>

    ```powershell
    $context = $storageaccount.Context
    ```

1. <span data-ttu-id="763e0-136">Para crear una cola nueva, escriba este comando y presione ENTRAR:</span><span class="sxs-lookup"><span data-stu-id="763e0-136">To create a new queue, type the following command and then press Enter:</span></span>

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a><span data-ttu-id="763e0-137">Incorporación de un mensaje a una cola</span><span class="sxs-lookup"><span data-stu-id="763e0-137">Add a Message to the Queue</span></span>

<span data-ttu-id="763e0-138">Ahora que creó una cola en la cuenta de almacenamiento, puede agregarle un mensaje.</span><span class="sxs-lookup"><span data-stu-id="763e0-138">Now that you have created a queue in the storage account, you can add a message to it.</span></span>

1. <span data-ttu-id="763e0-139">Para crear un mensaje, escriba este comando y presione ENTRAR:</span><span class="sxs-lookup"><span data-stu-id="763e0-139">To create a new message, type the following command and then press Enter:</span></span>

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

1. <span data-ttu-id="763e0-140">Para agregar el mensaje nuevo a la cola nueva, escriba el siguiente comando y presione ENTRAR:</span><span class="sxs-lookup"><span data-stu-id="763e0-140">To add the new message to the new queue, type the following command and then press Enter:</span></span>

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

1. <span data-ttu-id="763e0-141">En Azure Portal, en el panel de navegación de la izquierda, haga clic en **Todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="763e0-141">In the Azure Portal, in the navigation on the left, click **All resources**.</span></span>
1. <span data-ttu-id="763e0-142">En la lista de recursos, haga clic en la cuenta de almacenamiento que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="763e0-142">In the list of resources, click the storage account you created earlier.</span></span>
1. <span data-ttu-id="763e0-143">En la hoja de la cuenta de almacenamiento, haga clic en **Explorador de Storage (versión preliminar)**.</span><span class="sxs-lookup"><span data-stu-id="763e0-143">In the storage account blade, click **Storage Explorer (Preview)**.</span></span>
1. <span data-ttu-id="763e0-144">En el Explorador de Storage, en **COLAS**, haga clic en **musicsharingmessages**.</span><span class="sxs-lookup"><span data-stu-id="763e0-144">In the Storage Explorer, under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="763e0-145">El Explorador de Storage muestra el mensaje que acaba de agregar.</span><span class="sxs-lookup"><span data-stu-id="763e0-145">The Storage Explorer displays the message you just added.</span></span>

## <a name="retrieve-and-remove-the-message"></a><span data-ttu-id="763e0-146">Recuperación y eliminación del mensaje</span><span class="sxs-lookup"><span data-stu-id="763e0-146">Retrieve and Remove the Message</span></span>

<span data-ttu-id="763e0-147">Un componente de destino para un mensaje en una cola de almacenamiento debe recuperar el mensaje al frente de la cola, procesarlo y, a continuación, eliminarlo de la cola para que otros componentes no lo recuperen:</span><span class="sxs-lookup"><span data-stu-id="763e0-147">A destination component for a message in a Storage queue, must retrieve the message at the front of the queue, process it, and then delete it from the queue so that other components do not retrieve it:</span></span>

1. <span data-ttu-id="763e0-148">En Azure Cloud Shell, para poner el mensaje al frente de la cola, escriba el siguiente comando y presione ENTRAR:</span><span class="sxs-lookup"><span data-stu-id="763e0-148">In the Azure Cloud Shell, to get the message at the front of the queue, type the following command and then press Enter:</span></span>

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

1. <span data-ttu-id="763e0-149">Para mostrar el mensaje, escriba el siguiente comando y presione ENTRAR:</span><span class="sxs-lookup"><span data-stu-id="763e0-149">To display the message, type the following command and then press Enter:</span></span>

    ```powershell
    $retrievedMessage.AsString
    ```

1. <span data-ttu-id="763e0-150">Para mostrar todas las propiedades del mensaje, escriba el siguiente comando y presione ENTRAR:</span><span class="sxs-lookup"><span data-stu-id="763e0-150">To display all the properties of the message, type the following command and then press Enter:</span></span>

    ```powershell
    $retrievedMessage
    ```

1. <span data-ttu-id="763e0-151">Para quitar el mensaje de la cola, escriba el siguiente comando y presione ENTRAR:</span><span class="sxs-lookup"><span data-stu-id="763e0-151">To remove the message from the queue, type the following command and then press Enter:</span></span>

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

1. <span data-ttu-id="763e0-152">En Azure Portal, para actualizar la presentación de la cola, en la hoja Cuenta de almacenamiento, haga clic en **Introducción** y luego, en **Explorador de Storage**.</span><span class="sxs-lookup"><span data-stu-id="763e0-152">In the Azure Portal, to refresh the queue display, in the Storage Account blade, click **Overview** and then click **Storage Explorer**.</span></span>
1. <span data-ttu-id="763e0-153">En **COLAS**, haga clic en **musicsharingmessages**.</span><span class="sxs-lookup"><span data-stu-id="763e0-153">Under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="763e0-154">El Explorador de Storage muestra que la cola está vacía porque se quitó el único mensaje.</span><span class="sxs-lookup"><span data-stu-id="763e0-154">The Storage Explorer shows that the queue is empty because you removed the only message.</span></span>

## <a name="cleanup"></a><span data-ttu-id="763e0-155">Limpieza</span><span class="sxs-lookup"><span data-stu-id="763e0-155">Cleanup</span></span>

<span data-ttu-id="763e0-156">Para quitar todos los recursos creados durante este ejercicio, escriba este comando en Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="763e0-156">To remove all resources created during this exercise enter the following command in the Azure Cloud Shell</span></span> 
```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```


## <a name="summary"></a><span data-ttu-id="763e0-157">Resumen</span><span class="sxs-lookup"><span data-stu-id="763e0-157">Summary</span></span>

<span data-ttu-id="763e0-158">Aquí creó una cuenta de almacenamiento en su suscripción de Azure y creó una nueva cola en ella.</span><span class="sxs-lookup"><span data-stu-id="763e0-158">Here, you created a Storage Account in your Azure subscription and created a new queue in it.</span></span> <span data-ttu-id="763e0-159">También usó PowerShell para imitar las acciones de los componentes de aplicaciones distribuidas mediante la incorporación de un mensaje a la cola y posteriormente su recuperación y eliminación.</span><span class="sxs-lookup"><span data-stu-id="763e0-159">You also used PowerShell to simulate the actions of distributed application components by adding a message to the queue and then retrieving and removing it.</span></span>

<span data-ttu-id="763e0-160">Las colas de la cuenta de Azure Management son una buena solución cuando quiere pasar mensajes entre los componentes de una aplicación distribuida.</span><span class="sxs-lookup"><span data-stu-id="763e0-160">Azure Storage Account queues are a good solution when you want to pass messages between the components of a distributed application.</span></span> <span data-ttu-id="763e0-161">No elija colas de almacenamiento cuando quiera publicar eventos.</span><span class="sxs-lookup"><span data-stu-id="763e0-161">Do not choose Storage queues when you want to publish events.</span></span>