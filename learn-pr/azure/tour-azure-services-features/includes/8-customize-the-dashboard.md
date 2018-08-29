Aquí, creará y modificará los paneles mediante la interfaz de usuario del portal y editará el archivo JSON subyacente directamente.

## <a name="what-is-a-dashboard"></a>¿Qué es un panel?

Un _panel_ es una colección personalizable de iconos de interfaz de usuario mostrados en Azure Portal. Los iconos se agregan, quitan y colocan para crear la vista exacta deseada, y luego esa vista se guarda como un panel. Se admiten varios paneles y puede cambiar entre ellos según sea necesario. Incluso puede compartir sus paneles con otros miembros del equipo.

Los paneles proporcionan una flexibilidad considerable en términos de cómo se administra Azure. Por ejemplo, puede crear paneles para roles específicos dentro de la organización y luego usar Control de acceso basado en rol (RBAC) para controlar quién puede acceder a ese panel. Por lo tanto, el administrador de base de datos tendría un panel que contiene las vistas del servicio de base de datos SQL, mientras que el administrador de Azure Active Directory tendría las vistas de los usuarios y grupos dentro de Azure AD.

Los paneles se almacenan como archivos de notación de objetos de JavaScript (.JSON). Esto significa que se pueden cargar y descargar en otros equipos o compartir con los miembros del directorio de Azure. Azure almacena los paneles dentro de grupos de recursos, al igual que las máquinas virtuales o las cuentas de almacenamiento que puede administrar en el portal.

Como los paneles son archivos JSON, también puede personalizarlos mediante programación y así convertirlos en herramientas administrativas muy eficaces. Además, algunos tipos de iconos pueden basarse en la consulta por lo que se actualizan automáticamente cuando los datos de origen cambian.

## <a name="default-dashboard"></a>Panel predeterminado

El panel predeterminado se denomina simplemente Panel. Cuando inicia sesión en el portal, se le presenta este panel que contiene cinco elementos web.

![Elementos web predeterminados](../images/4-dashboard-default-webparts.png)

Estos elementos web predeterminados son:

1. Todos los recursos
2. Inicios rápidos y tutoriales
3. Service Health
4. Marketplace
5. Introducción a Azure

## <a name="creating-and-managing-dashboards"></a>Creación y administración de paneles

En la parte superior del panel están los controles que permiten crear, cargar, descargar, editar y compartir un panel. También puede cambiar de un panel a pantalla completa, clonarlo o eliminarlo.

![Personalización de los controles del Panel](../images/7-customise-dashboard-controls.PNG)

### <a name="select-dashboard"></a>Seleccionar panel

A la izquierda se encuentra el control de lista desplegable Seleccionar panel. Al hacer clic en este control, puede seleccionar entre los paneles que ya ha definido para la cuenta. Este control permite definir de forma simple varios paneles con diferentes propósitos, luego simplemente se cambia de uno a otro, según lo que intente hacer en ese momento.

Tenga en cuenta que los paneles que cree serán inicialmente privados; es decir, solo usted puede verlos. Para que un panel esté disponible en toda la empresa, deberá compartirlo. Para más información, consulte más adelante la sección sobre cómo compartir y dejar de compartir paneles.

### <a name="create-a-new-dashboard"></a>Creación de un nuevo panel

Para crear un panel, basta con hacer clic **Nuevo panel**. Aparece el área de trabajo del panel, sin iconos. Ahora puede agregar iconos, tal y como se detalla más adelante en la sección Edición de un panel mediante la interfaz de usuario. Cuando haya terminado de agregar y ajustar los iconos y haya cambiado el nombre del panel, haga clic simplemente en **Personalización finalizada** para guardar y cambiar a ese panel.

### <a name="upload-and-download"></a>Cargar y Descargar

Los botones **Cargar** y **Descargar** permiten descargar el panel actual como un archivo JSON, personalizarlo y luego distribuirlo y cargarlo; o bien, que otra persona cargue de nuevo ese archivo en Azure Portal, de forma que se reemplaza su panel actual.

Si hace clic en **Descargar**, el panel actual se descarga en la carpeta predeterminada de descargas. Al abrir el archivo descargado se muestra el código JSON.

![Código JSON del panel](../images/7-dashboard-json-code.PNG)

A continuación, puede editar ese código manualmente, por ejemplo, cambiar los tamaños de los iconos, y volver a cargarlo en Azure con el botón **Cargar**.

### <a name="edit-a-dashboard"></a>Edición de paneles

Para más información al respecto, consulte el tema Edición de un panel mediante la interfaz de usuario.

### <a name="shareunshare-a-dashboard"></a>Compartir y dejar de compartir un panel

Al definir un nuevo panel, es privado y solo es visible para su cuenta. Para que sea visible para otros usuarios, debe compartirlo. Sin embargo, como cualquier otro recurso de Azure, debe especificar un grupo de recursos (o usar un grupo de recursos existente) en el que almacenar los paneles compartidos. Si no tiene un grupo de recursos, Azure creará un grupo de recursos "paneles" en cualquier ubicación que especifique. Si ya tiene un grupo de recursos, puede especificar ese grupo de recursos para almacenar los paneles.

![Uso compartido y control de acceso 1](../images/7-share-dashboards-default.PNG)

Cuando se ha compartido la plantilla, verá una segunda hoja **Uso compartido y control de acceso**.

![Uso compartido y control de acceso 2](../images/7-share-dashboards-access-control.PNG)

A continuación, puede hacer clic en **Administrar usuarios** para especificar los usuarios que tienen acceso a ese panel.

### <a name="switching-to-a-shared-dashboard"></a>Cambio a un panel compartido

Para cambiar a un panel compartido, haga clic en la lista de paneles y, luego, en **Examinar todos los paneles**.

