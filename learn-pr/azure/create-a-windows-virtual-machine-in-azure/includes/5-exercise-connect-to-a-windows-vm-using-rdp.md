<span data-ttu-id="83310-101">En este ejercicio, usará el cliente RDP para conectarse a la máquina virtual Windows que ha creado en la unidad anterior.</span><span class="sxs-lookup"><span data-stu-id="83310-101">In this exercise, you'll use the RDP client to connect to the Windows VM that you created in the previous unit.</span></span> <span data-ttu-id="83310-102">Puede conectarse si descarga y ejecuta un archivo RDP desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="83310-102">You can connect by downloading and running an RDP file from the Azure portal.</span></span> <span data-ttu-id="83310-103">Este archivo RDP tendrá:</span><span class="sxs-lookup"><span data-stu-id="83310-103">This RDP file will have:</span></span>

* <span data-ttu-id="83310-104">La dirección IP pública de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="83310-104">The public IP address of the VM.</span></span>
* <span data-ttu-id="83310-105">El número de puerto.</span><span class="sxs-lookup"><span data-stu-id="83310-105">The port number.</span></span>

## <a name="motivation"></a><span data-ttu-id="83310-106">Motivación</span><span class="sxs-lookup"><span data-stu-id="83310-106">Motivation</span></span>

<span data-ttu-id="83310-107">De acuerdo con el escenario de nuestro ejercicio, ahora es un estudiante y quiere obtener información sobre cómo agregar roles y características a un equipo con Windows Server.</span><span class="sxs-lookup"><span data-stu-id="83310-107">From our exercise scenario, you're now a student and you want to learn about adding roles and features to a Windows Server computer.</span></span> <span data-ttu-id="83310-108">En cambio, el administrador de red no quiere que lo haga en un equipo físico en la red y los equipos de la escuela no están nada preparados para ejecutar Windows Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="83310-108">However, your network administrator doesn't want you to do this on a physical computer on the network, and the school's computers are too poorly specified to run Windows Hyper-V.</span></span> <span data-ttu-id="83310-109">Azure proporciona la solución perfecta.</span><span class="sxs-lookup"><span data-stu-id="83310-109">Azure provides the perfect solution.</span></span>

## <a name="configure-network-and-public-ip-address-settings"></a><span data-ttu-id="83310-110">Configuración de las opciones de la dirección IP pública y la red</span><span class="sxs-lookup"><span data-stu-id="83310-110">Configure network and public IP address settings</span></span>

1. <span data-ttu-id="83310-111">En Azure Portal, asegúrese de que está abierta la hoja de la máquina virtual que ha creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="83310-111">In the Azure portal, ensure the blade for the virtual machine that you created earlier is open.</span></span> <span data-ttu-id="83310-112">Puede encontrar la hoja en **Todos los recursos** si tiene que abrirla.</span><span class="sxs-lookup"><span data-stu-id="83310-112">You can find the blade under **All Resources** if you need to open it.</span></span>

1. <span data-ttu-id="83310-113">Vaya a la sección **Redes**.</span><span class="sxs-lookup"><span data-stu-id="83310-113">Go to the **Networking** section.</span></span> <span data-ttu-id="83310-114">En la parte superior de esta sección hay vínculos a la subred virtual y la dirección IP dinámica que se crearon junto con nuestra máquina virtual, ya que usamos los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="83310-114">The top of this section has links to the virtual subnet and dynamic IP address that were created along with our VM since we used the defaults.</span></span> <span data-ttu-id="83310-115">Podemos seguir estos vínculos si queremos cambiar esos recursos (por ejemplo, cambiar a una dirección IP estática).</span><span class="sxs-lookup"><span data-stu-id="83310-115">We would follow these links if we wanted to change those resources (for example, changing to a static IP address).</span></span>

1. <span data-ttu-id="83310-116">Haga clic en **Agregar regla de puerto de entrada**.</span><span class="sxs-lookup"><span data-stu-id="83310-116">Click **Add inbound port rule**.</span></span>

1. <span data-ttu-id="83310-117">En la parte superior del cuadro de diálogo **Agregar regla de seguridad de entrada**, haga clic en **Básica**.</span><span class="sxs-lookup"><span data-stu-id="83310-117">At the top of the **Add inbound security rule** dialog box, click **basic**.</span></span>

1. <span data-ttu-id="83310-118">En **Servicio**, seleccione **RDP** y después haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="83310-118">Under **Service**, select **RDP**, and then click **Add**.</span></span>

## <a name="connect-to-the-vm-by-using-rdp"></a><span data-ttu-id="83310-119">Conexión a la máquina virtual mediante RDP</span><span class="sxs-lookup"><span data-stu-id="83310-119">Connect to the VM by using RDP</span></span>

