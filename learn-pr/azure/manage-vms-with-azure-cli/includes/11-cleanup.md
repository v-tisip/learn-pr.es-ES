<span data-ttu-id="e6415-101">Ha creado una máquina virtual de Linux, ha cambiado su tamaño, la ha detenido e iniciado, y ha actualizado la configuración con la CLI Azure.</span><span class="sxs-lookup"><span data-stu-id="e6415-101">You've created a new Linux virtual machine, changed its size, stopped and started it, and updated the configuration with the Azure CLI.</span></span>

## <a name="cleanup"></a><span data-ttu-id="e6415-102">Limpieza</span><span class="sxs-lookup"><span data-stu-id="e6415-102">Cleanup</span></span>

<span data-ttu-id="e6415-103">Ahora que hemos terminados con la máquina virtual y ya no se necesita, vamos a eliminar los recursos.</span><span class="sxs-lookup"><span data-stu-id="e6415-103">Now that we're finished with the VM and no longer need it, let's delete the resources.</span></span> <span data-ttu-id="e6415-104">La limpieza es importante para que los recursos de proceso y almacenamiento se puedan seguir facturando en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="e6415-104">Cleanup is important for compute and storage resources that can continue to be billed against your account.</span></span> 

<span data-ttu-id="e6415-105">Puede eliminar recursos individuales con el comando `delete`, pero la forma más fácil de eliminarlos todos es con `az group delete`.</span><span class="sxs-lookup"><span data-stu-id="e6415-105">You can delete individual resources with the `delete` command, but the easiest way to remove everything is with `az group delete`.</span></span> <span data-ttu-id="e6415-106">Ejecute el comando siguiente en la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="e6415-106">Execute the following command in the Azure CLI:</span></span>

```azurecli
az group delete --name ExerciseResources --no-wait
```

<span data-ttu-id="e6415-107">Responda "sí" a la pregunta cuando se muestre, o utilice el parámetro `--yes` para responder automáticamente a la pregunta.</span><span class="sxs-lookup"><span data-stu-id="e6415-107">Answer "yes" to the prompt when shown, or use the `--yes` parameter to auto-answer the prompt.</span></span>

<span data-ttu-id="e6415-108">Este comando elimina todos los recursos asociados al grupo de recursos y se garantiza que los desasigna en el orden correcto.</span><span class="sxs-lookup"><span data-stu-id="e6415-108">This command deletes all of the resources associated with the resource group, and is guaranteed to deallocate them in the correct order.</span></span> <span data-ttu-id="e6415-109">El parámetro `--no-wait` evita que la CLI de Azure se bloquee mientras se realiza la eliminación.</span><span class="sxs-lookup"><span data-stu-id="e6415-109">The `--no-wait` parameter keeps the Azure CLI from blocking while the deletion takes place.</span></span> <span data-ttu-id="e6415-110">Déjelo desactivado para esperar a que se eliminen los recursos.</span><span class="sxs-lookup"><span data-stu-id="e6415-110">Leave it off to wait for the resources to be deleted.</span></span> <span data-ttu-id="e6415-111">También puede usar el comando `az group wait -n ExerciseResources --deleted` más adelante en el script para esperar a que la eliminación termine.</span><span class="sxs-lookup"><span data-stu-id="e6415-111">Or use the `az group wait -n ExerciseResources --deleted` command later in your script to wait for the deletion to finish.</span></span>


## <a name="further-reading"></a><span data-ttu-id="e6415-112">Lecturas adicionales</span><span class="sxs-lookup"><span data-stu-id="e6415-112">Further reading</span></span>

* [<span data-ttu-id="e6415-113">Información general sobre la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e6415-113">Azure CLI overview</span></span>](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
* [<span data-ttu-id="e6415-114">Referencia de comandos de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e6415-114">Azure CLI command reference</span></span>](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)
