Si es necesario, instale **Azure PowerShell** en la máquina local. Elija la sección adecuada para su sistema operativo.

## <a name="linux-and-mac"></a>Linux y Mac
En Linux y macOS, el primer paso es instalar **PowerShell Core**.

### <a name="linux"></a>Linux
Como se mencionó en la última unidad, la instalación de PowerShell para Linux implicará el uso de un administrador de paquetes. Usaremos **Ubuntu 18.04** en nuestro ejemplo aquí, pero tenemos [instrucciones detalladas para otras versiones y distribuciones en nuestra documentación](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).

Instalará PowerShell Core en Ubuntu Linux mediante Advanced Packaging Tool (**apt**) y la línea de comandos de Bash. 

1. Importe la clave de cifrado del repositorio de Ubuntu de Microsoft. Esto permitirá que el administrador de paquetes compruebe que el paquete de PowerShell Core que se instala proviene de Microsoft.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. Registre el **repositorio de Microsoft Ubuntu** para que el administrador de paquetes pueda localizar el paquete de PowerShell Core.

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. Actualice la lista de paquetes.

    ```bash
    sudo apt-get update
    ```

1. Instale PowerShell Core.

    ```bash
    sudo apt-get install -y powershell
    ```

1. Inicie PowerShell para verificar que está instalado correctamente.

    ```bash
    pwsh
    ```

### <a name="macos"></a>macOS
A continuación, instalará **PowerShell Core** en macOS con el administrador de paquetes de Homebrew.

> [!IMPORTANT]
> Si el comando **brew** no está disponible, es posible que deba instalar el administrador de paquetes de Homebrew. Para más información, vea el [sitio web de Homebrew](https://brew.sh/).

1. Instale Homebrew-Cask para obtener más paquetes, incluido el paquete de PowerShell Core:

    ```bash
    brew tap caskroom/cask
    ```
1. Instale PowerShell Core:

    ```bash
    brew cask install powershell
    ```

1. Inicie PowerShell Core para verificar que está instalado correctamente:

    ```bash
    pwsh
    ```

## <a name="install-azure-powershell"></a>Instalar Azure Powershell
Después de instalar el producto **PowerShell** base, instale **Azure PowerShell** para agregar los comandos específicos de Azure.

### <a name="windows"></a>Windows
Instale Azure PowerShell en Windows mediante el comando `Install-Module` de PowerShell.

> [!IMPORTANT]
> Necesita PowerShell versión 5.0 o posterior para instalar Azure PowerShell. Para comprobar la versión de PowerShell, use el siguiente comando: 
>
> `$PSVersionTable.PSVersion` 
>
>Si el número de versión es inferior a 5.0, siga las instrucciones para [actualizar la versión de Windows PowerShell existente](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).

1. Abra el menú **Inicio** y escriba **Windows PowerShell**.
2. Haga clic con el botón derecho en el icono **Windows PowerShell** y seleccione **Ejecutar como administrador**.
3. En el cuadro de diálogo **Control de cuentas de usuario**, seleccione **Sí**.
4. Escriba el siguiente comando y presione Entrar:

    ```powershell
    Install-Module -Name AzureRM
    ```
5. Si se le pregunta si confía en los módulos de PSGallery, responda **Sí** o **Sí a todo**.

> [!NOTE]
> Si recibe un mensaje de error que indica que ya está instalada una versión del módulo de Azure Powershell, puede actualizar a la versión _más reciente_ emitiendo el comando:
> 
> `Update-Module -Name AzureRM`
> 
> Al igual que con el comando `Install-Module`, responda **Sí** o **Sí a todo** cuando se le pregunte si confía en el módulo.

### <a name="linux-or-macos"></a>Linux o macOS
Usamos el mismo proceso básico para instalar Azure PowerShell en Linux o macOS. El procedimiento es el mismo para ambos sistemas operativos. La diferencia radica en la obtención de una sesión de PowerShell Core con privilegios elevados.

1. En un terminal, escriba el siguiente comando para iniciar PowerShell Core con privilegios elevados.

    ```bash
    sudo pwsh
    ```

1. Ejecute el siguiente comando en el símbolo del sistema de PowerShell Core para instalar Azure PowerShell.

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. Si se le pregunta si confía en los módulos de **PSGallery**, responda **Sí** o **Sí a todo**.

## <a name="summary"></a>Resumen
Ha configurado las máquinas locales para administrar recursos de Azure con Azure PowerShell. Ahora puede usar Azure PowerShell localmente para especificar comandos o ejecutar scripts. Azure PowerShell reenviará los comandos a los centros de datos de Azure, en donde se ejecutarán dentro de su suscripción de Azure.