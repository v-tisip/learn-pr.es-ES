En este ejercicio, continuaremos con nuestro ejemplo de transmisión por engranaje y agregaremos la lógica para el servicio de temperatura. En concreto, vamos a recibir datos de una solicitud HTTP.

## <a name="function-requirements"></a>Requisitos de la función
Definamos algunos requisitos de la lógica:
- las temperaturas entre 0 y 25 deberían marcarse como **OK** (Correcto)
- las temperaturas entre 50 y 26 deberían marcarse como **CAUTION** (Precaución)
- las temperaturas superiores a 50 deberían marcarse como **DANGER** (Peligro)

## <a name="adding-a-function-to-an-azure-function-app"></a>Incorporación de una función a una aplicación de función de Azure

Como ya aprendimos, Azure lo ayuda cuando está aprendiendo a trabajar con Azure Functions. Una excelente característica para empezar a usar Functions es generar uno una mediante el uso de una de muchas plantillas. En este ejercicio, usará la plantilla HttpTrigger para implementar el servicio de temperatura.

1. Inicie sesión en [Azure Portal](https://portal.azure.com) con su cuenta de Azure.
1. Acceda al grupo de recursos que creó en el primer ejercicio; para ello, elija **Todos los recursos** en el menú de la izquierda y luego seleccione **escalator-functions-group**.
1. Se mostrarán los recursos del grupo. Para acceder a la aplicación de función que creó en el ejercicio anterior, seleccione el elemento **escalator-functions-xxxxxxx** (que también se indica con el icono de rayo).
  ![Acceso a la aplicación de función](../images/6-access-function-app.png)
1. La hoja mostrará información general de la aplicación de función. También hay un árbol de navegación a la izquierda que muestra las funciones, los servidores proxy o las ranuras que se definieron. Aún no tenemos una función, por lo que estará vacío. Para crear una función, mueva el mouse sobre **Función** en el árbol de navegación y haga clic en el botón **+** que aparece.
  ![Incorporación de navegación de la función](../images/5-function-add-button.png)
1. En el formulario de función predefinida de inicio rápido, seleccione el vínculo **Función personalizada** de la sección **Get started on your own** (Empezar en el suyo).
  ![Formulario de función predefinida](../images/6-custom-function.png)
1. Ahora verá una lista de plantillas. Seleccione la implementación de JavaScript de la plantilla de desencadenador HTTP.
  ![Plantilla de desencadenador HTTP](../images/6-httptrigger-template.png)
1. Aparecerá una hoja que le permitirá definir qué generará la plantilla. En este caso, le interesa generar una función de JavaScript denominada **DriveGearTemperatureService**. Después de asignar el nombre de la función, presione el botón **Crear**.
  ![Creación de formulario de desencadenador HTTP](../images/6-create-httptrigger-form.png)
1. Transcurridos unos instantes, verá el código fuente con plantilla para la función. La función predefinida espera que se pase un nombre y devolverá **Hola, {nombre}**.

    ```javascript
    module.exports = function (context, req) {
        context.log('JavaScript HTTP trigger function processed a request.');

        if (req.query.name || (req.body && req.body.name)) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "Hello " + (req.query.name || req.body.name)
            };
        }
        else {
            context.res = {
                status: 400,
                body: "Please pass a name on the query string or in the request body"
            };
        }
        context.done();
    };
    ```

1. Al lado derecho de la vista de origen, verá dos pestañas. Puede ver todos los archivos que admiten la función en la pestaña **Ver archivos**. Puede seleccionar **function.json** para ver la configuración de la función. Aquí puede ver httpTrigger definido, así como el enlace de salida. Esta configuración describe que una solicitud HTTP inicia la función y el enlace de salida describe que la respuesta se enviará como una respuesta HTTP.

    ```javascript
    {
      "disabled": false,
      "bindings": [
        {
          "authLevel": "function",
          "type": "httpTrigger",
          "direction": "in",
          "name": "req"
        },
        {
          "type": "http",
          "direction": "out",
          "name": "res"
        }
      ]
    }
    ```

## <a name="running-the-premade-azure-function"></a>Ejecución de la función predefinida de Azure

Para ejecutar la función, puede iniciar una solicitud HTTP desde cURL en un símbolo del sistema. Para buscar la dirección URL del punto de conexión, vuelva a su código de función y seleccione el **obtener la dirección URL de función** vínculo. Copie este vínculo en el Portapapeles.  La dirección URL debe ser similar a la siguiente: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Obtener dirección URL del punto de conexión](../images/6-get-function-url.png)

Con esa dirección URL, ejecute un comando de cURL para iniciar la función (reemplace la dirección URL por una propia):

```bash
curl --header "Content-Type: application/json" --request POST --data "{\"name\": \"Azure Function\"}" https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg==
```

![Respuesta de cURL de función predefinida](../images/6-premadefunction-curl.png)

## <a name="adding-business-logic-to-the-function"></a>Incorporación de lógica de negocios a la función

La función espera una matriz de lecturas de temperatura por parte del cliente. Este es un ejemplo de cuerpo de la solicitud:

```javascript
{
    "readings": [
        {
            "driveGearId": 1,
            "timestamp": 1534263995,
            "temperature": 23
        },
        {
            "driveGearId": 3,
            "timestamp": 1534264048,
            "temperature": 45
        },
        {
            "driveGearId": 18,
            "timestamp": 1534264050,
            "temperature": 55
        }
    ]
}
```

Modifique el código de la función predefinida para implementar la lógica de negocios necesaria. Abra el archivo index.js y reemplácelo por la siguiente lista:

```javascript
module.exports = function (context, req) {
    context.log('Drive Gear Temperature Service triggered');
    if (req.body && req.body.readings) {
        for(var i=0; i<req.body.readings.length; i++){
            var reading = req.body.readings[i];
            if(reading.temperature<=25){
                context.log('Reading is OK');
                reading.status = 'OK';
                continue;
            }
            if(reading.temperature<=50){
                context.log('Reading is CAUTION');
                reading.status = 'CAUTION';
                continue;
            }
            context.log('Reading is DANGER');
            reading.status = 'DANGER'
        }
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: {
                "readings": req.body.readings
            }
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please send an array of readings in the request body"
        };
    }
    context.done();
};
```

Tenga en cuenta las instrucciones de registro. Cuando se ejecute la función, agregarán los mensajes en la ventana de registro.

## <a name="testing-your-business-logic"></a>Prueba de la lógica de negocios

Abra la ventana de prueba desde el menú flotante del lado derecho y pegue la solicitud de ejemplo anterior en el cuadro de texto del cuerpo de solicitud. Presione el botón **Ejecutar** y vea el resultado. También puede abrir la ventana de registro desde el menú flotante inferior para ver las instrucciones de registro en el registro.
![Prueba de la lógica de negocios](../images/6-portal-testing.png) En los datos JSON de la ventana de salida puede ver que el campo de estado de la temperatura se agregó correctamente a cada una de las lecturas. También puede visitar el panel de supervisión para ver que la solicitud se registró en Application Insights.
![Solicitud en Application Insights](../images/6-app-insights.png)
