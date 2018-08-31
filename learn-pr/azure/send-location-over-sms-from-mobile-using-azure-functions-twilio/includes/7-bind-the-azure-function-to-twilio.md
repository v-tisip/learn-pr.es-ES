<span data-ttu-id="bd3ed-101">En este punto, la aplicación móvil está completa y envía la lista de números de teléfono y la ubicación del usuario a una función de Azure que puede deserializar los datos.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-101">At this point, the mobile app is complete and sends the user's location and list of phone numbers to an Azure function that can deserialize the data.</span></span> <span data-ttu-id="bd3ed-102">En esta unidad, enlazará la función de Azure a Twilio para enviar mensajes SMS.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-102">In this unit, you bind the Azure function to Twilio to send SMS messages.</span></span>

<span data-ttu-id="bd3ed-103">Azure Functions se puede conectar a otros servicios, ya sean servicios en Azure o servicios de terceros.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-103">Azure Functions can be connected to other services, either services in Azure or third-party services.</span></span> <span data-ttu-id="bd3ed-104">Existen dos tipos de estas conexiones, llamadas enlaces: enlaces de entrada y de salida.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-104">These connections, called bindings, exist in two forms - input and output bindings.</span></span> <span data-ttu-id="bd3ed-105">Los enlaces de entrada proporcionan datos a la función y los enlaces de salida toman datos de la función y los envían a otro servicio.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-105">Input bindings provide data to your function and output bindings take data from your function and send it to another service.</span></span> <span data-ttu-id="bd3ed-106">Puede leer sobre los enlaces en los [documentos sobre los enlaces de Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).</span><span class="sxs-lookup"><span data-stu-id="bd3ed-106">You can read about bindings in the [Azure Functions Binding docs](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).</span></span>

<span data-ttu-id="bd3ed-107">Los enlaces para Azure Functions que se crean en Visual Studio se definen mediante parámetros de la función, decorados con atributos.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-107">Bindings for Azure Functions created in Visual Studio are defined using parameters to the function, decorated with attributes.</span></span>

## <a name="bind-the-azure-function-to-twilio"></a><span data-ttu-id="bd3ed-108">Enlace de la función de Azure a Twilio</span><span class="sxs-lookup"><span data-stu-id="bd3ed-108">Bind the Azure function to Twilio</span></span>

<span data-ttu-id="bd3ed-109">Enviar mensajes SMS a través de Twilio requiere un enlace de salida configurado con el identificador de la suscripción de cuenta (SID) y el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-109">Sending SMS messages via Twilio requires an output binding that is configured with your account subscription ID (SID) and Auth Token.</span></span>

1. <span data-ttu-id="bd3ed-110">Detenga el tiempo de ejecución de Azure Functions local si sigue en ejecución desde la unidad anterior.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-110">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

2. <span data-ttu-id="bd3ed-111">Agregue el paquete NuGet "Microsoft.Azure.WebJobs.Extensions.Twilio" al proyecto `ImHere.Functions`.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-111">Add the "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet package to the `ImHere.Functions` project.</span></span> <span data-ttu-id="bd3ed-112">Este paquete NuGet contiene las clases pertinentes para el enlace.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-112">This NuGet package contains the relevant classes for the binding.</span></span>

