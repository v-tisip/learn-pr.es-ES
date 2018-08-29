Una de las principales tareas que tendrá que hacer para ejecutar máquinas virtuales es iniciarlas y detenerlas.

## <a name="stopping-a-vm"></a>Detención de una máquina virtual

Se puede detener una máquina virtual en ejecución con el comando `vm stop`. Debe pasar el nombre y grupo de recursos, o el identificador único para la máquina virtual:

```azurecli
az vm stop -n SampleVM -g ExerciseResources
```

Podemos comprobar que se ha detenido intentando hacer ping a la dirección IP pública, mediante `ssh`, o a través del comando `vm get-instance-view`. Este enfoque final devuelve los mismos datos básicos que `vm show` pero incluye detalles acerca de la propia instancia. Pruebe a escribir el siguiente comando en Azure Cloud Shell para ver el estado de ejecución actual de la máquina virtual:

```azurecli
az vm get-instance-view -n SampleVM -g ExerciseResources --query "instanceView.statuses[?starts_with(code, 'PowerState/') == `true`].displayStatus" -o tsv
```

Este comando debe devolver `VM stopped` como resultado.

## <a name="starting-a-vm"></a>Inicio de una máquina virtual

Podemos hacer el proceso inverso con el comando `vm start`.

```azurecli
az vm start -n SampleVM -g ExerciseResources
```

Este comando iniciará una máquina virtual detenida. Podemos comprobarla a través de la consulta `vm get-instance-view`, que ahora debe devolver `VM running`.

## <a name="restarting-a-vm"></a>Reinicio de una máquina virtual

Por último, podemos reiniciar una máquina virtual si hemos realizado cambios que requieren un reinicio utilizando el comando `vm restart`. Puede agregar la marca `--no-wait` si desea que la CLI de Azure lo devuelva inmediatamente sin esperar a la máquina virtual se reinicie.

