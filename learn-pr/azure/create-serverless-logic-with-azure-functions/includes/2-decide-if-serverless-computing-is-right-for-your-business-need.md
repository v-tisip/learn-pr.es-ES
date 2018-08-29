Antes de crear el servicio de datos de temperatura, quiere asegurarse de que el proceso sin servidor es la mejor solución para el trabajo. 

## <a name="what-is-serverless-compute"></a>¿Qué es el proceso sin servidor?
El proceso sin servidor se puede considerar una función como servicio (FaaS) o un microservicio que se hospeda en una plataforma de nube. Esta función contiene el código de la lógica de negocios que se puede ejecutar sin aprovisionamiento manual ni escalar infraestructura. La plataforma de hospedaje se abstrae; no hay ningún servidor para acceder directamente ni escalado que calcular. 

## <a name="what-is-azure-functions"></a>¿Qué es Azure Functions?
Azure Functions es una plataforma de aplicaciones sin servidor. Permite que los desarrolladores hospeden la lógica de negocios que se puede ejecutar sin aprovisionar infraestructura. Azure Functions proporciona escalabilidad intrínseca y facturas solo por los recursos usados. Azure Functions se puede codificar en una variedad de lenguajes, como C#, F # y JavaScript y proporciona compatibilidad con NuGet y NPM, por lo que puede incluir muchas bibliotecas populares. 

## <a name="when-do-you-use-serverless-compute"></a>¿Cuándo se usa el proceso sin servidor?
El proceso sin servidor es una opción excelente para hospedar código de lógica de negocios en la nube. Tiene escalado automático, sin servidores para administrar, facturación de décimas de segundos y proporciona una opción de varios lenguajes de programación para la implementación. Estas son algunas características adicionales que también se proporcionan con el proceso sin servidor.

### <a name="avoid-overallocation-of-infrastructure"></a>Prevención de la sobreasignación de infraestructura
Suponga que aprovisionó servidores de máquina virtual y los configuró con recursos suficientes para controlar los tiempos de carga máxima. Cuando se carga es ligera, es posible que pudiera pagar por infraestructura que no usa. El proceso sin servidor ayuda a resolver el problema de la sobreasignación mediante el escalado o la reducción vertical automáticamente y solo se facturará cuando la función esté en ejecución.

### <a name="stateless-logic"></a>Lógica sin estado
Las funciones sin estado son excelentes candidatos para el proceso sin servidor; las instancias de funciones se crean y destruyen a petición. Si es necesario el estado, se puede almacenar en un servicio de almacenamiento asociado.

### <a name="event-driven"></a>Controladas por eventos
Las funciones de Azure son controladas por eventos; solo se ejecutan en respuesta a un evento, como recibir una solicitud HTTP o agregar un mensaje a una cola. La configuración de una función de Azure simplifica en gran medida el código base al permitirle declarar de dónde provienen los datos (enlace de entrada/desencadenador) y dónde van (enlace de salida). No es necesario escribir código para ver colas, blobs, centros, etc. El usuario se centra únicamente en la lógica de negocios.

## <a name="when-do-you-not-use-serverless-compute"></a>¿Cuándo no se usa el proceso sin servidor?
El proceso sin servidor no siempre será la solución adecuada para hospedar la lógica de negocios. Estas son algunas características de las funciones de Azure que pueden afectar a su decisión de hospedar los servicios en un proceso sin servidor. 

### <a name="execution-time"></a>Tiempo de ejecución
De manera predeterminada, las funciones de Azure tienen un tiempo de espera de 5 minutos. Se puede configurar a un máximo de 10 minutos. Si la función necesita más de 10 minutos para ejecutarse, puede hospedarla en una máquina virtual. Además, si el servicio se inicia a través de una solicitud HTTP y espera ese valor como una respuesta HTTP, el tiempo de espera se restringe aún más a 2,5 minutos.

### <a name="execution-frequency"></a>Frecuencia de ejecución
La segunda característica es la frecuencia de ejecución. Si espera que varios clientes ejecuten la función de manera continua, sería recomendable calcular el uso y el costo de usar las funciones de Azure en consecuencia. Perfectamente podría ser más barato hospedar el servicio en una máquina virtual.

Durante el escalado, solo se puede crear una instancia de aplicación de función cada 10 segundos, para hasta 200 instancias locales. Tenga en cuenta que cada instancia tiene la capacidad para atender varias ejecuciones simultáneas, por lo que no hay ningún límite establecido en la cantidad de tráfico que una sola instancia puede controlar. Diferentes tipos de desencadenadores tienen diferentes requisitos de escalado, por lo que se recomienda investigar el desencadenador que elija y sus límites.
