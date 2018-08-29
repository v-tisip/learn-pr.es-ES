Ahora que ya conoce los servicios de proceso de Azure disponibles, vamos a echar un vistazo a cada uno de ellos por separado, para ayudarle a decidir cuándo debe usar cada servicio.

## <a name="azure-virtual-machines"></a>Máquinas virtuales de Azure

Cuando se requiere un control total sobre el entorno y el sistema operativo, las máquinas virtuales son una opción ideal. Se puede personalizar todo el software que se ejecuta en la máquina virtual, al igual que un equipo físico. Esto resulta ideal cuando se ejecuta software personalizado o configuraciones de hospedaje personalizadas.

Las máquinas virtuales también son una opción excelente al pasar de un servidor físico a la nube. A menudo, se puede crear una imagen del servidor físico y hospedarla en una máquina virtual. Esto le ofrece total libertad para elegir entornos de ejecución de aplicaciones y sistemas operativos, lo cual significa que puede realizar el desarrollo en prácticamente cualquier lenguaje que use las herramientas que prefiera.

Sin embargo, se le pedirá que realice el mantenimiento de la máquina virtual. Esto significa actualizar el sistema operativo y el software que ejecuta. 

También se requieren algunas consideraciones adicionales al realizar el ajuste de escala. Se puede escalar verticalmente la máquina virtual, lo cual significa que se pueden agregar más recursos de proceso y memoria. Pero si necesita ejecutar varias instancias en paralelo, es posible que deba agregar servicios adicionales, como equilibradores de carga.

Imagine que está ejecutando un sitio web que hospeda un sitio web minorista. Si ha duplicado la máquina virtual, necesitará un servicio adicional para enrutar las solicitudes entre varias instancias de la máquina virtual de sitio web.

También hay servicios de máquinas virtuales avanzadas disponibles en Azure:

* Para ejecutar de forma coherente las instancias disponibles de la misma aplicación, o conjuntos de aplicaciones, en máquinas virtuales configuradas de forma similar, use la opción **Virtual Machine Scale Sets**. Genera automáticamente miles de máquinas virtuales idénticas cargadas con la aplicación en cuestión de minutos, por lo que los usuarios nunca tienen que esperar. Y, puesto que no tiene que aprovisionar máquinas virtuales previamente, se usan solo los recursos de proceso que su aplicación necesita en cualquier momento.

* Puede haber situaciones en que necesite potencia informática sin procesar o potencia de cálculo a nivel de superequipo. La opción **Batch** proporciona administración de procesos y programación de trabajos a escala de nube con la capacidad de ajustar la escala a decenas, cientos o miles de máquinas virtuales. Incluso puede especificar máquinas virtuales con las funcionalidades de superequipo.

## <a name="azure-containers"></a>Contenedores de Azure

Los contenedores son una excelente opción si desea ejecutar varias instancias de una aplicación en una sola máquina virtual. El orquestador de contenedores puede iniciar, detener y escalar horizontalmente las instancias de la aplicación, según sea necesario.

Sin embargo, los contenedores se usan normalmente para crear soluciones mediante una arquitectura de microservicios. Los contenedores a menudo se usan para dividir las soluciones en partes más pequeñas. Por ejemplo, se puede dividir un sitio web en un contenedor que hospeda el front-end, otro que hospeda el back-end y un tercero para el almacenamiento. Esto le permite separar las partes de la aplicación en secciones lógicas que se pueden mantener, escalar o actualizar independientemente.

Imagine que el back-end de su sitio web ha alcanzado el límite de su capacidad, pero el front-end y el almacenamiento no están sobrecargados. Puede escalar el back-end por separado para mejorar el rendimiento. O puede decidir utilizar un servicio de almacenamiento diferente. O puede reemplazar el contenedor de almacenamiento sin que ello afecte al resto de la aplicación.

 Si el equipo se encuentra cómodo con el uso de la orquestación de contenedores de Kubernetes, tenga en cuenta la opción **Azure Kubernetes Service (AKS)**. Simplifica y automatiza la administración, la implementación y las operaciones de la orquestación de Kubernetes.

## <a name="azure-functions"></a>Azure Functions

Azure Functions es una opción ideal si le preocupa sólo el código que ejecuta el servicio y no la infraestructura o la plataforma subyacente. Se usan normalmente cuando se debe realizar el trabajo en respuesta a un evento, a menudo a través de una solicitud REST, un temporizador o un mensaje de otro servicio de Azure y cuando el trabajo puede completarse rápidamente, en segundos o en menos tiempo.

Azure Functions realiza un ajuste de escala automáticamente, por lo que es una excelente opción cuando la demanda es variable y se le cobra solo cuando se desencadena una función. Por ejemplo, puede estar recibiendo mensajes de una solución de IoT que se usa para supervisar una flota de vehículos de entrega. Probablemente llegarán más datos durante el horario comercial.

Azure Functions no tiene estado; se comporta como si se reiniciara cada vez que se responde a un evento. Esto resulta ideal para procesar los datos entrantes. Y si el estado es necesario, puede estar conectado a un servicio Azure Storage.
