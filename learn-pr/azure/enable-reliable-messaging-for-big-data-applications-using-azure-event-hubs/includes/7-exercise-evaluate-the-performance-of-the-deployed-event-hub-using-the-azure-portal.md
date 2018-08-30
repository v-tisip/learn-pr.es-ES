En este ejercicio, usará Azure Portal para comprobar el centro de eventos está funcionando según las expectativas deseadas. También probaré cómo funciona la mensajería del centro de eventos cuando no está disponible temporalmente y usará las métricas de Event Hubs para comprobar el rendimiento del centro de eventos.

## <a name="view-event-hub-activity"></a>Vista de la actividad del centro de eventos

1. Iniciar sesión en [Azure Portal](https://portal.azure.com?azure-portal=true).
1. Busque el centro de eventos en la barra de búsqueda y ábralo.

1. En la página de información general, consulte los recuentos de mensajes.

    ![Vista de los mensajes del centro de eventos](../media-draft/6-view-messages.png)

1. Las aplicaciones SimpleSend y EventProcessorSample están configuradas para enviar y recibir 100 mensajes. Verá que el centro de eventos procesó 100 mensajes provenientes de la aplicación SimpleSend y transmitió 100 mensajes a la aplicación EventProcessorSample.

## <a name="test-event-hub-resilience"></a>Prueba de la resistencia del centro de eventos

Use estos pasos para ver qué sucede cuando una aplicación envía mensajes a un centro de eventos mientras no está disponible de manera temporal.

1. Reenvíe los mensajes al centro de eventos con la aplicación SimpleSend. Use el comando siguiente:

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. Cuando vea **Envío completo...**, presione ENTRAR.

1. En Azure Portal, haga clic en **Instancia de Event Hubs** > **CONFIGURACIÓN** > **Propiedades**.
1. En Estado del centro de eventos, haga clic en **Deshabilitado**.

    ![Deshabilitación del centro de eventos](../media-draft/7-disable-event-hub.png)

Espere un mínimo de cinco minutos.

1. Haga clic en **Activar** en Estado del centro de eventos para volver a habilitar el centro de eventos y guarde los cambios.
1. Vuelva a ejecutar la aplicación EventProcessorSample para recibir mensajes. Use el comando siguiente.

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. Cuando los mensajes dejen de aparecer en la consola, presione ENTRAR.

1. En Azure Portal, busque el **_espacio de nombres_** del centro de eventos y ábralo. 

1. Haga clic en **Espacio de nombres de Event Hubs** > **SUPERVISIÓN** > **Métricas (versión preliminar)**.

    ![Uso de las métricas del centro de eventos](../media-draft/7-event-hub-metrics.png)

1. En la lista **Métrica**, seleccione **Mensajes entrantes** y haga clic en **Agregar métrica**.
1. En la lista **Métrica**, seleccione **Mensajes salientes** y haga clic en **Agregar métrica**.
1. En la parte superior del gráfico, haga clic en **Últimas 24 horas (automático)** para cambiar el período de tiempo a **Últimos 30 minutos**.
1. Haga clic en **Aplicar**.

Verá que aunque los mensajes se enviaron antes de que el centro de eventos quedará sin conexión durante un período, se transmitieron correctamente los 100 mensajes.

## <a name="summary"></a>Resumen

En esta unidad, usó las métricas de Event Hubs para probar que el centro de eventos está procesando correctamente el envío y la recepción de mensajes.
