Ha creado una máquina virtual de Linux, ha cambiado su tamaño, la ha detenido e iniciado, y ha actualizado la configuración con la CLI Azure.

## <a name="cleanup"></a>Limpieza

Ahora que hemos terminados con la máquina virtual y ya no se necesita, vamos a eliminar los recursos. La limpieza es importante para que los recursos de proceso y almacenamiento se puedan seguir facturando en su cuenta. 

Puede eliminar recursos individuales con el comando `delete`, pero la forma más fácil de eliminarlos todos es con `az group delete`. Ejecute el comando siguiente en la CLI de Azure:

```azurecli
az group delete --name ExerciseResources --no-wait
```

Responda "sí" a la pregunta cuando se muestre, o utilice el parámetro `--yes` para responder automáticamente a la pregunta.

Este comando elimina todos los recursos asociados al grupo de recursos y se garantiza que los desasigna en el orden correcto. El parámetro `--no-wait` evita que la CLI de Azure se bloquee mientras se realiza la eliminación. Déjelo desactivado para esperar a que se eliminen los recursos. También puede usar el comando `az group wait -n ExerciseResources --deleted` más adelante en el script para esperar a que la eliminación termine.


## <a name="further-reading"></a>Lecturas adicionales

* [Información general sobre la CLI de Azure](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
* [Referencia de comandos de la CLI de Azure](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)
