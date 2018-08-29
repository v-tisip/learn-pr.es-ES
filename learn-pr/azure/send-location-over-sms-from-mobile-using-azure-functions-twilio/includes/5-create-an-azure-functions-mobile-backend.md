<span data-ttu-id="baea9-101">En este punto, la aplicación funciona con la intención de obtener la ubicación del usuario y está lista para enviarla a una función de Azure.</span><span class="sxs-lookup"><span data-stu-id="baea9-101">At this point, the app is working to get the user's location and is ready to be sent to an Azure function.</span></span> <span data-ttu-id="baea9-102">En esta unidad, va a crear la función de Azure.</span><span class="sxs-lookup"><span data-stu-id="baea9-102">In this unit, you build the Azure function.</span></span>

## <a name="create-an-azure-functions-project"></a><span data-ttu-id="baea9-103">Creación de un proyecto de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="baea9-103">Create an Azure Functions project</span></span>

1. <span data-ttu-id="baea9-104">Agregue un nuevo proyecto a la solución `ImHere`; haga clic con el botón derecho en la solución y seleccione *Agregar->Nuevo proyecto...*</span><span class="sxs-lookup"><span data-stu-id="baea9-104">Add a new project to the `ImHere` solution by right-clicking on the solution and selecting *Add->New Project...*.</span></span>

2. <span data-ttu-id="baea9-105">En el árbol del lado izquierdo, seleccione *Visual C#->Nube* y luego seleccione *Azure Functions* en el panel del centro.</span><span class="sxs-lookup"><span data-stu-id="baea9-105">From the tree on the left-hand side, select *Visual C#->Cloud*, and then select *Azure Functions* from the panel in the center.</span></span>

3. <span data-ttu-id="baea9-106">Asigne al proyecto el nombre "ImHere.Functions" y después haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="baea9-106">Name the project "ImHere.Functions", and then click **OK**.</span></span>

    ![Cuadro de diálogo Agregar nuevo proyecto](../media/5-add-new-functions-project.png)

4. <span data-ttu-id="baea9-108">En el cuadro de diálogo de configuración **Nuevo proyecto**, deje la versión de Functions establecida como *Azure Functions v1 (.NET Framework)*.</span><span class="sxs-lookup"><span data-stu-id="baea9-108">In the **New Project** configuration dialog, leave the Functions version set to *Azure Functions v1 (.NET Framework)*.</span></span> <span data-ttu-id="baea9-109">Seleccione *Desencadenador de HTTP*, deje la cuenta de almacenamiento establecida en *Emulador de almacenamiento* y establezca los derechos de acceso en *Anónimo*.</span><span class="sxs-lookup"><span data-stu-id="baea9-109">Select *Http Trigger*, leave the storage account set to *Storage Emulator*, and set the access rights to *Anonymous*.</span></span> <span data-ttu-id="baea9-110">A continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="baea9-110">Then click **OK**.</span></span>

    ![Cuadro de diálogo de configuración del proyecto de Azure Functions](../media/5-configure-trigger.png)

<span data-ttu-id="baea9-112">Se creará el proyecto y dispondrá de una función predeterminada denominada `Function1`.</span><span class="sxs-lookup"><span data-stu-id="baea9-112">The new project will be created and have a default function called `Function1`.</span></span>

> <span data-ttu-id="baea9-113">Esta función se creó con el acceso anónimo.</span><span class="sxs-lookup"><span data-stu-id="baea9-113">This function was created with anonymous access.</span></span> <span data-ttu-id="baea9-114">Una vez publicada en Azure, cualquier persona que sepa la dirección URL podrá llamar a esta función.</span><span class="sxs-lookup"><span data-stu-id="baea9-114">Once published to Azure, anybody who knows the URL will be able to call this function.</span></span> <span data-ttu-id="baea9-115">En un escenario real, la protegería con algún tipo de autenticación, como [Autenticación de Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) o [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c).</span><span class="sxs-lookup"><span data-stu-id="baea9-115">In a real-world scenario, you would protect this with some form of authentication, such as [Azure App Service authentication](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) or [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c).</span></span>

## <a name="create-the-function"></a><span data-ttu-id="baea9-116">Creación de la función</span><span class="sxs-lookup"><span data-stu-id="baea9-116">Create the function</span></span>

