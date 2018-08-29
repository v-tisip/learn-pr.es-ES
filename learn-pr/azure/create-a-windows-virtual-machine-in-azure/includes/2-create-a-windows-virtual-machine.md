Su empresa decidió administrar los datos de vídeo de sus cámaras de tráfico en Azure mediante máquinas virtuales. Para poder ejecutar los distintos códecs, primero es necesario crear las máquinas virtuales. También es necesario conectarse e interactuar con las máquinas virtuales. En esta unidad, obtendrá información sobre cómo crear una máquina virtual con Azure Portal. Configurará la máquina virtual para RDP, seleccionará una imagen de máquina virtual y elegirá la opción de almacenamiento adecuado.

## <a name="introduction-to-windows-virtual-machines-in-azure"></a>Introducción a las máquinas virtuales Windows en Azure

Las máquinas virtuales de Azure son un recurso de informática en la nube escalable y a petición. Son similares a las máquinas virtuales hospedadas en Windows Hyper-V. Incluyen un procesador, memoria, almacenamiento y recursos de red. Puede iniciar y detener las máquinas virtuales del mismo modo que lo haría con Hyper-V y administrarlas desde el portal o con la CLI de Azure. También puede usar un cliente RDP para conectarse directamente a la interfaz de usuario de escritorio de Windows y usar la máquina virtual como si hubiera iniciado sesión en un equipo Windows local.

## <a name="create-resources-for-a-windows-vm"></a>Creación de recursos para una máquina virtual Windows

Al crear una máquina virtual Windows en Azure, también crea recursos para hospedar la máquina virtual. Al igual que otros servicios de Azure, necesitará un **grupo de recursos**. Una práctica común es incluir otros servicios que están relacionados con la máquina virtual en el mismo grupo de recursos, incluidos:

* La máquina virtual
* Storage
* Redes virtuales 
* Interfaces de red
* Subred
* Dirección IP pública

Cuando crea una máquina virtual, puede usar un grupo de recursos existente o crear uno nuevo.

## <a name="choose-the-vm-image"></a>Elección de la imagen de máquina virtual

La selección de una imagen es una de las primeras y más importantes decisiones que deberá tomar al crear una máquina virtual. Una imagen es una plantilla que se usa para crear una máquina virtual. Estas plantillas incluyen un sistema operativo y, a menudo, otro software, como herramientas de desarrollo o entornos de hospedaje web.

Todo lo que puede haber instalado en un equipo se puede incluir en una imagen y eso es imponente. Puede crear una máquina virtual a partir de una imagen preconfigurada exactamente para las tareas que necesita, como el hospedaje de una aplicación de ASP.Net Core.

Opcionalmente, puede crear y cargar sus propias imágenes, pero que eso escapa del ámbito de este módulo.

> [!Note] 
> Es posible que observe una característica denominada "Máquina virtual (clásica)". Se trata de una característica heredada que se admite para los clientes que ya crearon instancias. Para las cargas de trabajo nuevas, se recomienda la característica "Azure Virtual Machines" o, para abreviar, "Virtual Machines".

## <a name="sizing-your-vm"></a>Ajuste del tamaño de la máquina virtual

Al igual que una máquina física tiene cierta cantidad de memoria y potencia de CPU, ocurre lo mismo con una máquina virtual. Azure ofrece una variedad de máquinas virtuales de distintos tamaños en distintos puntos de precio. Estas máquinas virtuales se inician con imágenes de desarrollo y prueba de nivel de entrada de la serie A hasta la serie D para informática de uso general. Incluyen la serie H para necesidades computacionales de alto rendimiento y la serie N para los roles optimizados para la unidad procesadora de gráficos (GPU).

Como verá más adelante en el módulo, podemos cambiar el tamaño de una máquina virtual una vez creada, pero eso requiere apagarla, lo que podría generar tiempos de inactividad para nuestras cargas de trabajo.

## <a name="choosing-storage-options"></a>Elección de las opciones de almacenamiento

La siguiente opción al especificar una máquina virtual es la tecnología de disco duro. Las opciones incluyen una unidad de disco duro (HDD) basada en placa tradicional o una unidad de estado sólido (SSD) más moderna. El uso del almacenamiento SSD es más costoso, pero brinda un mejor rendimiento, especialmente en entornos que admiten niveles altos de transferencia de datos o E/S frecuente.

> [!Note] 
> Las aplicaciones en Azure Virtual Machines también pueden conectarse a otras formas de persistencia de Azure, como Azure Cosmos DB y Azure Blob Storage.
