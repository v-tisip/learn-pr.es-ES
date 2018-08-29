Muchas aplicaciones constan de programas que se ejecutan en varios dispositivos o equipos diferentes. En esas aplicaciones distribuidas, se deben enviar los mensajes entre los componentes a través de redes y grandes distancias. Incluso en el mismo servidor o en el mismo centro de datos, las arquitecturas sin conexión directa requieren mecanismos para que los componentes se comuniquen. La mensajería de confianza suele ser un problema crítico.

Supongamos que trabaja en una compañía de software que desarrolla una aplicación para compartir música. Los músicos pueden cargar la música que crean en la plataforma con una aplicación móvil o web front-end. Pueden escuchar y comentar el trabajo de los otros miembros. La aplicación consta de un sitio web que se ejecuta en su ISP, una aplicación móvil que se ejecuta en los dispositivos móviles de los usuarios, una API web que se ejecuta en Azure y una instancia de Azure SQL Database donde se almacenan los datos.

Ha observado que, en momentos de alta demanda, algunos archivos de música no se cargaron correctamente y algunos comentarios no se publicaron. Las pruebas revelan que estos problemas se deben a mensajes quitados entre los componentes front-end y la API web. Planea solucionar estos problemas con una o varias de las siguientes tecnologías de Azure: colas de Storage, Event Hubs, Event Grid y Service Bus.

En este caso, obtendrá información sobre cómo elegir la tecnología de mensajería adecuada de Azure para cada tarea de comunicación de una aplicación distribuida.

## <a name="learning-objectives"></a>Objetivos de aprendizaje

- Describa eventos, mensajes y problemas; puede usarlos para solucionar problemas en una aplicación distribuida.
- Identifique escenarios en los que una cola de Azure Storage es la mejor tecnología de mensajería para una aplicación.
- Identifique escenarios en los que Azure Event Grid es la mejor tecnología de mensajería para una aplicación.
- Identifique escenarios en los que Azure Event Hubs es la mejor tecnología de mensajería para una aplicación.
- Identifique escenarios en los que Azure Service Bus es la mejor tecnología de mensajería para una aplicación.
