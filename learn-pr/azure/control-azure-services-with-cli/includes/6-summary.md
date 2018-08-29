## <a name="module-summary"></a><span data-ttu-id="f94f9-101">Resumen de módulo</span><span class="sxs-lookup"><span data-stu-id="f94f9-101">Module summary</span></span>
<span data-ttu-id="f94f9-102">En este módulo, usó los comandos de la CLI de Azure para crear un grupo de recursos e implementar una aplicación web mediante un pequeño grupo de comandos.</span><span class="sxs-lookup"><span data-stu-id="f94f9-102">In this module, you used the Azure CLI commands to create a resource group, and deploy a web app by using a small set of commands.</span></span> <span data-ttu-id="f94f9-103">Estos comandos se pueden combinar en un script de shell como parte de la solución de automatización.</span><span class="sxs-lookup"><span data-stu-id="f94f9-103">These commands could be combined into a shell script as part of automation solution.</span></span>

<span data-ttu-id="f94f9-104">La CLI de Azure es una buena elección para los menos familiarizados con la línea de comandos y el scripting de Azure.</span><span class="sxs-lookup"><span data-stu-id="f94f9-104">The Azure CLI is a good choice for anyone new to Azure command line and scripting.</span></span> <span data-ttu-id="f94f9-105">Su sintaxis simple y la compatibilidad multiplataforma ayudan a reducir el riesgo de errores al realizar tareas repetitivas y regulares.</span><span class="sxs-lookup"><span data-stu-id="f94f9-105">Its simple syntax and cross-platform compatibility help reduce the risk of errors when performing regular and repetitive tasks.</span></span>

## <a name="cleanup"></a><span data-ttu-id="f94f9-106">Limpieza</span><span class="sxs-lookup"><span data-stu-id="f94f9-106">Cleanup</span></span>
<span data-ttu-id="f94f9-107">La ejecución de aplicaciones web genera costos en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="f94f9-107">Running web apps incurs costs against your subscription.</span></span> <span data-ttu-id="f94f9-108">Quite los recursos innecesarios para evitar gastos innecesarios.</span><span class="sxs-lookup"><span data-stu-id="f94f9-108">Remove unneeded resources to avoid unnecessary charges.</span></span> <span data-ttu-id="f94f9-109">La manera más sencilla de limpiar la suscripción de Azure es quitar el grupo de recursos; así, también se eliminan todos los recursos del grupo.</span><span class="sxs-lookup"><span data-stu-id="f94f9-109">The easiest way to clean up your Azure subscription is to remove the resource group; this will also delete all the resources in the group.</span></span> <span data-ttu-id="f94f9-110">Cuando haya terminado con este módulo, ejecute el siguiente cmdlet de Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f94f9-110">When you're finished with this module, run the following Azure PowerShell cmdlet:</span></span>

    ```azurecli
    az group delete --resource-group popupResGroup
    ```

<span data-ttu-id="f94f9-111">Cuando se le pida que confirme la eliminación, responda **Sí**.</span><span class="sxs-lookup"><span data-stu-id="f94f9-111">When you're asked to confirm the delete, answer **Yes**.</span></span> <span data-ttu-id="f94f9-112">El comando puede tardar varios minutos en completarse cuando se eliminan los recursos.</span><span class="sxs-lookup"><span data-stu-id="f94f9-112">The command may take several minutes to complete as resources are deleted.</span></span> 