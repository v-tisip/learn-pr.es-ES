<span data-ttu-id="05782-101">La aplicación y la función de Azure ya están completas y se están ejecutando de forma local.</span><span class="sxs-lookup"><span data-stu-id="05782-101">The app and Azure function are now complete and running locally.</span></span> <span data-ttu-id="05782-102">En esta unidad, publicará la función de Azure en Azure para ejecutarla en la nube.</span><span class="sxs-lookup"><span data-stu-id="05782-102">In this unit, you publish the Azure function to Azure to run in the cloud.</span></span>

> <span data-ttu-id="05782-103">En esta unidad, publicará la función desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="05782-103">In this unit, you will publish your function from Visual Studio.</span></span> <span data-ttu-id="05782-104">Esta es una excelente manera de empezar a usar las pruebas de concepto, los prototipos y el aprendizaje, pero para una aplicación de calidad de producción **no** debe usar este método.</span><span class="sxs-lookup"><span data-stu-id="05782-104">This is a great way to get started for proof-of-concepts, prototypes, and learning, but for a production-quality app you should **not** use this method.</span></span> <span data-ttu-id="05782-105">Debería usar alguna forma de implementación basada en CI.</span><span class="sxs-lookup"><span data-stu-id="05782-105">You should use some form of CI-based deployment.</span></span> <span data-ttu-id="05782-106">Puede obtener más información sobre cómo hacerlo en la [documentación de implementación de Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).</span><span class="sxs-lookup"><span data-stu-id="05782-106">You can read more about doing this in the [Azure Functions Deployment docs](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).</span></span>
>
> <span data-ttu-id="05782-107">[![Los amigos no permiten que sus amigos hagan clic con el botón derecho en Publicar](../media/8-friends-dont-let-friends-publish.png)](https://damianbrady.com.au/2018/02/01/friends-dont-let-friends-right-click-publish/)</span><span class="sxs-lookup"><span data-stu-id="05782-107">[![Friends don't let friends right-click publish](../media/8-friends-dont-let-friends-publish.png)](https://damianbrady.com.au/2018/02/01/friends-dont-let-friends-right-click-publish/)</span></span>

## <a name="publishing-your-app-to-azure"></a><span data-ttu-id="05782-108">Publicación de la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="05782-108">Publishing your app to Azure</span></span>

<span data-ttu-id="05782-109">Las funciones de Azure se pueden publicar en Azure desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="05782-109">Azure functions can be published to Azure from inside Visual Studio.</span></span>

1. <span data-ttu-id="05782-110">Detenga la instancia local de Azure Functions Runtime si aún se está ejecutando desde la unidad anterior.</span><span class="sxs-lookup"><span data-stu-id="05782-110">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

2. <span data-ttu-id="05782-111">Haga clic con el botón derecho en la aplicación `ImHere.Functions` en el explorador de soluciones y seleccione *Publicar...*</span><span class="sxs-lookup"><span data-stu-id="05782-111">Right-click on the `ImHere.Functions` app in the solution explorer and select *Publish...*.</span></span>

    ![Haga clic con el botón derecho en Publicar en la aplicación de Functions](../media/8-right-click-publish.png)

3. <span data-ttu-id="05782-113">En el cuadro de diálogo **Elegir un destino de publicación**, seleccione *Azure Function App* y, para **Azure App Service**, seleccione *Crear nuevo*.</span><span class="sxs-lookup"><span data-stu-id="05782-113">From the **Pick a publish target** dialog, select *Azure Function App*, and for **Azure App Service**, select *Create New*.</span></span> <span data-ttu-id="05782-114">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="05782-114">Click **Publish**.</span></span>

    ![Creación de una nueva instancia de Azure App Service en la que publicar](../media/8-pick-publish-target.png)

4. <span data-ttu-id="05782-116">Si tiene más de una cuenta de Azure y no está seleccionada la adecuada, seleccione su cuenta de Azure en la lista desplegable de la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="05782-116">Select your Azure account from the drop-down in the top-right corner if you have more than one Azure accounts and the right one isn't selected.</span></span>

5. <span data-ttu-id="05782-117">Póngale un nombre a la aplicación de Functions.</span><span class="sxs-lookup"><span data-stu-id="05782-117">Give your Functions app a name.</span></span> <span data-ttu-id="05782-118">Este nombre debe ser único en todas las aplicaciones de Functions en todo Azure, así que use algo parecido a "ImHere-\<SuNombre\>".</span><span class="sxs-lookup"><span data-stu-id="05782-118">This name needs to be globally unique across all the Functions apps in the whole of Azure, so use something like "ImHere-\<YourName\>".</span></span>

6. <span data-ttu-id="05782-119">Seleccione la suscripción en la que quiera crear esta aplicación de Functions.</span><span class="sxs-lookup"><span data-stu-id="05782-119">Select the subscription you want to create this Functions app under.</span></span>

7. <span data-ttu-id="05782-120">Cree un grupo de recursos para esta aplicación de Functions; para ello, haga clic en el botón **Nuevo...** situado junto al menú desplegable **Grupo de recursos** y asígnele un nombre, por ejemplo, "ImHere".</span><span class="sxs-lookup"><span data-stu-id="05782-120">Create a new resource group for this Functions app by clicking the **New...** button next to the **Resource Group** drop-down and giving it a name such as "ImHere".</span></span> <span data-ttu-id="05782-121">Los nombres de los grupos de recursos deben ser únicos en su suscripción, no de forma global en Azure.</span><span class="sxs-lookup"><span data-stu-id="05782-121">Resource group names need to be unique to your subscription, not globally unique across Azure.</span></span> <span data-ttu-id="05782-122">Después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="05782-122">Then, click **OK**.</span></span>

    ![Creación de un nuevo grupo de recursos](../media/8-create-new-resource-group.png)

   <span data-ttu-id="05782-124">Si crea un nuevo grupo de recursos, será más fácil limpiarlo más adelante.</span><span class="sxs-lookup"><span data-stu-id="05782-124">Creating a new resource group makes it easier to clean up later.</span></span> <span data-ttu-id="05782-125">Puede eliminar el grupo de recursos y saber que todo lo que ha creado para esta aplicación de Functions se eliminará al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="05782-125">You can delete the resource group and know that everything you've created for this Functions app will all be deleted at the same time.</span></span>

8. <span data-ttu-id="05782-126">Cree un plan de hospedaje; para ello, haga clic en el botón **Nuevo...** situado junto al menú desplegable **Plan de hospedaje**.</span><span class="sxs-lookup"><span data-stu-id="05782-126">Create a new hosting plan by clicking the **New...** button next to the **Hosting Plan** drop-down.</span></span> <span data-ttu-id="05782-127">El nombre del plan de App Service será de forma predeterminada el nombre de su aplicación con “Plan” al final.</span><span class="sxs-lookup"><span data-stu-id="05782-127">The App Service plan name will default to your app name with "Plan" on the end.</span></span> <span data-ttu-id="05782-128">Establezca la **Ubicación** en la ubicación más cercana a usted y asegúrese de que **Tamaño** está establecido en Consumo.</span><span class="sxs-lookup"><span data-stu-id="05782-128">Set the **Location** to the closest location to you and make sure **Size** is set to consumption.</span></span> <span data-ttu-id="05782-129">Después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="05782-129">Then, click **OK**.</span></span>

    ![Configuración del plan de hospedaje](../media/8-configure-hosting-plan.png)

9. <span data-ttu-id="05782-131">Cree una cuenta de almacenamiento; para ello, haga clic en el botón **Nuevo...** situado junto al menú desplegable **Cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="05782-131">Create a new storage account by clicking the **New...** button next to the **Storage Account** drop-down.</span></span> <span data-ttu-id="05782-132">Se proporcionará un nombre predeterminado, de modo que mantenga todos los valores predeterminados y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="05782-132">A default name will be provided, so keep all the default values and click **OK**.</span></span>

    ![Creación de una cuenta de almacenamiento](../media/8-create-storage-account.png)

10. <span data-ttu-id="05782-134">Haga clic en **Crear** para aprovisionar todos los recursos de Azure y publicar la aplicación de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="05782-134">Click **Create** to provision all the resources on Azure and publish your Azure Functions app.</span></span>

    ![Creación de la instancia de App Service](../media/8-create-app-service.png)

<span data-ttu-id="05782-136">El aprovisionamiento tardará aproximadamente un par de minutos en ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="05782-136">Provisioning will take a couple of minutes or so to run.</span></span> <span data-ttu-id="05782-137">Se aprovisionarán los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="05782-137">The following resources will be provisioned:</span></span>

* <span data-ttu-id="05782-138">Una cuenta de almacenamiento para almacenar los archivos necesarios para la aplicación de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="05782-138">A storage account to store the files needed for the Azure Functions app</span></span>
* <span data-ttu-id="05782-139">Un plan de App Service para administrar los recursos de proceso que necesita la aplicación de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="05782-139">An App Service plan to manage the compute resources needed by the Azure Functions app</span></span>
* <span data-ttu-id="05782-140">La instancia de App Service que ejecuta la función de Azure</span><span class="sxs-lookup"><span data-stu-id="05782-140">The App Service that runs the Azure function</span></span>

<span data-ttu-id="05782-141">La función ya estará publicada y disponible para llamarla en https://<nombre-de-su-aplicación>.azurewebsites.net/api/SendLocation.</span><span class="sxs-lookup"><span data-stu-id="05782-141">The function will now be published and available to call at https://<your-app-name>.azurewebsites.net/api/SendLocation.</span></span>

## <a name="configuring-your-app"></a><span data-ttu-id="05782-142">Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="05782-142">Configuring your app</span></span>

<span data-ttu-id="05782-143">Cuando la función de Azure se ejecutaba de forma local, usaba las credenciales de Twilio que estaban almacenadas en un archivo `local.settings.json`.</span><span class="sxs-lookup"><span data-stu-id="05782-143">When the Azure function was running locally, it was using Twilio credentials that were stored in a `local.settings.json` file.</span></span> <span data-ttu-id="05782-144">Como sugiere el nombre, este archivo es para la configuración local, no para la configuración de Azure.</span><span class="sxs-lookup"><span data-stu-id="05782-144">As the name suggests, this file is for local settings, not Azure settings.</span></span> <span data-ttu-id="05782-145">Para poder llamar a la función de Azure dentro de Azure, es necesario configurar las opciones `TwilioAccountSid` y `TwilioAuthToken`.</span><span class="sxs-lookup"><span data-stu-id="05782-145">Before the Azure function can be called inside Azure, the `TwilioAccountSid` and `TwilioAuthToken` settings need to be configured.</span></span>

1. <span data-ttu-id="05782-146">En la pestaña Publicar, haga clic en la opción **Administrar configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="05782-146">From the Publish tab, click the **Manage Application Settings** option.</span></span>

    ![Opción Administrar configuración de la aplicación](../media/8-application-settings-option.png)

2. <span data-ttu-id="05782-148">Haga clic en el botón **Agregar** para agregar una nueva configuración.</span><span class="sxs-lookup"><span data-stu-id="05782-148">Click the **Add** button to add a new setting.</span></span> <span data-ttu-id="05782-149">Asígnele el nombre "TwilioAccountSid" y establezca el valor del SID de la cuenta de Twilio.</span><span class="sxs-lookup"><span data-stu-id="05782-149">Name it "TwilioAccountSid" and set the value to your Twilio account SID.</span></span> <span data-ttu-id="05782-150">Repita este paso para el token de autenticación con el nombre "TwilioAuthToken".</span><span class="sxs-lookup"><span data-stu-id="05782-150">Repeat this step for your Auth Token using the name "TwilioAuthToken".</span></span>

    ![Establecimiento de las credenciales de Twilio en la configuración de la aplicación](../media/8-set-creds-in-app-settings.png)

3. <span data-ttu-id="05782-152">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="05782-152">Click **OK**.</span></span>

4. <span data-ttu-id="05782-153">Haga clic en **Publicar** para volver a publicar la aplicación de Azure Functions con la nueva configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="05782-153">Click **Publish** to republish the Azure Functions app with the new application settings.</span></span>

    ![Botón Publicar](../media/8-publish-application-button.png)

## <a name="pointing-the-mobile-app-to-azure"></a><span data-ttu-id="05782-155">Dirigir la aplicación móvil a Azure</span><span class="sxs-lookup"><span data-stu-id="05782-155">Pointing the mobile app to Azure</span></span>

1. <span data-ttu-id="05782-156">En la pestaña Publicar, copie la **URL del sitio** con el botón Copiar que hay situado junto al valor.</span><span class="sxs-lookup"><span data-stu-id="05782-156">From the Publish tab, copy the **Site URL** using the copy button next to the value.</span></span>

    ![Copie la URL del sitio desde la pestaña Publicar](../media/8-copy-site-url.png)

2. <span data-ttu-id="05782-158">Abra `MainViewModel` desde el proyecto `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="05782-158">Open the `MainViewModel` from the `ImHere` project.</span></span>

3. <span data-ttu-id="05782-159">Actualice el valor del campo `baseUrl` para que sea la URL del sitio que ha copiado en la pestaña Publicar.</span><span class="sxs-lookup"><span data-stu-id="05782-159">Update the value of the `baseUrl` field to be the site URL copied from the Publish tab.</span></span>

4. <span data-ttu-id="05782-160">Cambie el protocolo de este valor de `http` a `https`.</span><span class="sxs-lookup"><span data-stu-id="05782-160">Change the protocol for this value from `http` to `https`.</span></span> <span data-ttu-id="05782-161">La URL del sitio se proporciona siempre mediante HTTP, pero tiene que usar HTTPS para llamar a una función de Azure.</span><span class="sxs-lookup"><span data-stu-id="05782-161">The site URL is always given using HTTP, but you have to use HTTPS to call an Azure function.</span></span>

## <a name="test-it-out"></a><span data-ttu-id="05782-162">Prueba</span><span class="sxs-lookup"><span data-stu-id="05782-162">Test it out</span></span>

1. <span data-ttu-id="05782-163">Establezca la aplicación `ImHere.UWP` como la aplicación de inicio y ejecútela.</span><span class="sxs-lookup"><span data-stu-id="05782-163">Set the `ImHere.UWP` app as the startup app and run it.</span></span>

2. <span data-ttu-id="05782-164">Escriba un número de teléfono y haga clic en el botón **Enviar ubicación**.</span><span class="sxs-lookup"><span data-stu-id="05782-164">Enter a phone number and click the **Send Location** button.</span></span>

3. <span data-ttu-id="05782-165">Debería recibir la ubicación como un mensaje SMS.</span><span class="sxs-lookup"><span data-stu-id="05782-165">You should receive the location as an SMS message.</span></span>

## <a name="summary"></a><span data-ttu-id="05782-166">Resumen</span><span class="sxs-lookup"><span data-stu-id="05782-166">Summary</span></span>

<span data-ttu-id="05782-167">En esta unidad, ha aprendido a publicar un proyecto de Azure Functions en Azure desde Visual Studio y a configurar las opciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="05782-167">In this unit, you learned how to publish an Azure Functions project to Azure from inside Visual Studio and configure application settings.</span></span>