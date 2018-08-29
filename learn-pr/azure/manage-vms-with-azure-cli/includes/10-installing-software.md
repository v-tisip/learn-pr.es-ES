<span data-ttu-id="2658a-101">Lo último que queremos probar en nuestra máquina virtual es la instalación de un servidor web.</span><span class="sxs-lookup"><span data-stu-id="2658a-101">The last thing we want to try on our VM is to install a web server.</span></span> <span data-ttu-id="2658a-102">Uno de los paquetes más fáciles de instalar es `nginx`.</span><span class="sxs-lookup"><span data-stu-id="2658a-102">One of the easiest packages to install is `nginx`.</span></span>

1. <span data-ttu-id="2658a-103">Ubique la dirección IP pública de su máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="2658a-103">Locate the public IP address of your Linux virtual machine.</span></span> <span data-ttu-id="2658a-104">Recuerde que puede usar el comando `vm list-ip-addresses` para buscarla.</span><span class="sxs-lookup"><span data-stu-id="2658a-104">Remember you can use the `vm list-ip-addresses` command to look it up.</span></span>

2. <span data-ttu-id="2658a-105">A continuación, abra una conexión `ssh` a la máquina como hizo cuando la probamos.</span><span class="sxs-lookup"><span data-stu-id="2658a-105">Next, open an `ssh` connection to the machine like you did when we tested it.</span></span> <span data-ttu-id="2658a-106">Recuerde que necesitará pasar el nombre del administrador ("**aldis**").</span><span class="sxs-lookup"><span data-stu-id="2658a-106">Remember you will need to pass in the admin name ("**aldis**").</span></span>

3. <span data-ttu-id="2658a-107">En el shell presentado, ejecute el siguiente comando para instalar el servidor web `nginx`.</span><span class="sxs-lookup"><span data-stu-id="2658a-107">In the presented shell, execute the following command to install the `nginx` web server.</span></span>

```azurecli
sudo apt-get -y update && sudo apt-get -y install nginx
```

4. <span data-ttu-id="2658a-108">En Azure Cloud Shell, use `curl` para leer la página predeterminada del servidor web de Linux.</span><span class="sxs-lookup"><span data-stu-id="2658a-108">In Azure Cloud Shell, use `curl` to read the default page from your Linux web server.</span></span> <span data-ttu-id="2658a-109">También puede abrir una nueva pestaña del explorador e ir a la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="2658a-109">Alternatively, you can open a new browser tab and browse to the public IP address.</span></span>

```azurecli
curl 168.61.54.62
```

<span data-ttu-id="2658a-110">Se producirá un error porque la máquina virtual de Linux no expone el puerto 80 (`http`) a través del firewall integrado.</span><span class="sxs-lookup"><span data-stu-id="2658a-110">It will fail because the Linux virtual machine doesn't expose port 80 (`http`) through the built-in firewall.</span></span> <span data-ttu-id="2658a-111">Afortunadamente, la CLI de Azure tiene un comando para eso: `vm open-port`.</span><span class="sxs-lookup"><span data-stu-id="2658a-111">Luckily, the Azure CLI has a command for that: `vm open-port`.</span></span> 

5. <span data-ttu-id="2658a-112">Escriba lo siguiente en Cloud Shell para abrir el puerto 80:</span><span class="sxs-lookup"><span data-stu-id="2658a-112">Type the following into Cloud Shell to open port 80:</span></span>

```
az vm open-port --port 80 --resource-group ExerciseResources --name SampleVM
```

<span data-ttu-id="2658a-113">Por último, intente `curl` de nuevo.</span><span class="sxs-lookup"><span data-stu-id="2658a-113">Finally, try `curl` again.</span></span> <span data-ttu-id="2658a-114">Esta vez debería devolver datos.</span><span class="sxs-lookup"><span data-stu-id="2658a-114">This time it should return data.</span></span> <span data-ttu-id="2658a-115">También puede ver la página en un explorador.</span><span class="sxs-lookup"><span data-stu-id="2658a-115">You can see the page in a browser as well.</span></span>



