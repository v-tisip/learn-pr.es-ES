Una función de Azure no funciona hasta que algo le indique que se ejecute. Por ejemplo, podríamos crear una función de Azure para enviar un mensaje de texto de recordatorio a nuestros clientes antes de una cita. Si no indicamos a la función cuándo debe ejecutarse, nuestros clientes nunca recibirán un mensaje. 

Aquí, examinará los desencadenadores a un alto nivel y explorará los tipos de desencadenadores más comunes.

## <a name="what-is-a-trigger"></a>¿Qué es un desencadenador?

Un desencadenador es un servicio que define cómo se invoca una función de Azure. Por ejemplo, si desea que una función se ejecute cada diez minutos, podría usar un desencadenador de temporizador.

Cada función debe tener exactamente un desencadenador asociado. Si desea ejecutar un fragmento de lógica en varias condiciones, deberá crear varias funciones.

## <a name="what-is-a-binding"></a>¿Qué es un enlace?

Un enlace es una conexión a datos dentro de la función. Los enlaces son opcionales y se presentan en forma de enlaces de entrada y salida. Un enlace de entrada se corresponde con los datos que la función recibe. Un enlace de salida se corresponde con los datos que la función envía.

A diferencia de un desencadenador, una función puede tener varios enlaces de entrada y salida.

## <a name="types-of-triggers"></a>Tipos de desencadenadores

Azure Functions admite una amplia gama de tipos de desencadenadores. Estos son algunos de los tipos más comunes:

| Escriba | Propósito | 
| --- | --- | 
| **Temporizador** | Ejecutar una función en un intervalo establecido. | 
| **HTTP** | Ejecutar una función cuando se recibe una solicitud HTTP. |  
| **Blob** | Ejecutar una función cuando se carga un archivo o se actualiza en Azure Blob Storage. | 
| **Cola** | Ejecutar una función cuando se agrega un mensaje a una cola de Azure Storage. | 
| **Cosmos DB** | Ejecutar una función cuando cambia un documento en una colección. | 
| **Event Hubs** | Ejecutar una función cuando un centro de eventos recibe un evento nuevo. | 

En este módulo, nos vamos a centrar en los tipos **temporizador**, **HTTP** y **blob**.

## <a name="summary"></a>Resumen

Para ejecutar una función de Azure, es necesario utilizar un desencadenador. Los desencadenadores de temporizador, HTTP y blob son los tres tipos más comunes que usará para ejecutar la lógica sin servidor.
