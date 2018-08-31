<span data-ttu-id="97d0c-101">En este momento, la aplicación móvil es una aplicación "Hola mundo" sencilla.</span><span class="sxs-lookup"><span data-stu-id="97d0c-101">At this point, the mobile app is a simple "Hello World" app.</span></span> <span data-ttu-id="97d0c-102">En esta unidad, se agregará la interfaz de usuario y lógica de aplicación básica.</span><span class="sxs-lookup"><span data-stu-id="97d0c-102">In this unit, you add the UI and some basic application logic.</span></span>

<span data-ttu-id="97d0c-103">La interfaz de usuario para la aplicación constará de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="97d0c-103">The UI for the app will consist of:</span></span>

* <span data-ttu-id="97d0c-104">Un control de entrada de texto para escribir algunos números de teléfono.</span><span class="sxs-lookup"><span data-stu-id="97d0c-104">A text-entry control to enter some phone numbers.</span></span>
* <span data-ttu-id="97d0c-105">Un botón para enviar la ubicación a esos números mediante una función de Azure.</span><span class="sxs-lookup"><span data-stu-id="97d0c-105">A button to send your location to those numbers using an Azure function.</span></span>
* <span data-ttu-id="97d0c-106">Una etiqueta en la que se mostrará un mensaje del estado actual al usuario, como la ubicación que se envía y si se ha enviado correctamente.</span><span class="sxs-lookup"><span data-stu-id="97d0c-106">A label that will show a message to the user of the current status, such as the location being sent and location sent successfully.</span></span>

<span data-ttu-id="97d0c-107">Xamarin.Forms es compatible con un patrón de diseño llamado Vista de modelo (MVVM).</span><span class="sxs-lookup"><span data-stu-id="97d0c-107">Xamarin.Forms supports a design pattern called Model-View-ViewModel (MVVM).</span></span> <span data-ttu-id="97d0c-108">Puede leer más sobre MVVM en la [documentación de MVVM de Xamarin](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm) pero, en esencia, cada página (View) tiene un ViewModel que expone las propiedades y el comportamiento.</span><span class="sxs-lookup"><span data-stu-id="97d0c-108">You can read more about MVVM in the [Xamarin MVVM docs](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm), but the essence of it is, each page (View) has a ViewModel that exposes properties and behavior.</span></span>

<span data-ttu-id="97d0c-109">Las propiedades de ViewModel se "enlazan" a los componentes de la interfaz de usuario por nombre y este enlace sincroniza los datos entre View y ViewModel.</span><span class="sxs-lookup"><span data-stu-id="97d0c-109">ViewModel properties are 'bound' to components on the UI by name, and this binding synchronizes data between the View and ViewModel.</span></span> <span data-ttu-id="97d0c-110">Por ejemplo, una propiedad `string` de un ViewModel denominado `Name` se podría enlazar a la propiedad `Text` de un control de entrada de texto en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="97d0c-110">For example, a `string` property on a ViewModel called `Name` could be bound to the `Text` property of a text-entry control on the UI.</span></span> <span data-ttu-id="97d0c-111">El control de entrada de texto muestra el valor en la propiedad `Name` y, cuando el usuario cambia el texto de la interfaz de usuario, se actualiza la propiedad `Name`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-111">The text-entry control shows the value in the `Name` property and, when the user changes the text in the UI, the `Name` property is updated.</span></span> <span data-ttu-id="97d0c-112">Si se modifica el valor de la propiedad `Name` en el modelo de vista, se genera un evento para notificar la actualización a la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="97d0c-112">If the value of the `Name` property is changed in the ViewModel, an event is raised to tell the UI to update.</span></span>

<span data-ttu-id="97d0c-113">El comportamiento de ViewModel se expone como propiedades de comando, donde un comando es un objeto que contiene una acción que se ejecuta cuando se invoca el comando.</span><span class="sxs-lookup"><span data-stu-id="97d0c-113">ViewModel behavior is exposed as command properties, a command being an object that wraps an action that is executed when the command is invoked.</span></span> <span data-ttu-id="97d0c-114">Estos comandos se enlazan por nombre a controles como los botones y pulsar un botón hace que se invoque el comando.</span><span class="sxs-lookup"><span data-stu-id="97d0c-114">These commands are bound by name to controls like buttons, and tapping a button will invoke the command.</span></span>

