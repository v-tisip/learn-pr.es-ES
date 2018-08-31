<span data-ttu-id="87429-101">Se ejecuta la aplicación móvil y se ha creado la versión inicial de la función de Azure.</span><span class="sxs-lookup"><span data-stu-id="87429-101">The mobile app runs and the initial version of the Azure function has been created.</span></span> <span data-ttu-id="87429-102">En esta unidad, llamará a la función de Azure desde la aplicación móvil, pasando la ubicación del usuario y la lista de números de teléfono a los que el usuario quiere enviar mensajes SMS.</span><span class="sxs-lookup"><span data-stu-id="87429-102">In this unit, you call the Azure function from the mobile app, passing in the user's location and the list of phone numbers the user wants to send SMS messages to.</span></span>

## <a name="calling-the-azure-function-from-the-mobile-app"></a><span data-ttu-id="87429-103">Llamar a la función de Azure desde la aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="87429-103">Calling the Azure function from the mobile app</span></span>

1. <span data-ttu-id="87429-104">Abra `MainViewModel`.</span><span class="sxs-lookup"><span data-stu-id="87429-104">Open the `MainViewModel`.</span></span>

2. <span data-ttu-id="87429-105">En esta clase, agregue un campo `HttpClient` privado denominado `client`.</span><span class="sxs-lookup"><span data-stu-id="87429-105">In this class, add a private `HttpClient` field called `client`.</span></span> <span data-ttu-id="87429-106">Deberá agregar una referencia al espacio de nombres `System.Net.Http`.</span><span class="sxs-lookup"><span data-stu-id="87429-106">You'll need to add a reference to the `System.Net.Http` namespace.</span></span>

    ```cs
    HttpClient client = new HttpClient();
    ```

3. <span data-ttu-id="87429-107">Agregue un campo constante para la URL base de la función.</span><span class="sxs-lookup"><span data-stu-id="87429-107">Add a constant field for the base URL for the function.</span></span> <span data-ttu-id="87429-108">Establézcalo en la dirección en la que está escuchando la instancia local de Azure Functions Runtime.</span><span class="sxs-lookup"><span data-stu-id="87429-108">Set this to the address that the local Azure Functions runtime is listening on.</span></span> <span data-ttu-id="87429-109">Una vez que la función se implemente en Azure, puede cambiar esta constante para que sea la URL de Azure.</span><span class="sxs-lookup"><span data-stu-id="87429-109">Once the function is deployed to Azure, this constant can be changed to be the Azure URL.</span></span>

    ```cs
    const string baseUrl = "http://localhost:7071";
    ```

4. <span data-ttu-id="87429-110">Dentro del método `SendLocation`, una vez que se haya encontrado la ubicación, cree una instancia de `PostData` mediante la ubicación y la lista de números de teléfono que ha especificado el usuario.</span><span class="sxs-lookup"><span data-stu-id="87429-110">Inside the `SendLocation` method, after the location has been found, create a new instance of `PostData` using the location and the list of phone numbers entered by the user.</span></span> <span data-ttu-id="87429-111">Tendrá que agregar una directiva using al espacio de nombres `ImHere.Data`.</span><span class="sxs-lookup"><span data-stu-id="87429-111">You'll need to add a using directive for the `ImHere.Data` namespace.</span></span>

    ```cs
    PostData postData = new PostData
    {
        Latitude = location.Latitude,
        Longitude = location.Longitude,
        ToNumbers = PhoneNumbers.Split('\n')
    };
    ```

    > <span data-ttu-id="87429-112">Esta supone que se han escrito los números de teléfono en el formato correcto, uno por línea en el control `Editor`.</span><span class="sxs-lookup"><span data-stu-id="87429-112">This assumes that the phone numbers have been entered in the correct format, one per line in the `Editor` control.</span></span> <span data-ttu-id="87429-113">En una aplicación de calidad de producción, habría una validación en torno a este proceso para garantizar que se han escrito uno o varios números de teléfono y que estos estaban en el formato correcto.</span><span class="sxs-lookup"><span data-stu-id="87429-113">In a production-quality app, there would be validation around this to ensure one or more phone numbers were entered and were in the correct format.</span></span>

5. <span data-ttu-id="87429-114">La forma más fácil de serializar `PostData` como JSON es usar el paquete de NuGet Newtonsoft.JSON.</span><span class="sxs-lookup"><span data-stu-id="87429-114">To serialize the `PostData` as JSON, the easiest way is to use the Newtonsoft.JSON NuGet package.</span></span> <span data-ttu-id="87429-115">Agregue este paquete de NuGet al proyecto `ImHere` de la misma manera que ha agregado Xamarin.Essentials en una unidad anterior.</span><span class="sxs-lookup"><span data-stu-id="87429-115">Add this NuGet package to the `ImHere` project in the same way that you added Xamarin.Essentials in an earlier unit.</span></span>

