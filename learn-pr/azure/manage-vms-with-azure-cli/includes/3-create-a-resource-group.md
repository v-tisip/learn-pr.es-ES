<span data-ttu-id="eb4aa-101">Nuestro objetivo es crear una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="eb4aa-101">Our goal is to create a new Azure virtual machine.</span></span> <span data-ttu-id="eb4aa-102">Tendremos que facilitar varios datos para identificar la ubicación del recurso, el sistema operativo que se va a utilizar y la configuración de hardware necesaria para la VM.</span><span class="sxs-lookup"><span data-stu-id="eb4aa-102">We'll need to supply several pieces of information to identify the resource location, OS to use, and the hardware configuration needed for the VM.</span></span> <span data-ttu-id="eb4aa-103">Comenzaremos por el **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="eb4aa-103">Let's start with the **resource group**.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="eb4aa-104">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="eb4aa-104">Create a resource group</span></span>

<span data-ttu-id="eb4aa-105">Azure usa _grupos de recursos_ para agrupar recursos relacionados como máquinas virtuales y bases de datos.</span><span class="sxs-lookup"><span data-stu-id="eb4aa-105">Azure uses _resource groups_ to group related resources such as virtual machines and databases together.</span></span> <span data-ttu-id="eb4aa-106">El grupo de recursos también identifica una ubicación específica (denominada "región") que determinará en qué centro de datos se coloca el recurso.</span><span class="sxs-lookup"><span data-stu-id="eb4aa-106">The resource group also identifies a specific location (called a "region") which will decide what data center the resource is placed into.</span></span>

<span data-ttu-id="eb4aa-107">Puesto que estamos experimentando, empiece por crear un grupo de recursos denominado `ExerciseResources` y colóquelo en la región `eastus`.</span><span class="sxs-lookup"><span data-stu-id="eb4aa-107">Since we're experimenting, start by creating a new resource group named `ExerciseResources` and place it into the `eastus` region.</span></span>

> [!NOTE]
> <span data-ttu-id="eb4aa-108">Asegúrese de utilizar este nombre exacto en el nuevo grupo de recursos, porque el sistema de aprendizaje de Microsoft buscará este nombre de recurso más adelante.</span><span class="sxs-lookup"><span data-stu-id="eb4aa-108">Make sure to use this exact name for your new resource group, because the Microsoft Learn system will be looking for this resource name later.</span></span> 

<span data-ttu-id="eb4aa-109">Escriba el siguiente comando de la CLI de Azure en Azure Cloud Shell para crear el grupo de recursos en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="eb4aa-109">Type the following Azure CLI command in Azure Cloud Shell to create the resource group in your subscription.</span></span>

```azurecli
az group create --name ExerciseResources --location eastus
```

<span data-ttu-id="eb4aa-110">Se devuelve un bloque JSON que indica que el grupo de recursos se ha creado.</span><span class="sxs-lookup"><span data-stu-id="eb4aa-110">This will return a JSON block indicating the resource group has been created.</span></span> <span data-ttu-id="eb4aa-111">Debe tener un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="eb4aa-111">It should look something like:</span></span>

```json
{
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources",
  "location": "eastus",
  "managedBy": null,
  "name": "ExerciseResources",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

<span data-ttu-id="eb4aa-112">Observe que devuelve el identificador único, la ubicación y el nombre de la suscripción como parte de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="eb4aa-112">Notice that it returns the subscription unique identifier, location, and name as part of the response.</span></span> <span data-ttu-id="eb4aa-113">Puede usar estos datos para comprobar que se creó en la suscripción y la ubicación adecuadas.</span><span class="sxs-lookup"><span data-stu-id="eb4aa-113">You can use these to verify it got created in the proper subscription and location.</span></span>

<span data-ttu-id="eb4aa-114">Ahora que tenemos un grupo de recursos, vamos a crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eb4aa-114">Now that we have a resource group, let's create a new virtual machine.</span></span>