Supongamos que va a planear la arquitectura de una aplicación para compartir música. Debe elegir la opción que le permita garantizar que los archivos de música se carguen en la API web de forma confiable desde la aplicación móvil.

Una vez haya entendido que esta comunicación debe ser un mensaje, debe elegir si usar las colas de Azure Storage o Service Bus, ya que ambos pueden usarse para almacenar las colas de los mensajes mientras esperan a su procesamiento.

## <a name="delivery-guarantees"></a>Garantías de entrega

Los sistemas de colas generalmente garantizan la entrega de cada mensaje de la cola a un componente de destino. Sin embargo, estas garantías pueden adoptar enfoques diferentes:

- **Entrega al menos una vez.** En este enfoque, se garantiza que cada mensaje se entregue al menos a uno de los componentes que recuperan los mensajes de la cola. Sin embargo, tenga en cuenta que, en determinadas circunstancias, puede que el mismo mensaje se entregue más de una vez. Por ejemplo, si hay dos instancias de una aplicación web que recupera mensajes de una cola, normalmente cada mensaje va solo a una de esas instancias. Sin embargo, si una instancia tarda mucho tiempo en procesar el mensaje y se agota el tiempo de espera, puede que el mensaje también se envíe a la otra instancia. El código de la aplicación web debe diseñarse teniendo en mente esta posibilidad.
- **Entrega como máximo una vez.** En este enfoque, no se garantiza la entrega de cada mensaje y hay muy pocas probabilidades de que no llegue. Sin embargo, no hay posibilidad de que el mensaje se entregue dos veces como en el caso de la entrega al menos una vez.
- **Primero en caducar primero en salir (FIFO).** En la mayoría de los sistemas de mensajería, los mensajes normalmente dejan la cola en el mismo orden en que se agregaron, pero debe considerar si se garantiza este orden. Si la aplicación distribuida requiere que los mensajes se proceden precisamente en el orden correcto, debe elegir un sistema de cola que incluya una garantía FIFO.

## <a name="transactions"></a>Transacciones

Algunos grupos estrechamente relacionados de mensajes pueden causar problemas cuando se produce un error en la entrega de un mensaje del grupo.

Por ejemplo, piense en una aplicación de comercio electrónico. Cuando el usuario hace clic en el botón "Comprar", se envía un mensaje con los detalles del pedido junto con un mensaje con los detalles de la tarjeta de crédito. Si no se entregó el mensaje de la tarjeta de crédito, puede que el pedido se envíe sin el pago.

Puede evitar estos tipos de problemas mediante la agrupación de los dos mensajes en una transacción. Las transacciones se realizan correctamente o con errores como una sola unidad. Si se produce un error con la entrega del mensaje de los detalles de la tarjeta de crédito, entonces se producirá también con el mensaje de los detalles del pedido.

## <a name="when-to-use-storage-queues"></a>Cuándo usar las colas de Storage

Las colas se utilizan para los mensajes pero no para los eventos.

Las cuentas de Azure Storage incluyen colas, que las aplicaciones distribuidas pueden utilizar como ubicaciones de almacenamiento temporal para los mensajes. Un componente de origen puede agregar un mensaje a la cola. Los componentes de destino recuperan el mensaje en la parte delantera de la cola para procesarlo. Dichas colas aumentan la confiabilidad del intercambio de mensajes porque, en los momentos de gran demanda, los mensajes pueden simplemente esperar a que un componente de destino esté listo para procesarlos.

Las colas también se proporcionan como parte de la mensajería de Azure Service Bus. Si ha decidido utilizar una cola de Azure para una comunicación específica, debe decidir si desea utilizar una cola de Storage o una de Service Bus.

Para realizar esta elección, plantéese estas preguntas:

- ¿Necesita una garantía de entrega como máximo una vez?
- ¿Necesita una garantía FIFO?
- ¿Necesita agrupar los mensajes en transacciones?
- ¿Necesita almacenar mensajes mayores de 64 KB?

Si la respuesta a alguna de estas preguntas es afirmativa, debe elegir usar una cola de Service Bus.

Tenga en cuenta además:

- ¿Necesita registros de servidor de todos los mensajes que pasan por la cola?
- ¿Espera que la cola supere el tamaño de 80 GB?

Si la respuesta a alguna de estas preguntas es afirmativa, debe elegir usar una cola de Storage.

## <a name="summary"></a>Resumen

Una cola es una ubicación de almacenamiento temporal simple para los mensajes enviados entre los componentes de una aplicación distribuida. Use una cola para organizar el mensaje y controlar correctamente aumentos impredecibles de la demanda.

Use colas de Azure Storage si desea disponer de un sistema de cola sencillo y fácil de codificar. Para las necesidades más avanzadas, use las colas de Azure Service Bus.