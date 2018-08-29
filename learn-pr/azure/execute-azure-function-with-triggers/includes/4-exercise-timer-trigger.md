<span data-ttu-id="ad930-101">En este ejercicio, creará una función de Azure que se invoca cada 20 segundos con un desencadenador de temporizador.</span><span class="sxs-lookup"><span data-stu-id="ad930-101">In this exercise, we create an Azure function that's invoked every 20 seconds using a timer trigger.</span></span>

> [!NOTE] 
> <span data-ttu-id="ad930-102">Para completar este ejercicio, asegúrese de que ha iniciado sesión en [Azure Portal](https://portal.azure.com/) con una cuenta válida.</span><span class="sxs-lookup"><span data-stu-id="ad930-102">To complete this exercise, make sure you're logged into the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="ad930-103">Creación de una función de Azure</span><span class="sxs-lookup"><span data-stu-id="ad930-103">Create an Azure function</span></span>

<span data-ttu-id="ad930-104">Comencemos por crear una función de Azure en el portal.</span><span class="sxs-lookup"><span data-stu-id="ad930-104">Let’s start by creating an Azure function in the portal.</span></span>

1. <span data-ttu-id="ad930-105">En el panel de la izquierda, seleccione **Crear un recurso**.</span><span class="sxs-lookup"><span data-stu-id="ad930-105">In the left navigation, select **Create a resource**.</span></span>

1. <span data-ttu-id="ad930-106">Seleccione **Proceso**.</span><span class="sxs-lookup"><span data-stu-id="ad930-106">Select **Compute**.</span></span>

1. <span data-ttu-id="ad930-107">Busque y seleccione **Function App**.</span><span class="sxs-lookup"><span data-stu-id="ad930-107">Locate and select **Function App**.</span></span> <span data-ttu-id="ad930-108">También puede usar la barra de búsqueda para buscar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ad930-108">You can also optionally use the search bar to locate the template.</span></span>

    ![Selección de Function App](../media/4-click-function-app.png)

1. <span data-ttu-id="ad930-110">En **Nombre de aplicación**, escriba un nombre único.</span><span class="sxs-lookup"><span data-stu-id="ad930-110">Enter a unique **App name**.</span></span>

1. <span data-ttu-id="ad930-111">Seleccione una opción en **Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="ad930-111">Select a **Subscription**.</span></span>

1. <span data-ttu-id="ad930-112">En **Grupo de recursos**, cree uno.</span><span class="sxs-lookup"><span data-stu-id="ad930-112">Create a new **Resource Group**.</span></span>

1. <span data-ttu-id="ad930-113">Elija **Windows** como **OS**.</span><span class="sxs-lookup"><span data-stu-id="ad930-113">Choose **Windows** as your **OS**.</span></span>

1. <span data-ttu-id="ad930-114">Elija **Plan de consumo** en **Plan de hospedaje**.</span><span class="sxs-lookup"><span data-stu-id="ad930-114">Choose **Consumption Plan** for your **Hosting Plan**.</span></span> <span data-ttu-id="ad930-115">Se le cobrará por cada ejecución de la función.</span><span class="sxs-lookup"><span data-stu-id="ad930-115">You're charged for each execution of your function.</span></span> <span data-ttu-id="ad930-116">Los recursos se asignan automáticamente según la carga de trabajo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad930-116">Resources are automatically allocated based on your application workload.</span></span>

1. <span data-ttu-id="ad930-117">Seleccione una **ubicación**.</span><span class="sxs-lookup"><span data-stu-id="ad930-117">Select a **Location**.</span></span>

1. <span data-ttu-id="ad930-118">En **Storage**, cree una cuenta.</span><span class="sxs-lookup"><span data-stu-id="ad930-118">Create a new **Storage** account.</span></span> <span data-ttu-id="ad930-119">(Este valor es obligatorio, pero no vamos a usarlo).</span><span class="sxs-lookup"><span data-stu-id="ad930-119">(This value is required, but we're not going to use it.)</span></span>

1. <span data-ttu-id="ad930-120">Desactive por ahora **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="ad930-120">Turn off **Application Insights**.</span></span>

1. <span data-ttu-id="ad930-121">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ad930-121">Select **Create**.</span></span>

## <a name="create-a-timer-trigger"></a><span data-ttu-id="ad930-122">Creación de un desencadenador de temporizador</span><span class="sxs-lookup"><span data-stu-id="ad930-122">Create a timer trigger</span></span>

<span data-ttu-id="ad930-123">Ahora, vamos a crear un desencadenador de temporizador dentro de nuestra función de Azure.</span><span class="sxs-lookup"><span data-stu-id="ad930-123">Now we're going to create a timer trigger inside our Azure function.</span></span>

1. <span data-ttu-id="ad930-124">Después de crear la función de Azure, seleccione **Todos los recursos** en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="ad930-124">After the Azure function is created, select **All resources** from the left navigation.</span></span>

1. <span data-ttu-id="ad930-125">Busque y seleccione la función de Azure.</span><span class="sxs-lookup"><span data-stu-id="ad930-125">Locate and select your Azure function.</span></span>

1. <span data-ttu-id="ad930-126">En la nueva hoja, seleccione **Funciones** y seleccione el icono de signo más (+).</span><span class="sxs-lookup"><span data-stu-id="ad930-126">On the new blade, point to **Functions** and select the plus (+) icon.</span></span>

    ![Selección de Functions y el signo más](../media/4-hover-function.png)

1. <span data-ttu-id="ad930-128">Seleccione **Temporizador**.</span><span class="sxs-lookup"><span data-stu-id="ad930-128">Select **Timer**.</span></span>

1. <span data-ttu-id="ad930-129">Seleccione **CSharp** como lenguaje.</span><span class="sxs-lookup"><span data-stu-id="ad930-129">Select **CSharp** as the language.</span></span>

1. <span data-ttu-id="ad930-130">Seleccione **Crear esta función**.</span><span class="sxs-lookup"><span data-stu-id="ad930-130">Select **Create this function**.</span></span>

## <a name="configure-the-timer-trigger"></a><span data-ttu-id="ad930-131">Configuración del desencadenador de temporizador</span><span class="sxs-lookup"><span data-stu-id="ad930-131">Configure the timer trigger</span></span>

<span data-ttu-id="ad930-132">Tenemos una función de Azure con lógica para imprimir un mensaje en la ventana de registro.</span><span class="sxs-lookup"><span data-stu-id="ad930-132">We have an Azure function with logic to print a message to the log window.</span></span> <span data-ttu-id="ad930-133">Vamos a programar el temporizador para que se ejecute cada 20 segundos.</span><span class="sxs-lookup"><span data-stu-id="ad930-133">We're going to set the schedule of the timer to execute every 20 seconds.</span></span>

1. <span data-ttu-id="ad930-134">Seleccione **Integrar**.</span><span class="sxs-lookup"><span data-stu-id="ad930-134">Select **Integrate**.</span></span>

1. <span data-ttu-id="ad930-135">Escriba el siguiente valor en el cuadro **Programar**:</span><span class="sxs-lookup"><span data-stu-id="ad930-135">Enter the following value into the **Schedule** box:</span></span>

    ```
    */20 * * * * *
    ```

1. <span data-ttu-id="ad930-136">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ad930-136">Select **Save**.</span></span>

## <a name="start-the-timer"></a><span data-ttu-id="ad930-137">Inicio del temporizador</span><span class="sxs-lookup"><span data-stu-id="ad930-137">Start the timer</span></span>

<span data-ttu-id="ad930-138">Ahora que hemos configurado el temporizador, estamos listos para iniciarlo.</span><span class="sxs-lookup"><span data-stu-id="ad930-138">Now that we've configured the timer, we're ready to start it.</span></span>

1. <span data-ttu-id="ad930-139">Seleccione **TimerTriggerCSharp1**.</span><span class="sxs-lookup"><span data-stu-id="ad930-139">Select **TimerTriggerCSharp1**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="ad930-140">**TimerTriggerCSharp1** es un nombre predeterminado.</span><span class="sxs-lookup"><span data-stu-id="ad930-140">**TimerTriggerCSharp1** is a default name.</span></span> <span data-ttu-id="ad930-141">Se selecciona automáticamente cuando se crea el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="ad930-141">It's automatically selected when you create the trigger.</span></span>

1. <span data-ttu-id="ad930-142">Seleccione **Run** (Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="ad930-142">Select **Run**.</span></span> 

<span data-ttu-id="ad930-143">En este punto, verá un mensaje cada 20 segundos en la ventana de registro.</span><span class="sxs-lookup"><span data-stu-id="ad930-143">At this point, you should see a message every 20 seconds in the log window.</span></span>

## <a name="clean-up"></a><span data-ttu-id="ad930-144">Limpieza</span><span class="sxs-lookup"><span data-stu-id="ad930-144">Clean up</span></span>

<span data-ttu-id="ad930-145">Para asegurarse de que no se le cobra por esta función, encima de la ventana de registro, seleccione **Pausar** para detener el temporizador.</span><span class="sxs-lookup"><span data-stu-id="ad930-145">To ensure that you aren't charged for this function, above the log window, select **Pause** to stop the timer.</span></span>

![Pausar](../media/4-pause-timer.png)