<span data-ttu-id="baea9-117">El proyecto de Azure Functions se crea con una única función de desencadenador de HTTP denominada `Function1`.</span><span class="sxs-lookup"><span data-stu-id="baea9-117">The Azure Functions project is created with a single HTTP trigger function called `Function1`.</span></span> <span data-ttu-id="baea9-118">La propia función se implementa como un método `Run` estático en la clase `Function1`.</span><span class="sxs-lookup"><span data-stu-id="baea9-118">The function itself is implemented as a static `Run` method in the `Function1` class.</span></span>

1. <span data-ttu-id="baea9-119">Cambie el nombre del archivo en el Explorador de soluciones de "Function1.cs" a "SendLocation.cs".</span><span class="sxs-lookup"><span data-stu-id="baea9-119">Rename the file in Solution Explorer from "Function1.cs" to "SendLocation.cs".</span></span> <span data-ttu-id="baea9-120">Cuando se le solicite cambiar el nombre de todas las referencias al elemento de código `Function1`, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="baea9-120">When prompted to rename all references to the code element `Function1`, click **Yes**.</span></span>

2. <span data-ttu-id="baea9-121">Cambie el nombre de la función en el atributo por "SendLocation".</span><span class="sxs-lookup"><span data-stu-id="baea9-121">Rename the function name in the attribute to "SendLocation".</span></span>

    ```cs
    [FunctionName("SendLocation")]
    ```

3. <span data-ttu-id="baea9-122">Elimine el contenido de la función, excepto la primera línea que escribe un mensaje informativo en el registrador.</span><span class="sxs-lookup"><span data-stu-id="baea9-122">Delete the contents of the function, except the first line that writes an information message to the logger.</span></span>

    ```cs
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                       TraceWriter log)
    {
        log.Info("C# HTTP trigger function processed a request.");
    }
    ```

## <a name="create-a-class-to-share-data-between-the-mobile-app-and-function"></a><span data-ttu-id="baea9-123">Creación de una clase para compartir datos entre la aplicación móvil y la función</span><span class="sxs-lookup"><span data-stu-id="baea9-123">Create a class to share data between the mobile app and function</span></span>

<span data-ttu-id="baea9-124">Cuando se envían datos a la función de Azure, se enviarán como JSON.</span><span class="sxs-lookup"><span data-stu-id="baea9-124">When data is sent to the Azure function, it will be sent as JSON.</span></span> <span data-ttu-id="baea9-125">La aplicación móvil serializará datos en JSON y la función anulará la serialización de JSON.</span><span class="sxs-lookup"><span data-stu-id="baea9-125">The mobile app will serialize data into JSON and the function will deserialize from JSON.</span></span> <span data-ttu-id="baea9-126">Para mantener la coherencia de los datos entre la aplicación móvil y la función, cree un proyecto que contenga una clase para hospedar los datos de ubicación y número de teléfono.</span><span class="sxs-lookup"><span data-stu-id="baea9-126">To keep this data consistent between the mobile app and the function, create a new project that contains a class to hold the location and phone number data.</span></span> <span data-ttu-id="baea9-127">A continuación, la aplicación y la función harán referencia a este proyecto.</span><span class="sxs-lookup"><span data-stu-id="baea9-127">This project will then be referenced by the app and function.</span></span>

1. <span data-ttu-id="baea9-128">Cree un proyecto en la solución `ImHere`; para ello, haga clic con el botón derecho en la solución y seleccione *Agregar->Nuevo proyecto...*</span><span class="sxs-lookup"><span data-stu-id="baea9-128">Create a new project under the `ImHere` solution by right-clicking on the solution and selecting *Add->New Project...*.</span></span>

2. <span data-ttu-id="baea9-129">En el árbol del lado izquierdo, seleccione *Visual C#->.NET Standard* y luego seleccione *Biblioteca de clases (.NET Standard)* en el panel del centro.</span><span class="sxs-lookup"><span data-stu-id="baea9-129">From the tree on the left-hand side, select *Visual C#->.NET Standard*, and then select *Class Library (.NET Standard)* from the panel in the center.</span></span>

3. <span data-ttu-id="baea9-130">Asigne al proyecto el nombre "ImHere.Data" y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="baea9-130">Name the project "ImHere.Data", and then click **OK**.</span></span>

    ![Cuadro de diálogo Agregar nuevo proyecto](../media/5-add-new-net-standard-project.png)

