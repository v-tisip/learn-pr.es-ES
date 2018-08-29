Los productos de Azure tienen una profunda jerarquía. Por ejemplo, supongamos que necesita crear una máquina virtual Linux. Podría navegar por estos niveles: **Inicio** **>** **Máquinas virtuales** **>** **Proceso** **>** **Ubuntu Server**. Azure Portal optimiza su interfaz de usuario para que este tipo de secuencia de navegación se realice de manera intuitiva. Aquí, inspeccionará los elementos principales de la interfaz de usuario que hacen esto posible. Navegará por los menús y submenús y usará hojas para buscar y configurar servicios.

## <a name="azure-portal-layout"></a>Diseño de Azure Portal

Azure Portal es la interfaz gráfica de usuario (GUI) principal para controlar Microsoft Azure. La gran mayoría de las acciones de administración se pueden llevar a cabo en el portal y el portal es normalmente la mejor interfaz para realizar tareas individuales o donde puede examinar las opciones de configuración de forma detallada.

En el panel izquierdo del portal está el panel de recursos, que enumera los tipos de recursos principales. Tenga en cuenta que Azure tiene ahora muchos más tipos de recursos que los que se muestran.

## <a name="using-blades-in-azure-portal"></a>Uso de hojas en Azure Portal

Azure Portal usa un modelo de navegación basado en hojas. Una _hoja_ es un panel deslizante que contiene la interfaz de usuario de un único nivel en una secuencia de navegación. Por ejemplo, cada uno de estos elementos de la secuencia se representaría mediante una hoja: **Máquinas virtuales** **>** **Proceso** **>** **Ubuntu Server**.

Cada hoja dentro de la interfaz de usuario normalmente contiene una serie de opciones configurables. Algunas de estas opciones generan otra hoja, que se muestra a la derecha de la hoja existente. En la hoja nueva, las opciones que se pueden seguir configurando generan otra hoja y así sucesivamente. Muy pronto, puede acabar con varias hojas abiertas al mismo tiempo. También puede maximizar las hojas para que rellenen toda la pantalla.

Si intenta cerrar una hoja sin guardar los cambios de configuración que ha realizado, recibirá un aviso.

## <a name="configuring-settings-in-azure-portal"></a>Configuración de opciones en Azure Portal

Azure Portal muestra varias opciones de configuración, principalmente en la barra de estado de la parte superior derecha de la pantalla.

### <a name="notifications"></a>Notificaciones

Al hacer clic en el icono de campana se muestra el panel Notificaciones. Este panel muestra las últimas acciones que se han realizado, junto con su estado.

![Hoja Notificaciones](../images/2-notifications-blade.PNG)

### <a name="cloud-shell"></a>Cloud Shell

Si hace clic en el icono de Cloud Shell (> _), se creará una nueva sesión de Cloud Shell. En esa sesión se le pide que use Linux Bash o PowerShell en Linux.

![Cloud Shell](../images/2-choose-shell.PNG)

### <a name="settings"></a>Configuración

Haga clic en el icono de "engranaje" para cambiar la configuración de Azure Portal. Esta configuración incluye:

* Hora de cierre de sesión
* Combinación de colores
* Tema de contraste alto
* Notificaciones del sistema (a un dispositivo móvil)
* Hacer doble clic para cambiar el tema
* Idioma
* Formato regional

![Configuración del portal](../images/2-settings-blade.PNG)

Cuando haya cambiado la configuración, haga clic en **Aplicar** para aceptar los cambios.

### <a name="feedback-blade"></a>Hoja de comentarios

El icono de cara sonriente abre la hoja **Envíenos comentarios**. Aquí puede enviar comentarios a Microsoft acerca de Azure. Observe que puede especificar si Microsoft puede responder a sus comentarios por correo electrónico.

![Comentarios](../images/2-feedback-blade.PNG)

### <a name="help-blade"></a>Hoja Ayuda

Haga clic en el signo de interrogación para mostrar la hoja **Ayuda**. Aquí puede elegir entre varios temas, como:

* Novedades
* Azure Roadmap
* Iniciar paseo guiado
* Métodos abreviados de teclado
* Mostrar diagnósticos
* Privacidad y términos

### <a name="directory-and-subscription"></a>Directorio y suscripción

Haga clic en el icono de libro y filtro para mostrar la hoja **Directorio y suscripción**.

Azure le permite tener más de una suscripción asociada con un directorio. En la hoja Directorio y suscripción, puede cambiar entre suscripciones. Aquí, puede cambiar su suscripción, o cambiar a otro directorio.

![Directorio](../images/2-directory-blade-1.PNG)

### <a name="profile-settings"></a>Configuración del perfil

Si hace clic en su nombre en la esquina superior derecha, puede cambiar la configuración del perfil.
Las opciones incluyen:

* Cerrar la sesión en Azure
* Cambiar contraseña
* Cambiar la información de contacto
* Ver permisos
* Enviar una idea al equipo de Azure
* Ver la factura
* Cambiar directorio (se muestra la hoja Directorio y suscripción como en la sección anterior)

![Configuración del perfil](../images/2-portal-menu.png)

Si ahora hace clic en **Ver mi factura**, Azure le lleva a la página **Administración de costos + facturación - Facturas**, que le ayuda a analizar dónde se generan los costos de Azure.

![Página de facturación](../images/2-portal-billing.PNG)

## <a name="summary"></a>Resumen

Azure es un producto grande y la interfaz de usuario del portal así lo refleja. Para ayudar a navegar por esta complejidad, el portal usa hojas para indicar jerarquía. Las hojas le permiten centrarse en una tarea específica, al tiempo que indican claramente el camino que tomó para llegar a ese punto.