En este momento, la aplicación móvil es una aplicación "Hola mundo" sencilla. En esta unidad, se agregará la interfaz de usuario y lógica de aplicación básica.

La interfaz de usuario para la aplicación constará de lo siguiente:

* Un control de entrada de texto para escribir algunos números de teléfono.
* Un botón para enviar la ubicación a esos números mediante una función de Azure.
* Una etiqueta en la que se mostrará un mensaje del estado actual al usuario, como la ubicación que se envía y si se ha enviado correctamente.

Xamarin.Forms es compatible con un patrón de diseño llamado Vista de modelo (MVVM). Puede leer más sobre MVVM en la [documentación de MVVM de Xamarin](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm) pero, en esencia, cada página (View) tiene un ViewModel que expone las propiedades y el comportamiento.

Las propiedades de ViewModel se "enlazan" a los componentes de la interfaz de usuario por nombre y este enlace sincroniza los datos entre View y ViewModel. Por ejemplo, una propiedad `string` de un ViewModel denominado `Name` se podría enlazar a la propiedad `Text` de un control de entrada de texto en la interfaz de usuario. El control de entrada de texto muestra el valor en la propiedad `Name` y, cuando el usuario cambia el texto de la interfaz de usuario, se actualiza la propiedad `Name`. Si se modifica el valor de la propiedad `Name` en el modelo de vista, se genera un evento para notificar la actualización a la interfaz de usuario.

El comportamiento de ViewModel se expone como propiedades de comando, donde un comando es un objeto que contiene una acción que se ejecuta cuando se invoca el comando. Estos comandos se enlazan por nombre a controles como los botones y pulsar un botón hace que se invoque el comando.

## <a name="create-a-base-viewmodel"></a>Creación de una clase ViewModel base

Todas las instancias de ViewModel implementan la interfaz `INotifyPropertyChanged`. Esta interfaz tiene un solo evento, `PropertyChanged`, que se usa para notificar las actualizaciones a la interfaz de usuario. Este evento tiene argumentos de evento que contienen el nombre de la propiedad que ha cambiado. Es una práctica común crear una clase ViewModel base que implemente esta interfaz y proporcionar algunos métodos auxiliares.

1. Cree una clase en el proyecto estándar de .NET `ImHere` con el nombre `BaseViewModel`; para ello, haga clic con el botón derecho en el proyecto y, después, seleccione *Agregar->Clase...*. Asigne el nombre "BaseViewModel" a la nueva clase y haga clic en **Agregar**.

2. Haga que la clase sea `public` y que se derive de `INotifyPropertyChanged`. Tendrá que agregar una directiva using para `System.ComponentModel`.

3. Agregue el evento `PropertyChanged` para implementar la interfaz `INotifyPropertyChanged`:

    ```cs
    public event PropertyChangedEventHandler PropertyChanged;
    ```

4. El patrón común para las propiedades de ViewModel es tener una propiedad pública con un campo de respaldo privado. En el establecedor de la propiedad, el campo de respaldo se compara con el valor nuevo. Si el valor nuevo es diferente al campo de respaldo, el campo de respaldo se actualiza y se genera el evento `PropertyChanged`. Esta lógica es fácil de factorizar en un método, por lo que agregue el método `Set`. Tendrá que agregar una directiva using para el espacio de nombres `System.Runtime.CompilerServices`.

    ```cs
    protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
    {
        if (Equals(field, value)) return;
        field = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
    ```

    Este método toma una referencia al campo de respaldo, el valor nuevo y el nombre de la propiedad. Si el campo no ha cambiado, el método devuelve; de lo contrario, se actualiza y se genera el evento `PropertyChanged`. El parámetro `propertyName` del método `Set` es un parámetro predeterminado y se marca con el atributo `CallerMemberName`. Cuando se llama a este método desde un establecedor de propiedad, este parámetro normalmente se mantiene como el valor predeterminado. Después, el compilador establecerá automáticamente el valor del parámetro en el nombre de la propiedad que realiza la llamada.

A continuación se muestra el código completo de esta clase.

```cs
using System.ComponentModel;
using System.Runtime.CompilerServices;

namespace ImHere
{
    public class BaseViewModel : INotifyPropertyChanged
    {
        public event PropertyChangedEventHandler PropertyChanged;

        protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
        {
            if (Equals(field, value)) return;
            field = value;
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```

## <a name="create-a-viewmodel-for-the-page"></a>Creación de una clase ViewModel para la página

`MainPage` tendrá un control de entrada de texto para números de teléfono y una etiqueta para mostrar un mensaje. Estos controles se enlazarán a las propiedades de una clase ViewModel.

1. Cree una clase denominada `MainViewModel` en el proyecto estándar de .NET `ImHere`.

2. Convierta en pública esta clase y derívela de `BaseViewModel`.

3. Agregue dos propiedades `string` (`PhoneNumbers` y `Message`) cada una con un campo de respaldo. En el establecedor de propiedad, use el método `Set` de la clase base para actualizar el valor y generar el evento `PropertyChanged`.

   ```cs
    string message = "";
    public string Message
    {
        get => message;
        set => Set(ref message, value);
    }

    string phoneNumbers = "";
    public string PhoneNumbers
    {
        get => phoneNumbers;
        set => Set(ref phoneNumbers, value);
    }
   ```

