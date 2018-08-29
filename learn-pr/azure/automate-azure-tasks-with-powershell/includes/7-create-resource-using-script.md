Las tareas complejas o repetitivas suelen consumir una gran cantidad de tiempo administrativo. Las organizaciones prefieren automatizar estas tareas para reducir los costos y evitar errores.

Esto es importante en el ejemplo de la empresa Administración de relaciones con los clientes (CRM). En ese ejemplo, el software se prueba en varias máquinas virtuales (VM) con Linux que es necesario eliminar y volver a crear de forma continua. Le interesará usar un script de PowerShell para automatizar la creación de las máquinas virtuales.

Además de la operación básica de crear una máquina virtual, hay varios requisitos adicionales para el script. 
- Creará varias máquinas virtuales, por lo que le interesa colocar la creación dentro de un bucle
- Tendrá que crear las máquinas virtuales en tres grupos de recursos diferentes, por lo que el nombre del grupo de recursos se debe pasar al script como un parámetro

En esta sección, verá cómo escribir y ejecutar un script de PowerShell de Azure que cumple estos requisitos.

## <a name="what-is-a-powershell-script"></a>¿Qué es un script de PowerShell?
Un script de PowerShell es un archivo de texto que contiene comandos y construcciones de control. Los comandos son invocaciones de los cmdlets. Las construcciones de control son características de programación como bucles, variables, parámetros, comentarios, etc., proporcionadas por PowerShell.

Los archivos de script de PowerShell tienen la extensión de archivo **.ps1**. Puede crear y guardar estos archivos con cualquier editor de texto. 

> [!TIP]
> Si va a escribir scripts de PowerShell en Windows, puede usar el entorno de scripting integrado (ISE) de Windows PowerShell. Este editor proporciona características como color de sintaxis y una lista de los cmdlets disponibles.
>
>![El ISE de Windows PowerShell](../media-drafts/7-windows-powershell-ise-screenshot.png)

Después de escribir el script, para ejecutarlo desde la línea de comandos de PowerShell, pase el nombre del archivo precedido por un punto y una barra diagonal inversa:

```powershell
.\myScript.ps1
```

## <a name="powershell-techniques"></a>Técnicas de PowerShell
PowerShell tiene muchas características que se encuentran en los lenguajes de programación típicos. Se pueden definir variables, usar bifurcaciones y bucles, parámetros de línea de comandos de captura, escribir funciones, agregar comentarios y así sucesivamente. En este script se necesitarán tres características: variables, bucles y parámetros.

### <a name="variables"></a>Variables
PowerShell admite las variables. Use **$** para declarar una variable y **=** para asignar un valor. Por ejemplo:

```powershell
$loc = "East US"
$iterations = 3
```

Las variables pueden contener objetos. Por ejemplo, en la definición siguiente se establece la variable **adminCredential** para el objeto devuelto por el cmdlet **Get-Credential**.

```powershell
$adminCredential = Get-Credential
```

Para obtener el valor almacenado en una variable, use el prefijo **$** y su nombre como se muestra a continuación: 

```powershell
$loc = "East US"
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location $loc
```

### <a name="loops"></a>Bucles
PowerShell tiene varios bucles: **For**, **Do...While**, **For...Each**, etc. El bucle **For** es la mejor coincidencia para nuestras necesidades ya que ejecutará un cmdlet un número fijo de veces.

A continuación se muestra la sintaxis básica; el ejemplo se ejecuta durante dos iteraciones y, cada vez, se imprime el valor de **i**. Los operadores de comparación se escriben **-lt** para "menor que", **-le** para "menor o igual que", **eq** para "igual", **ne** para "no igual", etc.

```powershell
For ($i = 1; $i -lt 3; $i++)
{
    $i
}
```

### <a name="parameters"></a>Parámetros
Cuando se ejecuta un script, se pueden pasar argumentos en la línea de comandos. Se pueden proporcionar nombres para cada parámetro para ayudar a que el script extraiga los valores. Por ejemplo:

```powershell
.\setupEnvironment.ps1 -size 5 -location "East US"
```

Dentro del script, los valores se capturan en variables. En este ejemplo, los parámetros se comparan por nombre:

```powershell
param([string]$location, [int]$size)
```

Puede omitir los nombres de la línea de comandos. Por ejemplo:

```powershell
.\setupEnvironment.ps1 5 "East US"
```

Dentro del script, se recurre a la posición para buscar coincidencias cuando los parámetros no tienen nombre:

```powershell
param([int]$size, [string]$location)
```

## <a name="how-to-create-a-linux-virtual-machine"></a>Cómo crear una máquina virtual con Linux
Azure PowerShell proporciona el cmdlet **New-AzureRmVm** para crear una máquina virtual. El cmdlet tiene muchos parámetros para controlar la gran cantidad de opciones de configuración de la máquina virtual. La mayoría de los parámetros tiene valores predeterminados razonables, por lo que solo es necesario especificar cinco elementos:
- **ResourceGroupName**: el grupo de recursos en el que se colocará la nueva máquina virtual.
- **Name**: el nombre de la máquina virtual en Azure.
- **Location**: ubicación geográfica donde se aprovisionará la máquina virtual.
- **Credential**: un objeto que contiene el nombre de usuario y la contraseña para la cuenta de administrador de la máquina virtual. Usaremos el cmdlet **Get-Credential** para solicitar un nombre de usuario y una contraseña. **Get-Credential** empaqueta el nombre de usuario y la contraseña en un objeto de credencial, que devuelve como su resultado.
- **Image**: identidad del sistema operativo que se va a usar para la máquina virtual. Usaremos "UbuntuLTS".

A continuación se muestra la sintaxis del cmdlet:

```powershell
   New-AzureRmVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

## <a name="summary"></a>Resumen
La combinación de PowerShell y Azure PowerShell ofrece todas las herramientas necesarias para la automatización de Azure. En nuestro ejemplo CRM, podremos crear varias máquinas virtuales con Linux con un parámetro para que el script sea genérico y un bucle para evitar código repetido. Esto significa que una operación que antes era compleja ahora se puede ejecutar en un solo paso.