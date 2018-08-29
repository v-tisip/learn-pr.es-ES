<span data-ttu-id="cab09-101">Una de las principales tareas que tendrá que hacer para ejecutar máquinas virtuales es iniciarlas y detenerlas.</span><span class="sxs-lookup"><span data-stu-id="cab09-101">One of the main tasks you'll want to do to running virtual machines is to start and stop them.</span></span>

## <a name="stopping-a-vm"></a><span data-ttu-id="cab09-102">Detención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cab09-102">Stopping a VM</span></span>

<span data-ttu-id="cab09-103">Se puede detener una máquina virtual en ejecución con el comando `vm stop`.</span><span class="sxs-lookup"><span data-stu-id="cab09-103">We can stop a running VM with the `vm stop` command.</span></span> <span data-ttu-id="cab09-104">Debe pasar el nombre y grupo de recursos, o el identificador único para la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="cab09-104">You must pass the name and resource group, or the unique ID for the VM:</span></span>

```azurecli
az vm stop -n SampleVM -g ExerciseResources
```

<span data-ttu-id="cab09-105">Podemos comprobar que se ha detenido intentando hacer ping a la dirección IP pública, mediante `ssh`, o a través del comando `vm get-instance-view`.</span><span class="sxs-lookup"><span data-stu-id="cab09-105">We can verify it has stopped by attempting to ping the public IP address, using `ssh`, or through the `vm get-instance-view` command.</span></span> <span data-ttu-id="cab09-106">Este enfoque final devuelve los mismos datos básicos que `vm show` pero incluye detalles acerca de la propia instancia.</span><span class="sxs-lookup"><span data-stu-id="cab09-106">This final approach returns the same basic data as `vm show` but includes details about the instance itself.</span></span> <span data-ttu-id="cab09-107">Pruebe a escribir el siguiente comando en Azure Cloud Shell para ver el estado de ejecución actual de la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="cab09-107">Try typing the following command into Azure Cloud Shell to see the current running state of your VM:</span></span>

```azurecli
az vm get-instance-view -n SampleVM -g ExerciseResources --query "instanceView.statuses[?starts_with(code, 'PowerState/')].displayStatus" -o tsv
```

<span data-ttu-id="cab09-108">Este comando debe devolver `VM stopped` como resultado.</span><span class="sxs-lookup"><span data-stu-id="cab09-108">This command should return `VM stopped` as the result.</span></span>

## <a name="starting-a-vm"></a><span data-ttu-id="cab09-109">Inicio de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cab09-109">Starting a VM</span></span>

<span data-ttu-id="cab09-110">Podemos hacer el proceso inverso con el comando `vm start`.</span><span class="sxs-lookup"><span data-stu-id="cab09-110">We can do the reverse through the `vm start` command.</span></span>

```azurecli
az vm start -n SampleVM -g ExerciseResources
```

<span data-ttu-id="cab09-111">Este comando iniciará una máquina virtual detenida.</span><span class="sxs-lookup"><span data-stu-id="cab09-111">This command will start a stopped VM.</span></span> <span data-ttu-id="cab09-112">Podemos comprobarla a través de la consulta `vm get-instance-view`, que ahora debe devolver `VM running`.</span><span class="sxs-lookup"><span data-stu-id="cab09-112">We can verify it through the `vm get-instance-view` query, which should now return `VM running`.</span></span>

## <a name="restarting-a-vm"></a><span data-ttu-id="cab09-113">Reinicio de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cab09-113">Restarting a VM</span></span>

<span data-ttu-id="cab09-114">Por último, podemos reiniciar una máquina virtual si hemos realizado cambios que requieren un reinicio utilizando el comando `vm restart`.</span><span class="sxs-lookup"><span data-stu-id="cab09-114">Finally, we can restart a VM if we have made changes that require a reboot using the `vm restart` command.</span></span> <span data-ttu-id="cab09-115">Puede agregar la marca `--no-wait` si desea que la CLI de Azure lo devuelva inmediatamente sin esperar a la máquina virtual se reinicie.</span><span class="sxs-lookup"><span data-stu-id="cab09-115">You can add the `--no-wait` flag if you want the Azure CLI to return immediately without waiting for the VM to reboot.</span></span>

