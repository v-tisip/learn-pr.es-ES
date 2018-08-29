<span data-ttu-id="016ae-101">Ahora que se creó una máquina virtual, podemos obtener información sobre ella a través de otros comandos.</span><span class="sxs-lookup"><span data-stu-id="016ae-101">Now that a virtual machine has been created, we can get information about it through other commands.</span></span>

<span data-ttu-id="016ae-102">Comencemos con `vm list`.</span><span class="sxs-lookup"><span data-stu-id="016ae-102">Let's start with `vm list`.</span></span>

```azurecli
az vm list
```

<span data-ttu-id="016ae-103">Este comando devolverá _todas_ las máquinas virtuales definidas en esta suscripción.</span><span class="sxs-lookup"><span data-stu-id="016ae-103">This command will return _all_ virtual machines defined in this subscription.</span></span> <span data-ttu-id="016ae-104">La salida se puede filtrar a un grupo de recursos específico mediante el parámetro `--resource-group`.</span><span class="sxs-lookup"><span data-stu-id="016ae-104">The output can be filtered to a specific resource group through the `--resource-group` parameter.</span></span> 

## <a name="output-types"></a><span data-ttu-id="016ae-105">Tipos de salida</span><span class="sxs-lookup"><span data-stu-id="016ae-105">Output types</span></span>
<span data-ttu-id="016ae-106">Tenga en cuenta que el tipo de respuesta predeterminada para todos los comandos que hemos realizado hasta ahora es JSON.</span><span class="sxs-lookup"><span data-stu-id="016ae-106">Notice that the default response type for all the commands we've done so far is JSON.</span></span> <span data-ttu-id="016ae-107">Esto es fantástico para los scripts, pero para la mayoría de las personas es más difícil de leer.</span><span class="sxs-lookup"><span data-stu-id="016ae-107">This is great for scripting - but most people find it harder to read.</span></span> <span data-ttu-id="016ae-108">Puede cambiar el estilo de salida de todas las respuestas a través de la marca `--output`.</span><span class="sxs-lookup"><span data-stu-id="016ae-108">You can change the output style for any response through the `--output` flag.</span></span> <span data-ttu-id="016ae-109">Por ejemplo, pruebe este comando en Azure Cloud Shell para ver el estilo de salida distinto.</span><span class="sxs-lookup"><span data-stu-id="016ae-109">For example, try the following command in Azure Cloud Shell to see the different output style.</span></span>

```azurecli
az vm list --output table
```

<span data-ttu-id="016ae-110">Junto con `table`, puede especificar `json` (el valor predeterminado), `jsonc` (JSON coloreado) o `tsv` (valores separados por tablas).</span><span class="sxs-lookup"><span data-stu-id="016ae-110">Along with `table`, you can specify `json` (the default), `jsonc` (colorized JSON), or `tsv` (Table-Separated Values).</span></span> <span data-ttu-id="016ae-111">Pruebe algunas variaciones con el comando anterior para ver la diferencia.</span><span class="sxs-lookup"><span data-stu-id="016ae-111">Try a few variations with the above command to see the difference.</span></span>

## <a name="getting-the-ip-address"></a><span data-ttu-id="016ae-112">Obtención de la dirección IP</span><span class="sxs-lookup"><span data-stu-id="016ae-112">Getting the IP address</span></span>

<span data-ttu-id="016ae-113">Otro comando útil es `vm list-ip-addresses`, que enumerará las direcciones IP públicas y privadas de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="016ae-113">Another useful command is `vm list-ip-addresses`, which will list the public and private IP addresses for a VM.</span></span> <span data-ttu-id="016ae-114">Si cambian o no las capturó durante la creación, puede recuperarlas en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="016ae-114">If they change, or you didn't capture them during creation, you can retrieve them at any time.</span></span>

```azurecli
az vm list-ip-addresses -n SampleVM -o table
```

<span data-ttu-id="016ae-115">Esto devuelve:</span><span class="sxs-lookup"><span data-stu-id="016ae-115">This returns:</span></span>

```
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM          168.61.54.62         10.0.0.4
```

