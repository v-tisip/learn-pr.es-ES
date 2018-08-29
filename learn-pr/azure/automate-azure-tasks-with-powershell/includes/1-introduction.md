La creación de scripts de administración es una manera eficaz para optimizar el flujo de trabajo. Puede automatizar tareas comunes y repetitivas y, una vez comprobado, un script se ejecutará constantemente, lo que probablemente reduzca los errores.

Supongamos que trabaja en una empres que utiliza Azure Virtual Machines (VM) para probar el software de administración de las relaciones con el cliente (CRM). Las máquinas virtuales se crean a partir de imágenes que incluyen una web front-end, un servicio web que implementa la lógica de negocios y una base de datos SQL.

Ha estado ejecutando varias rondas de pruebas en una sola máquina virtual, pero ha notado que los cambios en la base de datos y los archivos de configuración pueden causar resultados incoherentes. En un caso, un error creó un registro de llamada telefónica sin un cliente correspondiente en la base de datos. El registro huérfano ocasionó que las pruebas de integración posteriores no se realizaran incluso después de corregir el error. Piensa resolver este problema mediante la implementación de una nueva máquina virtual para cada ciclo de pruebas. Quiere automatizar la instalación de la creación de máquina virtual porque se ejecutará muchas veces por semana. 

Aquí, verá cómo administrar recursos de Azure mediante Azure PowerShell. Utilizará Azure PowerShell interactivamente para tareas aisladas y escribirá scripts para automatizar tareas repetitivas. 

## <a name="learning-objectives"></a>Objetivos de aprendizaje
> [!div class="checklist"]
> * Decidir si Azure PowerShell es la herramienta adecuada para sus tareas de administración de Azure
> * Instalar Azure PowerShell en Linux, macOS y Windows
> * Conectarse a una suscripción de Azure con Azure PowerShell
> * Crear recursos de Azure con Azure PowerShell

## <a name="prerequisites"></a>Requisitos previos
- Experiencia con una interfaz de línea de comandos como PowerShell o Bash
- Conocimiento de conceptos básicos de Azure como grupos de recursos y máquinas virtuales
- Experiencia con la administración de recursos de Azure mediante Azure Portal
