En este ejercicio, vamos a crear una función de Azure que muestra el nombre y el tamaño de un blob cuando se crea o actualiza. 

> [!NOTE]
> Para completar este ejercicio, asegúrese de que ha iniciado sesión en [Azure Portal](https://portal.azure.com/) con una cuenta válida.

## <a name="create-a-blob-trigger"></a>Creación de un desencadenador de blobs

Nuevamente, vamos a seguir usando nuestra aplicación de Azure Functions existente y agregarle un desencadenador de blobs.

1. Vaya a **Functions** y seleccione el icono de signo más (+).

    ![Selección de Functions y el signo más](../media/4-hover-function.png)

1. Seleccione **Desencadenador de blobs**.

1. Seleccione **C#** como lenguaje. 

1. Deje el **Nombre** establecido en el valor predeterminado.

1. Deje la **Ruta** establecida en el valor predeterminado.

1. Seleccione una cuenta de Azure Storage existente o seleccione **Crear** si desea que Azure cree una nueva cuenta en su lugar.

## <a name="download-storage-explorer"></a>Descarga del Explorador de Storage

Ahora que hemos creado un desencadenador de blobs, vamos a descargar el Explorador de Storage, que nos permitirá crear fácilmente un blob.

- Descargue el [Explorador de Storage](http://storageexplorer.com).

## <a name="connect-to-your-azure-storage-account"></a>Conexión a la cuenta de Azure Storage

Ya tenemos descargado el Explorador de Storage. Vamos a iniciar sesión con las credenciales proporcionadas.

1. En el Explorador de Storage, seleccione el icono de signo más (+) de la izquierda.

1. Seleccione **Usar un nombre y clave de la cuenta de almacenamiento**.

1. Seleccione **Next** (Siguiente).

1. En Azure, en el desencadenador de blobs, seleccione **Integración**.

1. Seleccione **Documentación** para expandir la vista.

1. Copie el **Nombre de cuenta** y la **Clave de cuenta**.

1. De nuevo en el Explorador de Storage, pegue el **Nombre de cuenta** y la **Clave de cuenta**.

1. Especifique un **Nombre para mostrar**. Este valor es el nombre de la conexión en el Explorador de Storage.

1. Seleccione **Next** (Siguiente).

1. Seleccione **Conectar**. 

## <a name="create-a-blob-container"></a>Creación de un contenedor de blobs

No estamos conectados a nuestra cuenta de Azure Storage. Recuerde que el desencadenador de blobs está supervisando solo la ubicación que se describe en el campo **Ruta**. De forma predeterminada, la ruta de acceso debe ser:

> samples-workitems/{name}

Es necesario crear un contenedor denominado **samples-workitems**.

1. En el Explorador de Storage, expanda la cuenta de almacenamiento. El nombre debe ser el **Nombre para mostrar** que haya proporcionado durante el proceso de conexión.

1. Haga clic con el botón derecho en **Contenedores de blobs** y seleccione **Crear contenedor de blobs**.

1. Escriba **samples-workitems**.

## <a name="turn-on-your-blob-trigger"></a>Activación del desencadenador de blobs

Ahora que hemos creado nuestro contenedor para supervisar, vamos a ejecutar la función para que podamos ver la salida cuando se crea un blob.

1. Seleccione el desencadenador de blobs para abrir la pantalla del código.

1. Seleccione **Run** (Ejecutar).

## <a name="create-a-blob"></a>Creación de un blob

El desencadenador de blobs ya está listo para escuchar la actividad. Vamos a crear un blob para ver si se recibe un mensaje de registro.

1. En el Explorador de Storage, seleccione el contenedor **samples-workitems**.

1. Seleccione **Cargar**. 

1. Seleccione **Cargar archivos**.

1. Seleccione cualquier archivo de su equipo.

1. Seleccione **Cargar**.

1. Vuelva a Azure. Busque en los registros un mensaje que indique qué archivo se cargó.

## <a name="clean-up"></a>Limpieza

Para asegurarse de que no se le cobra por esta función, seleccione **Pausar** encima de la ventana de registro.

![Pausar](../media/4-pause-timer.png)