6. <span data-ttu-id="87429-116">Serialice `PostData` a una `string` mediante la clase estática `JsonConvert`.</span><span class="sxs-lookup"><span data-stu-id="87429-116">Serialize the `PostData` to a `string` using the `JsonConvert` static class.</span></span> <span data-ttu-id="87429-117">Tendrá que agregar una directiva using al espacio de nombres `Newtonsoft.Json`.</span><span class="sxs-lookup"><span data-stu-id="87429-117">You'll need to add a using directive for the `Newtonsoft.Json` namespace.</span></span> <span data-ttu-id="87429-118">Codifique esta cadena en una clase `StringContent` para que se pueda pasar a la función de Azure como JSON.</span><span class="sxs-lookup"><span data-stu-id="87429-118">Encode this string into a `StringContent` class so that it can be passed to the Azure function as JSON.</span></span>

    ```cs
    string data = JsonConvert.SerializeObject(postData);
    StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
    ```

7. <span data-ttu-id="87429-119">Publique estos datos en la función y obtenga el resultado.</span><span class="sxs-lookup"><span data-stu-id="87429-119">Post this data to the function and get the result back.</span></span>

   ```cs
    HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                        content);
   ```

   <span data-ttu-id="87429-120">Se accede a las funciones de Azure mediante `/api/<function name>`, por lo que, suponiendo que el puerto que ha elegido la instancia local de Functions Runtime sea el 7071, se podrá acceder a la función `SendLocation` desde `http://localhost:7071/api/SendLocation`.</span><span class="sxs-lookup"><span data-stu-id="87429-120">Azure functions are accessed using `/api/<function name>`, so assuming the port chosen by the local Functions runtime is 7071, the `SendLocation` function will be accessible at `http://localhost:7071/api/SendLocation`.</span></span>

8. <span data-ttu-id="87429-121">En función del resultado, se muestra un mensaje en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="87429-121">Depending on the result, show a message on the UI.</span></span>

    ```cs
    if (result.IsSuccessStatusCode)
        Message = "Location sent successfully";
    else
        Message = $"Error - {result.ReasonPhrase}";
    ```

<span data-ttu-id="87429-122">A continuación se muestra el código completo de los nuevos campos y el método `SendLocation`.</span><span class="sxs-lookup"><span data-stu-id="87429-122">The full code for the new fields and the `SendLocation` method is below.</span></span>

```cs
HttpClient client = new HttpClient();
const string baseUrl = "http://localhost:7071";

async Task SendLocation()
{
    Location location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";

        PostData postData = new PostData
        {
            Latitude = location.Latitude,
            Longitude = location.Longitude,
            ToNumbers = PhoneNumbers.Split('\n')
        };

        string data = JsonConvert.SerializeObject(postData);
        StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
        HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                            content);

        if (result.IsSuccessStatusCode)
            Message = "Location sent successfully";
        else
            Message = $"Error - {result.ReasonPhrase}";
    }
}
```

## <a name="testing-it-out"></a><span data-ttu-id="87429-123">Prueba</span><span class="sxs-lookup"><span data-stu-id="87429-123">Testing it out</span></span>

1. <span data-ttu-id="87429-124">Asegúrese de que la función de Azure aún se está ejecutando de forma local y que el puerto coincide con el método `SendLocation`.</span><span class="sxs-lookup"><span data-stu-id="87429-124">Make sure the Azure function is still running locally and the port matches the `SendLocation` method.</span></span>

2. <span data-ttu-id="87429-125">Establezca la aplicación de UWP como la aplicación de inicio y ejecútela.</span><span class="sxs-lookup"><span data-stu-id="87429-125">Set the UWP app as the startup app and run it.</span></span> <span data-ttu-id="87429-126">Haga clic en el botón **Enviar ubicación**.</span><span class="sxs-lookup"><span data-stu-id="87429-126">Click the **Send Location** button.</span></span> <span data-ttu-id="87429-127">Verá la salida en la ventana de la consola de la instancia de Functions Runtime, en donde se muestra la función a la que se llama, y el registro, en donde se muestra la URL generada.</span><span class="sxs-lookup"><span data-stu-id="87429-127">You'll see output in the Functions runtime console window showing the function being called, and the logging showing the generated URL.</span></span>

    ![Salida de la función a la que se llama](../media-drafts/6-function-called.png)

3. <span data-ttu-id="87429-129">Para probar la generación de URL, péguela desde la consola en un explorador.</span><span class="sxs-lookup"><span data-stu-id="87429-129">To test the URL generation, paste it from the console into a browser.</span></span> <span data-ttu-id="87429-130">Debería mostrar su ubicación actual.</span><span class="sxs-lookup"><span data-stu-id="87429-130">It should show your current location.</span></span>

## <a name="summary"></a><span data-ttu-id="87429-131">Resumen</span><span class="sxs-lookup"><span data-stu-id="87429-131">Summary</span></span>

<span data-ttu-id="87429-132">En esta unidad, ha aprendido a llamar a una función de Azure desde la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="87429-132">In this unit, you learned how to call an Azure function from the mobile app.</span></span> <span data-ttu-id="87429-133">Esta llamada ha pasado la ubicación del usuario y los números de teléfono que se han escrito como JSON.</span><span class="sxs-lookup"><span data-stu-id="87429-133">This call passed the user's location and the phone numbers they entered as JSON.</span></span> <span data-ttu-id="87429-134">En la unidad siguiente, enlazará la función de Azure con Twilio para enviar esta ubicación como un mensaje SMS.</span><span class="sxs-lookup"><span data-stu-id="87429-134">In the next unit, you'll bind the Azure function to Twilio to send this location as an SMS message.</span></span>