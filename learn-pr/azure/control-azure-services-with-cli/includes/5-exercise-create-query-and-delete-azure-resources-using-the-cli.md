
En este ejercicio, usará la CLI de Azure en el equipo local para crear un grupo de recursos y después para implementar una aplicación web en este grupo de recursos. 

### <a name="steps-to-create-a-resource-group"></a>Pasos para crear un grupo de recursos
1. Abra un shell de Bash en Linux o macOS, o bien abra la ventana del símbolo del sistema o PowerShell si trabaja en Windows.

1. Inicie la CLI de Azure y ejecute el comando de inicio de sesión.

    ```bash
    az login
    ```
    Si no aparece una página de inicio de sesión de Azure en el explorador web, siga las instrucciones de la línea de comandos y escriba un código de autorización en [https://aka.ms/devicelogin](https://aka.ms/devicelogin).

1. Cree un grupo de recursos.

    ```bash
    az group create --location westeurope --name popupResGroup
    ```

1. Muestre todos sus grupos de recursos en una tabla para comprobar que el grupo de recursos se ha creado correctamente.

    ```bash
    az group list --output table
    ```
1. Si quiere, confirme que el recurso se ha creado en Azure Portal. Abra un explorador web, inicie sesión en el portal y vaya a la sección **Grupos de recursos** (ver a continuación). El nuevo grupo de recursos debería mostrarse en la lista.

![Uso del portal para enumerar los grupos de recursos](../media-drafts/5-listing-resource-groups.png)

### <a name="steps-to-create-a-service-plan"></a>Pasos para crear un plan de servicio
Al ejecutar Web Apps, mediante Azure App Service, paga por los recursos de proceso de Azure que use la aplicación y esto depende del plan de App Service asociado con Web Apps. Los planes de servicio determinan la región que se usa para el centro de datos de la aplicación, el número de máquinas virtuales que se usan y el plan de tarifa.

1. Cree un plan de App Service para ejecutar la aplicación. El nombre de la aplicación y el plan deben ser únicos, así que cambie la cadena "12345" por un número aleatorio. El siguiente comando no especifica un plan de tarifa ni detalles de la instancia de la máquina virtual, de modo que, de forma predeterminada, obtendrá un plan **Básico** con una instancia de máquina virtual **pequeña**.

    ```bash
    az appservice plan create --name popupapp12345 --resource-group popupResGroup --location westeurope
    ```

1. Muestre todos sus planes en una tabla para comprobar que el plan de servicio se ha creado correctamente.

    ```bash
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a>Pasos para crear una aplicación web
A continuación, creará la aplicación web en su plan de servicio. Puede implementar el código al mismo tiempo, pero, en nuestro ejemplo, lo haremos en pasos distintos.

1. Cree la aplicación web, sin olvidarse de cambiar la cadena "12345" por el mismo número aleatorio que ha usado antes.
    ```bash
    az webapp create --name popupapp12345 --resource-group popupResGroup --plan popupapp12345
    ```

1. Muestre todas las aplicaciones en una tabla para comprobar que la aplicación se ha creado correctamente.

    ```bash
    az webapp list --output table
    ```

1. Apunte el valor de **DefaultHostName**; lo necesitará más adelante.

### <a name="steps-to-deploy-code-from-github"></a>Pasos para implementar código desde GitHub
1. El último paso consiste en implementar código desde un repositorio de GitHub en la aplicación web, recordando de nuevo cambiar la cadena "12345" por el mismo número aleatorio que ha usado antes.
    ```bash
    az webapp deployment source config --name popupapp12345 --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. Copie la siguiente URL en un explorador para ver la aplicación web.
http://popupapp12345.azurewebsites.net

1. La página muestra “HelloWorld!”.

1. Cierre la ventana del explorador.

## <a name="summary"></a>Resumen
Este ejercicio ha mostrado un patrón típico de una sesión interactiva de la CLI de Azure. Primero ha usado un comando estándar para crear un grupo de recursos. Después ha usado un conjunto de comandos para implementar un recurso (en este ejemplo, una aplicación web) en este grupo de recursos. Este conjunto de comandos podría combinarse fácilmente en un script de shell y ejecutarse cada vez que necesite crear el mismo recurso.