> [!NOTE]
> <span data-ttu-id="016ae-116">Tenga en cuenta que estamos usando una sintaxis abreviada para la marca `--output` como `-o`.</span><span class="sxs-lookup"><span data-stu-id="016ae-116">Notice that we are using a shorthand syntax for the `--output` flag as `-o`.</span></span> <span data-ttu-id="016ae-117">La mayoría de los parámetros de los comandos de la CLI de Azure se pueden abreviar como un solo guion y una letra.</span><span class="sxs-lookup"><span data-stu-id="016ae-117">Most parameters to Azure CLI commands can be shortened to a single dash and letter.</span></span> <span data-ttu-id="016ae-118">Por ejemplo, `--name` se puede abreviar como `-n` y `--resource-group` como `-g`.</span><span class="sxs-lookup"><span data-stu-id="016ae-118">For example, `--name` can be shortened to `-n` and `--resource-group` to `-g`.</span></span> <span data-ttu-id="016ae-119">Esto resulta útil para escribir, pero en los scripts se recomienda usar el nombre completo de la opción para mayor claridad.</span><span class="sxs-lookup"><span data-stu-id="016ae-119">This is handy for typing, but we recommend using the full option name in scripts for clarity.</span></span> <span data-ttu-id="016ae-120">Consulte la documentación para más detalles sobre cada comando.</span><span class="sxs-lookup"><span data-stu-id="016ae-120">Check the documentation for details on each command.</span></span>

## <a name="getting-vm-details"></a><span data-ttu-id="016ae-121">Obtención de detalles de VM</span><span class="sxs-lookup"><span data-stu-id="016ae-121">Getting VM details</span></span>

<span data-ttu-id="016ae-122">Es posible obtener información más detallada sobre una máquina virtual específica por nombre o identificador con el comando `vm show`.</span><span class="sxs-lookup"><span data-stu-id="016ae-122">We can get more detailed information about a specific virtual machine by name or ID using the `vm show` command.</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM
```

<span data-ttu-id="016ae-123">Esto devolverá un bloque JSON bastante grande con todo tipo de información sobre la máquina virtual, incluidos los dispositivos de almacenamiento conectado, las interfaces de red y todos los identificadores de objeto para los recursos a los que está conectada la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="016ae-123">This will return a fairly large JSON block with all sorts of information about the VM, including attached storage devices, network interfaces, and all of the object IDs for resources that the VM is connected to.</span></span> <span data-ttu-id="016ae-124">Nuevamente, podríamos cambiar a un formato de tabla, pero eso omite prácticamente todos los datos de interés.</span><span class="sxs-lookup"><span data-stu-id="016ae-124">Again, we could change to a table format, but that omits almost all of the interesting data.</span></span> <span data-ttu-id="016ae-125">En su lugar, podemos volver a un lenguaje de consulta integrada de JSON llamado [JMESPath](http://jmespath.org/).</span><span class="sxs-lookup"><span data-stu-id="016ae-125">Instead, we can turn to a built-in query language for JSON called [JMESPath](http://jmespath.org/).</span></span>

## <a name="adding-filters-to-queries-with-jmespath"></a><span data-ttu-id="016ae-126">Incorporación de filtros a consultas con JMESPath</span><span class="sxs-lookup"><span data-stu-id="016ae-126">Adding filters to queries with JMESPath</span></span>

<span data-ttu-id="016ae-127">JMESPath es un lenguaje de consulta estándar del sector creado en torno a los objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="016ae-127">JMESPath is an industry-standard query language built around JSON objects.</span></span> <span data-ttu-id="016ae-128">La consulta más sencilla consiste en especificar un _identificador_ que selecciona una clave en el objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="016ae-128">The simplest query is to specify an _identifier_ that selects a key in the JSON object.</span></span>

<span data-ttu-id="016ae-129">Por ejemplo, dado el objeto:</span><span class="sxs-lookup"><span data-stu-id="016ae-129">For example, given the object:</span></span>

```json
{
  "people": [
    {
      "name": "Fred",
      "age": 28
    },
    {
      "name": "Barney",
      "age": 25
    },
    {
      "name": "Wilma",
      "age": 27
    }
  ]
}
```

<span data-ttu-id="016ae-130">Podemos usar la consulta `people` para devolver la matriz de valores para la matriz `people`.</span><span class="sxs-lookup"><span data-stu-id="016ae-130">We can use the query `people` to return the array of values for the `people` array.</span></span> <span data-ttu-id="016ae-131">Si solo queremos _una_ de las personas, podemos usar un indexador.</span><span class="sxs-lookup"><span data-stu-id="016ae-131">If we just want _one_ of the people, we can use an indexer.</span></span> <span data-ttu-id="016ae-132">Por ejemplo, `people[1]` devolvería:</span><span class="sxs-lookup"><span data-stu-id="016ae-132">For example, `people[1]` would return:</span></span>

```json
{
    "name": "Barney",
    "age": 25
}
```

<span data-ttu-id="016ae-133">También podemos agregar calificadores específicos que devolverían solo los objetos `Fred` y `Wilma`.</span><span class="sxs-lookup"><span data-stu-id="016ae-133">We can also add specific qualifiers that would return just the `Fred` and `Wilma` objects.</span></span> 

```json
[
  {
    "name": "Fred",
    "age": 28
  },
  {
    "name": "Wilma",
    "age": 27
  }
]
```

<span data-ttu-id="016ae-134">Por último, los resultados se pueden restringir si se agrega una instrucción select: `people[?age > '25'].[name]` que devuelve solo los nombres:</span><span class="sxs-lookup"><span data-stu-id="016ae-134">Finally, we can constrain the results by adding a select: `people[?age > '25'].[name]` that returns just the names:</span></span>

```json
[
  [
    "Fred"
  ],
  [
    "Wilma"
  ]
]
```

<span data-ttu-id="016ae-135">JMESQuery tiene varias otras características de consulta interesantes.</span><span class="sxs-lookup"><span data-stu-id="016ae-135">JMESQuery has several other interesting query features.</span></span> <span data-ttu-id="016ae-136">Cuando tenga tiempo, consulte el [tutorial en línea](http://jmespath.org/tutorial.html) disponible en el sitio [JMESPath.org](http://jmespath.org/).</span><span class="sxs-lookup"><span data-stu-id="016ae-136">When you have time, check out the [online tutorial](http://jmespath.org/tutorial.html) available on the [JMESPath.org](http://jmespath.org/) site.</span></span>

## <a name="filtering-our-azure-cli-queries"></a><span data-ttu-id="016ae-137">Filtrado de consultas de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="016ae-137">Filtering our Azure CLI queries</span></span>

<span data-ttu-id="016ae-138">Con un conocimiento básico de las consultas JMES, podemos agregar filtros a los datos devueltos por las consultas, como el comando `vm show`.</span><span class="sxs-lookup"><span data-stu-id="016ae-138">With a basic understanding of JMES queries, we can add filers to the data being returned by queries like the `vm show` command.</span></span> <span data-ttu-id="016ae-139">Por ejemplo, podemos recuperar el nombre de usuario del administrador:</span><span class="sxs-lookup"><span data-stu-id="016ae-139">For example, we can retrieve the admin user name:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "osProfile.adminUsername"
```

