En este ejercicio, creará una función de Azure que se invoca cada 20 segundos con un desencadenador de temporizador.

> [!NOTE] 
> Para completar este ejercicio, asegúrese de que ha iniciado sesión en [Azure Portal](https://portal.azure.com/) con una cuenta válida.

## <a name="create-an-azure-function"></a>Creación de una función de Azure

Comencemos por crear una función de Azure en el portal.

1. En el panel de la izquierda, seleccione **Crear un recurso**.

1. Seleccione **Proceso**.

1. Busque y seleccione **Function App**. También puede usar la barra de búsqueda para buscar la plantilla.

    ![Selección de Function App](../media/4-click-function-app.png)

1. En **Nombre de aplicación**, escriba un nombre único.

1. Seleccione una opción en **Suscripción**.

1. En **Grupo de recursos**, cree uno.

1. Elija **Windows** como **OS**.

1. Elija **Plan de consumo** en **Plan de hospedaje**. Se le cobrará por cada ejecución de la función. Los recursos se asignan automáticamente según la carga de trabajo de aplicación.

1. Seleccione una **ubicación**.

1. En **Storage**, cree una cuenta. (Este valor es obligatorio, pero no vamos a usarlo).

1. Desactive por ahora **Application Insights**.

1. Seleccione **Crear**.

## <a name="create-a-timer-trigger"></a>Creación de un desencadenador de temporizador

Ahora, vamos a crear un desencadenador de temporizador dentro de nuestra función de Azure.

1. Después de crear la función de Azure, seleccione **Todos los recursos** en el panel de navegación izquierdo.

1. Busque y seleccione la función de Azure.

1. En la nueva hoja, seleccione **Funciones** y seleccione el icono de signo más (+).

    ![Selección de Functions y el signo más](../media/4-hover-function.png)

1. Seleccione **Temporizador**.

1. Seleccione **CSharp** como lenguaje.

1. Seleccione **Crear esta función**.

## <a name="configure-the-timer-trigger"></a>Configuración del desencadenador de temporizador

Tenemos una función de Azure con lógica para imprimir un mensaje en la ventana de registro. Vamos a programar el temporizador para que se ejecute cada 20 segundos.

1. Seleccione **Integrar**.

1. Escriba el siguiente valor en el cuadro **Programar**:

    ```
    */20 * * * * *
    ```

1. Seleccione **Guardar**.

## <a name="start-the-timer"></a>Inicio del temporizador

Ahora que hemos configurado el temporizador, estamos listos para iniciarlo.

1. Seleccione **TimerTriggerCSharp1**. 

    > [!NOTE]
    > **TimerTriggerCSharp1** es un nombre predeterminado. Se selecciona automáticamente cuando se crea el desencadenador.

1. Seleccione **Run** (Ejecutar). 

En este punto, verá un mensaje cada 20 segundos en la ventana de registro.

## <a name="clean-up"></a>Limpieza

Para asegurarse de que no se le cobra por esta función, encima de la ventana de registro, seleccione **Pausar** para detener el temporizador.

![Pausar](../media/4-pause-timer.png)


