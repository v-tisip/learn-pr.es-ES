Azure PowerShell le permite escribir comandos y ejecutarlos de inmediato. Esto se conoce como **modo interactivo**.

Recuerde que el objetivo general del ejemplo de Administración de relaciones con los clientes (CRM) es crear tres entornos de prueba que contienen máquinas virtuales. Usará los grupos de recursos para garantizar que las máquinas virtuales se organizan en entornos independientes: uno para las pruebas unitarias, otro para las pruebas de integración y un tercero para las pruebas de aceptación. Solo tiene que crear los grupos de recursos una vez, por lo que usar el modo interactivo de PowerShell es una buena elección.

En esta sección, se muestran algunos ejemplos del uso de PowerShell de forma interactiva para iniciar sesión en su suscripción de Azure y crear grupos de recursos.

## <a name="what-are-powershell-cmdlets"></a>¿Qué son los cmdlets de PowerShell?
Un comando de PowerShell se denomina **cmdlet** (que se pronuncia “command-let”). Un cmdlet es un comando que manipula una sola característica. El término **cmdlet** pretende implicar que es un "comando pequeño". Por convención, se recomienda a los autores de los cmdlets que los mantengan sencillos y con un único propósito.

El producto base de PowerShell incluye cmdlets que funcionan con características como las sesiones y los trabajos en segundo plano. Agregue módulos a la instalación de PowerShell para obtener cmdlets que manipulen otras características. Por ejemplo, hay módulos de terceros para trabajar con FTP, administrar el sistema operativo, acceder al sistema de archivos, etc.

Los cmdlets siguen una convención de nomenclatura de verbo-sustantivo; por ejemplo, **Get-Process**, **Format-Table** y **Start-Service**. También hay una convención para la elección del verbo: "get" para recuperar datos, "set" para insertar o actualizar datos, "format" para dar formato a datos, "out" para dirigir la salida a un destino, etc.

Se recomienda a los autores de los cmdlets que incluyan un archivo de ayuda con cada cmdlet. El cmdlet **Get-Help** muestra el archivo de ayuda de cualquier cmdlet:

```powershell
Get-Help <cmdlet-name> -detailed
```

## <a name="what-is-azurerm"></a>¿Qué es AzureRM?
**AzureRM** es el nombre formal del módulo de Azure PowerShell que contiene cmdlets para trabajar con las características de Azure (**RM** significa **Resource Manager**). Contiene cientos de cmdlets que le permiten controlar casi cualquier aspecto de todos los recursos de Azure. Puede trabajar con grupos de recursos, almacenamiento, máquinas virtuales, Azure Active Directory, contenedores, aprendizaje automático, etc.

## <a name="how-to-create-a-resource-group"></a>Cómo crear un grupo de recursos
A continuación, crearemos un grupo de recursos mediante una instalación local de Azure PowerShell. 

Hay cuatro pasos: 
1. Importar los cmdlets de Azure.
1. Conectarse a la suscripción de Azure.
1. Crear el grupo de recursos.
1. Comprobar que se ha creado correctamente (ver a continuación).

![Pasos para crear un recurso en Azure mediante Azure PowerShell](../media-drafts/5-create-resource-overview.png)

Cada paso se corresponde con un cmdlet diferente.

### <a name="import"></a>Importar
Durante el inicio, PowerShell carga solo los cmdlets principales de forma predeterminada. Esto significa que no se cargarán los cmdlets que necesita para trabajar con Azure. La manera más confiable de cargar los cmdlets que necesita es importarlos de forma manual al principio de la sesión de PowerShell.

Use el cmdlet **Import-Module** para cargar módulos. Este cmdlet tiene muchos parámetros para controlar una variedad de situaciones. Por ejemplo, puede cargar varios módulos, la versión concreta de un módulo, parte de un módulo, etc. Para cargar un módulo completo, la sintaxis es simplemente:

```powershell
Import-Module <module-name>
```

> [!TIP]
> Si descubre que trabaja con Azure PowerShell con frecuencia, hay dos maneras de automatizar el proceso de carga de módulos. Puede agregar una entrada a su perfil de PowerShell para importar el módulo de Azure durante el inicio o usar las versiones más recientes de PowerShell, que cargan el módulo contenedor de forma automática cuando se usa un cmdlet.

### <a name="connect"></a>Conectar
Puesto que está trabajando con una instalación local de Azure PowerShell, tendrá que autenticarse para poder ejecutar comandos de Azure. El cmdlet **Connect-AzureRmAccount** le pide sus credenciales de Azure y luego se conecta a su suscripción de Azure. Tiene muchos parámetros opcionales, pero, si lo único que necesita es un aviso interactivo, no se necesitan parámetros:

```powershell
Connect-AzureRmAccount
```

### <a name="create"></a>Crear
El cmdlet **New-AzureRmResourceGroup** crea un grupo de recursos. Debe especificar un nombre y una ubicación. El nombre debe ser único dentro de su suscripción. La ubicación determina dónde se almacenarán los metadatos del grupo de recursos (lo que puede ser importante por motivos de cumplimiento). Use cadenas como "West US", "North Europe" o "West India" para especificar la ubicación. Al igual que con la mayoría de los cmdlets de Azure, **New-AzureRmResourceGroup** tiene muchos parámetros opcionales; en cambio, la sintaxis principal es:

```powershell
New-AzureRmResourceGroup -Name <name> -Location <location>
```

### <a name="verify"></a>Comprobar
El cmdlet **Get-AzureRmResource** enumera los recursos de Azure. Esto resulta útil en este caso para comprobar si la creación del grupo de recursos se ha completado correctamente.

```powershell
Get-AzureRmResource
```

Para obtener una vista más concisa, puede enviar la salida del cmdlet **Get-AzureRmResource** al cmdlet **Format-Table** mediante una canalización “|”.

```powershell
Get-AzureRmResource | Format-Table
```

## <a name="summary"></a>Resumen
El modo interactivo de PowerShell es adecuado para tareas aisladas. En nuestro ejemplo, usaremos el mismo grupo de recursos durante todo el proyecto, por lo que crearlo de forma interactiva es razonable. El modo interactivo suele ser más rápido y sencillo para esta tarea que escribir un script y ejecutarlo solo una vez.