4. <span data-ttu-id="baea9-132">Elimine el archivo "Class1.cs" generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="baea9-132">Delete the auto-generated "Class1.cs" file.</span></span>

5. <span data-ttu-id="baea9-133">Cree una clase en el proyecto `ImHere.Data` llamada `PostData`; para ello, haga clic con el botón derecho en el proyecto y luego seleccione *Agregar->Clase...* Asigne el nombre "PostData" a la nueva clase y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="baea9-133">Create a new class in the `ImHere.Data` project called `PostData` by right-clicking on the project and then selecting *Add->Class...*. Name the new class "PostData" and click **OK**.</span></span>

6. <span data-ttu-id="baea9-134">Agregue las propiedades `double` para la latitud y longitud, así como una propiedad `string[]` para los números de teléfono a los que enviarlas.</span><span class="sxs-lookup"><span data-stu-id="baea9-134">Add `double` properties for the latitude and longitude, as well as a `string[]` property for the phone numbers to send to.</span></span>

    ```cs
    public class PostData
    {
        public double Latitude { get; set; }
        public double Longitude { get; set; }
        public string[] ToNumbers { get; set; }
    }
    ```

7. <span data-ttu-id="baea9-135">Agregue una referencia a este proyecto para los proyectos `ImHere.Functions` y `ImHere`; para ello, haga clic con el botón derecho en el proyecto y luego seleccione *Agregar->Referencia...* Seleccione *Proyectos* en el árbol del lado izquierdo y luego marque la casilla *ImHere.Data*.</span><span class="sxs-lookup"><span data-stu-id="baea9-135">Add a reference to this project to both the `ImHere.Functions` and `ImHere` projects by right-clicking on the project and then selecting *Add->Reference...*. Select *Projects* from the tree on the left-hand side, and then check the box next to *ImHere.Data*.</span></span>

    ![Configuración de las referencias de proyectos](../media/5-configure-project-references.png)

## <a name="read-the-data-sent-to-the-function"></a><span data-ttu-id="baea9-137">Lectura de los datos enviados a la función</span><span class="sxs-lookup"><span data-stu-id="baea9-137">Read the data sent to the function</span></span>

<span data-ttu-id="baea9-138">En la función de Azure, el parámetro `req` contiene la solicitud HTTP realizada y los datos contenidos en esta solicitud serán un objeto `PostData` JSON serializado.</span><span class="sxs-lookup"><span data-stu-id="baea9-138">In the Azure function, the `req` parameter contains the HTTP request that was made and the data inside this request will be a JSON serialized `PostData` object.</span></span>

1. <span data-ttu-id="baea9-139">Abra la clase `SendLocation` en el proyecto `ImHere.Functions`.</span><span class="sxs-lookup"><span data-stu-id="baea9-139">Open the `SendLocation` class in the `ImHere.Functions` project.</span></span>

2. <span data-ttu-id="baea9-140">Lea el contenido de la solicitud HTTP en un objeto `PostData` y agregue una directiva de uso para el espacio de nombres `ImHere.Data`.</span><span class="sxs-lookup"><span data-stu-id="baea9-140">Read the contents of the HTTP request into a `PostData` object, adding a using directive for the `ImHere.Data` namespace.</span></span>

    ```cs
    PostData data = await req.Content.ReadAsAsync<PostData>();
    ```

3. <span data-ttu-id="baea9-141">Creación de una dirección URL de Google Maps con la latitud y longitud de `PostData`.</span><span class="sxs-lookup"><span data-stu-id="baea9-141">Construct a Google Maps URL using the latitude and longitude from the `PostData`.</span></span>

   ```cs
   string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
   ```

4. <span data-ttu-id="baea9-142">Registre la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="baea9-142">Log the URL.</span></span>

    ```cs
    log.Info($"URL created - {url}");
    ```

5. <span data-ttu-id="baea9-143">Se devuelve un código de estado 200 para indicar que la función se ha completado sin errores.</span><span class="sxs-lookup"><span data-stu-id="baea9-143">Return a 200 status code to show the function completed without error.</span></span>

    ```cs
    return req.CreateResponse(HttpStatusCode.OK);
    ```