## <a name="create-a-base-viewmodel"></a><span data-ttu-id="97d0c-115">Creación de una clase ViewModel base</span><span class="sxs-lookup"><span data-stu-id="97d0c-115">Create a base ViewModel</span></span>

<span data-ttu-id="97d0c-116">Todas las instancias de ViewModel implementan la interfaz `INotifyPropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-116">ViewModels all implement the `INotifyPropertyChanged` interface.</span></span> <span data-ttu-id="97d0c-117">Esta interfaz tiene un solo evento, `PropertyChanged`, que se usa para notificar las actualizaciones a la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="97d0c-117">This interface has a single event, `PropertyChanged`, which is used to notify the UI of any updates.</span></span> <span data-ttu-id="97d0c-118">Este evento tiene argumentos de evento que contienen el nombre de la propiedad que ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="97d0c-118">This event has event args that contain the name of the property that has changed.</span></span> <span data-ttu-id="97d0c-119">Es una práctica común crear una clase ViewModel base que implemente esta interfaz y proporcionar algunos métodos auxiliares.</span><span class="sxs-lookup"><span data-stu-id="97d0c-119">It's common practice to create a base ViewModel class implementing this interface and providing some helper methods.</span></span>

1. <span data-ttu-id="97d0c-120">Cree una clase en el proyecto estándar de .NET `ImHere` con el nombre `BaseViewModel`; para ello, haga clic con el botón derecho en el proyecto y, después, seleccione *Agregar->Clase...*. Asigne el nombre "BaseViewModel" a la nueva clase y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="97d0c-120">Create a new class in the `ImHere` .NET standard project called `BaseViewModel` by right-clicking on the project, and then selecting *Add->Class...*. Name the new class "BaseViewModel" and click **Add**.</span></span>

2. <span data-ttu-id="97d0c-121">Haga que la clase sea `public` y que se derive de `INotifyPropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-121">Make the class `public` and derive from `INotifyPropertyChanged`.</span></span> <span data-ttu-id="97d0c-122">Tendrá que agregar una directiva using para `System.ComponentModel`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-122">You'll need to add a using directive for `System.ComponentModel`.</span></span>

3. <span data-ttu-id="97d0c-123">Agregue el evento `PropertyChanged` para implementar la interfaz `INotifyPropertyChanged`:</span><span class="sxs-lookup"><span data-stu-id="97d0c-123">Implement the `INotifyPropertyChanged` interface by adding the `PropertyChanged` event:</span></span>

    ```cs
    public event PropertyChangedEventHandler PropertyChanged;
    ```