<span data-ttu-id="016ae-140">Podemos obtener el tamaño asignado a la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="016ae-140">We can get the size assigned to our VM:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query hardwareProfile.vmSize
```

<span data-ttu-id="016ae-141">O bien, para recuperar todos los identificadores para las interfaces de red, puede usar la consulta:</span><span class="sxs-lookup"><span data-stu-id="016ae-141">Or to retrieve all the IDs for your network interfaces, you can use the query:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id"
```

<span data-ttu-id="016ae-142">Esta técnica de consulta funcionará con cualquier comando de CLI de Azure y se puede usar para extraer elementos específicos de datos en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="016ae-142">This query technique will work with any Azure CLI command and can be used to pull specific bits of data out on the command line.</span></span> <span data-ttu-id="016ae-143">También es útil para los scripts. Por ejemplo, puede extraer un valor de la cuenta de Azure y almacenarlo en una variable de entorno o script.</span><span class="sxs-lookup"><span data-stu-id="016ae-143">It is useful for scripting as well - for example, you can pull a value out of your Azure account and store it in an environment or script variable.</span></span> <span data-ttu-id="016ae-144">Si decide usarla este modo, es un marcador útil para agregar el parámetro `--output tsv` (que se puede abreviar como `-o tsv`).</span><span class="sxs-lookup"><span data-stu-id="016ae-144">If you decide to use it this way, a useful flag to add is the `--output tsv` parameter (which can be shortened to `-o tsv`).</span></span> <span data-ttu-id="016ae-145">Esto devolverá los resultados en valores separados por tabulaciones que solo incluyan los valores de datos con separadores de tabulación.</span><span class="sxs-lookup"><span data-stu-id="016ae-145">This will return the results in tab-separated values that only include the actual data values with tab separators.</span></span>

<span data-ttu-id="016ae-146">Como ejemplo,</span><span class="sxs-lookup"><span data-stu-id="016ae-146">As an example,</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id" -o tsv
```

<span data-ttu-id="016ae-147">devuelve el texto: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`</span><span class="sxs-lookup"><span data-stu-id="016ae-147">returns the text: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`</span></span>