<span data-ttu-id="baea9-144">La función completa se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="baea9-144">The complete function is shown below.</span></span>

```cs
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                "get", "post",
                                                                Route = null)]HttpRequestMessage req,
                                                    TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");
    PostData data = await req.Content.ReadAsAsync<PostData>();
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.Info($"URL created - {url}");
    return req.CreateResponse(HttpStatusCode.OK);
}
```

## <a name="run-the-azure-function-locally"></a><span data-ttu-id="baea9-145">Ejecución local de la función de Azure</span><span class="sxs-lookup"><span data-stu-id="baea9-145">Run the Azure function locally</span></span>

<span data-ttu-id="baea9-146">Las funciones se pueden ejecutar a nivel local con una cuenta de almacenamiento local y el tiempo de ejecución local de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="baea9-146">Functions can be run locally using a local storage account and local Azure Functions runtime.</span></span> <span data-ttu-id="baea9-147">Este tiempo de ejecución local permite probar la función antes de implementarla en Azure.</span><span class="sxs-lookup"><span data-stu-id="baea9-147">This local runtime allows you to test out your function before deploying it to Azure.</span></span>

1. <span data-ttu-id="baea9-148">Haga clic con el botón derecho en el proyecto `ImHere.Functions` en el Explorador de soluciones y seleccione *Establecer como proyecto de inicio*.</span><span class="sxs-lookup"><span data-stu-id="baea9-148">Right-click on the `ImHere.Functions` project in the solution explorer, and then select *Set as StartUp project*.</span></span>

2. <span data-ttu-id="baea9-149">En el menú *Depurar*, seleccione *Iniciar sin depuración*.</span><span class="sxs-lookup"><span data-stu-id="baea9-149">From the *Debug* menu, select *Start Without Debugging*.</span></span> <span data-ttu-id="baea9-150">El tiempo de ejecución local de Azure Functions se lanzará dentro de una ventana de la consola e iniciará la función y escuchará en un puerto disponible en `localhost`.</span><span class="sxs-lookup"><span data-stu-id="baea9-150">The local Azure Functions runtime will launch inside a console window and start your function, listening on an available port on `localhost`.</span></span>

    ![Ejecución local de la función de Azure](../media/5-function-running-locally.png)

3. <span data-ttu-id="baea9-152">Tome nota del puerto en el que la función escucha.</span><span class="sxs-lookup"><span data-stu-id="baea9-152">Take a note of the port that the function is listening on.</span></span> <span data-ttu-id="baea9-153">Lo necesitará en la siguiente unidad para probar la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="baea9-153">You'll need this in the next unit to test out the mobile app.</span></span> <span data-ttu-id="baea9-154">En la imagen anterior, la función escucha en el puerto **7071**.</span><span class="sxs-lookup"><span data-stu-id="baea9-154">In the image above, the function is listening on port **7071**.</span></span>

    ```sh
    Listening on http://localhost:7071/
    ```

4. <span data-ttu-id="baea9-155">Deje la función en ejecución para que pueda probar la aplicación móvil en la siguiente unidad.</span><span class="sxs-lookup"><span data-stu-id="baea9-155">Leave the function running so that you can test the mobile app in the next unit.</span></span>

## <a name="summary"></a><span data-ttu-id="baea9-156">Resumen</span><span class="sxs-lookup"><span data-stu-id="baea9-156">Summary</span></span>

<span data-ttu-id="baea9-157">En esta unidad, aprendió a crear un proyecto de Azure Functions en Visual Studio, agregó un proyecto compartido con un objeto de datos para compartirse entre la aplicación móvil y la función y aprendió a crear una implementación básica de la función para deserializar los datos pasados.</span><span class="sxs-lookup"><span data-stu-id="baea9-157">In this unit, you learned how to create an Azure Functions project in Visual Studio, added a shared project with a data object to be shared between the mobile app and the function, and learned how to create a basic implementation of the function to deserialize the data passed in.</span></span> <span data-ttu-id="baea9-158">También aprendió cómo ejecutar una función de Azure localmente.</span><span class="sxs-lookup"><span data-stu-id="baea9-158">You also learned how to run an Azure function locally.</span></span> <span data-ttu-id="baea9-159">En la siguiente unidad, llamará a la función de Azure desde la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="baea9-159">In the next unit, you'll call the Azure function from the mobile app.</span></span>