En este ejercicio creará una nueva cuenta de almacenamiento en su suscripción de Azure. A continuación, usará Azure Cloud Shell para crear una nueva cola, agregarle un mensaje y, a continuación, leer ese mensaje y quitarlo de la cola.

Estas son las mismas acciones realizadas por los componentes de una aplicación distribuida. Por ejemplo, una aplicación móvil puede agregar un mensaje a una cola, donde espera que un servicio web la recupere y procese.

## <a name="create-a-storage-account"></a>Creación de una cuenta de almacenamiento

Puesto que las colas de almacenamiento forman parte de las cuentas de almacenamiento de Azure de uso general, debe empezar creando una cuenta de almacenamiento:

1. En un explorador, vaya a [Azure Portal](http://portal.azure.com) e inicie sesión con sus credenciales normales.
1. En la esquina superior izquierda, haga clic en **Todos los servicios**.
1. Desplácese hacia abajo hasta la sección **Almacenamiento** y haga clic en **Cuentas de almacenamiento**.
1. En la esquina superior izquierda de la hoja **Cuentas de almacenamiento**, haga clic en **Agregar**.

    ![Creación de una cuenta de almacenamiento](../images/5-create-a-storage-account-1.png)

1. En el cuadro de texto **Nombre**, escriba un nombre único para la cuenta de almacenamiento.
1. En **Modelo de implementación**, asegúrese de que **Resource Manager** está seleccionado.
1. En la lista desplegable **Tipo de cuenta**seleccione **Almacenamiento (uso general v2)**.
1. En la lista desplegable **Ubicación**, seleccione una región cercana.
1. En la lista desplegable **Replicación**, seleccione **Almacenamiento con redundancia local (LRS)**.
1. En **Rendimiento**, seleccione **Estándar**.
1. En **Nivel de acceso**, seleccione **Esporádico**.
1. En **Se requiere transferencia segura**, seleccione **Deshabilitado**.
1. En **Suscripción**, seleccione la suscripción.

    ![Creación de una cuenta de almacenamiento](../images/5-create-a-storage-account-2.png)

1. En **Grupo de recursos** seleccione **Crear nuevo** y en el cuadro de texto, escriba **MusicSharingResourceGroup**.
1. En **Redes virtuales**, seleccione **Deshabilitadas** y haga clic en **Crear**.

    ![Creación de una cuenta de almacenamiento](../images/5-create-a-storage-account-3.png)

Azure crea la nueva cuenta de almacenamiento y el nuevo grupo de recursos.

## <a name="create-a-queue"></a>Creación de una cola

Ahora que se creó la cuenta de almacenamiento, puede agregarle una cola nueva. Debe crear la cola mediante con los comandos de PowerShell:

1. En la esquina superior derecha del portal, haga clic en el vínculo **Cloud Shell**.

    ![Inicio de Cloud Shell](../images/5-create-a-storage-queue-1.png)

1. En la pantalla de **bienvenida a Azure Cloud Shell**, haga clic en **PowerShell (Linux)**.
1. Si aparece la pantalla **You have no storage mounted** (No tiene montado ningún almacenamiento), haga clic en **Crear almacenamiento**.
1. Cuando aparezca el símbolo del sistema `PS Azure`, para obtener la cuenta de almacenamiento, escriba este comando sustituyendo `<storageaccountname>` por el nombre único de la cuenta de almacenamiento y presione ENTRAR:

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

1. Para obtener el contexto de la cuenta de almacenamiento, escriba este comando y presione ENTRAR:

    ```powershell
    $context = $storageaccount.Context
    ```

1. Para crear una cola nueva, escriba este comando y presione ENTRAR:

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a>Incorporación de un mensaje a una cola

Ahora que creó una cola en la cuenta de almacenamiento, puede agregarle un mensaje.

1. Para crear un mensaje, escriba este comando y presione ENTRAR:

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

1. Para agregar el mensaje nuevo a la cola nueva, escriba el siguiente comando y presione ENTRAR:

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

1. En Azure Portal, en el panel de navegación de la izquierda, haga clic en **Todos los recursos**.
1. En la lista de recursos, haga clic en la cuenta de almacenamiento que creó anteriormente.
1. En la hoja de la cuenta de almacenamiento, haga clic en **Explorador de Storage (versión preliminar)**.
1. En el Explorador de Storage, en **COLAS**, haga clic en **musicsharingmessages**. El Explorador de Storage muestra el mensaje que acaba de agregar.

## <a name="retrieve-and-remove-the-message"></a>Recuperación y eliminación del mensaje

Un componente de destino para un mensaje en una cola de almacenamiento debe recuperar el mensaje al frente de la cola, procesarlo y, a continuación, eliminarlo de la cola para que otros componentes no lo recuperen:

1. En Azure Cloud Shell, para poner el mensaje al frente de la cola, escriba el siguiente comando y presione ENTRAR:

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

1. Para mostrar el mensaje, escriba el siguiente comando y presione ENTRAR:

    ```powershell
    $retrievedMessage.AsString
    ```

1. Para mostrar todas las propiedades del mensaje, escriba el siguiente comando y presione ENTRAR:

    ```powershell
    $retrievedMessage
    ```

1. Para quitar el mensaje de la cola, escriba el siguiente comando y presione ENTRAR:

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

1. En Azure Portal, para actualizar la presentación de la cola, en la hoja Cuenta de almacenamiento, haga clic en **Introducción** y luego, en **Explorador de Storage**.
1. En **COLAS**, haga clic en **musicsharingmessages**. El Explorador de Storage muestra que la cola está vacía porque se quitó el único mensaje.

## <a name="cleanup"></a>Limpieza

Para quitar todos los recursos creados durante este ejercicio, escriba este comando en Azure Cloud Shell. 
```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```


## <a name="summary"></a>Resumen

Aquí creó una cuenta de almacenamiento en su suscripción de Azure y creó una nueva cola en ella. También usó PowerShell para imitar las acciones de los componentes de aplicaciones distribuidas mediante la incorporación de un mensaje a la cola y posteriormente su recuperación y eliminación.

Las colas de la cuenta de Azure Management son una buena solución cuando quiere pasar mensajes entre los componentes de una aplicación distribuida. No elija colas de almacenamiento cuando quiera publicar eventos.