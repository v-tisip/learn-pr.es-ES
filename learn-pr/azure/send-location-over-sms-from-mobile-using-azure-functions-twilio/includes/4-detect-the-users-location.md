La aplicación tiene una interfaz de usuario y una clase ViewModel. En esta unidad, agregará la búsqueda de ubicaciones a la clase ViewModel con Xamarin.Essentials.

## <a name="enable-location-permissions"></a>Habilitar los permisos de ubicación

Todas las plataformas móviles tienen seguridad en torno a la información del usuario y determinado hardware, como la cámara, la biblioteca de fotos y la ubicación del usuario. Para que una aplicación pueda acceder a la ubicación del usuario, este tiene que concederle permiso, ya sea al concederle estos permisos de forma implícita durante la instalación o al decidir conceder un permiso en tiempo de ejecución. Cuando vea una aplicación de UWP en la tienda, la lista mostrará los permisos que necesita la aplicación. Al instalar la aplicación, se concede permiso de forma implícita. Estos permisos se configuran en un archivo de manifiesto de la aplicación.

1. En el proyecto de aplicación `ImHere.UWP`, abra el archivo `Package.appxmanifest`.

2. Vaya a la pestaña **Funcionalidades** y compruebe la funcionalidad *Ubicación*.

    ![Pestaña de funcionalidades de UWP](../media-drafts/4-uwp-location-capability.png)

> Si quiere admitir Android o iOS, los permisos deben configurarse de forma diferente. Esto se detalla en la [documentación de geolocalización de Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=android#getting-started).

## <a name="query-for-the-users-location"></a>Consulta de la ubicación del usuario

Hay dos maneras de obtener la ubicación del usuario: la última conocida o la actual. La ubicación actual puede tardar algo en obtenerse porque puede que el dispositivo tenga que establecer un vínculo GPS y esperar a que se recupere la ubicación exacta. La forma más rápida es obtener la última ubicación conocida que haya detectado el dispositivo. La última ubicación conocida es probablemente menos precisa, pero es una llamada mucho más rápida. Las ubicaciones se proporcionan como la latitud y longitud en [grados decimales](https://en.wikipedia.org/wiki/Decimal_degrees) y la altitud del dispositivo en metros por encima del nivel del mar.

1. Abra la clase `MainViewModel` en el proyecto estándar de .NET `ImHere`.

2. En el método `SendLocation`, realice una llamada al método estático `GetLastKnownLocationAsync` en la clase `Geolocation` en el espacio de nombres `Xamarin.Essentials`.

    ```cs
    Location location = await Geolocation.GetLastKnownLocationAsync();
    ```

3. Actualice la propiedad `Message` con la ubicación del usuario si se ha encontrado una.

    ```cs
    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
    ```

A continuación se muestra el código completo de este método.

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

Ejecute la aplicación y haga clic en el botón **Enviar ubicación** para ver la ubicación en la interfaz de usuario.

![La aplicación en ejecución muestra la ubicación del usuario](../media-drafts/4-running-app-showing-location.png)

> Esta aplicación usa la última ubicación conocida. En una aplicación de calidad de producción, querrá obtener la ubicación actual precisa con un tiempo de espera y, si no se encuentra ninguna a tiempo, recurrir a la última conocida. Puede obtener más información sobre cómo hacerlo en la [documentación de geolocalización de Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation). Esta aplicación no tiene control de errores. En una aplicación de calidad de producción, debería controlar las excepciones que se produzcan, por ejemplo, si la ubicación no estaba disponible y se desencadenó una excepción.

## <a name="summary"></a>Resumen

En esta unidad, ha aprendido a usar Xamarin.Essentials para obtener la ubicación del usuario. En la siguiente unidad, creará una función de Azure para que actúe como un back-end para la aplicación móvil.