![Examinar todos los paneles](../images/7-browse-dashboards.PNG)

Ahora verá la hoja Todos los paneles, con los nombres de los paneles compartidos. Simplemente haga clic en un panel para aplicarlo a Azure Portal.

![Paneles compartidos](../images/7-select-shared-dashboard.png)

### <a name="display-a-dashboard-as-a-full-screen"></a>Visualización de un panel en pantalla completa

Si realmente quiere el estado real más grande del panel, haga clic en el botón **Pantalla completa** para mostrar el panel actual sin los menús del explorador. Si tiene iconos que están fuera de los límites de la pantalla, aparecerán barras de control deslizantes en la parte derecha e inferior de la pantalla.

Cuando haya terminado de trabajar en modo de pantalla completa, presione la tecla ESC o haga clic en **Salir de pantalla completa** junto al nombre del panel en la parte superior de la pantalla.

### <a name="clone-a-dashboard"></a>Clonación de un panel

Al clonar un panel simplemente se crea una copia instantánea denominada "Clon de (nombre del panel)" y se cambia a dicha copia como el panel actual. La clonación también es una manera fácil de crear paneles antes de compartirlos. Por ejemplo, si tiene un panel que es casi como lo quiere, clónelo, luego realice los cambios que sean necesarios y compártalo.

### <a name="delete-a-dashboard"></a>Eliminación de un panel

Al eliminar un panel se quita de la lista de paneles disponibles. Se le pedirá que confirme que quiere eliminar el panel, pero no hay ninguna funcionalidad para recuperar un panel que se ha eliminado.

## <a name="edit-a-dashboard-through-the-user-interface"></a>Edición de un panel mediante la interfaz de usuario

Aunque para editar un panel puede descargar el archivo JSON, cambiar los valores del archivo y cargar de nuevo el archivo en Azure, ese enfoque no es nada intuitivo para diseñar una interfaz de usuario. Para usar la interfaz gráfica de usuario para configurar el panel actual, haga clic en el botón **Editar** o haga clic con el botón derecho en el panel y haga clic en **Editar**. El panel cambia al modo de edición.

![Edición del panel](../images/7-edit-dashboard.PNG)

En el lado izquierdo aparece la Galería de iconos con varios iconos. Puede filtrar la Galería de iconos por los siguientes criterios:

* General
* Escriba
* Search
* Grupo de recursos
* Etiqueta

![Galería de iconos](../images/7-tile-gallery.png)

También puede acotar más cada una de estas opciones por categoría, por ejemplo, Azure Active Directory, Internet de las cosas, Microsoft Intune, etc.

Agregar iconos es simplemente una cuestión de seleccionar el icono de la lista de la izquierda y, a continuación, arrastrarlo y colocarlo en el área de trabajo. Luego puede mover cada icono, cambiar su tamaño o cambiar los datos que muestra.

El área de trabajo en modo de edición está dividida en cuadrados. Cada icono debe ocupar al menos un cuadrado, y los iconos se ajustan al conjunto más grande y cercano de divisores de iconos. Los iconos que se solapan se quitan del medio. Al crear un icono más pequeño, los iconos que lo rodean retroceden con respecto a él.

### <a name="change-tile-sizes"></a>Cambio de tamaño de los iconos

Algunos iconos tienen un tamaño establecido y solo puede modificarlo mediante programación. Sin embargo, los iconos con una esquina inferior derecha de color gris se pueden editar arrastrando y colocando el indicador de la esquina.

![Icono ajustable](../images/7-resizable-tile.png)

Como alternativa, haga clic con el botón derecho en el menú contextual y especifique el tamaño que desee.

![Tamaño del icono](../images/7-tile-size.png)

Para crear el panel, solo tiene que extraer iconos de la Galería de iconos al área de trabajo y luego organizarlos.

### <a name="change-tile-settings"></a>Cambio de la configuración de los iconos

Algunos iconos tienen valores editables. Por ejemplo, con el icono de reloj, cuando se arrastra al área de trabajo, se abre el icono **Editar reloj**. Luego puede establecer la zona horaria que muestra y también el formato: 12 o 24 horas.

![Editar reloj](../images/7-edit-clock.png)

Para empresas multinacionales o transcontinentales, puede agregar más relojes de diferentes zonas horarias.

### <a name="accepting-your-edits"></a>Aceptación de las modificaciones

Cuando haya organizado los iconos como prefiera, haga clic en **Personalización finalizada**, o haga clic con el botón derecho y haga clic en **Personalización finalizada**.

## <a name="edit-a-dashboard-by-changing-the-json-file"></a>Edición de un panel mediante la modificación del archivo .JSON

También puede editar un panel mediante la modificación del archivo .JSON. Este enfoque proporciona más opciones para cambiar la configuración, pero no puede ver los cambios hasta que se carga de nuevo el archivo en Azure.

![Configuración de JSON](../images/7-json-code.png)

En el ejemplo anterior, para cambiar el tamaño del icono, editó las variables colSpan y rowSpan y luego guardó el archivo y lo volvió a cargar en Azure. También puede distribuir el archivo a otros usuarios.

## <a name="reset-a-dashboard"></a>Restablecimiento de un panel

Puede restablecer cualquier panel al estilo predeterminado. En modo de edición, haga clic con el botón derecho y seleccione **Restaurar al estado predeterminado**. Un cuadro de diálogo le pedirá que confirme que desea restablecer ese panel.

## <a name="summary"></a>Resumen

Los paneles ofrecen una herramienta flexible para administrar distintos aspectos de los servicios de Azure en el portal. Permiten supervisar cómodamente el estado de los servicios. Como se pueden compartir, ayudan a garantizar que todos los miembros de un equipo ven los mismos datos y están al corriente del estado de los componentes críticos.