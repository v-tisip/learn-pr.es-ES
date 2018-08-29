Ahora que tenemos una aplicación de función creada, aprenderemos a crear, configurar y ejecutar una función de Azure.

### <a name="triggers"></a>Desencadenadores
Las funciones de Azure se controlan mediante eventos y se ejecutan en respuesta a un evento, como recibir una solicitud HTTP o agregar un mensaje a una cola. 

El tipo de evento que inicia la función se denomina desencadenador. Las funciones de Azure requieren al menos que se configure un desencadenador. De lo contrario, no tendríamos forma de ejecutar la función.

 Azure admite una gran variedad de desencadenadores, incluidos:
* HTTPTrigger
* TimerTrigger
* Webhook de GitHub
* CosmosDBTrigger
* BlobTrigger
* QueueTrigger
* EventHubTrigger
* ServiceBusQueueTrigger
* ServiceBusTopicTrigger

### <a name="bindings"></a>Enlaces
Los enlaces de función de Azure son una manera declarativa de conectarse a los datos de la función mediante programación.

Los enlaces son la conexión con los servicios de datos. En una función de Azure con cero, uno o más enlaces permiten acceder a varios orígenes de datos. También los define como enlaces de entrada o salida, o puede pensar en ellos como enlaces de lectura o escritura.

Suponga que tenía un desencadenador QueueTrigger que iniciaba una función cuando se agregaba un blob a una cola. Se usaría un enlace de blob de entrada para conectarse a Azure Blob Storage. 

Los enlaces de salida se usan para almacenar datos. Por ejemplo, envían el valor devuelto de la función al almacenamiento de tabla de Azure.

Hay una lista completa de enlaces disponible en la [documentación de Azure](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings).

### <a name="a-sample-trigger-and-binding-functionjson"></a>Un desencadenador y enlace de ejemplo (function.json)
Esta es una definición de ejemplo de un desencadenador y un enlace para una función. Puede observar que, según el tipo de enlace que se está describiendo, hay otros valores de propiedad diferentes que deben establecerse. Cada enlace también tiene una dirección que define si se trata de un enlace de entrada o salida. Los desencadenadores son siempre enlaces de entrada. Este ejemplo muestra una función que se desencadena mediante un mensaje que se agrega a una cola denominada **myqueue-items**. Después, envía el valor devuelto de la función a la tabla **outTable** del almacenamiento de tabla de Azure.