3. <span data-ttu-id="bd3ed-113">Agregue un parámetro nuevo al método `Run` estático en la clase estática `SendLocation` llamada `messages`.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-113">Add a new parameter to the static `Run` method on the `SendLocation` static class called `messages`.</span></span> <span data-ttu-id="bd3ed-114">Este parámetro tendrá un tipo de `ICollector<SMSMessage>`.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-114">This parameter will have a type of `ICollector<SMSMessage>`.</span></span> <span data-ttu-id="bd3ed-115">Tendrá que agregar una directiva using al espacio de nombres `Twilio`.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-115">You'll need to add a using directive for the `Twilio` namespace.</span></span>

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                      ICollector<SMSMessage> messages,
                                                      TraceWriter log)
    ```

4. <span data-ttu-id="bd3ed-116">Decore el nuevo parámetro `messages` con el atributo `TwilioSms`.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-116">Decorate the new `messages` parameter with the `TwilioSms` attribute.</span></span> <span data-ttu-id="bd3ed-117">Este atributo tiene tres parámetros que debe establecer.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-117">This attribute has three parameters you need to set.</span></span>

    | <span data-ttu-id="bd3ed-118">Configuración</span><span class="sxs-lookup"><span data-stu-id="bd3ed-118">Setting</span></span>      |  <span data-ttu-id="bd3ed-119">Valor</span><span class="sxs-lookup"><span data-stu-id="bd3ed-119">Value</span></span>   | <span data-ttu-id="bd3ed-120">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="bd3ed-120">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="bd3ed-121">**AccountSidSetting**</span><span class="sxs-lookup"><span data-stu-id="bd3ed-121">**AccountSidSetting**</span></span> | <span data-ttu-id="bd3ed-122">"TwilioAccountSid"</span><span class="sxs-lookup"><span data-stu-id="bd3ed-122">"TwilioAccountSid"</span></span> | <span data-ttu-id="bd3ed-123">El SID de la cuenta de Twilio.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-123">The SID for your Twilio account.</span></span> <span data-ttu-id="bd3ed-124">En lugar de establecer directamente el SID, este parámetro es el nombre de un valor de la configuración de la aplicación de función que se usará para recuperar el SID.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-124">Rather than set the SID directly, this parameter is the name of a value in the function app settings that will be used to retrieve the SID.</span></span> |
    | <span data-ttu-id="bd3ed-125">**AuthTokenSetting**</span><span class="sxs-lookup"><span data-stu-id="bd3ed-125">**AuthTokenSetting**</span></span> | <span data-ttu-id="bd3ed-126">"TwilioAuthToken"</span><span class="sxs-lookup"><span data-stu-id="bd3ed-126">"TwilioAuthToken"</span></span> | <span data-ttu-id="bd3ed-127">Token de autenticación de la cuenta de Twilio.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-127">The Auth Token for your Twilio account.</span></span> <span data-ttu-id="bd3ed-128">En lugar de establecer directamente el token de autenticación, este parámetro es el nombre de un valor de la configuración de la aplicación de función que se usará para recuperar el token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-128">Rather than set the Auth Token directly, this parameter is the name of a value in the function app settings that will be used to retrieve the Auth Token.</span></span> |
    | <span data-ttu-id="bd3ed-129">**From**</span><span class="sxs-lookup"><span data-stu-id="bd3ed-129">**From**</span></span> | <span data-ttu-id="bd3ed-130">El número de teléfono de Twilio</span><span class="sxs-lookup"><span data-stu-id="bd3ed-130">Your Twilio phone number</span></span> | <span data-ttu-id="bd3ed-131">El número de teléfono de Twilio desde el que se enviarán los mensajes SMS en formato internacional (+\<código de país\>\<número de teléfono\>, por ejemplo, "+1555123456").</span><span class="sxs-lookup"><span data-stu-id="bd3ed-131">The Twilio phone number that the SMS messages will come from in international format (+\<country code\>\<phone number\>, for example "+1555123456").</span></span> |

    <span data-ttu-id="bd3ed-132">Cuando crea una cuenta de Twilio, se le asigna un número de teléfono desde el que puede enviar mensajes.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-132">When you create a Twilio account, you are assigned a phone number that you can send messages from.</span></span> <span data-ttu-id="bd3ed-133">Puede encontrar este número de teléfono en el panel **Números de teléfono** de Twilio.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-133">You can find this phone number on the Twilio **Phone Numbers** dashboard.</span></span> <span data-ttu-id="bd3ed-134">En el sitio de Twilio, seleccione los puntos suspensivos que aparecen en la parte inferior del menú de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-134">From the Twilio site, select the ellipses at the bottom of the left-hand menu.</span></span> <span data-ttu-id="bd3ed-135">Luego, seleccione *SUPER NETWORK->Phone Numbers* (SUPER RED -> Números de teléfono).</span><span class="sxs-lookup"><span data-stu-id="bd3ed-135">Then, select *SUPER NETWORK->Phone Numbers*.</span></span> <span data-ttu-id="bd3ed-136">Puede usar el icono de anclar para anclar este panel al menú de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-136">You can pin this dashboard to the left-hand menu using the pin icon.</span></span> <span data-ttu-id="bd3ed-137">Su número de Twilio estará en *Manage Numbers->Active Numbers* (Administrar números -> Números activos).</span><span class="sxs-lookup"><span data-stu-id="bd3ed-137">Your Twilio number will be under *Manage Numbers->Active Numbers*.</span></span> <span data-ttu-id="bd3ed-138">Deberá quitar cualquier espacio que haya en el número.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-138">You'll need to remove any spaces from the number.</span></span>

    ![Búsqueda del número de Twilio](../media-drafts/7-twilio-find-number.png)

    ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
               AuthTokenSetting = "TwilioAuthToken",
               From = "+1xxxxxxxxx")]ICollector<SMSMessage> messages,
    ```