4. <span data-ttu-id="97d0c-124">El patrón común para las propiedades de ViewModel es tener una propiedad pública con un campo de respaldo privado.</span><span class="sxs-lookup"><span data-stu-id="97d0c-124">The common pattern for ViewModel properties is to have a public property with a private backing field.</span></span> <span data-ttu-id="97d0c-125">En el establecedor de la propiedad, el campo de respaldo se compara con el valor nuevo.</span><span class="sxs-lookup"><span data-stu-id="97d0c-125">In the property setter, the backing field is checked against the new value.</span></span> <span data-ttu-id="97d0c-126">Si el valor nuevo es diferente al campo de respaldo, el campo de respaldo se actualiza y se genera el evento `PropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-126">If the new value is different to the backing field, the backing field is updated and the `PropertyChanged` event is raised.</span></span> <span data-ttu-id="97d0c-127">Esta lógica es fácil de factorizar en un método, por lo que agregue el método `Set`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-127">This logic is easy to factor out into a method, so add the `Set` method.</span></span> <span data-ttu-id="97d0c-128">Tendrá que agregar una directiva using para el espacio de nombres `System.Runtime.CompilerServices`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-128">You'll need to add a using directive for the `System.Runtime.CompilerServices` namespace.</span></span>

    ```cs
    protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
    {
        if (Equals(field, value)) return;
        field = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
    ```

    <span data-ttu-id="97d0c-129">Este método toma una referencia al campo de respaldo, el valor nuevo y el nombre de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="97d0c-129">This method takes a reference to the backing field, the new value, and the property name.</span></span> <span data-ttu-id="97d0c-130">Si el campo no ha cambiado, el método devuelve; de lo contrario, se actualiza y se genera el evento `PropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-130">If the field hasn't changed, the method returns, otherwise, the field is updated and the `PropertyChanged` event is raised.</span></span> <span data-ttu-id="97d0c-131">El parámetro `propertyName` del método `Set` es un parámetro predeterminado y se marca con el atributo `CallerMemberName`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-131">The `propertyName` parameter on the `Set` method is a default parameter and is marked with the `CallerMemberName` attribute.</span></span> <span data-ttu-id="97d0c-132">Cuando se llama a este método desde un establecedor de propiedad, este parámetro normalmente se mantiene como el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="97d0c-132">When this method is called from a property setter, this parameter is normally left as the default value.</span></span> <span data-ttu-id="97d0c-133">Después, el compilador establecerá automáticamente el valor del parámetro en el nombre de la propiedad que realiza la llamada.</span><span class="sxs-lookup"><span data-stu-id="97d0c-133">The compiler will then automatically set the parameter value to be the name of the calling property.</span></span>

<span data-ttu-id="97d0c-134">A continuación se muestra el código completo de esta clase.</span><span class="sxs-lookup"><span data-stu-id="97d0c-134">The full code for this class is below.</span></span>

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

## <a name="create-a-viewmodel-for-the-page"></a><span data-ttu-id="97d0c-135">Creación de una clase ViewModel para la página</span><span class="sxs-lookup"><span data-stu-id="97d0c-135">Create a ViewModel for the page</span></span>

<span data-ttu-id="97d0c-136">`MainPage` tendrá un control de entrada de texto para números de teléfono y una etiqueta para mostrar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="97d0c-136">The `MainPage` will have a text-entry control for phone numbers and a label to display a message.</span></span> <span data-ttu-id="97d0c-137">Estos controles se enlazarán a las propiedades de una clase ViewModel.</span><span class="sxs-lookup"><span data-stu-id="97d0c-137">These controls will be bound to properties on a ViewModel.</span></span>

1. <span data-ttu-id="97d0c-138">Cree una clase denominada `MainViewModel` en el proyecto estándar de .NET `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-138">Create a class called `MainViewModel` in the `ImHere` .NET standard project.</span></span>

2. <span data-ttu-id="97d0c-139">Convierta en pública esta clase y derívela de `BaseViewModel`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-139">Make this class public and derive from `BaseViewModel`.</span></span>

3. <span data-ttu-id="97d0c-140">Agregue dos propiedades `string` (`PhoneNumbers` y `Message`) cada una con un campo de respaldo.</span><span class="sxs-lookup"><span data-stu-id="97d0c-140">Add two `string` properties, `PhoneNumbers` and `Message`, each with a backing field.</span></span> <span data-ttu-id="97d0c-141">En el establecedor de propiedad, use el método `Set` de la clase base para actualizar el valor y generar el evento `PropertyChanged`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-141">In the property setter, use the base class `Set` method to update the value and raise the `PropertyChanged` event.</span></span>

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

4. <span data-ttu-id="97d0c-142">Agregue una propiedad de comando de solo lectura denominada `SendLocationCommand`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-142">Add a read-only command property called `SendLocationCommand`.</span></span> <span data-ttu-id="97d0c-143">Este comando tendrá un tipo de `ICommand` del espacio de nombres `System.Windows.Input`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-143">This command will have a type of `ICommand` from the `System.Windows.Input` namespace.</span></span>

    ```cs
    public ICommand SendLocationCommand { get; }
    ```

5. <span data-ttu-id="97d0c-144">Agregue un constructor a la clase y, dentro de él, inicialice `SendLocationCommand` como una instancia nueva de `Command` desde el espacio de nombres `Xamarin.Forms`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-144">Add a constructor to the class, and in this constructor, initialize the `SendLocationCommand` as a new `Command` from the `Xamarin.Forms` namespace.</span></span> <span data-ttu-id="97d0c-145">El constructor para este comando toma un elemento `Action` que se ejecutará al invocar el comando, por lo que debe crear un método `async` llamado `SendLocation` y pasar una función lambda que aplique `await` a esta llamada al constructor.</span><span class="sxs-lookup"><span data-stu-id="97d0c-145">The constructor for this command takes an `Action` to run when the command is invoked, so create an `async` method called `SendLocation` and pass a lambda function that `await`s this call to the constructor.</span></span> <span data-ttu-id="97d0c-146">El cuerpo del método `SendLocation` se implementará en unidades posteriores de este módulo.</span><span class="sxs-lookup"><span data-stu-id="97d0c-146">The body of the `SendLocation` method will be implemented in later units in this module.</span></span> <span data-ttu-id="97d0c-147">Tendrá que agregar una directiva using para que el espacio de nombres `System.Threading.Tasks` pueda devolver `Task`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-147">You'll need to add a using directive for the `System.Threading.Tasks` namespace to be able to return a `Task`.</span></span>

    ```cs
    public MainViewModel()
    {
        SendLocationCommand = new Command(async () => await SendLocation());
    }

    async Task SendLocation()
    {
    }
    ```

<span data-ttu-id="97d0c-148">A continuación se muestra el código de esta clase.</span><span class="sxs-lookup"><span data-stu-id="97d0c-148">The code for this class is shown below.</span></span>

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

## <a name="create-the-user-interface"></a><span data-ttu-id="97d0c-149">Creación de la interfaz del usuario</span><span class="sxs-lookup"><span data-stu-id="97d0c-149">Create the user interface</span></span>

<span data-ttu-id="97d0c-150">Las interfaces de usuario de Xamarin.Forms se pueden crear con XAML.</span><span class="sxs-lookup"><span data-stu-id="97d0c-150">Xamarin.Forms UIs can be built using XAML.</span></span>

1. <span data-ttu-id="97d0c-151">Abra el archivo `MainPage.xaml` desde el proyecto `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-151">Open the `MainPage.xaml` file from the `ImHere` project.</span></span> <span data-ttu-id="97d0c-152">La página se abrirá en el editor de XAML.</span><span class="sxs-lookup"><span data-stu-id="97d0c-152">The page will open in the XAML editor.</span></span>

    <span data-ttu-id="97d0c-153">NOTA: El proyecto `ImHere.UWP` también contiene un archivo denominado `MainPage.xaml`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-153">NOTE - The `ImHere.UWP` project also contains a file called `MainPage.xaml`.</span></span> <span data-ttu-id="97d0c-154">Asegúrese de que va a modificar el de la biblioteca estándar de .NET.</span><span class="sxs-lookup"><span data-stu-id="97d0c-154">Make sure you're editing the one in the .NET standard library.</span></span>

2. <span data-ttu-id="97d0c-155">Antes de poder enlazar controles a las propiedades de una clase ViewModel, tendrá que configurar una instancia de ViewModel como el contexto de enlace de la página.</span><span class="sxs-lookup"><span data-stu-id="97d0c-155">Before you can bind controls to properties on a ViewModel, you have to set an instance of the ViewModel as the binding context of the page.</span></span> <span data-ttu-id="97d0c-156">Agregue el código XAML siguiente al elemento `ContentPage` de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="97d0c-156">Add the following XAML inside the top-level `ContentPage`.</span></span>

    ```xml
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    ```

3. <span data-ttu-id="97d0c-157">Elimine el contenido de `StackLayout` y agregue espaciado en su interior para mejorar el aspecto de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="97d0c-157">Delete the contents of the `StackLayout` and add some padding inside it to help make the UI look better.</span></span>

    ```xml
    <StackLayout Padding="20">
    </StackLayout>
    ```

4. <span data-ttu-id="97d0c-158">Agregue un control `Editor` que el usuario pueda utilizar para agregar números de teléfono al elemento `StackLayout`, con un elemento `Label` por encima que describa para qué sirve el control de entrada.</span><span class="sxs-lookup"><span data-stu-id="97d0c-158">Add an `Editor` control that the user can use to add phone numbers to the `StackLayout`, with a `Label` above to describe what the entry control is for.</span></span> <span data-ttu-id="97d0c-159">Los controles secundarios de `StackLayout` se apilan de forma horizontal o vertical en el orden en que se agregan los controles, por lo que si primero se agrega `Label`, se colocará sobre `Editor`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-159">`StackLayout`'s stack child controls either horizontally or vertically in the order in which the controls are added, so adding the `Label` first will put it above the `Editor`.</span></span> <span data-ttu-id="97d0c-160">Los controles `Editor` son de entrada multilínea y permiten que el usuario escriba varios números de teléfono, uno por línea.</span><span class="sxs-lookup"><span data-stu-id="97d0c-160">`Editor` controls are multi-line entry controls, allowing the user to enter multiple phone numbers, one per line.</span></span>

    ```xml
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Center"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
    </StackLayout>
    ```

    <span data-ttu-id="97d0c-161">La propiedad `Text` de `Editor` está enlazada a la propiedad `PhoneNumbers` de `MainViewModel`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-161">The `Text` property on the `Editor` is bound to the `PhoneNumbers` property on the `MainViewModel`.</span></span> <span data-ttu-id="97d0c-162">La sintaxis para el enlace consiste en establecer el valor de la propiedad en `"{Binding <property name>}"`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-162">The syntax for binding is to set the property value to `"{Binding <property name>}"`.</span></span> <span data-ttu-id="97d0c-163">Las llaves indican al compilador XAML que este valor es especial y que se debe tratar de manera distinta a un elemento `string` sencillo.</span><span class="sxs-lookup"><span data-stu-id="97d0c-163">The curly braces will tell the XAML compiler that this value is special and should be treated differently from a simple `string`.</span></span>

5. <span data-ttu-id="97d0c-164">Agregue un elemento `Button` para enviar la ubicación del usuario por debajo de `Editor`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-164">Add a `Button` to send the user's location below the `Editor`.</span></span>

    ```xml
    <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
            Command="{Binding SendLocationCommand}" />
    ```

    <span data-ttu-id="97d0c-165">La propiedad `Command` se enlaza al comando `SendLocationCommand` de ViewModel.</span><span class="sxs-lookup"><span data-stu-id="97d0c-165">The `Command` property is bound to the `SendLocationCommand` command on the ViewModel.</span></span> <span data-ttu-id="97d0c-166">Cuando se pulsa el botón, el comando se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="97d0c-166">When the button is tapped, the command will be executed.</span></span>

6. <span data-ttu-id="97d0c-167">Agregue un elemento `Label` para mostrar el mensaje de estado por debajo del elemento `Button`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-167">Add a `Label` to show the status message below the `Button`.</span></span>

    ```xml
    <Label Text="{Binding Message}"
           HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    ```

<span data-ttu-id="97d0c-168">A continuación se muestra el código completo de esta página.</span><span class="sxs-lookup"><span data-stu-id="97d0c-168">The full code for this page is below.</span></span>

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

<span data-ttu-id="97d0c-169">Ejecute la aplicación para ver la nueva interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="97d0c-169">Run the app to see the new UI.</span></span> <span data-ttu-id="97d0c-170">Si quiere validar ahora los enlaces, puede hacerlo si agrega puntos de interrupción a las propiedades o al método `SendLocation`.</span><span class="sxs-lookup"><span data-stu-id="97d0c-170">If you want to validate the bindings at this point, you can do so by adding breakpoints to the properties or the `SendLocation` method.</span></span>

![La interfaz de usuario de la nueva aplicación](../media-drafts/3-new-ui.png)

## <a name="summary"></a><span data-ttu-id="97d0c-172">Resumen</span><span class="sxs-lookup"><span data-stu-id="97d0c-172">Summary</span></span>

<span data-ttu-id="97d0c-173">En esta unidad, ha aprendido a crear la interfaz de usuario para la aplicación mediante XAML, junto con una clase ViewModel para controlar la lógica de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="97d0c-173">In this unit, you learned how to create the UI for the app using XAML, along with a ViewModel to handle the applications logic.</span></span> <span data-ttu-id="97d0c-174">También ha aprendido a enlazar el ViewModel a la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="97d0c-174">You also learned how to bind the ViewModel to the UI.</span></span> <span data-ttu-id="97d0c-175">En la unidad siguiente, agregará la búsqueda de la ubicación a ViewModel.</span><span class="sxs-lookup"><span data-stu-id="97d0c-175">In the next unit, you add location lookup to the ViewModel.</span></span>