En este ejercicio, vamos a crear una aplicación de función de Azure.

1. Inicie sesión en [Azure Portal](https://portal.azure.com) con su cuenta de Azure.
1. Seleccione el botón **Crear un recurso** que se encuentra en la esquina superior izquierda de Azure Portal y luego seleccione **Compute > Function App**.
  ![Creación de un recurso de aplicación de función](../images/4-create-function-app-blade.png)
1. Elija un nombre de aplicación gobalmente único. Esto servirá como la dirección URL base del servicio. Puede asignarle el nombre **escalator-functions-xxxxxxx**, donde las x pueden reemplazarse por sus iniciales y el año de nacimiento. Si no es único globalmente, puede probar cualquier otra combinación. Los caracteres válidos son a-z, 0-9 y -.
1. Seleccione la suscripción de Azure donde desea que se hospede la aplicación de función.
1. Crear un nuevo grupo de recursos denominado **escalator-functions-group**. Esto le ayudará con la limpieza más adelante.
1. Seleccione **Windows** para el sistema operativo.
1. Para **Plan de hospedaje**, seleccione **Plan de consumo**, de modo que podemos aprovechar las características de Azure sin servidor.
1. Seleccione la ubicación geográfica más cercana a usted (o a sus clientes).
1. Crear una nueva cuenta de almacenamiento y asígnele el nombre **escalatorfunctions**.
1. Asegúrese de que Azure Application Insights está **activada** y seleccione la región que tenga más cerca.
1. Seleccione **Crear**; la implementación tardará unos minutos. Recibirá una notificación cuando haya terminado.
  ![Configuración de la aplicación de función](../images/4-create-function-app-settings.png)

## <a name="verify-your-azure-function-app"></a>Comprobación de la aplicación de función de Azure

1. En el menú de la izquierda de Azure Portal, seleccione **Grupos de recursos**. Verá **escalator-functions-group** en la lista de grupos disponibles.
  ![Grupos de recursos](../images/4-resource-group.png)
1. Seleccione **escalator-functions-group**. Debería ver una lista de recursos similar a la siguiente: ![Lista de recursos](../images/4-resource-list.png)
