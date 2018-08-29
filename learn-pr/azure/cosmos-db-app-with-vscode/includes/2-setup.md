En este módulo se creará una aplicación de consola simple mediante el terminal integrado, se instalarán paquetes NuGet y se usará la extensión de Azure Cosmos DB para ver las bases de datos y las colecciones creadas en el módulo anterior. Podrá recuperar la cadena de conexión de Azure Cosmos DB de la extensión y, a continuación, empezar a desarrollar con Azure Cosmos DB. 

## <a name="create-a-console-app"></a>Creación de una aplicación de consola

1. Abra Visual Studio Code y, a continuación, seleccione **Archivo** > **Abrir carpeta**.

2. Cree una carpeta denominada **learning-module** donde desea guardar el nuevo proyecto de C# y, a continuación, haga clic en **Seleccionar carpeta**.

2. Abra el terminal integrado desde Visual Studio Code; para ello, seleccione **Ver** > **Terminal integrado** en el menú principal.

3. En la ventana del terminal, escriba **dotnet new console**.

    Este comando crea un archivo **Program.cs** en la carpeta con un programa "Hola mundo" sencillo que ya está escrito, junto con un archivo de proyecto de C# llamado **learning-module.csproj**.

4. En la ventana del terminal, escriba el siguiente comando para ejecutar el programa "Hola mundo". 

    ```
    dotnet run
    ```

    La ventana del terminal muestra "Hola mundo" como salida.

## <a name="connect-the-app-to-azure-cosmos-db"></a>Conexión de la aplicación a Azure Cosmos DB

1. Inicie sesión en Azure; para ello, haga clic en **Ver** > **Paleta de comandos** y escriba **Azure: Iniciar sesión**.

    Siga las indicaciones para copiar y pegar el código proporcionado en el explorador web, que autentica la sesión de Visual Studio Code.

2. Haga clic en el ![icono del explorador](../media/2-setup/visual-studio-code-explorer-icon.png) icono del **explorador** en el menú de la izquierda y luego expanda **Azure Cosmos DB**.

3. Expanda su suscripción de Azure > cuenta de Azure Cosmos DB. Si creó la base de datos **Productos** y la colección **Ropa** en los módulos anteriores, la extensión las muestra.

   ![Extensión de Visual Studio Code en Azure Cosmos DB](../media/2-setup/azure-cosmos-db-vs-code-extension.png) 

4. Ahora vamos a crear una base de datos y una colección para los clientes.

    En la ventana del explorador, haga clic con el botón derecho en la cuenta y luego haga clic en **Crear base de datos**. 
    
    En el cuadro de texto de la parte superior de la pantalla, escriba **Users** para el nombre de la base de datos > **ENTRAR** > **WebCustomers** para el nombre de la colección > **ENTRAR** > **userId** para la clave de partición > **ENTRAR** > **1000** para la capacidad de rendimiento inicial > **ENTRAR**.

    ![Extensión de Visual Studio Code en Azure Cosmos DB](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) <!--Retake on fresh machine without the other subscriptions showing-->

    La nueva base de datos Users y la colección WebCustomers se muestran en la ventana del explorador.

5. En el terminal integrado, ejecute cada uno de los siguientes comandos en un símbolo del sistema nuevo para instalar los paquetes NuGet necesarios.

    ```
    dotnet add package System.Net.Http
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet add package Bogus
    dotnet restore
    ```

6. En la parte superior del panel del explorador, haga clic en **Program.cs** para abrir el archivo.

7. Agregue las siguientes instrucciones using después de `using System;`.

    ```csharp
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

8. Agregue las dos constantes siguientes y la variable *client* a la clase Program:

    ```csharp
    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;
    ```

    <!--TODO: Use more secure method-->

9. Copie la cadena de conexión de la extensión de Azure Cosmos DB; para ello, haga clic con el botón derecho en la cuenta learning-module y haga clic en **Copia de la cadena de conexión**.

    ![Extensión de Visual Studio Code en Azure Cosmos DB](../media/2-setup/vs-code-copy-connection-string.gif) 

10. Pegue la cadena de conexión en un archivo de texto y luego copie la parte **AccountEndpoint** del archivo de texto en **EndpointUrl** en Program.cs.

    AccountEndpoint debe presentar un aspecto parecido al siguiente código:

    ```csharp
    private const string EndpointUrl = "https://<account name>.documents.azure.com:443/;
    ```

12. Ahora copie el valor **AccountKey** del valor de texto en el valor **PrimaryKey** en Program.cs.

12. En el terminal integrado, escriba el siguiente comando para ejecutar el programa a fin de garantizar su ejecución.

    ```csharp
    dotnet run
    ```

13. Agregue una nueva tarea asincrónica para crear un cliente y comprobar si existe la base de datos Users mediante la adición del siguiente método después del método main.
    
    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });
    }
    ```

14. En el terminal integrado, escriba de nuevo el siguiente comando para ejecutar el programa a fin de garantizar su ejecución.

    ```csharp
    dotnet run
    ```

15. Copie y pegue el siguiente código en el método **Main**, a fin de sobrescribir la línea `Console.WriteLine("Hello World!");` actual.

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

16. En el terminal integrado, escriba de nuevo el siguiente comando para ejecutar el programa a fin de garantizar su ejecución.

    ```csharp
    dotnet run
    ```

    La consola muestra el resultado siguiente.
    
    ```
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

## <a name="summary"></a>Resumen

En este módulo, ha configurado las bases para la aplicación de Azure Cosmos DB. También ha configurado el entorno de desarrollo en Visual Studio Code, ha creado un proyecto sencillo HelloWorld, ha conectado el proyecto al punto de conexión de Azure Cosmos DB y se ha asegurado de la existencia de la base de datos y la colección.