<span data-ttu-id="83310-120">Para descargar el archivo RDP y conectarse a la máquina virtual, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="83310-120">To download the RDP file and connect to the VM, carry out the following steps.</span></span>

### <a name="download-the-rdp-file"></a><span data-ttu-id="83310-121">Descarga del archivo RDP</span><span class="sxs-lookup"><span data-stu-id="83310-121">Download the RDP file</span></span>

1. <span data-ttu-id="83310-122">En la sección **Introducción** de la hoja de la máquina virtual, haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="83310-122">In the **Overview** section of the virtual machine's blade, click **Connect**.</span></span>

1. <span data-ttu-id="83310-123">En la hoja **Conectarse a una máquina virtual**, observe las opciones de configuración **Dirección IP** y **Número de puerto**; después, haga clic en **Descargar archivo RDP**.</span><span class="sxs-lookup"><span data-stu-id="83310-123">In the **Connect to virtual machine** blade, note the **IP address** and **Port number** settings, then click **Download RDP File**.</span></span>

1. <span data-ttu-id="83310-124">En el explorador, haga clic en **Abrir** o en **Ejecutar** para abrir el archivo RDP.</span><span class="sxs-lookup"><span data-stu-id="83310-124">In your browser, click **Open** or **Run** to open the RDP file.</span></span>

### <a name="connect-to-the-windows-vm"></a><span data-ttu-id="83310-125">Conexión a la máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="83310-125">Connect to the Windows VM</span></span>

1. <span data-ttu-id="83310-126">En el cuadro de diálogo **Conexión a Escritorio remoto**, observe la advertencia de seguridad y la dirección IP del equipo remoto, y haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="83310-126">In the **Remote Desktop Connection** dialog box, note the security warning and the remote computer IP address, then click **Connect**.</span></span>

1. <span data-ttu-id="83310-127">En el cuadro de diálogo **Seguridad de Windows**, escriba el nombre de usuario y la contraseña que ha usado en los pasos 6 y 7.</span><span class="sxs-lookup"><span data-stu-id="83310-127">In the **Windows Security** dialog box, enter your user name and password that you used in steps 6 and 7.</span></span>

1. <span data-ttu-id="83310-128">En el segundo cuadro de diálogo **Conexión a Escritorio remoto**, observe los errores de certificado y, después, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="83310-128">In the second **Remote Desktop Connection** dialog box, note the certificate errors, then click **Yes**.</span></span>

   > [!Note]
   > <span data-ttu-id="83310-129">El escritorio de la máquina virtual tarda un poco en aparecer.</span><span class="sxs-lookup"><span data-stu-id="83310-129">The virtual machine desktop takes a while to appear.</span></span> <span data-ttu-id="83310-130">Este efecto se debe a que la imagen de B1 se ha subespecificado.</span><span class="sxs-lookup"><span data-stu-id="83310-130">This effect is because the B1 image is under-specified.</span></span> <span data-ttu-id="83310-131">Puede que reciba un mensaje sobre la asignación de memoria baja.</span><span class="sxs-lookup"><span data-stu-id="83310-131">You may receive a message about low memory allocation.</span></span>

1. <span data-ttu-id="83310-132">En el cuadro de diálogo **Redes**, haga clic en **No**.</span><span class="sxs-lookup"><span data-stu-id="83310-132">In the **Networks** dialog, click **No**.</span></span>

### <a name="resize-the-vm-in-the-azure-portal"></a><span data-ttu-id="83310-133">Cambio del tamaño de la máquina virtual en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="83310-133">Resize the VM in the Azure portal</span></span>

1. <span data-ttu-id="83310-134">Vuelva a Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="83310-134">Switch back to the Azure portal.</span></span> <span data-ttu-id="83310-135">En la página de propiedades de la máquina virtual, en **Propiedades**, haga clic en **Tamaño**.</span><span class="sxs-lookup"><span data-stu-id="83310-135">On the virtual machine properties page, under **Settings**, click **Size**.</span></span>

1. <span data-ttu-id="83310-136">Haga clic en **D2s_v3** (2 vCPU, 8 GB de RAM) y después en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="83310-136">Click **D2s_v3** (2 vCPUs, 8-GB RAM), and then click **Select**.</span></span> <span data-ttu-id="83310-137">Se mostrará un mensaje de cambio de tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="83310-137">A resizing virtual machine message will display.</span></span> <span data-ttu-id="83310-138">También se cerrará la máquina virtual de la ventana de RDP.</span><span class="sxs-lookup"><span data-stu-id="83310-138">The VM in the RDP window will also close down.</span></span>

1. <span data-ttu-id="83310-139">Vuelva a Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="83310-139">Switch back to the Azure portal.</span></span> <span data-ttu-id="83310-140">En el panel izquierdo, haga clic en **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="83310-140">In the left pane, click **Virtual machines**.</span></span>

