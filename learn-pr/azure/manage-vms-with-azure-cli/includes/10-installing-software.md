Lo último que queremos probar en nuestra máquina virtual es la instalación de un servidor web. Uno de los paquetes más fáciles de instalar es `nginx`.

1. Ubique la dirección IP pública de su máquina virtual Linux. Recuerde que puede usar el comando `vm list-ip-addresses` para buscarla.

2. A continuación, abra una conexión `ssh` a la máquina como hizo cuando la probamos. Recuerde que necesitará pasar el nombre del administrador ("**aldis**").

3. En el shell presentado, ejecute el siguiente comando para instalar el servidor web `nginx`.

```azurecli
sudo apt-get -y update && sudo apt-get -y install nginx
```

4. En Azure Cloud Shell, use `curl` para leer la página predeterminada del servidor web de Linux. También puede abrir una nueva pestaña del explorador e ir a la dirección IP pública.

```azurecli
curl 168.61.54.62
```

Se producirá un error porque la máquina virtual de Linux no expone el puerto 80 (`http`) a través del firewall integrado. Afortunadamente, la CLI de Azure tiene un comando para eso: `vm open-port`. 

5. Escriba lo siguiente en Cloud Shell para abrir el puerto 80:

```
az vm open-port --port 80 --resource-group ExerciseResources --name SampleVM
```

Por último, intente `curl` de nuevo. Esta vez debería devolver datos. También puede ver la página en un explorador.



