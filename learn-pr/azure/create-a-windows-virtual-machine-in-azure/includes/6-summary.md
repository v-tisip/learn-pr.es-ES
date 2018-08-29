<span data-ttu-id="f1b28-101">En este módulo, ha aprendido a crear una máquina virtual Windows en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f1b28-101">In this module, you learned how to create a Windows VM using the Azure portal.</span></span> <span data-ttu-id="f1b28-102">A continuación, se ha conectado a la dirección IP pública de dicha máquina virtual y la ha administrado con RDP.</span><span class="sxs-lookup"><span data-stu-id="f1b28-102">You then connected to the public IP address of that VM and managed it over RDP.</span></span> <span data-ttu-id="f1b28-103">Ha descubierto cómo RDP en Azure ofrece una experiencia similar con el inicio de sesión interactivo en un equipo físico.</span><span class="sxs-lookup"><span data-stu-id="f1b28-103">You discovered how RDP in Azure provides a similar experience to logging on interactively to a physical computer.</span></span>

<span data-ttu-id="f1b28-104">Ha observado que, mientras que RDP nos permite interactuar con el sistema operativo y el software de la máquina virtual, el portal nos permite configurar la conectividad y el hardware virtual.</span><span class="sxs-lookup"><span data-stu-id="f1b28-104">You saw that while RDP allows us to interact with the operating system and software of the virtual machine, the portal allows us to configure the virtual hardware and connectivity.</span></span> <span data-ttu-id="f1b28-105">También podríamos usar PowerShell o la CLI de Azure en caso de que prefiramos un entorno de línea de comandos o que permita ejecutar scripts en lugar del portal.</span><span class="sxs-lookup"><span data-stu-id="f1b28-105">We also could have used PowerShell or the Azure CLI, if we prefer a command-line or scriptable environment instead of the portal.</span></span>

## <a name="clean-up-lab-resources"></a><span data-ttu-id="f1b28-106">Limpieza de los recursos de laboratorio</span><span class="sxs-lookup"><span data-stu-id="f1b28-106">Clean up lab resources</span></span>

<span data-ttu-id="f1b28-107">Para quitar todos los recursos creados como parte de este módulo, elimine el grupo de recursos de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f1b28-107">To remove all the resources that you created as part of this module, delete the resource group from the Azure portal.</span></span>

1. <span data-ttu-id="f1b28-108">Inicie sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f1b28-108">Sign in to the Azure portal.</span></span>
1. <span data-ttu-id="f1b28-109">En el menú izquierdo, seleccione **Todos los servicios**.</span><span class="sxs-lookup"><span data-stu-id="f1b28-109">On the left menu, select **All Services**.</span></span>
1. <span data-ttu-id="f1b28-110">Seleccione **Grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="f1b28-110">Select **Resource Groups**.</span></span>
1. <span data-ttu-id="f1b28-111">Busque el grupo de recursos que creó en el primer ejercicio.</span><span class="sxs-lookup"><span data-stu-id="f1b28-111">Find the resource group that you created in the first exercise.</span></span> <span data-ttu-id="f1b28-112">Haga clic en los puntos suspensivos (...) en el lado derecho de la vista de lista.</span><span class="sxs-lookup"><span data-stu-id="f1b28-112">Click the ellipsis (...) on the right side of the list view.</span></span>
1. <span data-ttu-id="f1b28-113">Seleccione **Eliminar grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="f1b28-113">Select **Delete resource group**.</span></span>
1. <span data-ttu-id="f1b28-114">En la pantalla siguiente, escriba el nombre del grupo de recursos para confirmar la eliminación.</span><span class="sxs-lookup"><span data-stu-id="f1b28-114">On the next screen, enter the resource group name to confirm deletion.</span></span>
1. <span data-ttu-id="f1b28-115">Hacer clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="f1b28-115">Click **Delete**.</span></span>