En este ejercicio, usará el cliente RDP para conectarse a la máquina virtual Windows que ha creado en la unidad anterior. Puede conectarse si descarga y ejecuta un archivo RDP desde Azure Portal. Este archivo RDP tendrá:

* La dirección IP pública de la máquina virtual.
* El número de puerto.

## <a name="motivation"></a>Motivación

De acuerdo con el escenario de nuestro ejercicio, ahora es un estudiante y quiere obtener información sobre cómo agregar roles y características a un equipo con Windows Server. En cambio, el administrador de red no quiere que lo haga en un equipo físico en la red y los equipos de la escuela no están nada preparados para ejecutar Windows Hyper-V. Azure proporciona la solución perfecta.

## <a name="configure-network-and-public-ip-address-settings"></a>Configuración de las opciones de la dirección IP pública y la red

1. En Azure Portal, asegúrese de que está abierta la hoja de la máquina virtual que ha creado anteriormente. Puede encontrar la hoja en **Todos los recursos** si tiene que abrirla.

1. Vaya a la sección **Redes**. En la parte superior de esta sección hay vínculos a la subred virtual y la dirección IP dinámica que se crearon junto con nuestra máquina virtual, ya que usamos los valores predeterminados. Podemos seguir estos vínculos si queremos cambiar esos recursos (por ejemplo, cambiar a una dirección IP estática).

1. Haga clic en **Agregar regla de puerto de entrada**.

1. En la parte superior del cuadro de diálogo **Agregar regla de seguridad de entrada**, haga clic en **Básica**.

1. En **Servicio**, seleccione **RDP** y después haga clic en **Agregar**.

## <a name="connect-to-the-vm-by-using-rdp"></a>Conexión a la máquina virtual mediante RDP

Para descargar el archivo RDP y conectarse a la máquina virtual, siga estos pasos.

### <a name="download-the-rdp-file"></a>Descarga del archivo RDP

1. En la sección **Introducción** de la hoja de la máquina virtual, haga clic en **Conectar**.

1. En la hoja **Conectarse a una máquina virtual**, observe las opciones de configuración **Dirección IP** y **Número de puerto**; después, haga clic en **Descargar archivo RDP**.

1. En el explorador, haga clic en **Abrir** o en **Ejecutar** para abrir el archivo RDP.

### <a name="connect-to-the-windows-vm"></a>Conexión a la máquina virtual Windows

1. En el cuadro de diálogo **Conexión a Escritorio remoto**, observe la advertencia de seguridad y la dirección IP del equipo remoto, y haga clic en **Conectar**.

1. En el cuadro de diálogo **Seguridad de Windows**, escriba el nombre de usuario y la contraseña que ha usado en los pasos 6 y 7.

1. En el segundo cuadro de diálogo **Conexión a Escritorio remoto**, observe los errores de certificado y, después, haga clic en **Sí**.

   > [!Note]
   > El escritorio de la máquina virtual tarda un poco en aparecer. Este efecto se debe a que la imagen de B1 se ha subespecificado. Puede que reciba un mensaje sobre la asignación de memoria baja.

1. En el cuadro de diálogo **Redes**, haga clic en **No**.

### <a name="resize-the-vm-in-the-azure-portal"></a>Cambio del tamaño de la máquina virtual en Azure Portal

1. Vuelva a Azure Portal. En la página de propiedades de la máquina virtual, en **Propiedades**, haga clic en **Tamaño**.

1. Haga clic en **D2s_v3** (2 vCPU, 8 GB de RAM) y después en **Seleccionar**. Se mostrará un mensaje de cambio de tamaño de la máquina virtual. También se cerrará la máquina virtual de la ventana de RDP.

1. Vuelva a Azure Portal. En el panel izquierdo, haga clic en **Máquinas virtuales**.

1. En **Máquinas virtuales**, espere hasta que la máquina virtual muestre el estado **En ejecución**. Puede que tenga que hacer clic en **Actualizar**.

1. Haga clic en el nombre de la máquina virtual y, en **Configuración**, haga clic en **Tamaño**. Observe que el tamaño de la máquina virtual ahora está establecido en **D2s_v3**.

### <a name="reconnect-to-the-resized-vm"></a>Nueva conexión a la máquina virtual a la que se ha cambiado el tamaño

1. Haga clic en **Máquinas virtuales** y después en su máquina virtual. Observe que es probable que el valor de **Dirección IP pública** haya cambiado. Haga clic en **Conectar**  y después en **Ejecutar** o **Abrir** en el explorador.

1. En el cuadro de diálogo **Conexión a Escritorio remoto**, observe la advertencia de seguridad y la dirección IP del equipo remoto, y haga clic en **Conectar**.

1. En el cuadro de diálogo **Seguridad de Windows**, escriba el nombre de usuario y la contraseña que ha usado en los pasos 6 y 7.

1. En el segundo cuadro de diálogo **Conexión a Escritorio remoto**, observe los errores de certificado y, después, haga clic en **Sí**. Fíjese en que la máquina virtual responde mucho mejor al proceso de inicio de sesión.

1. Haga clic con el botón derecho en la barra de tareas y haga clic en **Administrador de tareas**.

1. En la ventana **Administrador de tareas**, haga clic en **Más detalles**.

1. Haga clic en la pestaña **Rendimiento**. Observe que la memoria total disponible es de 8 GB, de los cuales aproximadamente 1,2 GB estarán en uso. Cierre el **Administrador de tareas**.

## <a name="summary"></a>Resumen

Se ha conectado a una máquina virtual de Windows mediante RDP. Con el acceso a la interfaz de usuario de escritorio, puede administrar esta máquina virtual como lo haría con cualquier equipo Windows.
