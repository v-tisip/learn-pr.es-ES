En este punto, la aplicación móvil está completa y envía la lista de números de teléfono y la ubicación del usuario a una función de Azure que puede deserializar los datos. En esta unidad, enlazará la función de Azure a Twilio para enviar mensajes SMS.

Azure Functions se puede conectar a otros servicios, ya sean servicios en Azure o servicios de terceros. Existen dos tipos de estas conexiones, llamadas enlaces: enlaces de entrada y de salida. Los enlaces de entrada proporcionan datos a la función y los enlaces de salida toman datos de la función y los envían a otro servicio. Puede leer sobre los enlaces en los [documentos sobre los enlaces de Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).

Los enlaces para Azure Functions que se crean en Visual Studio se definen mediante parámetros de la función, decorados con atributos.

## <a name="bind-the-azure-function-to-twilio"></a>Enlace de la función de Azure a Twilio

Enviar mensajes SMS a través de Twilio requiere un enlace de salida configurado con el identificador de la suscripción de cuenta (SID) y el token de autenticación.

1. Detenga el tiempo de ejecución de Azure Functions local si sigue en ejecución desde la unidad anterior.

2. Agregue el paquete NuGet "Microsoft.Azure.WebJobs.Extensions.Twilio" al proyecto `ImHere.Functions`. Este paquete NuGet contiene las clases pertinentes para el enlace.

3. Agregue un parámetro nuevo al método `Run` estático en la clase estática `SendLocation` llamada `messages`. Este parámetro tendrá un tipo de `ICollector<SMSMessage>`. Tendrá que agregar una directiva using al espacio de nombres `Twilio`.

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                      ICollector<SMSMessage> messages,
                                                      TraceWriter log)
    ```

4. Decore el nuevo parámetro `messages` con el atributo `TwilioSms`. Este atributo tiene tres parámetros que debe establecer.

    | Configuración      |  Valor   | DESCRIPCIÓN                                        |
    | --- | --- | ---|
    | **AccountSidSetting** | "TwilioAccountSid" | El SID de la cuenta de Twilio. En lugar de establecer directamente el SID, este parámetro es el nombre de un valor de la configuración de la aplicación de función que se usará para recuperar el SID. |
    | **AuthTokenSetting** | "TwilioAuthToken" | Token de autenticación de la cuenta de Twilio. En lugar de establecer directamente el token de autenticación, este parámetro es el nombre de un valor de la configuración de la aplicación de función que se usará para recuperar el token de autenticación. |
    | **From** | El número de teléfono de Twilio | El número de teléfono de Twilio desde el que se enviarán los mensajes SMS en formato internacional (+\<código de país\>\<número de teléfono\>, por ejemplo, "+1555123456"). |

    Cuando crea una cuenta de Twilio, se le asigna un número de teléfono desde el que puede enviar mensajes. Puede encontrar este número de teléfono en el panel **Números de teléfono** de Twilio. En el sitio de Twilio, seleccione los puntos suspensivos que aparecen en la parte inferior del menú de la izquierda. Luego, seleccione *SUPER NETWORK->Phone Numbers* (SUPER RED -> Números de teléfono). Puede usar el icono de anclar para anclar este panel al menú de la izquierda. Su número de Twilio estará en *Manage Numbers->Active Numbers* (Administrar números -> Números activos). Deberá quitar cualquier espacio que haya en el número.

    ![Búsqueda del número de Twilio](../media/7-twilio-find-number.png)

    ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
               AuthTokenSetting = "TwilioAuthToken",
               From = "+1xxxxxxxxx")]ICollector<SMSMessage> messages,
    ```

5. La configuración de la aplicación de función se puede configurar localmente dentro del archivo `local.settings.json`. Agregue el SID y el token de autenticación de la cuenta de Twilio a este archivo JSON con los nombres de configuración que se pasaron al atributo `TwilioSMS`.

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

    Reemplace \<Your SID\> (Su SID) y \<Your Auth Token\> (Su token de autenticación) por los valores que aparecen en su panel de Twilio.

    > Esta configuración local solo será para ejecución local. En una aplicación de producción, estos valores serían las credenciales de cuenta de prueba o desarrollo local. Una vez que la función de Azure se implementó en Azure, podrá configurar los valores de producción.
    > Si el código se confirma en el control de código fuente, también se confirmarán estos valores de configuración de la aplicación local, por lo que debe tener cuidado de no confirmar ningún valor real en estos archivos si el código es abierto o público de cualquier forma.

## <a name="create-the-sms-messages"></a>Creación de los mensajes SMS

El parámetro `ICollector<SMSMessage>` es una recopilación de instancias de `SMSMessage` que se usa para recopilar los mensajes SMS que quiere enviar. Cuando la función termina de ejecutarse, cualquier instancia de `SMSMessage` que se haya agregado a esta colección se pasa a Twilio y se envía a los destinatarios correspondientes.

1. En la función `SendLocation`, agregue código al bucle mediante los números de teléfono que hay en `PostData` y cree un mensaje SMS para cada uno.

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

    El mensaje necesita el número de teléfono al que se enviará y un cuerpo que contenga la dirección URL de Google Maps creada a partir de la ubicación del usuario.

2. Registre cada mensaje y agréguelo a la colección `messages`.

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

Todo el método `SendLocation` aparece a continuación.

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

## <a name="test-it-out"></a>Prueba

1. Establezca la aplicación `ImHere.Functions` como el proyecto de inicio y comiéncelo sin depuración.

2. Establezca la aplicación `ImHere.UWP` como el proyecto de inicio y ejecútelo.

3. Escriba su propio número de teléfono en formato internacional (+\<código de país\>\<número de teléfono\>) en la aplicación Xamarin.Forms. Las cuentas de evaluación de Twilio puede enviar mensajes solo a números de teléfono comprobados por lo que, por ahora, solo podrá enviarse mensajes a usted mismo a menos que actualice a una cuenta de pago o compruebe otros números.

4. Haga clic en el botón **Enviar ubicación**. Si el mensaje SMS se envió correctamente, verá un mensaje en la aplicación Xamarin.Forms que indica "Location sent successfully" (La ubicación se envió correctamente).

    ![La aplicación Xamarin.Forms mostrando la ubicación como enviada](../media/7-ui-location-sent.png)

5. En los registros de consola para la función de Azure, verá que se crea y envía el mensaje. Si se produce algún error (como que el número tiene un formato incorrecto), se registrará aquí.

    ![La consola de la función de Azure mostrando que el mensaje se envió](../media/7-function-message-sent.png)

6. Revise el teléfono por si tiene un mensaje. Siga el vínculo en el mensaje para ver su ubicación.

    ![Mensaje SMS recibido en un teléfono móvil](../media/7-message-received.png)

## <a name="summary"></a>Resumen

En esta unidad aprendió a crear un enlace de Twilio para la función de Azure y a enviar un mensaje SMS con la ubicación del usuario a una función que se ejecutaba de manera local. En la unidad siguiente, publicará la función en Azure.