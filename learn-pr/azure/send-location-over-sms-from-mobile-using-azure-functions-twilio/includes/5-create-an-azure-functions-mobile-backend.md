En este punto, la aplicación funciona con la intención de obtener la ubicación del usuario y está lista para enviarla a una función de Azure. En esta unidad, va a crear la función de Azure.

## <a name="create-an-azure-functions-project"></a>Creación de un proyecto de Azure Functions

1. Agregue un nuevo proyecto a la solución `ImHere`; haga clic con el botón derecho en la solución y seleccione *Agregar->Nuevo proyecto...*

2. En el árbol del lado izquierdo, seleccione *Visual C#->Nube* y luego seleccione *Azure Functions* en el panel del centro.

3. Asigne al proyecto el nombre "ImHere.Functions" y después haga clic en **Aceptar**.

    ![Cuadro de diálogo Agregar nuevo proyecto](../media/5-add-new-functions-project.png)

4. En el cuadro de diálogo de configuración **Nuevo proyecto**, deje la versión de Functions establecida como *Azure Functions v1 (.NET Framework)*. Seleccione *Desencadenador de HTTP*, deje la cuenta de almacenamiento establecida en *Emulador de almacenamiento* y establezca los derechos de acceso en *Anónimo*. A continuación, haga clic en **Aceptar**.

    ![Cuadro de diálogo de configuración del proyecto de Azure Functions](../media/5-configure-trigger.png)

Se creará el proyecto y dispondrá de una función predeterminada denominada `Function1`.

> Esta función se creó con el acceso anónimo. Una vez publicada en Azure, cualquier persona que sepa la dirección URL podrá llamar a esta función. En un escenario real, la protegería con algún tipo de autenticación, como [Autenticación de Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) o [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c).

## <a name="create-the-function"></a>Creación de la función

El proyecto de Azure Functions se crea con una única función de desencadenador de HTTP denominada `Function1`. La propia función se implementa como un método `Run` estático en la clase `Function1`.

1. Cambie el nombre del archivo en el Explorador de soluciones de "Function1.cs" a "SendLocation.cs". Cuando se le solicite cambiar el nombre de todas las referencias al elemento de código `Function1`, haga clic en **Sí**.

2. Cambie el nombre de la función en el atributo por "SendLocation".

    ```cs
    [FunctionName("SendLocation")]
    ```

3. Elimine el contenido de la función, excepto la primera línea que escribe un mensaje informativo en el registrador.

    ```cs
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                       TraceWriter log)
    {
        log.Info("C# HTTP trigger function processed a request.");
    }
    ```

## <a name="create-a-class-to-share-data-between-the-mobile-app-and-function"></a>Creación de una clase para compartir datos entre la aplicación móvil y la función

Cuando se envían datos a la función de Azure, se enviarán como JSON. La aplicación móvil serializará datos en JSON y la función anulará la serialización de JSON. Para mantener la coherencia de los datos entre la aplicación móvil y la función, cree un proyecto que contenga una clase para hospedar los datos de ubicación y número de teléfono. A continuación, la aplicación y la función harán referencia a este proyecto.

1. Cree un proyecto en la solución `ImHere`; para ello, haga clic con el botón derecho en la solución y seleccione *Agregar->Nuevo proyecto...*

2. En el árbol del lado izquierdo, seleccione *Visual C#->.NET Standard* y luego seleccione *Biblioteca de clases (.NET Standard)* en el panel del centro.

3. Asigne al proyecto el nombre "ImHere.Data" y luego haga clic en **Aceptar**.

    ![Cuadro de diálogo Agregar nuevo proyecto](../media/5-add-new-net-standard-project.png)

4. Elimine el archivo "Class1.cs" generado automáticamente.

5. Cree una clase en el proyecto `ImHere.Data` llamada `PostData`; para ello, haga clic con el botón derecho en el proyecto y luego seleccione *Agregar->Clase...* Asigne el nombre "PostData" a la nueva clase y haga clic en **Aceptar**.

6. Agregue las propiedades `double` para la latitud y longitud, así como una propiedad `string[]` para los números de teléfono a los que enviarlas.

    ```cs
    public class PostData
    {
        public double Latitude { get; set; }
        public double Longitude { get; set; }
        public string[] ToNumbers { get; set; }
    }
    ```

7. Agregue una referencia a este proyecto para los proyectos `ImHere.Functions` y `ImHere`; para ello, haga clic con el botón derecho en el proyecto y luego seleccione *Agregar->Referencia...* Seleccione *Proyectos* en el árbol del lado izquierdo y luego marque la casilla *ImHere.Data*.

    ![Configuración de las referencias de proyectos](../media/5-configure-project-references.png)

## <a name="read-the-data-sent-to-the-function"></a>Lectura de los datos enviados a la función

En la función de Azure, el parámetro `req` contiene la solicitud HTTP realizada y los datos contenidos en esta solicitud serán un objeto `PostData` JSON serializado.

1. Abra la clase `SendLocation` en el proyecto `ImHere.Functions`.

2. Lea el contenido de la solicitud HTTP en un objeto `PostData` y agregue una directiva de uso para el espacio de nombres `ImHere.Data`.

    ```cs
    PostData data = await req.Content.ReadAsAsync<PostData>();
    ```

3. Creación de una dirección URL de Google Maps con la latitud y longitud de `PostData`.

   ```cs
   string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
   ```

4. Registre la dirección URL.

    ```cs
    log.Info($"URL created - {url}");
    ```

5. Se devuelve un código de estado 200 para indicar que la función se ha completado sin errores.

    ```cs
    return req.CreateResponse(HttpStatusCode.OK);
    ```

La función completa se muestra a continuación.

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

## <a name="run-the-azure-function-locally"></a>Ejecución local de la función de Azure

Las funciones se pueden ejecutar a nivel local con una cuenta de almacenamiento local y el tiempo de ejecución local de Azure Functions. Este tiempo de ejecución local permite probar la función antes de implementarla en Azure.

1. Haga clic con el botón derecho en el proyecto `ImHere.Functions` en el Explorador de soluciones y seleccione *Establecer como proyecto de inicio*.

2. En el menú *Depurar*, seleccione *Iniciar sin depuración*. El tiempo de ejecución local de Azure Functions se lanzará dentro de una ventana de la consola e iniciará la función y escuchará en un puerto disponible en `localhost`.

    ![Ejecución local de la función de Azure](../media/5-function-running-locally.png)

3. Tome nota del puerto en el que la función escucha. Lo necesitará en la siguiente unidad para probar la aplicación móvil. En la imagen anterior, la función escucha en el puerto **7071**.

    ```sh
    Listening on http://localhost:7071/
    ```

4. Deje la función en ejecución para que pueda probar la aplicación móvil en la siguiente unidad.

## <a name="summary"></a>Resumen

En esta unidad, aprendió a crear un proyecto de Azure Functions en Visual Studio, agregó un proyecto compartido con un objeto de datos para compartirse entre la aplicación móvil y la función y aprendió a crear una implementación básica de la función para deserializar los datos pasados. También aprendió cómo ejecutar una función de Azure localmente. En la siguiente unidad, llamará a la función de Azure desde la aplicación móvil.