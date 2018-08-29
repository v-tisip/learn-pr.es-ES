
En este ejercicio, instalará la CLI de Azure en el equipo local y luego ejecutará un comando simple para comprobar la instalación. 

## <a name="installing-the-azure-cli"></a>Instalación de la CLI de Azure
El método que se usa para instalar la CLI de Azure depende del sistema operativo del equipo. Elija los pasos correspondientes a su sistema operativo.

### <a name="linux"></a>Linux
Aquí utilizará Advanced Packaging Tool (**apt**) y la línea de comandos de Bash para instalar la CLI de Azure en Ubuntu Linux.

> [!NOTE]
> Los comandos mostrados a continuación son para Ubuntu versión 18.04. Si usa otra versión de Ubuntu, debe agregar un repositorio distinto. Para más información, vea [Instalación de la CLI de Azure 2.0 con apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).

1. Modifique la lista de orígenes para que el repositorio de Microsoft quede registrado y el administrador de paquetes pueda localizar el paquete de la CLI de Azure.

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```
1. Importe la clave de cifrado del repositorio de Ubuntu de Microsoft. Esto permitirá que el administrador de paquetes compruebe que el paquete de la CLI Azure que se instala proviene de Microsoft.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. Instale la CLI de Azure.

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

### <a name="macos"></a>macOS
Aquí instalará la CLI de Azure en macOS con el administrador de paquetes de Homebrew.

> [!IMPORTANT]
> Si el comando **brew** no está disponible, es posible que deba instalar el administrador de paquetes de Homebrew. Para más información, vea el [sitio web de Homebrew](https://brew.sh/).

1. Actualice el repositorio de brew para asegurarse de que obtiene el paquete más reciente de la CLI de Azure.

    ```bash
    brew update
    ```
1. Instale la CLI de Azure.

    ```bash
    brew install azure-cli
    ```

### <a name="windows"></a>Windows
Aquí instalará la CLI de Azure en Windows con el instalador MSI.

1. Vaya a [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows) y, en el cuadro de diálogo de seguridad del explorador, haga clic en **Ejecutar**.
1. En el instalador, acepte los términos de licencia y haga clic en **Instalar**.
1. En el cuadro de diálogo **Control de cuentas de usuario**, seleccione **Sí**.

## <a name="running-the-azure-cli"></a>Ejecución de la CLI de Azure
Puede ejecutar la CLI de Azure abriendo un shell de bash (Linux y macOS) o desde el símbolo del sistema o PowerShell (Windows).

1. Inicie la CLI de Azure y compruebe la instalación ejecutando la comprobación de versión.

    ```bash
    az --version
    ```

> [!NOTE]
> En Windows, la ejecución de la CLI de Azure en PowerShell tiene algunas ventajas con respecto a la ejecución de la CLI de Azure desde el símbolo del sistema; por ejemplo, PowerShell ofrece más características de finalización de pestañas que las disponibles desde la línea de comandos. 

## <a name="summary"></a>Resumen
Configure las máquinas locales para administrar recursos de Azure con la CLI de Azure. Ahora puede usar la CLI de Azure localmente para especificar comandos o ejecutar scripts. La CLI de Azure reenviará los comandos a los centros de datos de Azure, en donde se ejecutarán dentro de su suscripción de Azure.
