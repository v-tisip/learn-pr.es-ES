<span data-ttu-id="8ee8d-101">En este ejercicio, usará Azure Portal para comprobar el centro de eventos está funcionando según las expectativas deseadas.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-101">In this exercise, you'll use the Azure portal to verify your event hub is working and performing according to the desired expectations.</span></span> <span data-ttu-id="8ee8d-102">También probaré cómo funciona la mensajería del centro de eventos cuando no está disponible temporalmente y usará las métricas de Event Hubs para comprobar el rendimiento del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-102">You'll also test how event hub messaging works when it's temporarily unavailable and use Event Hubs metrics to check the performance of your event hub.</span></span>

## <a name="view-event-hub-activity"></a><span data-ttu-id="8ee8d-103">Vista de la actividad del centro de eventos</span><span class="sxs-lookup"><span data-stu-id="8ee8d-103">View event hub activity</span></span>

1. <span data-ttu-id="8ee8d-104">Iniciar sesión en [Azure Portal](https://portal.azure.com?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="8ee8d-104">Sing in to your [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>
1. <span data-ttu-id="8ee8d-105">Busque el centro de eventos en la barra de búsqueda y ábralo.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-105">Find your event hub, using the Search bar, and open it.</span></span>

1. <span data-ttu-id="8ee8d-106">En la página de información general, consulte los recuentos de mensajes.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-106">On the Overview page, view the message counts.</span></span>

    ![Vista de los mensajes del centro de eventos](../media-draft/6-view-messages.png)

1. <span data-ttu-id="8ee8d-108">Las aplicaciones SimpleSend y EventProcessorSample están configuradas para enviar y recibir 100 mensajes.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-108">The SimpleSend and EventProcessorSample applications are configured to send/receive 100 messages.</span></span> <span data-ttu-id="8ee8d-109">Verá que el centro de eventos procesó 100 mensajes provenientes de la aplicación SimpleSend y transmitió 100 mensajes a la aplicación EventProcessorSample.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-109">You'll see that the event hub has processed 100 messages from the SimpleSend application, and has transmitted 100 messages to the EventProcessorSample application.</span></span>

## <a name="test-event-hub-resilience"></a><span data-ttu-id="8ee8d-110">Prueba de la resistencia del centro de eventos</span><span class="sxs-lookup"><span data-stu-id="8ee8d-110">Test event hub resilience</span></span>

<span data-ttu-id="8ee8d-111">Use estos pasos para ver qué sucede cuando una aplicación envía mensajes a un centro de eventos mientras no está disponible de manera temporal.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-111">Use the following steps to see what happens when an application sends messages to an event hub while it's temporarily unavailable.</span></span>

1. <span data-ttu-id="8ee8d-112">Reenvíe los mensajes al centro de eventos con la aplicación SimpleSend.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-112">Resend messages to the event hub using the SimpleSend application.</span></span> <span data-ttu-id="8ee8d-113">Use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="8ee8d-113">Use the following command:</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. <span data-ttu-id="8ee8d-114">Cuando vea **Envío completo...**, presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-114">When you see **Send Complete...**, press ENTER.</span></span>

1. <span data-ttu-id="8ee8d-115">En Azure Portal, haga clic en **Instancia de Event Hubs** > **CONFIGURACIÓN** > **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-115">In the Azure portal, click **Event Hubs Instance** > **SETTINGS** > **Properties**.</span></span>
1. <span data-ttu-id="8ee8d-116">En Estado del centro de eventos, haga clic en **Deshabilitado**.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-116">Under Event Hub state, click **Disabled**.</span></span>

    ![Deshabilitación del centro de eventos](../media-draft/7-disable-event-hub.png)

<span data-ttu-id="8ee8d-118">Espere un mínimo de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-118">Wait for a minimum of five minutes.</span></span>

1. <span data-ttu-id="8ee8d-119">Haga clic en **Activar** en Estado del centro de eventos para volver a habilitar el centro de eventos y guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-119">Click **Active** under Event Hub state to re-enable your event hub and save your changes.</span></span>
1. <span data-ttu-id="8ee8d-120">Vuelva a ejecutar la aplicación EventProcessorSample para recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-120">Rerun the EventProcessorSample application to receive messages.</span></span> <span data-ttu-id="8ee8d-121">Use el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-121">Use the following command.</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. <span data-ttu-id="8ee8d-122">Cuando los mensajes dejen de aparecer en la consola, presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-122">When messages stop being displayed to the console, press ENTER.</span></span>

1. <span data-ttu-id="8ee8d-123">En Azure Portal, busque el **_espacio de nombres_** del centro de eventos y ábralo.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-123">In the Azure portal, find your event hub **_namespace_** and open it.</span></span> 

1. <span data-ttu-id="8ee8d-124">Haga clic en **Espacio de nombres de Event Hubs** > **SUPERVISIÓN** > **Métricas (versión preliminar)**.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-124">Click **Event Hubs Namespace** > **MONITORING** > **Metrics (preview)**.</span></span>

    ![Uso de las métricas del centro de eventos](../media-draft/7-event-hub-metrics.png)

1. <span data-ttu-id="8ee8d-126">En la lista **Métrica**, seleccione **Mensajes entrantes** y haga clic en **Agregar métrica**.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-126">From the **Metric** list, select **Incoming Messages** and click **Add Metric**.</span></span>
1. <span data-ttu-id="8ee8d-127">En la lista **Métrica**, seleccione **Mensajes salientes** y haga clic en **Agregar métrica**.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-127">From the **Metric** list, select **Outgoing Messages** and click **Add Metric**.</span></span>
1. <span data-ttu-id="8ee8d-128">En la parte superior del gráfico, haga clic en **Últimas 24 horas (automático)** para cambiar el período de tiempo a **Últimos 30 minutos**.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-128">At the top of the chart, click **Last 24 hours (Automatic)** to change the time period to **Last 30 minutes**.</span></span>
1. <span data-ttu-id="8ee8d-129">Haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-129">Click **Apply**.</span></span>

<span data-ttu-id="8ee8d-130">Verá que aunque los mensajes se enviaron antes de que el centro de eventos quedará sin conexión durante un período, se transmitieron correctamente los 100 mensajes.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-130">You'll see that though the messages were sent before the event hub was taken offline for a period, all 100 messages were successfully transmitted.</span></span>

## <a name="summary"></a><span data-ttu-id="8ee8d-131">Resumen</span><span class="sxs-lookup"><span data-stu-id="8ee8d-131">Summary</span></span>

<span data-ttu-id="8ee8d-132">En esta unidad, usó las métricas de Event Hubs para probar que el centro de eventos está procesando correctamente el envío y la recepción de mensajes.</span><span class="sxs-lookup"><span data-stu-id="8ee8d-132">In this unit, you used the Event Hubs metrics to test that your event hub is successfully processing the sending and receiving messages.</span></span>
