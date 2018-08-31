<span data-ttu-id="9ff33-101">En este ejercicio, vamos a crear una función de Azure que acepta una solicitud HTTP con una sola cadena.</span><span class="sxs-lookup"><span data-stu-id="9ff33-101">In this exercise, we're going to create an Azure function that accepts an HTTP request with a single string.</span></span> <span data-ttu-id="9ff33-102">La función devuelve una cadena al autor de la llamada para representar si se ha completado correctamente o no.</span><span class="sxs-lookup"><span data-stu-id="9ff33-102">The function returns a string back to the caller to represent success or failure.</span></span>

> [!NOTE]
> <span data-ttu-id="9ff33-103">Para completar este ejercicio, asegúrese de que ha iniciado sesión en [Azure Portal](https://portal.azure.com/) con una cuenta válida.</span><span class="sxs-lookup"><span data-stu-id="9ff33-103">To complete this exercise, make sure you're signed in to the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-an-http-trigger"></a><span data-ttu-id="9ff33-104">Creación de un desencadenador HTTP</span><span class="sxs-lookup"><span data-stu-id="9ff33-104">Create an HTTP trigger</span></span>

<span data-ttu-id="9ff33-105">Vamos a continuar usando nuestra aplicación de Azure Functions existente y agregar un desencadenador HTTP.</span><span class="sxs-lookup"><span data-stu-id="9ff33-105">Let's continue using our existing Azure Functions application and add an HTTP trigger.</span></span>

1. <span data-ttu-id="9ff33-106">Vaya a **Functions** y seleccione el icono de signo más (+).</span><span class="sxs-lookup"><span data-stu-id="9ff33-106">Point to **Functions** and select the plus (+) icon.</span></span>

    ![Selección de Functions y puntero sobre el signo más](../media-drafts/4-hover-function.png)

1. <span data-ttu-id="9ff33-108">Seleccione **Desencadenador HTTP**.</span><span class="sxs-lookup"><span data-stu-id="9ff33-108">Select **HTTP trigger**.</span></span>

1. <span data-ttu-id="9ff33-109">Seleccione **C#** como lenguaje.</span><span class="sxs-lookup"><span data-stu-id="9ff33-109">Select **C#** as the language.</span></span> 

1. <span data-ttu-id="9ff33-110">Deje el **Nombre** establecido en el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="9ff33-110">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="9ff33-111">Establezca el **Nivel de autorización** en **Anónimo**.</span><span class="sxs-lookup"><span data-stu-id="9ff33-111">Set the **Authorization level** to **Anonymous**.</span></span>

1. <span data-ttu-id="9ff33-112">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9ff33-112">Select **Create**.</span></span>

1. <span data-ttu-id="9ff33-113">Eche un vistazo rápido al código generado automáticamente para hacerse una idea sobre lo que está ocurriendo.</span><span class="sxs-lookup"><span data-stu-id="9ff33-113">Take a quick look at the auto-generated code to get an idea about what's going on.</span></span> <span data-ttu-id="9ff33-114">El parámetro *req* representa la solicitud entrante y contiene un parámetro *name*.</span><span class="sxs-lookup"><span data-stu-id="9ff33-114">The *req* parameter represents the incoming request and contains a *name* parameter.</span></span> <span data-ttu-id="9ff33-115">Comprobamos si *name* tiene un valor.</span><span class="sxs-lookup"><span data-stu-id="9ff33-115">We check to see if *name* has a value.</span></span> <span data-ttu-id="9ff33-116">Si es así, devolvemos un saludo.</span><span class="sxs-lookup"><span data-stu-id="9ff33-116">If it does, we return a greeting.</span></span> <span data-ttu-id="9ff33-117">En caso contrario, devolvemos un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="9ff33-117">Otherwise, we return an error message.</span></span>

## <a name="get-your-function-url"></a><span data-ttu-id="9ff33-118">Obtención de la dirección URL de función</span><span class="sxs-lookup"><span data-stu-id="9ff33-118">Get your function URL</span></span>

<span data-ttu-id="9ff33-119">Ahora que hemos creado el desencadenador HTTP, vamos a obtener la dirección URL de la función para que podamos empezar a realizar una solicitud.</span><span class="sxs-lookup"><span data-stu-id="9ff33-119">Now that we've created the HTTP trigger, let's get the function URL so we can begin to make a request.</span></span>

1. <span data-ttu-id="9ff33-120">Seleccione el desencadenador HTTP para abrir la pantalla de código.</span><span class="sxs-lookup"><span data-stu-id="9ff33-120">Select your HTTP trigger to open the code screen.</span></span>

1. <span data-ttu-id="9ff33-121">A la derecha de **Ejecutar**, seleccione **Obtención de dirección URL de la función**.</span><span class="sxs-lookup"><span data-stu-id="9ff33-121">To the right of **Run**, select **Get function URL**.</span></span>

1. <span data-ttu-id="9ff33-122">Haga clic en **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="9ff33-122">Select **Copy**.</span></span>

1. <span data-ttu-id="9ff33-123">Haga clic en **Ejecutar** para iniciar la función.</span><span class="sxs-lookup"><span data-stu-id="9ff33-123">Select **Run** to start your function.</span></span>

## <a name="issue-a-get-request-to-your-http-trigger"></a><span data-ttu-id="9ff33-124">Emisión de una solicitud GET al desencadenador HTTP</span><span class="sxs-lookup"><span data-stu-id="9ff33-124">Issue a GET request to your HTTP trigger</span></span>

<span data-ttu-id="9ff33-125">Ahora tenemos nuestra dirección URL de la función copiada en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="9ff33-125">We now have our function URL copied to our clipboard.</span></span> <span data-ttu-id="9ff33-126">Vamos a emitir una solicitud GET para ver si se obtiene una respuesta.</span><span class="sxs-lookup"><span data-stu-id="9ff33-126">Let's issue a GET request to see if we get a response.</span></span>

1. <span data-ttu-id="9ff33-127">Abra una nueva pestaña en el explorador web.</span><span class="sxs-lookup"><span data-stu-id="9ff33-127">Open a new tab in your web browser.</span></span>

1. <span data-ttu-id="9ff33-128">Pegue la dirección URL en la barra de direcciones.</span><span class="sxs-lookup"><span data-stu-id="9ff33-128">Paste the URL into the address bar.</span></span>

1. <span data-ttu-id="9ff33-129">Agregue un parámetro de cadena de consulta denominado *name* con su nombre; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9ff33-129">Add a query string parameter called *name* with your name for example:</span></span>

    ```
    .../api/HttpTriggerCSharp1?name=Jesse
    ```

1. <span data-ttu-id="9ff33-130">Presione ENTRAR para enviar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="9ff33-130">Select ENTER to submit the request.</span></span>

## <a name="clean-up"></a><span data-ttu-id="9ff33-131">Limpieza</span><span class="sxs-lookup"><span data-stu-id="9ff33-131">Clean up</span></span>

<span data-ttu-id="9ff33-132">Para asegurarse de que no se le cobra por esta función, seleccione **Pausar** encima de la ventana de registro.</span><span class="sxs-lookup"><span data-stu-id="9ff33-132">To ensure that you aren't charged for this function, select **Pause** above the log window.</span></span>

![Pausar](../media-drafts/4-pause-timer.png)