4. Agregue una propiedad de comando de solo lectura denominada `SendLocationCommand`. Este comando tendrá un tipo de `ICommand` del espacio de nombres `System.Windows.Input`.

    ```cs
    public ICommand SendLocationCommand { get; }
    ```

5. Agregue un constructor a la clase y, dentro de él, inicialice `SendLocationCommand` como una instancia nueva de `Command` desde el espacio de nombres `Xamarin.Forms`. El constructor para este comando toma un elemento `Action` que se ejecutará al invocar el comando, por lo que debe crear un método `async` llamado `SendLocation` y pasar una función lambda que aplique `await` a esta llamada al constructor. El cuerpo del método `SendLocation` se implementará en unidades posteriores de este módulo. Tendrá que agregar una directiva using para que el espacio de nombres `System.Threading.Tasks` pueda devolver `Task`.

    ```cs
    public MainViewModel()
    {
        SendLocationCommand = new Command(async () => await SendLocation());
    }

    async Task SendLocation()
    {
    }
    ```

A continuación se muestra el código de esta clase.

```cs
using System.Threading.Tasks;
using System.Windows.Input;
using Xamarin.Forms;

namespace ImHere
{
    public class MainViewModel : BaseViewModel
    {
        string message = "";
        public string Message
        {
            get => message;
            set => Set(ref message, value);
        }

        string phoneNumbers = "";
        public string PhoneNumbers
        {
            get => phoneNumbers;
            set => Set(ref phoneNumbers, value);
        }

        public MainViewModel()
        {
            SendLocationCommand = new Command(async () => await SendLocation());
        }

        public ICommand SendLocationCommand { get; }

        async Task SendLocation()
        {
        }
    }
}
```

## <a name="create-the-user-interface"></a>Creación de la interfaz del usuario

Las interfaces de usuario de Xamarin.Forms se pueden crear con XAML.

1. Abra el archivo `MainPage.xaml` desde el proyecto `ImHere`. La página se abrirá en el editor de XAML.

    NOTA: El proyecto `ImHere.UWP` también contiene un archivo denominado `MainPage.xaml`. Asegúrese de que va a modificar el de la biblioteca estándar de .NET.

2. Antes de poder enlazar controles a las propiedades de una clase ViewModel, tendrá que configurar una instancia de ViewModel como el contexto de enlace de la página. Agregue el código XAML siguiente al elemento `ContentPage` de nivel superior.

    ```xml
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    ```

3. Elimine el contenido de `StackLayout` y agregue espaciado en su interior para mejorar el aspecto de la interfaz de usuario.

    ```xml
    <StackLayout Padding="20">
    </StackLayout>
    ```

4. Agregue un control `Editor` que el usuario pueda utilizar para agregar números de teléfono al elemento `StackLayout`, con un elemento `Label` por encima que describa para qué sirve el control de entrada. Los controles secundarios de `StackLayout` se apilan de forma horizontal o vertical en el orden en que se agregan los controles, por lo que si primero se agrega `Label`, se colocará sobre `Editor`. Los controles `Editor` son de entrada multilínea y permiten que el usuario escriba varios números de teléfono, uno por línea.

    ```xml
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
    </StackLayout>
    ```

    La propiedad `Text` de `Editor` está enlazada a la propiedad `PhoneNumbers` de `MainViewModel`. La sintaxis para el enlace consiste en establecer el valor de la propiedad en `"{Binding <property name>}"`. Las llaves indican al compilador XAML que este valor es especial y que se debe tratar de manera distinta a un elemento `string` sencillo.

5. Agregue un elemento `Button` para enviar la ubicación del usuario por debajo de `Editor`.

    ```xml
    <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
            Command="{Binding SendLocationCommand}" />
    ```

    La propiedad `Command` se enlaza al comando `SendLocationCommand` de ViewModel. Cuando se pulsa el botón, el comando se ejecuta.

6. Agregue un elemento `Label` para mostrar el mensaje de estado por debajo del elemento `Button`.

    ```xml
    <Label Text="{Binding Message}"
           HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    ```

A continuación se muestra el código completo de esta página.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:ImHere"
             x:Class="ImHere.MainPage">
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
        <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
                Command="{Binding SendLocationCommand}" />
        <Label Text="{Binding Message}"
               HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    </StackLayout>
</ContentPage>
```

Ejecute la aplicación para ver la nueva interfaz de usuario. Si quiere validar ahora los enlaces, puede hacerlo si agrega puntos de interrupción a las propiedades o al método `SendLocation`.

![La interfaz de usuario de la nueva aplicación](../media-drafts/3-new-ui.png)

## <a name="summary"></a>Resumen

En esta unidad, ha aprendido a crear la interfaz de usuario para la aplicación mediante XAML, junto con una clase ViewModel para controlar la lógica de la aplicación. También ha aprendido a enlazar el ViewModel a la interfaz de usuario. En la unidad siguiente, agregará la búsqueda de la ubicación a ViewModel.