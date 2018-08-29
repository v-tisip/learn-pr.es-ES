<span data-ttu-id="bee13-101">La aplicación tiene una interfaz de usuario y una clase ViewModel.</span><span class="sxs-lookup"><span data-stu-id="bee13-101">The app has a UI and a ViewModel.</span></span> <span data-ttu-id="bee13-102">En esta unidad, agregará la búsqueda de ubicaciones a la clase ViewModel con Xamarin.Essentials.</span><span class="sxs-lookup"><span data-stu-id="bee13-102">In this unit, you add location lookup to the ViewModel using Xamarin.Essentials.</span></span>

## <a name="enable-location-permissions"></a><span data-ttu-id="bee13-103">Habilitar los permisos de ubicación</span><span class="sxs-lookup"><span data-stu-id="bee13-103">Enable location permissions</span></span>

<span data-ttu-id="bee13-104">Todas las plataformas móviles tienen seguridad en torno a la información del usuario y determinado hardware, como la cámara, la biblioteca de fotos y la ubicación del usuario.</span><span class="sxs-lookup"><span data-stu-id="bee13-104">All mobile platforms have security around user information and certain hardware, such as the camera, photo library, and the user's location.</span></span> <span data-ttu-id="bee13-105">Para que una aplicación pueda acceder a la ubicación del usuario, este tiene que concederle permiso, ya sea al concederle estos permisos de forma implícita durante la instalación o al decidir conceder un permiso en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="bee13-105">Before an app can access the user's location, the user has to grant permission - either by implicitly granting these permissions at install time or by choosing to grant a permission at runtime.</span></span> <span data-ttu-id="bee13-106">Cuando vea una aplicación de UWP en la tienda, la lista mostrará los permisos que necesita la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bee13-106">When you view a UWP app on the store, the listing will show the permissions that the app needs.</span></span> <span data-ttu-id="bee13-107">Al instalar la aplicación, se concede permiso de forma implícita.</span><span class="sxs-lookup"><span data-stu-id="bee13-107">By installing the app, you implicitly grant permission.</span></span> <span data-ttu-id="bee13-108">Estos permisos se configuran en un archivo de manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bee13-108">These permissions are configured in an app manifest file.</span></span>

1. <span data-ttu-id="bee13-109">En el proyecto de aplicación `ImHere.UWP`, abra el archivo `Package.appxmanifest`.</span><span class="sxs-lookup"><span data-stu-id="bee13-109">In the `ImHere.UWP` app project, open the `Package.appxmanifest` file.</span></span>

2. <span data-ttu-id="bee13-110">Vaya a la pestaña **Funcionalidades** y compruebe la funcionalidad *Ubicación*.</span><span class="sxs-lookup"><span data-stu-id="bee13-110">Head to the **Capabilities** tab and check the *Location* capability.</span></span>

    ![Pestaña de funcionalidades de UWP](../media/4-uwp-location-capability.png)

