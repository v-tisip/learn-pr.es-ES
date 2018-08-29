<span data-ttu-id="6983d-101">En este ejercicio, continuaremos con nuestro ejemplo de transmisión por engranaje y agregaremos la lógica para el servicio de temperatura.</span><span class="sxs-lookup"><span data-stu-id="6983d-101">In this exercise, we'll continue with our gear drive example and add the logic for the temperature service.</span></span> <span data-ttu-id="6983d-102">En concreto, vamos a recibir datos de una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="6983d-102">Specifically, we're going to receive data from an HTTP request.</span></span>

## <a name="function-requirements"></a><span data-ttu-id="6983d-103">Requisitos de la función</span><span class="sxs-lookup"><span data-stu-id="6983d-103">Function requirements</span></span>
<span data-ttu-id="6983d-104">Definamos algunos requisitos de la lógica:</span><span class="sxs-lookup"><span data-stu-id="6983d-104">Let's define some requirements for our logic:</span></span>
- <span data-ttu-id="6983d-105">las temperaturas entre 0 y 25 deberían marcarse como **OK** (Correcto)</span><span class="sxs-lookup"><span data-stu-id="6983d-105">temperatures between 0-25 should be flagged as **OK**</span></span>
- <span data-ttu-id="6983d-106">las temperaturas entre 50 y 26 deberían marcarse como **CAUTION** (Precaución)</span><span class="sxs-lookup"><span data-stu-id="6983d-106">temperatures between 26-50 should be flagged as **CAUTION**</span></span>
- <span data-ttu-id="6983d-107">las temperaturas superiores a 50 deberían marcarse como **DANGER** (Peligro)</span><span class="sxs-lookup"><span data-stu-id="6983d-107">temperatures above 50 should be flagged as **DANGER**</span></span>

## <a name="adding-a-function-to-an-azure-function-app"></a><span data-ttu-id="6983d-108">Incorporación de una función a una aplicación de función de Azure</span><span class="sxs-lookup"><span data-stu-id="6983d-108">Adding a function to an Azure function app</span></span>

<span data-ttu-id="6983d-109">Como ya aprendimos, Azure lo ayuda cuando está aprendiendo a trabajar con Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="6983d-109">As we have already learned, Azure provides a helping hand when you're learning how to work with Azure Functions.</span></span> <span data-ttu-id="6983d-110">Una excelente característica para empezar a usar Functions es generar uno una mediante el uso de una de muchas plantillas.</span><span class="sxs-lookup"><span data-stu-id="6983d-110">One great feature to get your feet wet with Functions is to generate one using one of many templates.</span></span> <span data-ttu-id="6983d-111">En este ejercicio, usará la plantilla HttpTrigger para implementar el servicio de temperatura.</span><span class="sxs-lookup"><span data-stu-id="6983d-111">In this exercise, you will be using the HttpTrigger template to implement the temperature service.</span></span>

