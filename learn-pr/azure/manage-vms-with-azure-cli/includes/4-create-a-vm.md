La CLI de Azure incluye el comando `vm` para trabajar con máquinas virtuales en Azure. Podemos proporcionar varios subcomandos para realizar tareas específicas. Los más comunes incluyen:

| Subcomando | DESCRIPCIÓN |
|-------------|-------------|
| `create`    | Creación de una máquina virtual |
| `deallocate` | Desasignación de una máquina virtual |
| `delete` | Eliminación de una máquina virtual |
| `list` | Lista de las máquinas virtuales creadas en su suscripción |
| `open-port` | Apertura de un puerto de red específico para el tráfico entrante |
| `restart` | Reinicio de una máquina virtual |
| `show` | Obtención de los detalles de una máquina virtual |
| `start` | Inicio de una máquina virtual detenida |
| `stop` | Detención de una máquina virtual en ejecución |
| `update` | Actualización de una propiedad de una máquina virtual |

> [!NOTE]
> Para una lista completa de comandos, puede comprobar la [documentación de referencia de la CLI de Azure](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).

Comencemos con el primero: `az vm create`. Este comando se utiliza para crear una máquina virtual en un grupo de recursos. Hay varios parámetros que se pueden pasar para configurar todos los aspectos de la nueva máquina virtual. Los tres parámetros que se deben proporcionar son:

| Parámetro | DESCRIPCIÓN |
|-----------|-------------|
| `resource-group` | El grupo de recursos que poseerá la máquina virtual. |
| `name` | El nombre de la máquina virtual; tiene que ser único dentro del grupo de recursos. |
| `image` | La imagen de sistema operativo que se va a usar para crear la máquina virtual. |

Además, resulta útil agregar la marca `--verbose` para ver el progreso mientras se crea la máquina virtual. 

## <a name="create-a-linux-virtual-machine"></a>Creación de una máquina virtual con Linux

Vamos a crear una máquina virtual con Linux. Ejecute el comando siguiente en Azure Cloud Shell:

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --verbose 
```

Este comando creará una nueva máquina virtual con Linux **Debian** con el nombre `SampleVM`. Tenga en cuenta que la herramienta CLI de Azure se bloquea mientras se está creando la máquina virtual. Si prefiere no esperar, puede usar la opción `--no-wait` para indicar a la herramienta CLI de Azure que vuelva de inmediato, por ejemplo, si está ejecutando el comando en un script. Más adelante, en el script, utilice el comando `azure vm wait --name [vm-name]` para esperar a que la máquina virtual termine de crearse.

Si observa las respuestas detalladas, también verá que el nombre `SampleVM` se usa para denominar varias dependencias de la máquina virtual.

```
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

Puede invalidar estos nombres de recurso generados automáticamente mediante los parámetros opcionales a `vm create`, como `--vnet-name` y `--public-ip-address-dns-name`.

Tenga en cuenta que especificamos el nombre de cuenta de administrador a través de la marca `admin-username` para que sea "aldis". Si omite esto, el comando `vm create` usará el _nombre de usuario actual_. Puesto que las reglas de los nombres de cuenta son diferentes para cada sistema operativo, es más seguro especificar un nombre concreto. No se permiten nombres comunes como "raíz" y "admin" para la mayoría de las imágenes.

También usamos la marca `generate-ssh-keys`. Este parámetro se usa para las distribuciones de Linux y crea un par de claves de seguridad, por lo que podemos usar la herramienta `ssh` para acceder a la máquina virtual de forma remota. Los dos archivos se colocan en la carpeta `.ssh` en el equipo y en la máquina virtual. Si ya tiene una clave SSH llamada `id_rsa` en la carpeta de destino, se utilizará en lugar de generar una nueva clave.

Una vez que haya terminado de crear la máquina virtual, obtendrá una respuesta JSON que incluye el estado actual de la máquina virtual y sus direcciones IP públicas y privadas asignadas por Azure:

```json
{
  "fqdns": "",
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Compute/virtualMachines/SampleVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-1A-D9-74",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "168.61.54.62",
  "resourceGroup": "ExerciseResources",
  "zones": ""
}
```

