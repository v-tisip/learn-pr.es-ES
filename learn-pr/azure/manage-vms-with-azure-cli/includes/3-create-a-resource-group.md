Nuestro objetivo es crear una máquina virtual de Azure. Tendremos que facilitar varios datos para identificar la ubicación del recurso, el sistema operativo que se va a utilizar y la configuración de hardware necesaria para la VM. Comenzaremos por el **grupo de recursos**.

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Azure usa _grupos de recursos_ para agrupar recursos relacionados como máquinas virtuales y bases de datos. El grupo de recursos también identifica una ubicación específica (denominada "región") que determinará en qué centro de datos se coloca el recurso.

Puesto que estamos experimentando, empiece por crear un grupo de recursos denominado `ExerciseResources` y colóquelo en la región `eastus`.

> [!NOTE]
> Asegúrese de utilizar este nombre exacto en el nuevo grupo de recursos, porque el sistema de aprendizaje de Microsoft buscará este nombre de recurso más adelante. 

Escriba el siguiente comando de la CLI de Azure en Azure Cloud Shell para crear el grupo de recursos en su suscripción.

```azurecli
az group create --name ExerciseResources --location eastus
```

Se devuelve un bloque JSON que indica que el grupo de recursos se ha creado. Debe tener un aspecto similar al siguiente:

```json
{
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources",
  "location": "eastus",
  "managedBy": null,
  "name": "ExerciseResources",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

Observe que devuelve el identificador único, la ubicación y el nombre de la suscripción como parte de la respuesta. Puede usar estos datos para comprobar que se creó en la suscripción y la ubicación adecuadas.

Ahora que tenemos un grupo de recursos, vamos a crear una máquina virtual.