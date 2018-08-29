<span data-ttu-id="de510-101">Las tareas complejas o repetitivas suelen consumir una gran cantidad de tiempo administrativo.</span><span class="sxs-lookup"><span data-stu-id="de510-101">Complex or repetitive tasks often take a great deal of administrative time.</span></span> <span data-ttu-id="de510-102">Las organizaciones prefieren automatizar estas tareas para reducir los costos y evitar errores.</span><span class="sxs-lookup"><span data-stu-id="de510-102">Organizations prefer to automate these tasks to reduce costs and avoid errors.</span></span>

<span data-ttu-id="de510-103">Esto es importante en el ejemplo de la empresa Administración de relaciones con los clientes (CRM).</span><span class="sxs-lookup"><span data-stu-id="de510-103">This is important in the Customer Relationship Management (CRM) company example.</span></span> <span data-ttu-id="de510-104">En ese ejemplo, el software se prueba en varias máquinas virtuales (VM) con Linux que es necesario eliminar y volver a crear de forma continua.</span><span class="sxs-lookup"><span data-stu-id="de510-104">There, you test your software on multiple Linux Virtual Machines (VMs) that you need to continuously delete and recreate.</span></span> <span data-ttu-id="de510-105">Le interesará usar un script de PowerShell para automatizar la creación de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="de510-105">You want to use a PowerShell script to automate the creation of the VMs.</span></span>

<span data-ttu-id="de510-106">Además de la operación básica de crear una máquina virtual, hay varios requisitos adicionales para el script.</span><span class="sxs-lookup"><span data-stu-id="de510-106">Beyond the core operation of creating a VM you have a few additional requirements for your script.</span></span> 
- <span data-ttu-id="de510-107">Creará varias máquinas virtuales, por lo que le interesa colocar la creación dentro de un bucle</span><span class="sxs-lookup"><span data-stu-id="de510-107">You will create multiple VMs, so you want to put the creation inside a loop</span></span>
- <span data-ttu-id="de510-108">Tendrá que crear las máquinas virtuales en tres grupos de recursos diferentes, por lo que el nombre del grupo de recursos se debe pasar al script como un parámetro</span><span class="sxs-lookup"><span data-stu-id="de510-108">You need to create VMs in three different resource groups, so the name of the resource group should be passed to the script as a parameter</span></span>

<span data-ttu-id="de510-109">En esta sección, verá cómo escribir y ejecutar un script de PowerShell de Azure que cumple estos requisitos.</span><span class="sxs-lookup"><span data-stu-id="de510-109">In this section, you will see how to write and execute an Azure PowerShell script that meets these requirements.</span></span>

## <a name="what-is-a-powershell-script"></a><span data-ttu-id="de510-110">¿Qué es un script de PowerShell?</span><span class="sxs-lookup"><span data-stu-id="de510-110">What is a PowerShell script?</span></span>
<span data-ttu-id="de510-111">Un script de PowerShell es un archivo de texto que contiene comandos y construcciones de control.</span><span class="sxs-lookup"><span data-stu-id="de510-111">A PowerShell script is a text file containing commands and control constructs.</span></span> <span data-ttu-id="de510-112">Los comandos son invocaciones de los cmdlets.</span><span class="sxs-lookup"><span data-stu-id="de510-112">The commands are invocations of cmdlets.</span></span> <span data-ttu-id="de510-113">Las construcciones de control son características de programación como bucles, variables, parámetros, comentarios, etc., proporcionadas por PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de510-113">The control constructs are programming features like loops, variables, parameters, comments, etc. supplied by PowerShell.</span></span>

<span data-ttu-id="de510-114">Los archivos de script de PowerShell tienen la extensión de archivo **.ps1**.</span><span class="sxs-lookup"><span data-stu-id="de510-114">PowerShell script files have a **.ps1** file extension.</span></span> <span data-ttu-id="de510-115">Puede crear y guardar estos archivos con cualquier editor de texto.</span><span class="sxs-lookup"><span data-stu-id="de510-115">You can create and save these files with any text editor.</span></span> 

> [!TIP]
> <span data-ttu-id="de510-116">Si va a escribir scripts de PowerShell en Windows, puede usar el entorno de scripting integrado (ISE) de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de510-116">If you’re writing PowerShell scripts under Windows, you can use the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="de510-117">Este editor proporciona características como color de sintaxis y una lista de los cmdlets disponibles.</span><span class="sxs-lookup"><span data-stu-id="de510-117">This editor provides features such as syntax coloring and a list of available cmdlets.</span></span>
>
>![El ISE de Windows PowerShell](../media-drafts/7-windows-powershell-ise-screenshot.png)

<span data-ttu-id="de510-119">Después de escribir el script, para ejecutarlo desde la línea de comandos de PowerShell, pase el nombre del archivo precedido por un punto y una barra diagonal inversa:</span><span class="sxs-lookup"><span data-stu-id="de510-119">Once you have written the script, execute it from the PowerShell command line by passing the name of the file preceded by a dot and a backslash:</span></span>

