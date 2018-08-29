Supongamos que va a planear la arquitectura de una aplicación distribuida para compartir música. Desea asegurarse de que la aplicación es tan confiable y escalable como sea posible y piensa utilizar tecnologías de Azure para crear una infraestructura de comunicación sólida.

Para poder elegir la tecnología de Azure adecuada, debe conocer todas las comunicaciones individuales que los componentes de la aplicación intercambian. Puede elegir una tecnología de Azure diferente para cada comunicación.

Lo primero que hay que saber sobre una comunicación es si envía mensajes o eventos. Algunas tecnologías de Azure están destinadas a eventos y otras a mensajes, por lo que se trata de una elección fundamental.

## <a name="what-is-a-message"></a>¿Qué es un mensaje?

En la terminología de las aplicaciones distribuidas, los **mensajes** tienen las siguientes características:

- Un mensaje contiene datos sin procesar producidos por un componente, que será consumido por otro componente.
- Un mensaje contiene los datos, no solo una referencia a esos datos.
- El componente de envío espera a que el componente de destino procese el contenido del mensaje de una forma determinada. La integridad del sistema global puede depender de que el remitente y receptor realicen un trabajo específico.

Por ejemplo, supongamos que un usuario carga una canción nueva con la aplicación móvil para compartir música. La aplicación móvil debe enviar dicha canción a la API web que se ejecuta en Azure. Se debe enviar el archivo multimedia de la canción, no solo una alerta que indique que se ha agregado una canción nueva. La aplicación móvil espera que la API web almacene la canción nueva en la base de datos y que la ponga a disposición de otros usuarios. Este es un ejemplo de un mensaje.

## <a name="what-is-an-event"></a>¿Qué es un evento?

Los **eventos** pesan algo menos que los mensajes y son los que se usan con más frecuencia para las comunicaciones de difusión. Los componentes que envían el evento se llaman **publicadores** y los destinatarios se conocen como **suscriptores**.

Con los eventos, los componentes destinatarios, por lo general, decidirán qué comunicaciones les interesan y se "suscribirán" a ellas. La suscripción la suele administrar un intermediario, como Azure Event Grid o Azure Event Hubs. Cuando los publicadores envían un evento, el intermediario enrutará ese evento a los suscriptores interesados. Se conoce como una "arquitectura publicación-suscripción", que no es la única manera de tratar los eventos, pero sí la más común.

Los eventos tienen las siguientes características:

- Un evento es una notificación ligera que indica que algo ha sucedido.
- El evento puede enviarse a varios destinatarios o a ninguno.
- Los eventos suelen estar diseñados para la "distribución ramificada de salida" o para disponer de un número elevado de suscriptores para cada publicador.
- El publicador del evento no tiene ninguna expectativa sobre la acción que realiza un componente receptor.
- Algunos eventos son unidades discretas y no están relacionados con otros eventos. 
- Algunos eventos forman parte de una serie ordenada y relacionada.  

Por ejemplo, supongamos que se ha completado la carga del archivo de música y que se ha agregado la nueva canción a la base de datos. Para informar a los usuarios del nuevo archivo, la API web debe informar a los usuarios de la aplicación móvil y front-end del nuevo archivo. Los usuarios pueden optar por escuchar la canción nueva, por lo que la notificación inicial no incluye el archivo de música, sino que solo notifica a los usuarios que la canción está disponible. El remitente no tiene ninguna expectativa específica de que los destinatarios del evento harán algo en particular como respuesta a la recepción de este evento.

Este es un ejemplo de un evento discreto.

## <a name="how-to-choose-messages-or-events"></a>Elección de los mensajes o eventos

Es probable que una única aplicación use eventos para algunos propósitos y mensajes para otros. Antes de elegir, debe analizar la arquitectura de la aplicación y todos sus casos de uso para identificar todas las distintas finalidades que sus componentes tienen para comunicarse entre sí. 

Es más probable que los eventos se usen para difusiones y que suelan ser efímeros, lo que significa que puede que un destinatario no tenga la posibilidad de administrar una comunicación si no hay ningún suscriptor actualmente. Es más probable que los mensajes se usen si la aplicación distribuida requiere una garantía de que se procese la comunicación.

Para cada comunicación, plantéese la pregunta: ¿el componente de envío espera que el componente de destino procese la comunicación de una forma determinada?

Si la respuesta es afirmativa, opte por usar un mensaje. Si la respuesta es no, es posible que pueda utilizar los eventos.

## <a name="summary"></a>Resumen

Los componentes de una aplicación distribuida se comunican entre sí para muchos propósitos diferentes. Para cada uno de estos propósitos, debe elegir si desea utilizar eventos o mensajes para que pueda elegir una tecnología de Azure que está diseñada para ese propósito. 

Después de entender por qué los componentes se comunican y saber si usan eventos o mensajes, puede elegir entre las colas de Azure Storage, Event Hubs, Event Grid o Service Bus para intercambiar la información.