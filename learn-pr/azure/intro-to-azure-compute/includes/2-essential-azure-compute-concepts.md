El equipo de investigación necesita realizar un procesamiento de datos con un uso intenso de cálculo y no tiene el equipo para realizar el trabajo. Se ha decidido usar Azure para realizar el análisis de datos.

## <a name="what-is-azure-compute"></a>¿Qué es Azure Compute?
Azure Compute es un servicio de recursos informáticos a petición para ejecutar aplicaciones basadas en la nube. Proporciona recursos informáticos, como procesadores de núcleo múltiple y supercomputadoras a través de máquinas virtuales y contenedores. También proporciona informática sin servidor para habilitar la ejecución de aplicaciones sin necesidad de configurar o instalar infraestructura. Los recursos están disponibles a petición y normalmente se pueden crear en minutos o incluso en segundos. Solo se paga por los recursos que se usan y solo durante el tiempo que se usan.

Existen tres técnicas comunes para realizar el proceso en Azure:
1. Máquinas virtuales
1. Contenedores
1. Informática sin servidor

## <a name="what-are-virtual-machines"></a>¿Qué son las máquinas virtuales?

Una **máquina virtual (VM)** es una emulación de software de un equipo físico. Incluyen un procesador virtual, memoria, almacenamiento y recursos de red. Hospedan un sistema operativo y permiten instalar y ejecutar software, al igual que en un equipo físico. Además, si usa un cliente de escritorio remoto, podrá utilizar y controlar las máquinas virtuales como si se estuviera sentado delante de un terminal físico.

### <a name="virtual-machines-in-azure"></a>Máquinas virtuales en Azure

Se pueden crear y hospedar máquinas virtuales en Azure. Normalmente se pueden crear y aprovisionar nuevas máquinas virtuales en cuestión de minutos, seleccionando una imagen de máquina virtual preconfigurada.

Seleccionar una imagen es una de las decisiones más importantes que debe tomar al crear una máquina virtual. Una imagen es una plantilla usada para crear una máquina virtual. Estas plantillas ya incluyen un sistema operativo (SO) y a menudo otro software, como herramientas de desarrollo o entornos de hospedaje de web.

## <a name="what-are-containers"></a>¿Qué son los contenedores?

Los contenedores son un entorno de virtualización, pero no incluyen un sistema operativo, a diferencia de una máquina virtual. Como alternativa, hacen referencia al sistema operativo del entorno de host que ejecuta el contenedor. Por ejemplo, si cinco contenedores se están ejecutando en un servidor con un kernel de Linux específico, los cinco contenedores se están ejecutando en ese mismo kernel. 

Los contenedores normalmente contienen una aplicación escrita por el usuario e incluirán las bibliotecas necesarias para que la aplicación se ejecute en el kernel del entorno de host. 

Los contenedores se han diseñado para ser ligeros y para que se creen, se escalen horizontalmente y se detengan dinámicamente cuando el entorno y la demanda cambien.

Una ventaja del uso de contenedores es la capacidad de ejecutar varias aplicaciones aisladas en una máquina virtual. Dado que los propios contenedores están protegidos y aislados, no es estrictamente necesario separar las máquinas virtuales para cargas de trabajo independientes.

Azure admite contenedores de Docker y varias maneras de administrar estos contenedores. Los contenedores se pueden administrar manualmente o con servicios de Azure como Azure Kubernetes Service.

### <a name="what-is-serverless-computing"></a>¿Qué es la informática sin servidor?

La informática sin servidor es un entorno de ejecución hospedado en la nube que ejecuta el código pero abstrae por completo el entorno de hospedaje subyacente. El usuario crea una instancia del servicio y agrega el código, pero no debe —incluso no se le permite— realizar ningún mantenimiento ni configuración de la infraestructura.

Las aplicaciones sin servidor se configuran para responder a eventos. Podría tratarse de un punto de conexión REST, un temporizador o un mensaje recibido de otro servicio de Azure. La aplicación sin servidor se ejecuta solo cuando la desencadena un evento. 

La infraestructura no es responsabilidad del usuario. El ajuste de escala y el rendimiento se controlan automáticamente y se facturan solo los recursos exactos que se usan. Incluso no hay ninguna necesidad de reservar capacidad.

Azure tiene dos implementaciones de proceso sin servidor: **Azure Functions**, que puede ejecutar código prácticamente en cualquier lenguaje moderno, y **Azure Logic Apps**, que permite ejecutar lógica desencadenada por servicios de Azure sin escribir código.
