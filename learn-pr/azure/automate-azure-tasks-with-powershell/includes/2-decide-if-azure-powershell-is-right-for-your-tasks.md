Supongamos que necesita elegir una herramienta para administrar los recursos de Azure que se usan para probar su sistema de administración de las relaciones con el cliente (CRM). Las operaciones clave que necesita hacer son: crear grupos de recursos y aprovisionar máquinas virtuales (VM).

Desea algo que a los administradores les resulte fácil de aprender, pero con la suficiente eficacia como para automatizar la instalación y configuración de varias máquinas virtuales o crear scripts para un entorno de aplicación completo. Hay varias herramientas disponibles; deberá encontrar la mejor para su personal y sus tareas.

## <a name="what-tools-are-available"></a>¿Qué herramientas están disponibles?
Azure proporciona tres herramientas de administración entre las que puede elegir: 

1. Azure Portal 
2. La CLI de Azure
3. Azure PowerShell

Todas ofrecen prácticamente el mismo nivel de control; cualquier tarea que pueda hacer con una de las herramientas, probablemente también podrá realizarla con las otras dos. Las tres son multiplataforma, es decir, que se ejecutan en Windows, macOS y Linux. Se diferencian en la sintaxis, los requisitos de configuración y si son compatibles con la automatización.

En este caso, vamos a describir cada una de las tres opciones y ofrecemos algunos consejos sobre cómo decidir entre ellas. 

## <a name="what-is-the-azure-portal"></a>¿Qué es Azure Portal?
Azure Portal es un sitio web que le permite crear, configurar y modificar los recursos de su suscripción de Azure. El portal es una interfaz gráfica de usuario (GUI) que resulta conveniente para localizar el recurso que necesite y ejecutar todos los cambios necesarios. También ofrece orientación para tareas administrativas complejas con asistentes e información sobre herramientas.

El portal no proporciona ninguna manera de automatizar tareas repetitivas. Por ejemplo, para configurar quince máquinas virtuales, necesitaría crearlas una a una completando el asistente para cada una de ellas. Esto puede llevar mucho tiempo y ser propenso a errores si se trata de tareas complejas. 

## <a name="what-is-the-azure-cli"></a>¿Qué es la CLI de Azure?
La CLI de Azure es un programa de línea de comandos multiplataforma para conectarse a Azure y ejecutar comandos administrativos en recursos de Azure. Por ejemplo, para crear una máquina virtual, podría utilizar un comando similar al siguiente:

```bash
az vm create \
  --resource-group CrmTestingResourceGroup \
  --name CrmUnitTests \
  --image UbuntuLTS
  ...
```

La CLI de Azure está disponible de dos formas: dentro de un explorador mediante Azure Cloud Shell o con una instalación local en Linux, Mac o Windows. En ambos casos, se puede usar de forma interactiva o con scripts. Para un uso interactivo, inicie primero un shell como `cmd.exe` en Windows o Bash en Linux o macOS y, a continuación, emita el comando en el símbolo del shell. Para automatizar tareas repetitivas, ensamble los comandos en un script de shell con la sintaxis de script del shell elegido y, a continuación, ejecute el script.

## <a name="what-is-azure-powershell"></a>¿Qué es Azure PowerShell?
Azure PowerShell es un módulo que se agrega a Windows PowerShell o PowerShell Core para permitirle conectarse a la suscripción de Azure y administrar recursos. Azure PowerShell requiere PowerShell para funcionar. PowerShell proporciona servicios como la ventana de shell, análisis de comandos y mucho más. Azure PowerShell agrega los comandos específicos de Azure.

Por ejemplo, Azure PowerShell proporciona el comando **New-AzureRmVM** que crea una máquina virtual automáticamente dentro de su suscripción de Azure. Para ello, debería iniciar la aplicación de PowerShell y luego emitir un comando como el siguiente:

```powershell
New-AzureRmVm `
    -ResourceGroupName "CrmTestingResourceGroup" `
    -Name "CrmUnitTests" `
    -Image "UbuntuLTS"
    ...
```

Azure PowerShell también está disponible de dos formas: dentro de un explorador mediante Azure Cloud Shell o con una instalación local en Linux, Mac o Windows. En ambos casos, tiene dos modos para elegir. Puede usarlo en modo interactivo, en el que emite manualmente un comando a la vez, o bien en modo de scripting, en el que ejecuta un script que consta de varios comandos.

## <a name="how-to-choose-an-administrative-tool"></a>Elección de una herramienta administrativa
Existe una similitud aproximada entre Azure Portal, la CLI de Azure y Azure PowerShell con respecto a los objetos de Azure que pueden administrar y las configuraciones que pueden crear. Todas son también multiplataforma. Esto significa que normalmente podrá tener en cuenta otros factores diversos al realizar la elección:

- **Automatización**: ¿Necesita automatizar un conjunto de tareas repetitivas o complejas? Azure PowerShell y la CLI de Azure sí lo permiten, pero Azure Portal no.

- **Curva de aprendizaje**: ¿Necesita completar una tarea rápidamente sin aprender nuevos comandos o sintaxis? Azure Portal no requiere el aprendizaje de sintaxis o la memorización de comandos. En Azure PowerShell y en la CLI de Azure, debe conocer la sintaxis detallada de cada comando que use.

- **Conjunto de aptitudes del equipo**: ¿El equipo tiene experiencia? Por ejemplo, el equipo puede haber usado PowerShell para administrar Windows. En su caso, sus miembros se familiarizarán rápidamente con el uso de Azure PowerShell.

## <a name="example"></a>Ejemplo
Recuerde que ha elegido una herramienta administrativa para crear los entornos de prueba para la aplicación de CRM. Los administradores tienen dos tareas de Azure específicas que necesitarán para:

1. Crear un grupo de recursos para cada categoría de prueba (unidad, integración y aceptación).
2. Crear varias máquinas virtuales en cada grupo de recursos antes de cada ronda de pruebas.

Para crear los grupos de recursos, Azure Portal es una opción razonable. Estas son tareas de ejecución única, por lo que no necesita scripts para llevarlas a cabo.

Buscar la mejor herramienta para crear las máquinas virtuales es una decisión más complicada. Deberá crear varias y necesita hacerlo repetidamente, probablemente varias veces a la semana. Esto significa que precisará de automatización, así que, Azure Portal no es una buena opción. En este caso, Azure PowerShell o la CLI de Azure satisfarán sus necesidades. Si los miembros del equipo tienen algunos conocimientos de PowerShell, Azure PowerShell será probablemente la mejor opción. Azure PowerShell está disponible en los sistemas operativos que su equipo de administración utiliza, admite la automatización y a su equipo le debe resultar rápido de aprender.

## <a name="summary"></a>Resumen
La primera experiencia que la mayoría de los administradores tienen con Azure tiene lugar en Azure Portal. Es un excelente lugar para comenzar, ya que proporciona una interfaz gráfica limpia y bien estructurada, pero proporciona opciones limitadas para la automatización. Cuando necesite automatización, Azure ofrece dos opciones: Azure PowerShell para administradores con experiencia en PowerShell y la CLI de Azure para todos los demás.

En la práctica, las empresas suelen tener una combinación de tareas de una única ejecución y repetitivas. Esto significa que es habitual usar el portal y una solución de scripting. En nuestro ejemplo de CRM, es conveniente crear los grupos de recursos en Azure Portal y automatizar la creación de máquinas virtuales con PowerShell.

El resto de este módulo se centra en la instalación y el uso de Azure PowerShell.