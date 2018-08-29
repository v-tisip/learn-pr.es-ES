<span data-ttu-id="bd82b-101">En este módulo se creará una aplicación de consola simple mediante el terminal integrado, se instalarán paquetes NuGet y se usará la extensión de Azure Cosmos DB para ver las bases de datos y las colecciones creadas en el módulo anterior.</span><span class="sxs-lookup"><span data-stu-id="bd82b-101">In this module you will create a simple console app using the integrated terminal, install NuGet packages, and use the Azure Cosmos DB extension to see databases and collections created in the previous module.</span></span> <span data-ttu-id="bd82b-102">Podrá recuperar la cadena de conexión de Azure Cosmos DB de la extensión y, a continuación, empezar a desarrollar con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bd82b-102">You'll retrieve your Azure Cosmos DB connection string from the extension, and then start developing against Azure Cosmos DB.</span></span> 

## <a name="create-a-console-app"></a><span data-ttu-id="bd82b-103">Creación de una aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="bd82b-103">Create a console app</span></span>

1. <span data-ttu-id="bd82b-104">Abra Visual Studio Code y, a continuación, seleccione **Archivo** > **Abrir carpeta**.</span><span class="sxs-lookup"><span data-stu-id="bd82b-104">Open Visual Studio Code, and then select **File** > **Open Folder**.</span></span>

2. <span data-ttu-id="bd82b-105">Cree una carpeta denominada **learning-module** donde desea guardar el nuevo proyecto de C# y, a continuación, haga clic en **Seleccionar carpeta**.</span><span class="sxs-lookup"><span data-stu-id="bd82b-105">Create a new folder named **learning-module** where you want your new C# project to be, and then click **Select Folder**.</span></span>

2. <span data-ttu-id="bd82b-106">Abra el terminal integrado desde Visual Studio Code; para ello, seleccione **Ver** > **Terminal integrado** en el menú principal.</span><span class="sxs-lookup"><span data-stu-id="bd82b-106">Open the integrated terminal from Visual Studio Code by selecting **View** > **Integrated Terminal** from the main menu.</span></span>

3. <span data-ttu-id="bd82b-107">En la ventana del terminal, escriba **dotnet new console**.</span><span class="sxs-lookup"><span data-stu-id="bd82b-107">In the terminal window, type **dotnet new console**.</span></span>

    <span data-ttu-id="bd82b-108">Este comando crea un archivo **Program.cs** en la carpeta con un programa "Hola mundo" sencillo que ya está escrito, junto con un archivo de proyecto de C# llamado **learning-module.csproj**.</span><span class="sxs-lookup"><span data-stu-id="bd82b-108">This command creates a **Program.cs** file in your folder with a simple "Hello World" program already written, along with a C# project file named **learning-module.csproj**.</span></span>

4. <span data-ttu-id="bd82b-109">En la ventana del terminal, escriba el siguiente comando para ejecutar el programa "Hola mundo".</span><span class="sxs-lookup"><span data-stu-id="bd82b-109">In the terminal window, type the following command to run the "Hello World" program.</span></span> 

    ```
    dotnet run
    ```

    <span data-ttu-id="bd82b-110">La ventana del terminal muestra "Hola mundo"</span><span class="sxs-lookup"><span data-stu-id="bd82b-110">The terminal window displays "Hello world!"</span></span> <span data-ttu-id="bd82b-111">como salida.</span><span class="sxs-lookup"><span data-stu-id="bd82b-111">as output.</span></span>

## <a name="connect-the-app-to-azure-cosmos-db"></a><span data-ttu-id="bd82b-112">Conexión de la aplicación a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bd82b-112">Connect the app to Azure Cosmos DB</span></span>

1. <span data-ttu-id="bd82b-113">Inicie sesión en Azure; para ello, haga clic en **Ver** > **Paleta de comandos** y escriba **Azure: Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="bd82b-113">Sign in to Azure by clicking **View** > **Command Palette** and typing **Azure: Sign In**.</span></span>

    <span data-ttu-id="bd82b-114">Siga las indicaciones para copiar y pegar el código proporcionado en el explorador web, que autentica la sesión de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bd82b-114">Follow the prompts to copy and paste the code provided in the web browser, which authenticates your Visual Studio Code session.</span></span>

