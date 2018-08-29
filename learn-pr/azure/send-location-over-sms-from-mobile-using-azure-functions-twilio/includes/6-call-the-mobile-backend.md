Se ejecuta la aplicación móvil y se ha creado la versión inicial de la función de Azure. En esta unidad, llamará a la función de Azure desde la aplicación móvil, pasando la ubicación del usuario y la lista de números de teléfono a los que el usuario quiere enviar mensajes SMS.

## <a name="calling-the-azure-function-from-the-mobile-app"></a>Llamar a la función de Azure desde la aplicación móvil

1. Abra `MainViewModel`.

2. En esta clase, agregue un campo `HttpClient` privado denominado `client`. Deberá agregar una referencia al espacio de nombres `System.Net.Http`.

    ```cs
    HttpClient client = new HttpClient();
    ```

3. Agregue un campo constante para la URL base de la función. Establézcalo en la dirección en la que está escuchando la instancia local de Azure Functions Runtime. Una vez que la función se implemente en Azure, puede cambiar esta constante para que sea la URL de Azure.

    ```cs
    const string baseUrl = "http://localhost:7071";
    ```

4. Dentro del método `SendLocation`, una vez que se haya encontrado la ubicación, cree una instancia de `PostData` mediante la ubicación y la lista de números de teléfono que ha especificado el usuario. Tendrá que agregar una directiva using al espacio de nombres `ImHere.Data`.

    ```cs
    PostData postData = new PostData
    {
        Latitude = location.Latitude,
        Longitude = location.Longitude,
        ToNumbers = PhoneNumbers.Split('\n')
    };
    ```

    > Esta supone que se han escrito los números de teléfono en el formato correcto, uno por línea en el control `Editor`. En una aplicación de calidad de producción, habría una validación en torno a este proceso para garantizar que se han escrito uno o varios números de teléfono y que estos estaban en el formato correcto.

5. La forma más fácil de serializar `PostData` como JSON es usar el paquete de NuGet Newtonsoft.JSON. Agregue este paquete de NuGet al proyecto `ImHere` de la misma manera que ha agregado Xamarin.Essentials en una unidad anterior.

6. Serialice `PostData` a una `string` mediante la clase estática `JsonConvert`. Tendrá que agregar una directiva using al espacio de nombres `Newtonsoft.Json`. Codifique esta cadena en una clase `StringContent` para que se pueda pasar a la función de Azure como JSON.

    ```cs
    string data = JsonConvert.SerializeObject(postData);
    StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
    ```

7. Publique estos datos en la función y obtenga el resultado.

   ```cs
    HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                        content);
   ```

   Se accede a las funciones de Azure mediante `/api/<function name>`, por lo que, suponiendo que el puerto que ha elegido la instancia local de Functions Runtime sea el 7071, se podrá acceder a la función `SendLocation` desde `http://localhost:7071/api/SendLocation`.

8. En función del resultado, se muestra un mensaje en la interfaz de usuario.

    ```cs
    if (result.IsSuccessStatusCode)
        Message = "Location sent successfully";
    else
        Message = $"Error - {result.ReasonPhrase}";
    ```

A continuación se muestra el código completo de los nuevos campos y el método `SendLocation`.

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

## <a name="testing-it-out"></a>Prueba

1. Asegúrese de que la función de Azure aún se está ejecutando de forma local y que el puerto coincide con el método `SendLocation`.

2. Establezca la aplicación de UWP como la aplicación de inicio y ejecútela. Haga clic en el botón **Enviar ubicación**. Verá la salida en la ventana de la consola de la instancia de Functions Runtime, en donde se muestra la función a la que se llama, y el registro, en donde se muestra la URL generada.

    ![Salida de la función a la que se llama](../media/6-function-called.png)

3. Para probar la generación de URL, péguela desde la consola en un explorador. Debería mostrar su ubicación actual.

## <a name="summary"></a>Resumen

En esta unidad, ha aprendido a llamar a una función de Azure desde la aplicación móvil. Esta llamada ha pasado la ubicación del usuario y los números de teléfono que se han escrito como JSON. En la unidad siguiente, enlazará la función de Azure con Twilio para enviar esta ubicación como un mensaje SMS.