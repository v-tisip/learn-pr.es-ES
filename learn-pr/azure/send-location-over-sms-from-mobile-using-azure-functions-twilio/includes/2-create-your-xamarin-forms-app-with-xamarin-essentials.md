La aplicación que está creando es una aplicación móvil multiplataforma que se comunica con una función de Azure para compartir su ubicación. En esta unidad, crea la aplicación móvil en blanco con Visual Studio e instala un paquete NuGet que tiene una API para obtener la ubicación del usuario.

## <a name="create-the-xamarinforms-project"></a>Crear el proyecto Xamarin.Forms

1. En Visual Studio, seleccione *Archivo->Nuevo->Proyecto...*.

2. En el árbol de la izquierda, seleccione *Visual C#->Multiplataforma* y, a continuación, seleccione *Aplicación móvil (Xamarin.Forms)* en el panel del centro.

3. Llame "ImHere" a la solución.

4. Elija una ubicación adecuada para la solución.

    > Si ejecuta este módulo localmente en Windows y tiene pensado desarrollarlo para Android, asegúrese de que la ruta de acceso sea lo más corta posible. Existen limitaciones en cuanto a la longitud de la ruta de acceso con el SDK de Android, por lo que su ruta de acceso raíz debe ser lo más corta posible.

5. Haga clic en **OK**.

    ![Cuadro de diálogo Nueva solución](../media-drafts/2-new-solution-dialog.png)

6. En el cuadro de diálogo **Nueva aplicación multiplataforma**, seleccione la plantilla *Aplicación en blanco*.

7. Para este módulo creará una aplicación de UWP, de modo que desactive iOS y Android, y deje UWP activado.

    > Si ejecuta esto localmente, puede dejar Android activado, ya que el SDK de Android está instalado como parte de la carga de trabajo *Desarrollo móvil con .NET* dentro de Visual Studio. Si también desea desarrollarlo para iOS, tendrá que emparejarse con un agente de compilación macOS. Puede leer más información al respecto en los [documentos de Xamarin iOS](https://docs.microsoft.com/xamarin/ios/get-started/installation/windows/connecting-to-mac/).

8. En *Estrategia de uso compartido de código*, seleccione **.NET Standard**.

9. Haga clic en **OK**.

    ![Cuadro de diálogo Configure New Solution (Configurar nueva solución)](../media-drafts/2-configure-solution-dialog.png)

Visual Studio creará dos proyectos para usted: una aplicación de UWP llamada `ImHere.UWP` y una biblioteca .NET Standard, `ImHere`. Las aplicaciones Xamarin.Forms constan de dos partes: uno o varios proyectos de aplicación específicos de la plataforma y una biblioteca .NET Standard (o varias). Los proyectos de aplicación específicos de la plataforma contienen el código específico de la plataforma necesario para ejecutar una aplicación en la plataforma correspondiente. A continuación, estos proyectos inician una aplicación Xamarin.Forms que se define en una biblioteca .NET Standard multiplataforma. Usted crea su aplicación en código multiplataforma y, en tiempo de ejecución, cualquier interfaz de usuario que cree se traducirá en los componentes de interfaz de usuario específicos de la plataforma correspondiente.

## <a name="adding-xamarinessentials"></a>Agregar Xamarin.Essentials

Las plataformas UWP, Android e iOS proporcionan numerosas funcionalidades similares que aprovechan el sistema operativo y el hardware. Pese a estas similitudes, las API son muy diferentes. El uso de estas API a partir de código multiplataforma requiere la escritura de código específico de la plataforma en sus proyectos de aplicación expuestos en sus bibliotecas .NET Standard. [Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/) es un paquete NuGet que proporciona una abstracción multiplataforma a través de algunas de estas API, incluidas las API de geolocalización que usará en su aplicación para obtener la ubicación del usuario.

1. Haga clic con el botón derecho en la solución `ImHere` en el Explorador de soluciones de Visual Studio y seleccione *Administrar paquetes NuGet para la solución...*.

2. Seleccione la pestaña **Explorar** y busque "Xamarin.Essentials". Este paquete está disponible actualmente como paquete NuGet de versión preliminar, de modo que active la casilla *Incluir versión preliminar*.

3. Seleccione el paquete NuGet **Xamarin.Essentials**.

4. Compruebe todos sus proyectos en la lista de proyectos de la derecha.

5. Haga clic en el botón **Instalar** para instalar el paquete NuGet. Deberá aceptar la licencia para continuar.

    ![Adición del paquete NuGet Xamarin.Essentials a todos los proyectos de la solución](../media-drafts/2-add-essentials-nuget.png)

    > Si ejecuta este módulo localmente y desea que Android sea el destinatario, tendrá que realizar una configuración adicional. Para obtener más información consulte los [documentos de introducción a Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/get-started?context=xamarin%2Fios&tabs=windows%2Candroid).

## <a name="building-and-running-the-app"></a>Compilación y ejecución de la aplicación

1. Haga clic con el botón derecho en el proyecto `ImHere.UWP` en el Explorador de soluciones y seleccione *Establecer como proyecto de inicio*.

2. Establezca la configuración de compilación en **Depurar**, la plataforma en **x86** y el dispositivo donde se va a ejecutar en **Máquina local**.

    ![Establecimiento de la configuración Debug x86 que se va a ejecutar en el dispositivo local](../media-drafts/2-debug-configuration.png)

3. Inicie la depuración de la aplicación.

    ![Aplicación en ejecución](../media-drafts/2-debuging-app.png)

## <a name="summary"></a>Resumen

En esta unidad, creó una nueva aplicación móvil multiplataforma Xamarin.Forms y agregó el paquete NuGet Xamarin.Essentials. A continuación, usted aprende a desarrollar la lógica y la interfaz de usuario de la aplicación móvil.