2. <span data-ttu-id="bd82b-115">Haga clic en el ![icono del explorador](../media/2-setup/visual-studio-code-explorer-icon.png) icono del **explorador** en el menú de la izquierda y luego expanda **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="bd82b-115">Click the ![Explorer icon](../media/2-setup/visual-studio-code-explorer-icon.png) **Explorer** icon on the left menu, and then expand **Azure Cosmos DB**.</span></span>

3. <span data-ttu-id="bd82b-116">Expanda su suscripción de Azure > cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bd82b-116">Expand your Azure subscription > Azure Cosmos DB account.</span></span> <span data-ttu-id="bd82b-117">Si creó la base de datos **Productos** y la colección **Ropa** en los módulos anteriores, la extensión las muestra.</span><span class="sxs-lookup"><span data-stu-id="bd82b-117">If you created the **Products** database and **Clothing** collection in the previous modules, the extension displays them.</span></span>

   ![Extensión de Visual Studio Code en Azure Cosmos DB](../media/2-setup/azure-cosmos-db-vs-code-extension.png) 

4. <span data-ttu-id="bd82b-119">Ahora vamos a crear una base de datos y una colección para los clientes.</span><span class="sxs-lookup"><span data-stu-id="bd82b-119">Now let's create a new database and collection for your customers.</span></span>

    <span data-ttu-id="bd82b-120">En la ventana del explorador, haga clic con el botón derecho en la cuenta y luego haga clic en **Crear base de datos**.</span><span class="sxs-lookup"><span data-stu-id="bd82b-120">In the Explorer window, right-click your account, and then click **Create Database**.</span></span> 
    
    <span data-ttu-id="bd82b-121">En el cuadro de texto de la parte superior de la pantalla, escriba **Users** para el nombre de la base de datos > **ENTRAR** > **WebCustomers** para el nombre de la colección > **ENTRAR** > **userId** para la clave de partición > **ENTRAR** > **1000** para la capacidad de rendimiento inicial > **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="bd82b-121">In the text box at the top of the screen, type **Users** for the database name > **Enter** > **WebCustomers** for the collection name > **Enter** > **userId** for the partition key > **Enter** > **1000** for the initial throughput capacity > **Enter**.</span></span>

    <span data-ttu-id="bd82b-122">![Extensión de Visual Studio Code en Azure Cosmos DB](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) <!--Retake on fresh machine without the other subscriptions showing--></span><span class="sxs-lookup"><span data-stu-id="bd82b-122">![Azure Cosmos DB Visual Studio Code extension](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) <!--Retake on fresh machine without the other subscriptions showing--></span></span>

    <span data-ttu-id="bd82b-123">La nueva base de datos Users y la colección WebCustomers se muestran en la ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="bd82b-123">The new Users database and WebCustomers collection are displayed in the Explorer window.</span></span>

5. <span data-ttu-id="bd82b-124">En el terminal integrado, ejecute cada uno de los siguientes comandos en un símbolo del sistema nuevo para instalar los paquetes NuGet necesarios.</span><span class="sxs-lookup"><span data-stu-id="bd82b-124">In the integrated terminal, run each of the following commands at a new prompt to install the required NuGet packages.</span></span>

    ```
    dotnet add package System.Net.Http
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet add package Bogus
    dotnet restore
    ```

6. <span data-ttu-id="bd82b-125">En la parte superior del panel del explorador, haga clic en **Program.cs** para abrir el archivo.</span><span class="sxs-lookup"><span data-stu-id="bd82b-125">At the top of the Explorer pane, click **Program.cs** to open the file.</span></span>