5. <span data-ttu-id="bd3ed-140">La configuración de la aplicación de función se puede configurar localmente dentro del archivo `local.settings.json`.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-140">Function app settings can be configured locally inside the `local.settings.json` file.</span></span> <span data-ttu-id="bd3ed-141">Agregue el SID y el token de autenticación de la cuenta de Twilio a este archivo JSON con los nombres de configuración que se pasaron al atributo `TwilioSMS`.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-141">Add your Twilio account SID and Auth Token to this JSON file using the setting names that were passed to the `TwilioSMS` attribute.</span></span>

    ```json
    {
        "IsEncrypted": false,
        "Values": {
            "AzureWebJobsStorage": "UseDevelopmentStorage=true",
            "AzureWebJobsDashboard": "UseDevelopmentStorage=true",
            "TwilioAccountSid": "<Your SID>",
            "TwilioAuthToken": "<Your Auth Token>"
        }
    }
    ```

    <span data-ttu-id="bd3ed-142">Reemplace \<Your SID\> (Su SID) y \<Your Auth Token\> (Su token de autenticación) por los valores que aparecen en su panel de Twilio.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-142">Replace \<Your SID\> and \<Your Auth Token\> with the values from your Twilio dashboard.</span></span>

    > <span data-ttu-id="bd3ed-143">Esta configuración local solo será para ejecución local.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-143">These local settings will be only for running locally.</span></span> <span data-ttu-id="bd3ed-144">En una aplicación de producción, estos valores serían las credenciales de cuenta de prueba o desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-144">In a production app, these value would be your local development or test account credentials.</span></span> <span data-ttu-id="bd3ed-145">Una vez que la función de Azure se implementó en Azure, podrá configurar los valores de producción.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-145">Once the Azure Function has been deployed to Azure, you'll be able to configure the production values.</span></span>
    > <span data-ttu-id="bd3ed-146">Si el código se confirma en el control de código fuente, también se confirmarán estos valores de configuración de la aplicación local, por lo que debe tener cuidado de no confirmar ningún valor real en estos archivos si el código es abierto o público de cualquier forma.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-146">If you check your code into source control, these local application setting values will be checked in, too, so be careful not to check in any actual values in these files if your code is open source or public in any form.</span></span>

## <a name="create-the-sms-messages"></a><span data-ttu-id="bd3ed-147">Creación de los mensajes SMS</span><span class="sxs-lookup"><span data-stu-id="bd3ed-147">Create the SMS messages</span></span>

<span data-ttu-id="bd3ed-148">El parámetro `ICollector<SMSMessage>` es una recopilación de instancias de `SMSMessage` que se usa para recopilar los mensajes SMS que quiere enviar.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-148">The `ICollector<SMSMessage>` parameter is a collection of `SMSMessage` instances and is used to collect the SMS messages you want to send.</span></span> <span data-ttu-id="bd3ed-149">Cuando la función termina de ejecutarse, cualquier instancia de `SMSMessage` que se haya agregado a esta colección se pasa a Twilio y se envía a los destinatarios correspondientes.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-149">After the function has finished running, any instances of `SMSMessage` added to this collection are passed to Twilio and sent to the relevant recipients.</span></span>

