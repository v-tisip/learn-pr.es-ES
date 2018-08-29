## <a name="motivation"></a>Motivación
Imagine que su empresa ha elegido la CLI de Azure como solución de línea de comandos para administrar los recursos de Azure. Los administradores y programadores prefieren ejecutar sus comandos y scripts localmente en lugar de usar para ello un explorador. El equipo usa máquinas que ejecutan Windows, macOS y Linux. Deberá tener la CLI de Azure en funcionamiento en todos sus dispositivos.

## <a name="what-is-the-azure-cli"></a>¿Qué es la CLI de Azure?
La CLI de Azure es un programa de línea de comandos para conectarse a Azure y ejecutar comandos administrativos en recursos de Azure. Por ejemplo, para reiniciar una máquina virtual (VM), podría utilizar un comando similar al siguiente:

 ```bash
 az vm restart -g MyResourceGroup -n MyVm
 ```

La CLI de Azure proporciona herramientas de línea de comandos multiplataforma para administrar recursos de Azure, y puede instalarse localmente en equipos Windows, Mac o Linux. La CLI de Azure también se puede usar desde un explorador a través de Azure Cloud Shell. En ambos casos, se puede usar de forma interactiva o con scripts. Para un uso interactivo, inicie primero un shell como cmd.exe en Windows o Bash en Linux o macOS y, a continuación, emita el comando en el símbolo del shell. Para automatizar tareas repetitivas, ensamble los comandos de la CLI en un script de shell con la sintaxis de script del shell elegido y, a continuación, ejecute el script.

## <a name="how-to-install-azure-cli"></a>Instalación de la CLI de Azure
En Linux y macOS, utilice un administrador de paquetes para instalar PowerShell Core. El administrador de paquetes recomendado es diferente en función del sistema operativo y la distribución:
- Linux: **apt-get** en Ubuntu, **yum** en Red Hat y **zypper** en OpenSUSE
- Mac: **Homebrew**

La CLI de Azure está disponible en el repositorio de Microsoft, por lo que primero tendrá que agregar ese repositorio al administrador de paquetes.

En Windows, instale la CLI de Azure mediante la descarga y ejecución de un archivo MSI.

## <a name="using-the-azure-cli-in-scripts"></a>Uso de la CLI de Azure en scripts
Si desea usar los comandos de CLI de Azure en scripts, deberá tener en cuenta los problemas derivados del "shell" o el entorno utilizado para ejecutar el script. Por ejemplo, en un shell de bash, se utiliza la siguiente sintaxis al establecer las variables:

 ```bash
 variable="string"
 variable=integer
 ```

Si usa un entorno de PowerShell para ejecutar scripts de la CLI de Azure, deberá utilizar esta sintaxis para las variables:

 ```powershell
 $variable="string"
 $variable=integer
 ```

## <a name="summary"></a>Resumen
La CLI de Azure debe estar instalada para que pueda usarse a fin de administrar recursos de Azure desde un equipo local. Los pasos de instalación varían para Windows, Linux y macOS, pero una vez instalada, los comandos son iguales en todas las plataformas. 
