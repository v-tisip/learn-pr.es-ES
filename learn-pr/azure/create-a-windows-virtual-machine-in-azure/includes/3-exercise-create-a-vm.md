En este ejercicio, creará una máquina virtual Windows en Azure.

## <a name="motivation"></a>Motivación

Consideremos un escenario alternativo para este ejercicio. En este caso, su organización es una escuela que usa máquinas virtuales Windows para poner en marcha los entornos de prueba en los que los estudiantes instalan aplicaciones web, configuran dominios y exploran características y servicios de Windows sin que afecte a los equipos de la escuela. Los profesores se conectan a estas máquinas virtuales mediante RDP y comprueban el progreso de los estudiantes.

## <a name="create-a-windows-vm"></a>Creación de una máquina virtual Windows

Para crear una máquina virtual Windows, complete los siguientes pasos:

1. Inicie sesión en Azure a través de [Azure Portal](https://portal.azure.com).

1. Haga clic en **Crear un recurso** en la esquina superior izquierda de Azure Portal.

1. En la **barra de búsqueda**, escriba **Windows Server 2016 Datacenter** y después haga clic en el vínculo con el mismo título.

### <a name="configure-the-vm-settings"></a>Configuración de las opciones de la máquina virtual

1. En **Aspectos básicos**, en el campo **Nombre**, escriba un nombre para la máquina virtual, por ejemplo, "StudentVM".

1. En el campo **Tipo de disco de máquina virtual**, haga clic en el menú desplegable para ver las opciones. Asegúrese de que está seleccionada la opción **SSD**.

1. En el campo **Nombre de usuario**, escriba un nombre de usuario adecuado para usarlo al iniciar sesión en la máquina virtual.

1. En el campo **Contraseña**, escriba una contraseña que tenga al menos 12 caracteres de longitud. También debe tener caracteres en mayúsculas y minúsculas, números y caracteres especiales.

1. En **Grupo de recursos**, haga clic en **Crear nuevo**. Asigne al grupo de recursos un nombre, por ejemplo, "myTestRG".

1. Seleccione una ubicación adecuada para que se cree la máquina virtual y luego haga clic en **Aceptar**.

### <a name="select-the-vm-image-size-and-options"></a>Selección de las opciones y el tamaño de la imagen de máquina virtual

1. En la página **Elegir un tamaño**, haga clic en la imagen **B1s** y, después, en **Seleccionar**.

   > [!Note] 
   > La imagen B1 tiene solo 1 GB de RAM y dará lugar a errores de memoria la primera vez que inicie sesión. En cambio, puede cambiar el tamaño de la imagen más adelante como parte de un laboratorio posterior.

1. En la página **Configuración**, en **Seleccionar puertos de entrada públicos**, haga clic en **No hay puertos de entrada públicos**. Configuraremos el acceso RDP más tarde.

### <a name="finish-configuring-the-vm-and-create-the-image"></a>Finalización de la configuración de la máquina virtual y creación de la imagen

1. Desplácese hacia abajo y haga clic en **Aceptar**.

1. En **Crear**, compruebe las opciones que ha configurado. En la parte inferior, haga clic en **Crear**. El panel de Azure mostrará la máquina virtual que se va a implementar. Este proceso podría tardar varios minutos.

## <a name="summary"></a>Resumen

Acaba de crear una máquina virtual de Windows Server que es adecuada para los requisitos de los estudiantes y a la que se puede acceder desde la red de la escuela. En la siguiente unidad, examinará cómo conectarse a esa máquina virtual mediante RDP y cómo administrarla.
