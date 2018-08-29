Como administrador de red en una empresa de análisis de datos, es responsabilidad suya conectarse a máquinas virtuales en Azure y comprobar que están configuradas correctamente. Puede usarlo con un cliente del Protocolo de escritorio remoto para conectarse a la interfaz de usuario de escritorio de Windows de la máquina virtual.

## <a name="what-is-the-remote-desktop-protocol"></a>¿Qué es el Protocolo de escritorio remoto?

El Protocolo de escritorio remoto (RDP) proporciona conectividad remota a la interfaz de usuario de equipos con Windows. RDP permite iniciar sesión en un equipo remoto Windows físico o virtual y controlar dicho equipo como si estuviese sentado en la consola.

> [!Note]
> Windows Hyper-V en Windows Server 2016 y Windows 10 utiliza RDP para conectarse a máquinas virtuales que se ejecutan en el hipervisor.

Una conexión RDP permite llevar a cabo la gran mayoría de las operaciones que puede realizar desde la consola de un equipo físico, con la excepción de algunas funciones relacionadas con la potencia y el hardware.

Una conexión RDP requiere un cliente de RDP. Microsoft proporciona clientes de RDP para los siguientes sistemas operativos:

* Windows
* iOS
* MacOS
* Android

También hay clientes de Linux de código abierto, como Remmina, que le permiten conectarse a un equipo Windows desde una distribución de Ubuntu.

Windows 10 incluye un cliente de RDP.

![Cliente de RDP de Windows](../images/2-rdp-client.PNG)

## <a name="what-functionality-does-an-rdp-connection-support"></a>¿Qué funcionalidad admite una conexión RDP?

Con una conexión RDP, puede interactuar con la interfaz de usuario. Sin embargo, también puede conectarse a otros servicios en el equipo remoto. Estos servicios incluyen:

* Conexiones de impresora que permiten al equipo remoto imprimir en el dispositivo de impresión local.
* Reproducción de audio, donde se puede reproducir audio en el equipo local o en el dispositivo remoto.
* Grabación de audio, donde puede grabar audio desde el equipo local y dirigir ese sonido al dispositivo remoto.
* Puertos, que puede redirigir a los puertos en el equipo local.
* Unidades, incluidas las unidades de red asignadas, donde las unidades aparecerán como conectadas al equipo remoto.
* Dispositivos de captura de vídeo, como las cámaras web integradas.
* Otros dispositivos Plug and Play compatibles.

No todas estas características son compatibles en Azure, ya que existen restricciones en los recursos físicos que están disponibles en dicha plataforma. Por ejemplo, solo las impresoras de software pueden redirigirse a través de una conexión RDP desde una máquina virtual hospedada en Azure hasta los dispositivos de impresión del cliente de conexión.

## <a name="configure-network-settings-for-rdp-access-to-virtual-machines"></a>Configuración de red para el acceso de RDP a las máquinas virtuales

Las conexiones a las máquinas virtuales de Azure pueden realizarse de tres formas:

1. Directamente a la dirección IP pública de la máquina virtual.
2. A través de una conexión de red privada virtual (VPN).
3. A través de una conexión de ExpressRoute.

Una dirección IP pública puede ser dinámica o asignarse de forma permanentemente. También necesitará asegurarse de que tiene acceso a la dirección pública de la máquina virtual en el puerto 3389 (RDP). Esta disposición puede requerir la negociación con el equipo que administra la seguridad del firewall de su organización, con la configuración de una regla para la dirección IP pública de la máquina virtual en el puerto 3389.

Las direcciones IP públicas dinámicas se reasignan cada vez que se reinicia la máquina virtual. Las direcciones estáticas son persistentes, pero cuestan más.

Para conectarse a través de una VPN, la red local debe tener una conexión VPN activa a Microsoft Azure.

El enfoque del vínculo de ExpressRoute administra la conectividad a la máquina virtual. Este enfoque también ofrece la conexión con la latencia más baja y el ancho de banda más alto.

> [!Note]
> Con independencia de la opción que use para conectarse a Azure, necesita asegurarse de que se pueda acceder a la máquina virtual a través de RDP, normalmente en el puerto predeterminado 3389. Puede configurar la máquina virtual para que se pueda acceder a ella solo desde su propia dirección IP de cliente. La conexión a una máquina virtual a través del puerto 3389 en una dirección IP pública solo se recomienda para entornos de prueba. En entornos de producción, use la opción 2 o 3.

## <a name="how-do-you-connect-to-a-vm-in-azure-using-rdp"></a>¿Cómo me conecto a una máquina virtual en Azure con RDP?

Conectarse a una máquina virtual en Azure mediante RDP es un proceso sencillo. En Azure Portal, vaya a las propiedades de la máquina virtual y, en la parte superior, haga clic en **Conectar**. Esta acción descarga un archivo .RDP preconfigurado que Windows luego abre en el cliente de RDP. Puede elegir conectarse a través de la dirección IP pública de la máquina virtual en el archivo RDP. Como alternativa, si se conecta a través de VPN o ExpressRoute, puede seleccionar la dirección IP interna. También puede seleccionar el número de puerto para la conexión.

Si usa una dirección IP pública estática para la máquina virtual, puede guardar el archivo .RDP en su escritorio. Si usa una dirección IP dinámica, el archivo .RDP solo es válido mientras la máquina virtual esté en ejecución. Si detiene y reinicia la máquina virtual, debe descargar otro archivo .RDP.

> [!Note]
> También puede especificar la dirección IP pública de la máquina virtual en el cliente de RDP de Windows y hacer clic en **Conectar**.

Cuando se conecte, normalmente recibirá dos advertencias. Dichos componentes son:

* Advertencia del editor: porque el archivo .RDP no está firmado públicamente.
* Advertencia de certificado: porque el certificado de máquina no es de confianza.

En los entornos de prueba, estas advertencias pueden ignorarse. En entornos de producción, el archivo .RDP podría firmarse con RDPSIGN.EXE y el certificado de máquina puede ubicarse en el almacén de **entidades de certificación raíz de confianza** del cliente.

## <a name="summary"></a>Resumen

Ahora puede conectarse a una máquina virtual Windows con RDP. En el ejercicio siguiente, se utiliza RDP para conectarse a una máquina virtual y luego instalar un rol de servidor en ese equipo.