```powershell
.\myScript.ps1
```

## <a name="powershell-techniques"></a><span data-ttu-id="de510-120">Técnicas de PowerShell</span><span class="sxs-lookup"><span data-stu-id="de510-120">PowerShell techniques</span></span>
<span data-ttu-id="de510-121">PowerShell tiene muchas características que se encuentran en los lenguajes de programación típicos.</span><span class="sxs-lookup"><span data-stu-id="de510-121">PowerShell has many features found in typical programming languages.</span></span> <span data-ttu-id="de510-122">Se pueden definir variables, usar bifurcaciones y bucles, parámetros de línea de comandos de captura, escribir funciones, agregar comentarios y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="de510-122">You can define variables, use branches and loops, capture command-line parameters, write functions, add comments, and so on.</span></span> <span data-ttu-id="de510-123">En este script se necesitarán tres características: variables, bucles y parámetros.</span><span class="sxs-lookup"><span data-stu-id="de510-123">We will need three features for our script: variables, loops, and parameters.</span></span>

### <a name="variables"></a><span data-ttu-id="de510-124">Variables</span><span class="sxs-lookup"><span data-stu-id="de510-124">Variables</span></span>
<span data-ttu-id="de510-125">PowerShell admite las variables.</span><span class="sxs-lookup"><span data-stu-id="de510-125">PowerShell supports variables.</span></span> <span data-ttu-id="de510-126">Use **$** para declarar una variable y **=** para asignar un valor.</span><span class="sxs-lookup"><span data-stu-id="de510-126">Use **$** to declare a variable and **=** to assign a value.</span></span> <span data-ttu-id="de510-127">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="de510-127">For example:</span></span>

```powershell
$loc = "East US"
$iterations = 3
```

<span data-ttu-id="de510-128">Las variables pueden contener objetos.</span><span class="sxs-lookup"><span data-stu-id="de510-128">Variables can hold objects.</span></span> <span data-ttu-id="de510-129">Por ejemplo, en la definición siguiente se establece la variable **adminCredential** para el objeto devuelto por el cmdlet **Get-Credential**.</span><span class="sxs-lookup"><span data-stu-id="de510-129">For example, the following definition sets the **adminCredential** variable to the object returned by the **Get-Credential** cmdlet.</span></span>

```powershell
$adminCredential = Get-Credential
```

<span data-ttu-id="de510-130">Para obtener el valor almacenado en una variable, use el prefijo **$** y su nombre como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="de510-130">To obtain the value stored in a variable, use the **$** prefix and its name as shown below:</span></span> 

```powershell
$loc = "East US"
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location $loc
```

### <a name="loops"></a><span data-ttu-id="de510-131">Bucles</span><span class="sxs-lookup"><span data-stu-id="de510-131">Loops</span></span>
<span data-ttu-id="de510-132">PowerShell tiene varios bucles: **For**, **Do...While**, **For...Each**, etc.</span><span class="sxs-lookup"><span data-stu-id="de510-132">PowerShell has several loops: **For**, **Do...While**, **For...Each**, and so on.</span></span> <span data-ttu-id="de510-133">El bucle **For** es la mejor coincidencia para nuestras necesidades ya que ejecutará un cmdlet un número fijo de veces.</span><span class="sxs-lookup"><span data-stu-id="de510-133">The **For** loop is the best match for our needs because we will execute a cmdlet a fixed number of times.</span></span>

<span data-ttu-id="de510-134">A continuación se muestra la sintaxis básica; el ejemplo se ejecuta durante dos iteraciones y, cada vez, se imprime el valor de **i**.</span><span class="sxs-lookup"><span data-stu-id="de510-134">The core syntax is shown below; the example runs for two iterations and prints the value of **i** each time.</span></span> <span data-ttu-id="de510-135">Los operadores de comparación se escriben **-lt** para "menor que", **-le** para "menor o igual que", **eq** para "igual", **ne** para "no igual", etc.</span><span class="sxs-lookup"><span data-stu-id="de510-135">The comparison operators are written **-lt** for "less than", **-le** for "less than or equal", **eq** for "equal", **ne** for "not equal", etc.</span></span>

```powershell
For ($i = 1; $i -lt 3; $i++)
{
    $i
}
```

### <a name="parameters"></a><span data-ttu-id="de510-136">Parámetros</span><span class="sxs-lookup"><span data-stu-id="de510-136">Parameters</span></span>
<span data-ttu-id="de510-137">Cuando se ejecuta un script, se pueden pasar argumentos en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="de510-137">When you execute a script, you can pass arguments on the command line.</span></span> <span data-ttu-id="de510-138">Se pueden proporcionar nombres para cada parámetro para ayudar a que el script extraiga los valores.</span><span class="sxs-lookup"><span data-stu-id="de510-138">You can provide names for each parameter to help the script extract the values.</span></span> <span data-ttu-id="de510-139">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="de510-139">For example:</span></span>

```powershell
.\setupEnvironment.ps1 -size 5 -location "East US"
```

