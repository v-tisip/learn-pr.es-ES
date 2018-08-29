Las máquinas virtuales deben tener el tamaño adecuado para el trabajo que se espera. Una máquina virtual sin la cantidad correcta de memoria o de CPU generará un error en la carga o se ejecutará muy lentamente para que sea eficaz. 

Al crear una máquina virtual puede especificar un valor de _Tamaño de VM_ que determinará la cantidad de recursos de proceso que se dedicará a la máquina virtual. Esto incluye la CPU, la GPU y la memoria que Azure pone a disposición de la máquina virtual.

Azure define un conjunto de [tamaños de máquina virtual predefinidos](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) para Linux y Windows entre los que elegir según el uso previsto. 

| Escriba | Tamaños | DESCRIPCIÓN |
|------|-------|-------------|
| Uso general   | Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7 | Uso equilibrado de CPU y memoria. Ideal para desarrollo/pruebas, así como para soluciones de datos y aplicaciones de tamaño pequeño a mediano. |
| Proceso optimizado | Fs, F | Uso elevado de la CPU respecto a la memoria. Adecuado para aplicaciones, dispositivos de red y procesos por lotes con tráfico mediano. |
| Memoria optimizada  | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Uso elevado de memoria respecto al núcleo. Excelente para bases de datos relacionales, memorias caché de capacidad de media a grande y análisis en memoria. |
| Almacenamiento optimizado | LS | Alto rendimiento de disco y E/S. Perfecto para macrodatos y bases de datos SQL y NoSQL. |
| GPU optimizada | NV, NC | Máquinas virtuales especializadas específicas para actividades intensas de representación de gráficos y edición de vídeo. |
| Alto rendimiento | H, A8-11 | Nuestras máquinas virtuales con CPU más eficaces e interfaces de red de alto rendimiento (RDMA) opcionales. | 

Los tamaños disponibles cambian en función de la región en la que se crea la máquina virtual. Puede obtener una lista de los tamaños disponibles con el comando `vm list-sizes`. Pruebe a escribir esto en Azure Cloud Shell:

```azurecli
az vm list-sizes --location eastus --output table
```

Esta es una respuesta abreviada para `eastus`:

```
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          2048  Standard_B1ms                         1           1047552                    4096
                 2          1024  Standard_B1s                          1           1047552                    2048
                 4          8192  Standard_B2ms                         2           1047552                   16384
                 4          4096  Standard_B2s                          2           1047552                    8192
                 8         16384  Standard_B4ms                         4           1047552                   32768
                16         32768  Standard_B8ms                         8           1047552                   65536
                 4          3584  Standard_DS1_v2                       1           1047552                    7168
                 8          7168  Standard_DS2_v2                       2           1047552                   14336
                16         14336  Standard_DS3_v2                       4           1047552                   28672
                32         28672  Standard_DS4_v2                       8           1047552                   57344
                64         57344  Standard_DS5_v2                      16           1047552                  114688
        ....
                64       3891200  Standard_M128-32ms                  128           1047552                 4096000
                64       3891200  Standard_M128-64ms                  128           1047552                 4096000
                64       3891200  Standard_M128ms                     128           1047552                 4096000
                64       2048000  Standard_M128s                      128           1047552                 4096000
                64       1024000  Standard_M64                         64           1047552                 8192000
                64       1792000  Standard_M64m                        64           1047552                 8192000
                64       2048000  Standard_M128                       128           1047552                16384000
                64       3891200  Standard_M128m                      128           1047552                16384000
```

No se especificó un tamaño al crear la VM, por lo que Azure seleccionó un tamaño de uso general predeterminado de `Standard_DS1_v2` por nosotros. Pero se puede especificar el tamaño como parte del comando `vm create` con el parámetro `--size`.

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM \
  --image Debian --admin-username aldis --generate-ssh-keys --verbose \
  --size "Standard_DS5_v2"
```

## <a name="resizing-an-existing-vm"></a>Cambio del tamaño de una máquina virtual existente
También se puede cambiar el tamaño de una máquina virtual existente si la carga de trabajo cambia o si se especificó un tamaño incorrecto durante la creación. Antes de solicitar un cambio de tamaño, hay que comprobar si el tamaño que se quiere está disponible en el clúster del que la máquina virtual forma parte. Para ello, se puede usar el comando `vm list-vm-resize-options`:

```azurecli
az vm list-vm-resize-options --resource-group ExerciseResources --name SampleVM --output table
```

Este devolverá una lista de todas las configuraciones de tamaño posibles que hay disponibles en el grupo de recursos. Si el tamaño que se quiere no está disponible en el clúster, pero _está_  disponible en la región, se puede [desasignar la máquina virtual](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-deallocate). Este comando detendrá la máquina virtual en ejecución y la quitará del clúster actual sin perder ningún recurso. Entonces se puede cambiar el tamaño, con lo que volverá a crearse la máquina virtual en un nuevo clúster donde la configuración de tamaño esté disponible.

Para cambiar el tamaño de una máquina virtual, se utiliza el comando `vm resize`. Por ejemplo, vamos a reducir nuestros recursos de máquina virtual actuales al mínimo: 2 G de memoria, 1 núcleo de CPU y 4 G de espacio en disco. Escriba este comando en Cloud Shell:

```azurecli
az vm resize --resource-group ExerciseResources --name SampleVM --size "Standard_B1ms"
```

Este comando tardará unos minutos en reducir los recursos de la máquina virtual y, cuando finalice, devolverá una nueva configuración de JSON.