1. <span data-ttu-id="6983d-112">Inicie sesión en [Azure Portal](https://portal.azure.com) con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="6983d-112">Sign in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
1. <span data-ttu-id="6983d-113">Acceda al grupo de recursos que creó en el primer ejercicio; para ello, elija **Todos los recursos** en el menú de la izquierda y luego seleccione **escalator-functions-group**.</span><span class="sxs-lookup"><span data-stu-id="6983d-113">Access the resource group you created in the first exercise by choosing **All resources** in the left-hand menu, and then selecting **escalator-functions-group**.</span></span>
1. <span data-ttu-id="6983d-114">Se mostrarán los recursos del grupo.</span><span class="sxs-lookup"><span data-stu-id="6983d-114">The resources for the group will then be displayed.</span></span> <span data-ttu-id="6983d-115">Para acceder a la aplicación de función que creó en el ejercicio anterior, seleccione el elemento **escalator-functions-xxxxxxx** (que también se indica con el icono de rayo).</span><span class="sxs-lookup"><span data-stu-id="6983d-115">Access the function app that you created in the previous exercise by selecting the **escalator-functions-xxxxxxx** item (also indicated by the lightning bolt icon).</span></span>
  <span data-ttu-id="6983d-116">![Acceso a la aplicación de función](../images/6-access-function-app.png)</span><span class="sxs-lookup"><span data-stu-id="6983d-116">![Access the function app](../images/6-access-function-app.png)</span></span>
1. <span data-ttu-id="6983d-117">La hoja mostrará información general de la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="6983d-117">The blade will show an overview of your function app.</span></span> <span data-ttu-id="6983d-118">También hay un árbol de navegación a la izquierda que muestra las funciones, los servidores proxy o las ranuras que se definieron.</span><span class="sxs-lookup"><span data-stu-id="6983d-118">There is also a navigation tree on the left that shows any functions, proxies or slots that are defined.</span></span> <span data-ttu-id="6983d-119">Aún no tenemos una función, por lo que estará vacío.</span><span class="sxs-lookup"><span data-stu-id="6983d-119">We don't have a function yet, so this  will be empty.</span></span> <span data-ttu-id="6983d-120">Para crear una función, mueva el mouse sobre **Función** en el árbol de navegación y haga clic en el botón **+** que aparece.</span><span class="sxs-lookup"><span data-stu-id="6983d-120">To create a function, move your mouse over **Function** in the navigation tree and click  the **+** button that appears.</span></span>
  <span data-ttu-id="6983d-121">![Incorporación de navegación de la función](../images/5-function-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="6983d-121">![Add function navigation](../images/5-function-add-button.png)</span></span>
1. <span data-ttu-id="6983d-122">En el formulario de función predefinida de inicio rápido, seleccione el vínculo **Función personalizada** de la sección **Get started on your own** (Empezar en el suyo).</span><span class="sxs-lookup"><span data-stu-id="6983d-122">In the quickstart premade function form, select the **Custom function** link in the **Get started on your own** section.</span></span>
  <span data-ttu-id="6983d-123">![Formulario de función predefinida](../images/6-custom-function.png)</span><span class="sxs-lookup"><span data-stu-id="6983d-123">![Premade function form](../images/6-custom-function.png)</span></span>
1. <span data-ttu-id="6983d-124">Ahora verá una lista de plantillas.</span><span class="sxs-lookup"><span data-stu-id="6983d-124">You are now presented with a list of templates.</span></span> <span data-ttu-id="6983d-125">Seleccione la implementación de JavaScript de la plantilla de desencadenador HTTP.</span><span class="sxs-lookup"><span data-stu-id="6983d-125">Select the JavaScript implementation of the HTTP trigger template.</span></span>
  <span data-ttu-id="6983d-126">![Plantilla de desencadenador HTTP](../images/6-httptrigger-template.png)</span><span class="sxs-lookup"><span data-stu-id="6983d-126">![HTTP trigger template](../images/6-httptrigger-template.png)</span></span>
1. <span data-ttu-id="6983d-127">Aparecerá una hoja que le permitirá definir qué generará la plantilla.</span><span class="sxs-lookup"><span data-stu-id="6983d-127">A blade will appear, allowing you to define what the template will generate.</span></span> <span data-ttu-id="6983d-128">En este caso, le interesa generar una función de JavaScript denominada **DriveGearTemperatureService**.</span><span class="sxs-lookup"><span data-stu-id="6983d-128">In this case, you are interested in generating a JavaScript function named **DriveGearTemperatureService**.</span></span> <span data-ttu-id="6983d-129">Después de asignar el nombre de la función, presione el botón **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6983d-129">After you have named your function, press the **Create** button.</span></span>
  <span data-ttu-id="6983d-130">![Creación de formulario de desencadenador HTTP](../images/6-create-httptrigger-form.png)</span><span class="sxs-lookup"><span data-stu-id="6983d-130">![Create HTTP trigger form](../images/6-create-httptrigger-form.png)</span></span>
1. <span data-ttu-id="6983d-131">Transcurridos unos instantes, verá el código fuente con plantilla para la función.</span><span class="sxs-lookup"><span data-stu-id="6983d-131">After a few moments, you will be presented with the templated source code for your function.</span></span> <span data-ttu-id="6983d-132">La función predefinida espera que se pase un nombre y devolverá **Hola, {nombre}**.</span><span class="sxs-lookup"><span data-stu-id="6983d-132">The premade function expects a name to be passed in, and it will return **Hello, {name}**.</span></span>

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

1. <span data-ttu-id="6983d-133">Al lado derecho de la vista de origen, verá dos pestañas.</span><span class="sxs-lookup"><span data-stu-id="6983d-133">On the right-hand side of the source view, you will see two tabs.</span></span> <span data-ttu-id="6983d-134">Puede ver todos los archivos que admiten la función en la pestaña **Ver archivos**. Puede seleccionar **function.json** para ver la configuración de la función.</span><span class="sxs-lookup"><span data-stu-id="6983d-134">You are able to view all the files supporting the function in the **View files** tab. You can select **function.json** to view the configuration of the function.</span></span> <span data-ttu-id="6983d-135">Aquí puede ver httpTrigger definido, así como el enlace de salida.</span><span class="sxs-lookup"><span data-stu-id="6983d-135">Here you can see the httpTrigger defined, as well as the output binding.</span></span> <span data-ttu-id="6983d-136">Esta configuración describe que una solicitud HTTP inicia la función y el enlace de salida describe que la respuesta se enviará como una respuesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="6983d-136">This configuration describes that the function is initiated by an HTTP request, and the output binding describes that the response will be sent as an HTTP response.</span></span>

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

## <a name="running-the-premade-azure-function"></a><span data-ttu-id="6983d-137">Ejecución de la función predefinida de Azure</span><span class="sxs-lookup"><span data-stu-id="6983d-137">Running the premade Azure function</span></span>

<span data-ttu-id="6983d-138">Para ejecutar la función, puede iniciar una solicitud HTTP desde cURL en un símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="6983d-138">To run the function, you can initiate an HTTP request from cURL from a command prompt.</span></span> <span data-ttu-id="6983d-139">Para buscar la dirección URL del punto de conexión, vuelva a su código de función y seleccione el **obtener la dirección URL de función** vínculo.</span><span class="sxs-lookup"><span data-stu-id="6983d-139">To find the endpoint URL, return to your function code and select the **Get function URL** link.</span></span> <span data-ttu-id="6983d-140">Copie este vínculo en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="6983d-140">Copy this link to your clipboard.</span></span>  <span data-ttu-id="6983d-141">La dirección URL debe ser similar a la siguiente: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Obtener dirección URL del punto de conexión](../images/6-get-function-url.png)</span><span class="sxs-lookup"><span data-stu-id="6983d-141">Your URL should look something similar to the following: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Get endpoint URL](../images/6-get-function-url.png)</span></span>

