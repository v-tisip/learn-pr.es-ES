En este ejercicio, vamos a crear una función de Azure que acepta una solicitud HTTP con una sola cadena. La función devuelve una cadena al autor de la llamada para representar si se ha completado correctamente o no.

> [!NOTE]
> Para completar este ejercicio, asegúrese de que ha iniciado sesión en [Azure Portal](https://portal.azure.com/) con una cuenta válida.

## <a name="create-an-http-trigger"></a>Creación de un desencadenador HTTP

Vamos a continuar usando nuestra aplicación de Azure Functions existente y agregar un desencadenador HTTP.

1. Vaya a **Functions** y seleccione el icono de signo más (+).

    ![Selección de Functions y puntero sobre el signo más](../media/4-hover-function.png)

1. Seleccione **Desencadenador HTTP**.

1. Seleccione **C#** como lenguaje. 

1. Deje el **Nombre** establecido en el valor predeterminado.

1. Establezca el **Nivel de autorización** en **Anónimo**.

1. Seleccione **Crear**.

1. Eche un vistazo rápido al código generado automáticamente para hacerse una idea sobre lo que está ocurriendo. El parámetro *req* representa la solicitud entrante y contiene un parámetro *name*. Comprobamos si *name* tiene un valor. Si es así, devolvemos un saludo. En caso contrario, devolvemos un mensaje de error.

## <a name="get-your-function-url"></a>Obtención de la dirección URL de función

Ahora que hemos creado el desencadenador HTTP, vamos a obtener la dirección URL de la función para que podamos empezar a realizar una solicitud.

1. Seleccione el desencadenador HTTP para abrir la pantalla de código.

1. A la derecha de **Ejecutar**, seleccione **Obtención de dirección URL de la función**.

1. Seleccione **Copiar**.

1. Seleccione **Ejecutar** para iniciar la función.

## <a name="issue-a-get-request-to-your-http-trigger"></a>Emisión de una solicitud GET al desencadenador HTTP

Ahora tenemos nuestra dirección URL de la función copiada en el Portapapeles. Vamos a emitir una solicitud GET para ver si se obtiene una respuesta.

1. Abra una nueva pestaña en el explorador web.

1. Pegue la dirección URL en la barra de direcciones.

1. Agregue un parámetro de cadena de consulta denominado *name* con su nombre; por ejemplo:

    ```
    .../api/HttpTriggerCSharp1?name=Jesse
    ```

1. Presione ENTRAR para enviar la solicitud.

## <a name="clean-up"></a>Limpieza

Para asegurarse de que no se le cobra por esta función, seleccione **Pausar** encima de la ventana de registro.

![Pausar](../media/4-pause-timer.png)