<span data-ttu-id="de510-140">Dentro del script, los valores se capturan en variables.</span><span class="sxs-lookup"><span data-stu-id="de510-140">Inside the script, you capture the values into variables.</span></span> <span data-ttu-id="de510-141">En este ejemplo, los parámetros se comparan por nombre:</span><span class="sxs-lookup"><span data-stu-id="de510-141">In this example, the parameters are matched by name:</span></span>

```powershell
param([string]$location, [int]$size)
```

<span data-ttu-id="de510-142">Puede omitir los nombres de la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="de510-142">You can omit the names from the command line.</span></span> <span data-ttu-id="de510-143">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="de510-143">For example:</span></span>

```powershell
.\setupEnvironment.ps1 5 "East US"
```

<span data-ttu-id="de510-144">Dentro del script, se recurre a la posición para buscar coincidencias cuando los parámetros no tienen nombre:</span><span class="sxs-lookup"><span data-stu-id="de510-144">Inside the script, you rely on position for matching when the parameters are unnamed:</span></span>

```powershell
param([int]$size, [string]$location)
```

## <a name="how-to-create-a-linux-virtual-machine"></a><span data-ttu-id="de510-145">Cómo crear una máquina virtual con Linux</span><span class="sxs-lookup"><span data-stu-id="de510-145">How to create a Linux Virtual Machine</span></span>
<span data-ttu-id="de510-146">Azure PowerShell proporciona el cmdlet **New-AzureRmVm** para crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="de510-146">Azure PowerShell provides the **New-AzureRmVm** cmdlet to create a Virtual Machine.</span></span> <span data-ttu-id="de510-147">El cmdlet tiene muchos parámetros para controlar la gran cantidad de opciones de configuración de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="de510-147">The cmdlet has many parameters to let it handle the large number of VM configuration settings.</span></span> <span data-ttu-id="de510-148">La mayoría de los parámetros tiene valores predeterminados razonables, por lo que solo es necesario especificar cinco elementos:</span><span class="sxs-lookup"><span data-stu-id="de510-148">Most of the parameters have reasonable default values so we only need to specify five things:</span></span>
- <span data-ttu-id="de510-149">**ResourceGroupName**: el grupo de recursos en el que se colocará la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="de510-149">**ResourceGroupName**: The resource group into which the new VM will be placed.</span></span>
- <span data-ttu-id="de510-150">**Name**: el nombre de la máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="de510-150">**Name**: The name of the VM in Azure.</span></span>
- <span data-ttu-id="de510-151">**Location**: ubicación geográfica donde se aprovisionará la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="de510-151">**Location**: Geographic location where the VM will be provisioned.</span></span>
- <span data-ttu-id="de510-152">**Credential**: un objeto que contiene el nombre de usuario y la contraseña para la cuenta de administrador de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="de510-152">**Credential**: An object containing the username and password for the VM admin account.</span></span> <span data-ttu-id="de510-153">Usaremos el cmdlet **Get-Credential** para solicitar un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="de510-153">We will use the **Get-Credential** The cmdlet to prompt for a username and password.</span></span> <span data-ttu-id="de510-154">**Get-Credential** empaqueta el nombre de usuario y la contraseña en un objeto de credencial, que devuelve como su resultado.</span><span class="sxs-lookup"><span data-stu-id="de510-154">**Get-Credential** packages the username and password into a credential object, which it returns as its result.</span></span>
- <span data-ttu-id="de510-155">**Image**: identidad del sistema operativo que se va a usar para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="de510-155">**Image**: Identity of the operating system to use for the VM.</span></span> <span data-ttu-id="de510-156">Usaremos "UbuntuLTS".</span><span class="sxs-lookup"><span data-stu-id="de510-156">We will use "UbuntuLTS".</span></span>

<span data-ttu-id="de510-157">A continuación se muestra la sintaxis del cmdlet:</span><span class="sxs-lookup"><span data-stu-id="de510-157">The syntax for the cmdlet is shown below:</span></span>

```powershell
   New-AzureRmVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

## <a name="summary"></a><span data-ttu-id="de510-158">Resumen</span><span class="sxs-lookup"><span data-stu-id="de510-158">Summary</span></span>
<span data-ttu-id="de510-159">La combinación de PowerShell y Azure PowerShell ofrece todas las herramientas necesarias para la automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="de510-159">The combination of PowerShell and Azure PowerShell gives you all the tools you need to automate Azure.</span></span> <span data-ttu-id="de510-160">En nuestro ejemplo CRM, podremos crear varias máquinas virtuales con Linux con un parámetro para que el script sea genérico y un bucle para evitar código repetido.</span><span class="sxs-lookup"><span data-stu-id="de510-160">In our CRM example, we will be able to create multiple Linux VMs using a parameter to keep the script generic and a loop to avoid repeated code.</span></span> <span data-ttu-id="de510-161">Esto significa que una operación que antes era compleja ahora se puede ejecutar en un solo paso.</span><span class="sxs-lookup"><span data-stu-id="de510-161">This means that a formerly complex operation can now be executed in a single step.</span></span>