<span data-ttu-id="6983d-142">Con esa dirección URL, ejecute un comando de cURL para iniciar la función (reemplace la dirección URL por una propia):</span><span class="sxs-lookup"><span data-stu-id="6983d-142">With that URL, run a cURL command to initiate your function (replacing the URL with your own):</span></span>

```bash
curl --header "Content-Type: application/json" --request POST --data "{\"name\": \"Azure Function\"}" https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg==
```

![Respuesta de cURL de función predefinida](../images/6-premadefunction-curl.png)

## <a name="adding-business-logic-to-the-function"></a><span data-ttu-id="6983d-144">Incorporación de lógica de negocios a la función</span><span class="sxs-lookup"><span data-stu-id="6983d-144">Adding business logic to the function</span></span>

<span data-ttu-id="6983d-145">La función espera una matriz de lecturas de temperatura por parte del cliente.</span><span class="sxs-lookup"><span data-stu-id="6983d-145">Our function is expecting an array of temperature readings from the customer.</span></span> <span data-ttu-id="6983d-146">Este es un ejemplo de cuerpo de la solicitud:</span><span class="sxs-lookup"><span data-stu-id="6983d-146">This is an example of the request body:</span></span>

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

<span data-ttu-id="6983d-147">Modifique el código de la función predefinida para implementar la lógica de negocios necesaria.</span><span class="sxs-lookup"><span data-stu-id="6983d-147">Modify the premade function code to implement the required business logic.</span></span> <span data-ttu-id="6983d-148">Abra el archivo index.js y reemplácelo por la siguiente lista:</span><span class="sxs-lookup"><span data-stu-id="6983d-148">Open the index.js file, and replace it with the following listing:</span></span>

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

<span data-ttu-id="6983d-149">Tenga en cuenta las instrucciones de registro.</span><span class="sxs-lookup"><span data-stu-id="6983d-149">Notice the log statements.</span></span> <span data-ttu-id="6983d-150">Cuando se ejecute la función, agregarán los mensajes en la ventana de registro.</span><span class="sxs-lookup"><span data-stu-id="6983d-150">When the function runs, they will add messages in the log window.</span></span>

## <a name="testing-your-business-logic"></a><span data-ttu-id="6983d-151">Prueba de la lógica de negocios</span><span class="sxs-lookup"><span data-stu-id="6983d-151">Testing your business logic</span></span>

<span data-ttu-id="6983d-152">Abra la ventana de prueba desde el menú flotante del lado derecho y pegue la solicitud de ejemplo anterior en el cuadro de texto del cuerpo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="6983d-152">Open the test window from the right-hand side flyout menu, and paste the sample request from above into the request body text box.</span></span> <span data-ttu-id="6983d-153">Presione el botón **Ejecutar** y vea el resultado.</span><span class="sxs-lookup"><span data-stu-id="6983d-153">Press the **Run** button and view the output.</span></span> <span data-ttu-id="6983d-154">También puede abrir la ventana de registro desde el menú flotante inferior para ver las instrucciones de registro en el registro.</span><span class="sxs-lookup"><span data-stu-id="6983d-154">You can also open the log window from the bottom flyout menu to see the logging statements in the log.</span></span>
<span data-ttu-id="6983d-155">![Prueba de la lógica de negocios](../images/6-portal-testing.png) En los datos JSON de la ventana de salida puede ver que el campo de estado de la temperatura se agregó correctamente a cada una de las lecturas.</span><span class="sxs-lookup"><span data-stu-id="6983d-155">![Testing the business Logic](../images/6-portal-testing.png) You can see from the JSON data in the output window that our temperature status field has been added to each of the readings correctly.</span></span> <span data-ttu-id="6983d-156">También puede visitar el panel de supervisión para ver que la solicitud se registró en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6983d-156">You may also visit the Monitor dashboard to see that the request has been logged to Application Insights.</span></span>
<span data-ttu-id="6983d-157">![Solicitud en Application Insights](../images/6-app-insights.png)</span><span class="sxs-lookup"><span data-stu-id="6983d-157">![Request in Application Insights](../images/6-app-insights.png)</span></span>
