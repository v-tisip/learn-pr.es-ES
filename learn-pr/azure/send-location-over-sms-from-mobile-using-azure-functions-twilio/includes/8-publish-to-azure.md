La aplicación y la función de Azure ya están completas y se están ejecutando de forma local. En esta unidad, publicará la función de Azure en Azure para ejecutarla en la nube.

> En esta unidad, publicará la función desde Visual Studio. Esta es una excelente manera de empezar a usar las pruebas de concepto, los prototipos y el aprendizaje, pero para una aplicación de calidad de producción **no** debe usar este método. Debería usar alguna forma de implementación basada en CI. Puede obtener más información sobre cómo hacerlo en la [documentación de implementación de Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).
>
> [![Los amigos no permiten que sus amigos hagan clic con el botón derecho en Publicar](../media/8-friends-dont-let-friends-publish.png)](https://damianbrady.com.au/2018/02/01/friends-dont-let-friends-right-click-publish/)

## <a name="publishing-your-app-to-azure"></a>Publicación de la aplicación en Azure

Las funciones de Azure se pueden publicar en Azure desde Visual Studio.

1. Detenga la instancia local de Azure Functions Runtime si aún se está ejecutando desde la unidad anterior.

2. Haga clic con el botón derecho en la aplicación `ImHere.Functions` en el explorador de soluciones y seleccione *Publicar...*

    ![Haga clic con el botón derecho en Publicar en la aplicación de Functions](../media/8-right-click-publish.png)

3. En el cuadro de diálogo **Elegir un destino de publicación**, seleccione *Azure Function App* y, para **Azure App Service**, seleccione *Crear nuevo*. Haga clic en **Publicar**.

    ![Creación de una nueva instancia de Azure App Service en la que publicar](../media/8-pick-publish-target.png)

4. Si tiene más de una cuenta de Azure y no está seleccionada la adecuada, seleccione su cuenta de Azure en la lista desplegable de la esquina superior derecha.

5. Póngale un nombre a la aplicación de Functions. Este nombre debe ser único en todas las aplicaciones de Functions en todo Azure, así que use algo parecido a "ImHere-\<SuNombre\>".

6. Seleccione la suscripción en la que quiera crear esta aplicación de Functions.

7. Cree un grupo de recursos para esta aplicación de Functions; para ello, haga clic en el botón **Nuevo...** situado junto al menú desplegable **Grupo de recursos** y asígnele un nombre, por ejemplo, "ImHere". Los nombres de los grupos de recursos deben ser únicos en su suscripción, no de forma global en Azure. Después, haga clic en **Aceptar**.

    ![Creación de un nuevo grupo de recursos](../media/8-create-new-resource-group.png)

   Si crea un nuevo grupo de recursos, será más fácil limpiarlo más adelante. Puede eliminar el grupo de recursos y saber que todo lo que ha creado para esta aplicación de Functions se eliminará al mismo tiempo.

8. Cree un plan de hospedaje; para ello, haga clic en el botón **Nuevo...** situado junto al menú desplegable **Plan de hospedaje**. El nombre del plan de App Service será de forma predeterminada el nombre de su aplicación con “Plan” al final. Establezca la **Ubicación** en la ubicación más cercana a usted y asegúrese de que **Tamaño** está establecido en Consumo. Después, haga clic en **Aceptar**.

    ![Configuración del plan de hospedaje](../media/8-configure-hosting-plan.png)

9. Cree una cuenta de almacenamiento; para ello, haga clic en el botón **Nuevo...** situado junto al menú desplegable **Cuenta de almacenamiento**. Se proporcionará un nombre predeterminado, de modo que mantenga todos los valores predeterminados y haga clic en **Aceptar**.

    ![Creación de una cuenta de almacenamiento](../media/8-create-storage-account.png)

10. Haga clic en **Crear** para aprovisionar todos los recursos de Azure y publicar la aplicación de Azure Functions.

    ![Creación de la instancia de App Service](../media/8-create-app-service.png)

El aprovisionamiento tardará aproximadamente un par de minutos en ejecutarse. Se aprovisionarán los siguientes recursos:

* Una cuenta de almacenamiento para almacenar los archivos necesarios para la aplicación de Azure Functions.
* Un plan de App Service para administrar los recursos de proceso que necesita la aplicación de Azure Functions.
* La instancia de App Service que ejecuta la función de Azure

La función ya estará publicada y disponible para llamarla en https://<nombre-de-su-aplicación>.azurewebsites.net/api/SendLocation.

## <a name="configuring-your-app"></a>Configuración de la aplicación

Cuando la función de Azure se ejecutaba de forma local, usaba las credenciales de Twilio que estaban almacenadas en un archivo `local.settings.json`. Como sugiere el nombre, este archivo es para la configuración local, no para la configuración de Azure. Para poder llamar a la función de Azure dentro de Azure, es necesario configurar las opciones `TwilioAccountSid` y `TwilioAuthToken`.

1. En la pestaña Publicar, haga clic en la opción **Administrar configuración de la aplicación**.

    ![Opción Administrar configuración de la aplicación](../media/8-application-settings-option.png)

2. Haga clic en el botón **Agregar** para agregar una nueva configuración. Asígnele el nombre "TwilioAccountSid" y establezca el valor del SID de la cuenta de Twilio. Repita este paso para el token de autenticación con el nombre "TwilioAuthToken".

    ![Establecimiento de las credenciales de Twilio en la configuración de la aplicación](../media/8-set-creds-in-app-settings.png)

3. Haga clic en **Aceptar**.

4. Haga clic en **Publicar** para volver a publicar la aplicación de Azure Functions con la nueva configuración de la aplicación.

    ![Botón Publicar](../media/8-publish-application-button.png)

## <a name="pointing-the-mobile-app-to-azure"></a>Dirigir la aplicación móvil a Azure

1. En la pestaña Publicar, copie la **URL del sitio** con el botón Copiar que hay situado junto al valor.

    ![Copie la URL del sitio desde la pestaña Publicar](../media/8-copy-site-url.png)

2. Abra `MainViewModel` desde el proyecto `ImHere`.

3. Actualice el valor del campo `baseUrl` para que sea la URL del sitio que ha copiado en la pestaña Publicar.

4. Cambie el protocolo de este valor de `http` a `https`. La URL del sitio se proporciona siempre mediante HTTP, pero tiene que usar HTTPS para llamar a una función de Azure.

## <a name="test-it-out"></a>Prueba

1. Establezca la aplicación `ImHere.UWP` como la aplicación de inicio y ejecútela.

2. Escriba un número de teléfono y haga clic en el botón **Enviar ubicación**.

3. Debería recibir la ubicación como un mensaje SMS.

## <a name="summary"></a>Resumen

En esta unidad, ha aprendido a publicar un proyecto de Azure Functions en Azure desde Visual Studio y a configurar las opciones de la aplicación.