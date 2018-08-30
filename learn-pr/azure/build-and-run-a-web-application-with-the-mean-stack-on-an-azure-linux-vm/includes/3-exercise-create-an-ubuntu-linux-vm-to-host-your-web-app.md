La pila MEAN de componentes requiere un servidor. Podría ser una máquina Linux o una máquina virtual en ejecución en su propia sala de servidores, o bien se puede configurar en una máquina virtual basada en la nube. En este módulo configurará la pila para que se ejecute en una máquina virtual Ubuntu Linux que se ejecuta en Azure.

En este ejercicio, creará una máquina virtual Ubuntu Linux hospedada en Azure. También puede instalar los componentes de la pila MEAN en una máquina virtual existente o en un equipo host físico. Si crea una nueva con este ejercicio, se pueden unir todos los componentes en un grupo de recursos de Azure para facilitar la administración y la limpieza después de completar los ejercicios.

Usaremos la línea de comandos de Cloud Shell integrada en Azure Portal para crear la máquina virtual Linux.

## <a name="provision-an-ubuntu-linux-vm"></a>Aprovisionamiento de una máquina virtual Ubuntu Linux

1. Vaya a [Azure Portal](https://portal.azure.com?azure-portal=true).
1. Abra Cloud Shell desde el icono `>_` en la barra de herramientas de Azure Portal.
1. En Cloud Shell, ejecute el comando para crear un grupo de recursos de Azure, que se incluirá en nuestra máquina virtual. Sustituya el nombre del grupo de recursos propio por `<resource-group-name>` y la ubicación de Azure deseada por `<resource-group-location>` (`westus`, por ejemplo).

    ```bash
    az group create --name <resource-group-name> --location <resource-group-location>
    ```

    Recuerde el nombre del grupo de recursos porque lo usará en otros comandos.

1. En Cloud Shell, ejecute el siguiente comando para crear una nueva máquina virtual Ubuntu Linux. Sustituya el nombre del grupo de recursos propio por `<resource-group-name>` y el nombre de usuario administrador y la contraseña que prefiera por `<vm-admin-username>` y `<vm-admin-password>`.

    ```bash
    az vm create \
        --resource-group <resource-group-name> \
        --name MeanDemo \
        --image UbuntuLTS \
        --admin-username <vm-admin-username> \
        --admin-password <vm-admin-password> \
        --generate-ssh-keys
    ```

    Anote el nombre de usuario administrador y la contraseña para que pueda conectarse a esta máquina virtual más adelante.

    Este comando tarda unos 2 minutos en completarse. Cuando el comando finalice, la salida resultante será similar a esta.

    ```json
    {
        "fqdns": "",
        "id": "...",
        "location": "<location you chose for the resource group>",
        "macAddress": "00-0D-3A-3A-54-EC",
        "powerState": "VM running",
        "privateIpAddress": "10.0.0.4",
        "publicIpAddress": "<the public IP address of the newly created machine>",
        "resourceGroup": "<name you chose for thr resource group>",
        "zones": ""
    }
    ```

    También deseará guardar la dirección IP pública de la máquina virtual recién creada con el fin de conectarse a la máquina virtual.

1. Intente conectarse a la máquina virtual nueva.

    Abra un símbolo del sistema o una ventana de terminal y ejecute el siguiente comando. Sustituya el nombre de usuario administrador y la dirección IP pública de la máquina virtual mencionados por los marcadores de posición `<vm-admin-username>` y `<vm-public-ip>`.

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

    La primera vez que se conecte a la máquina, se le preguntará si confía en la máquina remota. Si responde `yes`, la huella digital de la clave ECDSA de la máquina se guardará localmente para que las conexiones subsiguientes sean de confianza.

    Si todo se ve bien, escriba `exit` para cerrar la sesión SSH.

1. Abra el puerto 80 para permitir el tráfico HTTP entrante a la aplicación web nueva que creará.

    Vuelva a Cloud Shell en Azure Portal y emita el siguiente comando, usando el nombre original del grupo de recursos para `<resource-group-name>`.

    ``` bash
    az vm open-port --port 80 --resource-group <resource-group-name> --name MeanDemo
    ```

    Con esto se abrirá el puerto HTTP de la máquina virtual que se denominó "MeanDemo" cuando se creó.

## <a name="summary"></a>Resumen

Con la nueva máquina virtual Ubuntu Linux lista para comenzar, ahora podemos conectarnos a ella para empezar la instalación de los distintos componentes de la pila MEAN.