> <span data-ttu-id="bee13-112">Si quiere admitir Android o iOS, los permisos deben configurarse de forma diferente.</span><span class="sxs-lookup"><span data-stu-id="bee13-112">If you want to support Android or iOS, the permissions need to be configured differently.</span></span> <span data-ttu-id="bee13-113">Esto se detalla en la [documentación de geolocalización de Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=android#getting-started).</span><span class="sxs-lookup"><span data-stu-id="bee13-113">This is detailed in the [Xamarin.Essentials Geolocation docs](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=android#getting-started).</span></span>

## <a name="query-for-the-users-location"></a><span data-ttu-id="bee13-114">Consulta de la ubicación del usuario</span><span class="sxs-lookup"><span data-stu-id="bee13-114">Query for the user's location</span></span>

<span data-ttu-id="bee13-115">Hay dos maneras de obtener la ubicación del usuario: la última conocida o la actual.</span><span class="sxs-lookup"><span data-stu-id="bee13-115">There are two ways to get the user's location - the last known or the current.</span></span> <span data-ttu-id="bee13-116">La ubicación actual puede tardar algo en obtenerse porque puede que el dispositivo tenga que establecer un vínculo GPS y esperar a que se recupere la ubicación exacta.</span><span class="sxs-lookup"><span data-stu-id="bee13-116">The current location can take some time to get because the device may need to establish a GPS link and wait for the accurate location to be retrieved.</span></span> <span data-ttu-id="bee13-117">La forma más rápida es obtener la última ubicación conocida que haya detectado el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bee13-117">The fastest way is to get the last known location detected by the device.</span></span> <span data-ttu-id="bee13-118">La última ubicación conocida es probablemente menos precisa, pero es una llamada mucho más rápida.</span><span class="sxs-lookup"><span data-stu-id="bee13-118">The last known location is potentially less accurate but is a much faster call.</span></span> <span data-ttu-id="bee13-119">Las ubicaciones se proporcionan como la latitud y longitud en [grados decimales](https://en.wikipedia.org/wiki/Decimal_degrees) y la altitud del dispositivo en metros por encima del nivel del mar.</span><span class="sxs-lookup"><span data-stu-id="bee13-119">Locations come as the latitude and longitude in [decimal degrees](https://en.wikipedia.org/wiki/Decimal_degrees) and the altitude of the device in meters above sea level.</span></span>

1. <span data-ttu-id="bee13-120">Abra la clase `MainViewModel` en el proyecto estándar de .NET `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="bee13-120">Open the `MainViewModel` class in the `ImHere` .NET standard project.</span></span>

2. <span data-ttu-id="bee13-121">En el método `SendLocation`, realice una llamada al método estático `GetLastKnownLocationAsync` en la clase `Geolocation` en el espacio de nombres `Xamarin.Essentials`.</span><span class="sxs-lookup"><span data-stu-id="bee13-121">In the `SendLocation` method, make a call to the `GetLastKnownLocationAsync` static method on the `Geolocation` class in the `Xamarin.Essentials` namespace.</span></span>

    ```cs
    Location location = await Geolocation.GetLastKnownLocationAsync();
    ```

3. <span data-ttu-id="bee13-122">Actualice la propiedad `Message` con la ubicación del usuario si se ha encontrado una.</span><span class="sxs-lookup"><span data-stu-id="bee13-122">Update the `Message` property with the user's location if one is found.</span></span>

    ```cs
    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
    ```

<span data-ttu-id="bee13-123">A continuación se muestra el código completo de este método.</span><span class="sxs-lookup"><span data-stu-id="bee13-123">The full code for this method is below.</span></span>

```cs
async Task SendLocation()
{
    Location location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
}
```

<span data-ttu-id="bee13-124">Ejecute la aplicación y haga clic en el botón **Enviar ubicación** para ver la ubicación en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="bee13-124">Run the app and click the **Send Location** button to see the location on the UI.</span></span>

![La aplicación en ejecución muestra la ubicación del usuario](../media/4-running-app-showing-location.png)

> <span data-ttu-id="bee13-126">Esta aplicación usa la última ubicación conocida.</span><span class="sxs-lookup"><span data-stu-id="bee13-126">This app uses the last known location.</span></span> <span data-ttu-id="bee13-127">En una aplicación de calidad de producción, querrá obtener la ubicación actual precisa con un tiempo de espera y, si no se encuentra ninguna a tiempo, recurrir a la última conocida.</span><span class="sxs-lookup"><span data-stu-id="bee13-127">In a production-quality app, you would want to get the current accurate location with a time-out, and if one is not found in time, fall back to the last known.</span></span> <span data-ttu-id="bee13-128">Puede obtener más información sobre cómo hacerlo en la [documentación de geolocalización de Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation). Esta aplicación no tiene control de errores.</span><span class="sxs-lookup"><span data-stu-id="bee13-128">You can read more on how to do this in the [Xamarin.Essentials Geolocation docs](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation). This app does not have error handling.</span></span> <span data-ttu-id="bee13-129">En una aplicación de calidad de producción, debería controlar las excepciones que se produzcan, por ejemplo, si la ubicación no estaba disponible y se desencadenó una excepción.</span><span class="sxs-lookup"><span data-stu-id="bee13-129">In a production-quality app, you should handle any exceptions that occur, for example, if the location was not available and an exception was thrown.</span></span>

## <a name="summary"></a><span data-ttu-id="bee13-130">Resumen</span><span class="sxs-lookup"><span data-stu-id="bee13-130">Summary</span></span>

<span data-ttu-id="bee13-131">En esta unidad, ha aprendido a usar Xamarin.Essentials para obtener la ubicación del usuario.</span><span class="sxs-lookup"><span data-stu-id="bee13-131">In this unit, you learned how to use Xamarin.Essentials to get the user's location.</span></span> <span data-ttu-id="bee13-132">En la siguiente unidad, creará una función de Azure para que actúe como un back-end para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="bee13-132">In the next unit, you'll create an Azure function to act as a back end for the mobile app.</span></span>