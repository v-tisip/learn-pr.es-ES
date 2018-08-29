Muchas aplicaciones usan eventos para notificar a los componentes distribuidos que se produjo un problema o que se modificó algún objeto. Puede usar Event Grid para que sea fácil distribuir esos eventos a través de Azure.

Suponga que tiene una aplicación para compartir música con una API Web que se ejecuta en Azure. Cuando un usuario carga un archivo de sonido nuevo, se debe notificar a todas las aplicaciones móviles instaladas en los dispositivos de usuarios de todo el mundo.

Puede usar las suscripciones a Azure Event Grid para lograr esta confiabilidad y hacerlo rápidamente.

## <a name="what-is-event-grid"></a>¿Qué es Event Grid?

Azure Event Grid es un servicio que distribuye los eventos desde los orígenes, como cuentas de Azure Blob Storage o Media Services, a los suscriptores, como Azure Functions o Webhooks.

Un origen de eventos es cualquier componente que puede generar un evento. Por ejemplo, un usuario podría agregar un archivo multimedia nuevo a una cuenta de Blob Storage. Esto genera un evento que se Event Grid puede distribuir.

Un suscriptor de eventos es cualquier componente que puede recibir eventos de Event Grid. Por ejemplo, una función de Azure pueden ejecutar código que responde al archivo multimedia nuevo de la cuenta de Blog Storage.

Event Grid permite conectar fácilmente los orígenes a varios suscriptores.

![Suscriptores y orígenes de Event Grid](../images/6-event-grid.png)

## <a name="event-sources"></a>Orígenes de eventos

Estos tipos de recursos de Azure pueden generar eventos:

- **Grupos de recursos y suscripciones de Azure.** Los grupos de recursos y las suscripciones generan eventos relacionados a las operaciones de administración en Azure. Por ejemplo, cuando un usuario crea una máquina virtual (VM), este origen genera un evento.
- **Cuentas de almacenamiento.** Las cuentas de almacenamiento pueden generar eventos cuando los usuarios agregan blobs, archivos, entradas de tabla o mensajes de cola. Puede usar las cuentas de blob y las cuentas de uso general como orígenes de eventos.
- **Media Services.** Media Services hospeda archivos multimedia de vídeo y audio y proporciona características de administración avanzadas para los archivos multimedia. Media Services puede generar eventos cuando un trabajo de codificación se inicia o se completa en un archivo de vídeo.
- **IoT Hub.** Azure IoT Hub se comunica con los dispositivos IoT y recopilan telemetría desde ellos. Puede generar eventos siempre que lleguen estas comunicaciones.
- **Eventos personalizados.** Eventos personalizados pueden generarse mediante la API REST o con el SDK de Azure en Java, GO,. NET, Node, Python y Ruby. Por ejemplo, podría crear un evento personalizado en un rol de trabajo de Azure Web App cuando escoge un mensaje de una cola de almacenamiento.

Esta integración amplia con diversos orígenes de eventos dentro de Azure garantiza que las instancias de Event Grid pueden distribuir eventos relacionados con casi cualquier recurso de Azure.

## <a name="topics"></a>Temas

En una instancia de Azure Event Grid, un tema es una colección de eventos relacionados. Al publicar eventos de un origen, puede decidir si esos eventos necesitan únicamente un solo tema o dividirse en varios temas. Los componentes que reciben y controlan los eventos se suscriben a temas para determinar los eventos que recibirán.

## <a name="subscriptions"></a>Suscripciones

Los controladores de eventos utilizan suscripciones para indicar a Event Grid cuáles son los eventos en un tema que desean recibir. La suscripción también corrige el punto de conexión: esta es la ubicación desde la que Event Grid envía notificaciones de eventos. Una suscripción también puede filtrar eventos por su tipo o por su asunto para que pueda asegurarse de que un controlador de eventos solo recibe los eventos pertinentes.

## <a name="event-handlers"></a>Controladores de eventos

Los siguientes tipos de objetos en Azure pueden recibir y controlar eventos desde Event Grid:

- **Azure Functions.** Una función de Azure consta de código personalizado que se ejecuta en Azure sin ningún contenedor o servidor virtual de host. Use una función de Azure como un controlador de eventos cuando quiera codificar una respuesta personalizada para el evento.
- **WebHooks.** Una instancia de WebHook es la API web que implementa una arquitectura de inserción.
- **Logic Apps.** Una instancia de Azure Logic Apps hospeda un proceso de negocio como un flujo de trabajo.
- **Microsoft Flow.** Flow también hospeda flujos de trabajo, pero es más fácil de usar para el personal no técnico.

## <a name="how-to-choose"></a>Cómo elegir

Use Event Grid cuando necesite estas características:

- **Simplicidad.** En Event Grid es muy fácil conectar orígenes a los suscriptores.
- **Filtro avanzado.** Las suscripciones tienen un control detallado sobre los eventos que reciben de un tema.
- **Distribución unificada.** Puede suscribir un número ilimitado de puntos de conexión a los mismos eventos y temas.
- **Confiabilidad** Event Grid reintenta la entrega de eventos durante hasta 24 horas para cada suscripción.
- **Pago por evento** Pague solo el número de eventos que transmite.

## <a name="summary"></a>Resumen

Event Grid es un sistema de distribución de eventos sencillo pero versátil. Puede usarlo para publicar eventos en los suscriptores, que recibirán esos eventos de manera rápida y confiable.