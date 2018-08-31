Ha creado correctamente una aplicación móvil multiplataforma con Xamarin y una función de Azure con un enlace de Twilio.

## <a name="clean-up-resources"></a>Limpieza de recursos

Cuando haya terminado de trabajar con esta aplicación de Azure Functions, puede eliminar todos los recursos creados durante el tutorial desde Azure Portal.

1. En Visual Studio, seleccione *Ver->Cloud Explorer*.

2. En la lista desplegable de la parte superior de este panel, seleccione *Grupos de recursos*.

3. Expanda la suscripción que usó para crear el grupo de recursos. Haga clic con el botón derecho en el grupo de recursos "ImHere" y seleccione *Abrir en el portal*.

    ![Apertura del grupo de recursos en el portal desde la ventana de Cloud Explorer](../media-drafts/9-open-resource-group-in-portal.png)

4. Si es necesario, inicie sesión en Azure Portal en el explorador.

5. El portal se abrirá en el grupo de recursos "ImHere". Haga clic en el botón **Eliminar grupo de recursos**.

    ![Eliminar el grupo de recursos](../media-drafts/9-delete-resource-group.png)

6. Escriba el nombre del grupo de recursos para confirmar la eliminación y haga clic en **Eliminar**.

    ![Escriba el nombre del grupo de recursos para confirmar la eliminación](../media-drafts/9-confirm-delete-resource-group.png)

## <a name="summary"></a>Resumen

En este tutorial, ha aprendido cómo:
> [!div class="checklist"]
> * Crear una aplicación de Xamarin.Forms multiplataforma que usa Xamarin.Essentials.
> * Crear una interfaz de usuario multiplataforma mediante XAML con lógica de aplicación en una clase ViewModel, así como enlazar las propiedades de ViewModel a la interfaz de usuario.
> * Detectar la ubicación del usuario.
> * Crear una función de Azure con un desencadenador HTTP y ejecutarla localmente.
> * Llamar a una función de Azure desde una aplicación móvil, pasando los datos como JSON.
> * Enlazar una función de Azure con Twilio para enviar un mensaje SMS.
> * Publicar una función de Azure en Azure.
