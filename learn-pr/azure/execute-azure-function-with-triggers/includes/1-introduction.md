Imagine un escenario donde una concurrida peluquería tiene un problema recurrente: los clientes faltan habitualmente a sus citas. Las citas son intervalos de tiempo reservados. Si un cliente falta a una cita, la peluquería pierde dinero. Para corregir este problema, la peluquería se pone en contacto con usted, un desarrollador de software. Para corregir el problema, decide enviar mensajes de texto como recordatorio. Cada mañana, envía un mensaje de texto a cada cliente que tiene una cita ese día.

Como desarrollador de Azure, decide resolver este problema con una función de Azure. Ya sabe cómo implementar la lógica para enviar un mensaje de texto. Ahora debe aprender a enviar el mensaje en un momento determinado. Por suerte, Azure Functions admite una característica denominada _desencadenadores_. Los desencadenadores se usan para determinar cómo se ejecuta una función de Azure.

## <a name="learning-objectives"></a>Objetivos de aprendizaje
> [!div class="checklist"]
> * Determinar qué desencadenador funciona mejor para sus necesidades empresariales.
> * Crear un desencadenador de temporizador para invocar una función según una programación coherente.
> * Crear un desencadenador HTTP para invocar una función cuando se recibe una solicitud HTTP.
> * Crear un desencadenador de blobs para invocar una función al crear o actualizar un blob en Azure Storage.