```javascript
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
## <a name="premade-functions-and-templates"></a>Plantillas y funciones predefinidas
Azure proporciona plantillas preconfiguradas para escenarios comunes de funciones de Azure.

### <a name="quickstart-templates"></a>Plantillas de inicio rápido
Para agregar una función de Azure, debe seleccionar una aplicación de función. La aplicación de función puede identificarse por el rayo en el icono de los corchetes angulares.  
![Icono de función](../images/5-function-icon.png)

Al agregar la primera función de Azure, se le presentará la pantalla Inicio rápido. Esta pantalla le permite realizar una selección del tipo de desencadenador deseado y el lenguaje de programación. A continuación, según las selecciones realizadas, Azure generará el código de función y la configuración de forma automática.  
![Inicio rápido de la función](../images/5-quickstart-form.png)

### <a name="function-templates"></a>Plantillas de función
La selección de plantillas no se limita a las que están disponibles en el inicio rápido. También tiene la posibilidad de elegir entre más de 30 plantillas diferentes. Puede acceder a la pantalla de lista de la plantillas al crear las funciones posteriores, o bien seleccionando la opción **Función personalizada** en la pantalla Inicio rápido.  
![Plantillas de función](../images/5-template-list.png)

## <a name="navigating-to-your-function-and-files"></a>Navegación a la función y archivos
Después de crear una función a partir de una plantilla, se crean varios archivos. Supongamos que optó por utilizar el inicio rápido Webhook + API mediante JavaScript. Los archivos generados serían un archivo de configuración, **function.json**, y un archivo de código fuente, **index.js**. Al acceder a la aplicación de función, se presentará un árbol de menús en el que se mostrarán las funciones que se han creado en la aplicación. Es también en este elemento de menú **Funciones** donde se pueden agregar funciones adicionales a la aplicación de función (aparecerá un icono de signo más + cuando mantenga el puntero sobre el elemento de menú).  
![Botón Agregar función](../images/5-function-add-button.png) 

En el caso de este inicio rápido mencionado anteriormente, al expandir **Funciones** en la vista de árbol, verá una función con un nombre predeterminado de **HttpTriggerJS1** (también se indica mediante el icono f de función). Al seleccionar esta función se abrirá una ventana de código y mostrará el archivo de código fuente **index.js**. En el lado derecho de la ventana de código, hay un menú flotante que incluye una pestaña **Ver archivos**. Al seleccionar esta pestaña se mostrará la estructura de archivos (imitada en el almacenamiento) que conforma la función.  
![Plantillas de función](../images/5-file-navigation.png)

## <a name="execution-options-for-testing-your-azure-function"></a>Opciones de ejecución para probar la función de Azure
Una vez creada una función de Azure, necesitará saber cómo probarla. Dispone de dos enfoques: ejecución manual y pruebas desde dentro de Azure Portal.

### <a name="manual-execution-of-a-function"></a>Ejecución manual de una función
Puede iniciar la ejecución de una función manualmente desencadenando el desencadenador configurado. Por ejemplo, si está utilizando un desencadenador HttpTrigger, puede usar una herramienta como Postman o cURL para iniciar una solicitud HTTP a la dirección URL del punto de conexión de función.  
![Ejecución Postman de una función](../images/5-postman-execution.png) Puede obtener la dirección URL del punto de conexión seleccionando el desencadenador HTTP en el panel de navegación izquierdo y luego seleccionando el botón **Obtener la dirección URL de la función**.  
![Obtener la dirección URL de la función](../images/5-get-function-url.png)

### <a name="testing-a-function-in-the-azure-portal"></a>Prueba de una función en Azure Portal
Como alternativa, Azure Portal también proporciona una manera cómoda de probar las funciones. En el lado derecho de la ventana de código, hay un menú de navegación con pestañas flotante. Este menú contiene un elemento **Prueba**. Al expandir el menú y seleccionar esta pestaña dispondrá de otra manera de ejecutar la función y ver el resultado. De acuerdo con el escenario del desencadenador HttpTrigger, puede establecer el método HTTP y agregar parámetros de cadena de consulta y encabezados HTTP a la solicitud. También puede cambiar el cuerpo de la solicitud para probar escenarios adicionales. En la ventana de salida muestra el resultado de la función.  
![Ejecución de una función mediante el portal](../images/5-portal-execution.png)

## <a name="monitoring-an-azure-function"></a>Supervisión de una función de Azure
Durante el desarrollo de la función de Azure, poder registrar los mensajes y determinar los escenarios de excepciones es esencial para garantizar que las funciones se están preparando para la producción. Esto es importante en un escenario de producción, al realizar el seguimiento del origen de un defecto. Azure Portal nos proporciona una interfaz de usuario que ofrece un panel de supervisión, así como una manera de revisar los registros de ejecución y las excepciones que se obtienen de las funciones de Azure.

### <a name="monitoring-dashboard"></a>Panel de supervisión
En el menú de navegación de la aplicación de función, una vez que expanda el nodo de función, verá un elemento de menú **Monitor**. El panel del monitor proporciona una forma rápida de ver el historial de ejecuciones de función. Esta vista muestra la marca de tiempo, el código de resultado, la duración y el identificador de operación, así como si se ha completado correctamente. Los datos se rellenan mediante Azure Application Insights.  
![Monitor de función](../images/5-monitor-function.png)

### <a name="log-window"></a>Ventana de registro
También puede agregar instrucciones de registro a la función. Estas instrucciones aparecerán en la ventana de registro de la función. La ventana de registro se encuentra en un menú flotante con pestañas en la parte inferior de la ventana de código. Cuando se use una función basada en JavaScript, agregaría una instrucción de registro mediante la sintaxis siguiente:
```javascript
  context.log('Enter your logging statement here');
```  
![Ventana de registro](../images/5-log-window.png)

### <a name="errors-and-warnings-window"></a>Ventana de errores y advertencias
Puede encontrar la pestaña de la ventana de errores y advertencias en el mismo menú flotante que la ventana de registro. Esta ventana mostrará los errores y las advertencias de compilación dentro del código. Dado que JavaScript es un lenguaje interpretado y dinámico, la siguiente imagen muestra un error de compilación en una función de C#.  
![Ventana de errores y advertencias](../images/5-errors-window.png)