1. <span data-ttu-id="83310-141">En **Máquinas virtuales**, espere hasta que la máquina virtual muestre el estado **En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="83310-141">Under **Virtual machines**, wait until your VM shows a status of **Running**.</span></span> <span data-ttu-id="83310-142">Puede que tenga que hacer clic en **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="83310-142">You may need to click **Refresh**.</span></span>

1. <span data-ttu-id="83310-143">Haga clic en el nombre de la máquina virtual y, en **Configuración**, haga clic en **Tamaño**.</span><span class="sxs-lookup"><span data-stu-id="83310-143">Click the virtual machine's name, then in **Settings**, click **Size**.</span></span> <span data-ttu-id="83310-144">Observe que el tamaño de la máquina virtual ahora está establecido en **D2s_v3**.</span><span class="sxs-lookup"><span data-stu-id="83310-144">Note the VM size is now set to **D2s_v3**.</span></span>

### <a name="reconnect-to-the-resized-vm"></a><span data-ttu-id="83310-145">Nueva conexión a la máquina virtual a la que se ha cambiado el tamaño</span><span class="sxs-lookup"><span data-stu-id="83310-145">Reconnect to the resized VM</span></span>

1. <span data-ttu-id="83310-146">Haga clic en **Máquinas virtuales** y después en su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="83310-146">Click **Virtual machines**, then click your VM.</span></span> <span data-ttu-id="83310-147">Observe que es probable que el valor de **Dirección IP pública** haya cambiado.</span><span class="sxs-lookup"><span data-stu-id="83310-147">Note the **Public IP Address** value has probably changed.</span></span> <span data-ttu-id="83310-148">Haga clic en **Conectar**  y después en **Ejecutar** o **Abrir** en el explorador.</span><span class="sxs-lookup"><span data-stu-id="83310-148">Click **Connect**, and then click **Run** or **Open** in your browser.</span></span>

1. <span data-ttu-id="83310-149">En el cuadro de diálogo **Conexión a Escritorio remoto**, observe la advertencia de seguridad y la dirección IP del equipo remoto, y haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="83310-149">In the **Remote Desktop Connection** dialog box, note the security warning and the remote computer IP address, then click **Connect**.</span></span>

1. <span data-ttu-id="83310-150">En el cuadro de diálogo **Seguridad de Windows**, escriba el nombre de usuario y la contraseña que ha usado en los pasos 6 y 7.</span><span class="sxs-lookup"><span data-stu-id="83310-150">In the **Windows Security** dialog box, enter your user name and password that you used in steps 6 and 7.</span></span>

1. <span data-ttu-id="83310-151">En el segundo cuadro de diálogo **Conexión a Escritorio remoto**, observe los errores de certificado y, después, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="83310-151">In the second **Remote Desktop Connection** dialog box, note the certificate errors, then click **Yes**.</span></span> <span data-ttu-id="83310-152">Fíjese en que la máquina virtual responde mucho mejor al proceso de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="83310-152">Notice how much more responsive the virtual machine is to the sign-in process.</span></span>

1. <span data-ttu-id="83310-153">Haga clic con el botón derecho en la barra de tareas y haga clic en **Administrador de tareas**.</span><span class="sxs-lookup"><span data-stu-id="83310-153">Right-click the taskbar and click **Task Manager**.</span></span>

1. <span data-ttu-id="83310-154">En la ventana **Administrador de tareas**, haga clic en **Más detalles**.</span><span class="sxs-lookup"><span data-stu-id="83310-154">In the **Task Manager** window, click **More details**.</span></span>

1. <span data-ttu-id="83310-155">Haga clic en la pestaña **Rendimiento**. Observe que la memoria total disponible es de 8 GB, de los cuales aproximadamente 1,2 GB estarán en uso.</span><span class="sxs-lookup"><span data-stu-id="83310-155">Click the **Performance** tab. Note the total available memory is 8 GB of which about 1.2 GB will be in use.</span></span> <span data-ttu-id="83310-156">Cierre el **Administrador de tareas**.</span><span class="sxs-lookup"><span data-stu-id="83310-156">Close **Task Manager**.</span></span>

## <a name="summary"></a><span data-ttu-id="83310-157">Resumen</span><span class="sxs-lookup"><span data-stu-id="83310-157">Summary</span></span>

<span data-ttu-id="83310-158">Se ha conectado a una máquina virtual de Windows mediante RDP.</span><span class="sxs-lookup"><span data-stu-id="83310-158">You have connected to a Windows VM by using RDP.</span></span> <span data-ttu-id="83310-159">Con el acceso a la interfaz de usuario de escritorio, puede administrar esta máquina virtual como lo haría con cualquier equipo Windows.</span><span class="sxs-lookup"><span data-stu-id="83310-159">With Desktop UI access, you can administer this VM as you would any Windows computer.</span></span>