1. <span data-ttu-id="bd3ed-150">En la función `SendLocation`, agregue código al bucle mediante los números de teléfono que hay en `PostData` y cree un mensaje SMS para cada uno.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-150">In the `SendLocation` function, add code to loop through the phone numbers in the `PostData` and create an SMS message for each one.</span></span>

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        SMSMessage message = new SMSMessage
        {
            Body = $"I'm here! {url}",
            To = toNo
        };
    }
    ```

    <span data-ttu-id="bd3ed-151">El mensaje necesita el número de teléfono al que se enviará y un cuerpo que contenga la dirección URL de Google Maps creada a partir de la ubicación del usuario.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-151">The message needs the phone number to send to and a body that contains the Google Maps URL created from the user's location.</span></span>

2. <span data-ttu-id="bd3ed-152">Registre cada mensaje y agréguelo a la colección `messages`.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-152">Log each message, and then add it to the `messages` collection.</span></span>

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

<span data-ttu-id="bd3ed-153">Todo el método `SendLocation` aparece a continuación.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-153">The complete `SendLocation` method is shown below.</span></span>

```cs
[FunctionName("SendLocation")]
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                "get", "post",
                                                                Route = null)]HttpRequestMessage req,
                                                    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
                                                                AuthTokenSetting = "TwilioAuthToken",
                                                                From = "<your Twilio phone number>")]ICollector<SMSMessage> messages,
                                                    TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");
    PostData data = await req.Content.ReadAsAsync<PostData>();
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.Info($"URL created - {url}");
    foreach (string toNo in data.ToNumbers)
    {
        SMSMessage message = new SMSMessage
        {
            Body = $"I'm here! {url}",
            To = toNo
        };
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    return req.CreateResponse(HttpStatusCode.OK);
}
```

## <a name="test-it-out"></a><span data-ttu-id="bd3ed-154">Prueba</span><span class="sxs-lookup"><span data-stu-id="bd3ed-154">Test it out</span></span>

1. <span data-ttu-id="bd3ed-155">Establezca la aplicación `ImHere.Functions` como el proyecto de inicio y comiéncelo sin depuración.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-155">Set the `ImHere.Functions` app as the startup project and start it without debugging.</span></span>

2. <span data-ttu-id="bd3ed-156">Establezca la aplicación `ImHere.UWP` como el proyecto de inicio y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-156">Set the `ImHere.UWP` app as the startup project and run it.</span></span>

3. <span data-ttu-id="bd3ed-157">Escriba su propio número de teléfono en formato internacional (+\<código de país\>\<número de teléfono\>) en la aplicación Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-157">Enter your own phone number in international format (+\<country code\>\<phone number\>) into the Xamarin.Forms app.</span></span> <span data-ttu-id="bd3ed-158">Las cuentas de evaluación de Twilio puede enviar mensajes solo a números de teléfono comprobados por lo que, por ahora, solo podrá enviarse mensajes a usted mismo a menos que actualice a una cuenta de pago o compruebe otros números.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-158">Twilio trial accounts can send  messages only to verified phone numbers, so for now, you'll only be able to message yourself unless you upgrade to a paid account or verify other numbers.</span></span>

4. <span data-ttu-id="bd3ed-159">Haga clic en el botón **Enviar ubicación**.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-159">Click the **Send Location** button.</span></span> <span data-ttu-id="bd3ed-160">Si el mensaje SMS se envió correctamente, verá un mensaje en la aplicación Xamarin.Forms que indica "Location sent successfully" (La ubicación se envió correctamente).</span><span class="sxs-lookup"><span data-stu-id="bd3ed-160">If the SMS message was sent successfully, you'll see a message in the Xamarin.Forms app saying "Location sent successfully".</span></span>

    ![La aplicación Xamarin.Forms mostrando la ubicación como enviada](../media-drafts/7-ui-location-sent.png)

5. <span data-ttu-id="bd3ed-162">En los registros de consola para la función de Azure, verá que se crea y envía el mensaje.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-162">In the console logs for the Azure function, you'll see the message being created and sent.</span></span> <span data-ttu-id="bd3ed-163">Si se produce algún error (como que el número tiene un formato incorrecto), se registrará aquí.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-163">If any errors occur (such as, the number is in the wrong format), they will be logged out here.</span></span>

    ![La consola de la función de Azure mostrando que el mensaje se envió](../media-drafts/7-function-message-sent.png)

6. <span data-ttu-id="bd3ed-165">Revise el teléfono por si tiene un mensaje.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-165">Check your phone for a message.</span></span> <span data-ttu-id="bd3ed-166">Siga el vínculo en el mensaje para ver su ubicación.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-166">Follow the link in the message to see your location.</span></span>

    ![Mensaje SMS recibido en un teléfono móvil](../media-drafts/7-message-received.png)

## <a name="summary"></a><span data-ttu-id="bd3ed-168">Resumen</span><span class="sxs-lookup"><span data-stu-id="bd3ed-168">Summary</span></span>

<span data-ttu-id="bd3ed-169">En esta unidad aprendió a crear un enlace de Twilio para la función de Azure y a enviar un mensaje SMS con la ubicación del usuario a una función que se ejecutaba de manera local.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-169">In this unit, you learned how to create a Twilio binding for the Azure function and send an SMS message with the user's location to a function that was running locally.</span></span> <span data-ttu-id="bd3ed-170">En la unidad siguiente, publicará la función en Azure.</span><span class="sxs-lookup"><span data-stu-id="bd3ed-170">In the next unit, you publish the function to Azure.</span></span>