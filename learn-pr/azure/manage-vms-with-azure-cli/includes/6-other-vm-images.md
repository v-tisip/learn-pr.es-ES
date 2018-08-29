Hemos utilizado `Debian` como imagen con la que se creará la máquina virtual. Azure tiene varias imágenes VM estándar que puede utilizar para crear una máquina virtual. 

Puede obtener una lista de las imágenes disponibles con el comando `az vm image list --output table`. Este generará las imágenes más populares que forman parte de una lista sin conexión integrada en la CLI de Azure. Aunque hay _cientos_ de opciones de imágenes disponibles en Azure Marketplace. 

> [!TIP]
> Puede obtener una lista completa agregando la marca `--all` al comando. Puesto que la lista de imágenes de Marketplace es muy grande, resulta útil filtrar la lista con las opciones `--publisher` u `–-offer`.

Algunas imágenes solo están disponibles en determinadas ubicaciones. Pruebe a agregar la marca `--location [location]` al comando para reducir el ámbito de los resultados a las disponibles en la región donde quiere crear la máquina virtual. Por ejemplo, escriba lo siguiente en Azure Cloud Shell para obtener una lista de imágenes disponibles en la región `eastus`.

```azurecli
az vm image list --location eastus --output table
```

> [!NOTE]
> Estas son las imágenes estándar que proporciona Azure. Tenga en cuenta que también puede [crear y cargar sus propias imágenes personalizadas](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-custom-images) para crear máquinas virtuales basadas en configuraciones únicas o en versiones o distribuciones de un sistema operativo menos comunes.