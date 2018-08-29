Suponga que ha elegido Azure PowerShell como solución de automatización. Los administradores prefieren ejecutar sus scripts localmente en lugar de en Azure Cloud Shell. El equipo usa máquinas que ejecutan Windows, macOS y Linux. Es preciso que la CLI de Azure funcione en todos los dispositivos. 

## <a name="what-must-be-installed"></a>¿Qué hay que instalar?
Repasaremos las instrucciones de instalación en la siguiente unidad, pero veamos los dos componentes que constituyen Azure PowerShell.

- **El producto PowerShell básico** Viene en dos variantes: PowerShell en Windows y PowerShell Core en macOS y Linux.
- **El módulo Azure PowerShell** Este módulo adicional debe estar instalado para agregar los comandos específicos de Azure PowerShell.

> [!NOTE]
> PowerShell se incluye con Windows (pero puede que haya una actualización disponible). Tendrá que instalar PowerShell Core en Linux y macOS.

Cuando haya instalado el producto base, agregue el módulo Azure PowerShell a la instalación.

## <a name="how-to-install-powershell-core"></a>Instalación de PowerShell Core
En Linux y macOS, utilice un administrador de paquetes para instalar PowerShell Core. El administrador de paquetes recomendado varía en función del sistema operativo y la distribución.

> [!NOTE]
> PowerShell Core está disponible en el repositorio de Microsoft, por lo que primero tendrá que agregar ese repositorio al administrador de paquetes.

### <a name="linux"></a>Linux
En Linux, el administrador de paquetes cambiará en función de la distribución de Linux que se elija.

| Distribuciones  | Administrador de paquetes |
|------------------|-----------------|
| Ubuntu, Debian   | `apt-get`       |
| Red Hat, CentOS  | `yum`           |
| OpenSUSE         | `zypper`        |
| Fedora           | `dnf`           |

### <a name="mac"></a>Mac
En macOS, utilizará `Homebrew` para instalar PowerShell Core.

## <a name="how-to-install-azure-powershell"></a>Instalación de Azure PowerShell
Cuando tenga PowerShell instalado, el método de instalación preferido del módulo Azure PowerShell es usar el comando `Install-Module` en PowerShell. Necesitará privilegios elevados para instalar módulos.

- En Windows, debe ejecutar PowerShell como administrador.
- En Linux y macOS, usará el comando `sudo` para obtener privilegios elevados.

## <a name="summary"></a>Resumen
En Windows, PowerShell está integrado, pero hay que instalar el módulo Azure PowerShell. En Linux y macOS, debe instalar PowerShell Core y el módulo Azure PowerShell. En la sección siguiente, repasará los pasos de instalación detallados para algunas plataformas comunes.