7. <span data-ttu-id="bd82b-126">Agregue las siguientes instrucciones using después de `using System;`.</span><span class="sxs-lookup"><span data-stu-id="bd82b-126">Add the following using statements after `using System;`.</span></span>

    ```csharp
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

8. <span data-ttu-id="bd82b-127">Agregue las dos constantes siguientes y la variable *client* a la clase Program:</span><span class="sxs-lookup"><span data-stu-id="bd82b-127">Add the following two constants and your *client* variable to the Program class:</span></span>

    ```csharp
    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;
    ```

    <!--TODO: Use more secure method-->

9. <span data-ttu-id="bd82b-128">Copie la cadena de conexión de la extensión de Azure Cosmos DB; para ello, haga clic con el botón derecho en la cuenta learning-module y haga clic en **Copia de la cadena de conexión**.</span><span class="sxs-lookup"><span data-stu-id="bd82b-128">Copy your connection string from the Azure Cosmos DB extension by right-clicking the learning-module account, and clicking **Copy Connection String**.</span></span>

    ![Extensión de Visual Studio Code en Azure Cosmos DB](../media/2-setup/vs-code-copy-connection-string.gif) 

10. <span data-ttu-id="bd82b-130">Pegue la cadena de conexión en un archivo de texto y luego copie la parte **AccountEndpoint** del archivo de texto en **EndpointUrl** en Program.cs.</span><span class="sxs-lookup"><span data-stu-id="bd82b-130">Paste the connection string into a text file, and then copy the **AccountEndpoint** portion from the text file into the **EndpointUrl** in Program.cs.</span></span>

    <span data-ttu-id="bd82b-131">AccountEndpoint debe presentar un aspecto parecido al siguiente código:</span><span class="sxs-lookup"><span data-stu-id="bd82b-131">The AccountEndpoint should look like the following code:</span></span>

    ```csharp
    private const string EndpointUrl = "https://<account name>.documents.azure.com:443/;
    ```

12. <span data-ttu-id="bd82b-132">Ahora copie el valor **AccountKey** del valor de texto en el valor **PrimaryKey** en Program.cs.</span><span class="sxs-lookup"><span data-stu-id="bd82b-132">Now copy the **AccountKey** value from the text value into the **PrimaryKey** value in Program.cs.</span></span>

12. <span data-ttu-id="bd82b-133">En el terminal integrado, escriba el siguiente comando para ejecutar el programa a fin de garantizar su ejecución.</span><span class="sxs-lookup"><span data-stu-id="bd82b-133">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

13. <span data-ttu-id="bd82b-134">Agregue una nueva tarea asincrónica para crear un cliente y comprobar si existe la base de datos Users mediante la adición del siguiente método después del método main.</span><span class="sxs-lookup"><span data-stu-id="bd82b-134">Add a new asynchronous task to create a new client, and check whether the Users database exists by adding the following method after the main method.</span></span>
    
    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });
    }
    ```

14. <span data-ttu-id="bd82b-135">En el terminal integrado, escriba de nuevo el siguiente comando para ejecutar el programa a fin de garantizar su ejecución.</span><span class="sxs-lookup"><span data-stu-id="bd82b-135">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

15. <span data-ttu-id="bd82b-136">Copie y pegue el siguiente código en el método **Main**, a fin de sobrescribir la línea `Console.WriteLine("Hello World!");` actual.</span><span class="sxs-lookup"><span data-stu-id="bd82b-136">Copy and paste the following code into the **Main** method, overwriting the current `Console.WriteLine("Hello World!");` line.</span></span>

    ```csharp
    try
            {
                    Program p = new Program();
                    p.BasicOperations().Wait();
            }
            catch (DocumentClientException de)
            {
                    Exception baseException = de.GetBaseException();
                    Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
            }
            catch (Exception e)
            {
                    Exception baseException = e.GetBaseException();
                    Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
            }
            finally
            {
                    Console.WriteLine("End of demo, press any key to exit.");
                    Console.ReadKey();
            }
    ```

16. <span data-ttu-id="bd82b-137">En el terminal integrado, escriba de nuevo el siguiente comando para ejecutar el programa a fin de garantizar su ejecución.</span><span class="sxs-lookup"><span data-stu-id="bd82b-137">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="bd82b-138">La consola muestra el resultado siguiente.</span><span class="sxs-lookup"><span data-stu-id="bd82b-138">The console displays the following output.</span></span>
    
    ```
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

## <a name="summary"></a><span data-ttu-id="bd82b-139">Resumen</span><span class="sxs-lookup"><span data-stu-id="bd82b-139">Summary</span></span>

<span data-ttu-id="bd82b-140">En este módulo, ha configurado las bases para la aplicación de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bd82b-140">In this module, you set up the groundwork for your Azure Cosmos DB application.</span></span> <span data-ttu-id="bd82b-141">También ha configurado el entorno de desarrollo en Visual Studio Code, ha creado un proyecto sencillo HelloWorld, ha conectado el proyecto al punto de conexión de Azure Cosmos DB y se ha asegurado de la existencia de la base de datos y la colección.</span><span class="sxs-lookup"><span data-stu-id="bd82b-141">You set up your development environment in Visual Studio Code, created a simple HelloWorld project, connected the project to the Azure Cosmos DB endpoint, and ensured your database and collection exist.</span></span>