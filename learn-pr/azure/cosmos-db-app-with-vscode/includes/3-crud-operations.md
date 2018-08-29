<!--TODO: explain Etag in knowledge needed-->
<!--TODO: Update to weave in the online retailer story-->


Los datos se almacenan en documentos JSON en Azure Cosmos DB. Los [documentos](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) se pueden crear, recuperar, reemplazar o eliminar en el portal, tal como se mostró en el módulo anterior, o mediante programación, como se describe en este módulo. Azure Cosmos DB proporciona el SDK de cliente para. NET, .NET Core, Java, Node.js y Python, cada uno de los cuales admite estas operaciones. En este módulo usaremos el SDK para .NET Core para llevar a cabo operaciones CRUD (crear, recuperar, actualizar y eliminar). 

Las operaciones principales para documentos de Azure Cosmos DB forman parte de clase [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet):
* [CreateDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [ReadDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [ReplaceDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* [UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet) Upsert realiza una operación de crear o reemplazar en función de si el documento ya existe.
* [DeleteDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

Para llevar a cabo cualquiera de estas operaciones, debe crear una clase que representa el objeto almacenado en la base de datos. Como estamos trabajando con una base de datos de usuarios, deseará crear una clase **User** para almacenar datos principales como su nombre y UserId (que es necesario, porque es la clave de partición para habilitar el escalado horizontal) y las subclases de preferencias de envío y el historial de pedidos.

Una vez creadas esas clases para representar a los usuarios, creará nuevos documentos de usuario para cada instancia y realizará algunas operaciones CRUD sencillas en los documentos.

## <a name="create-documents"></a>Creación de documentos

1. En primer lugar, cree una clase **User** que represente los objetos que va a almacenar en Azure Cosmos DB. También crearemos subclases **OrderHistory** y **ShippingPreference** que se usan dentro de **User**. Tenga en cuenta que los documentos deben tener una propiedad **Id** serializada como **id** en JSON. 

    Para crear estas clases, copie y pegue las siguientes clases **User**, **OrderHistory** y **ShippingPreference** bajo el método **BasicOperations**.

    <!--TODO: specify JSON for all of these? -->
    ```csharp
    public class User
    {
            [JsonProperty("id")]
            public string Id { get; set; }
            [JsonProperty("userId")]
            public string UserId { get; set; }
            [JsonProperty("lastName")]
            public string LastName { get; set; }
            [JsonProperty("firstName")]
            public string FirstName { get; set; }
            [JsonProperty("email")]
            public string Email { get; set; }
            [JsonProperty("dividend")]
            public string Dividend { get; set; }
            public OrderHistory[] OrderHistory { get; set; }
            public ShippingPreference[] ShippingPreference { get; set; }
            public CouponsUsed[] Coupons { get; set; }
            public override string ToString()
            {
            return JsonConvert.SerializeObject(this);
            }
    }
    
    public class OrderHistory
    {
            public string OrderId { get; set; }
            public string DateShipped { get; set; }
            public string Total { get; set; }
    }
    
    public class ShippingPreference
    {
            public int Priority { get; set; }
            public string AddressLine1 { get; set; }
            public string AddressLine2 { get; set; }
            public string City { get; set; }
            public string State { get; set; }
            public string ZipCode { get; set; }
            public string Country { get; set; }
    }
    
    public class CouponsUsed
    {
            public string CouponCode { get; set; }
    
    }
    
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }
    ```

2. En el terminal integrado, escriba el siguiente comando para ejecutar el programa a fin de garantizar su ejecución.

    ```csharp
    dotnet run
    ```

3. Ahora copie y pegue la tarea **CreateUserDocumentIfNotExists** en la clase **ShippingPreference**.

    ```csharp
    private async Task CreateUserDocumentIfNotExists(string databaseName, string collectionName, User user)
    {
            try
            {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey("user.userId") });
            this.WriteToConsoleAndPromptToContinue("Found {0}", user.Id);
            }
            catch (DocumentClientException de)
            {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                    await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), user);
                    this.WriteToConsoleAndPromptToContinue("Created User {0}", user.Id);
            }
            else
            {
                    throw;
            }
            }
    }
    ```

4. Luego agregue lo siguiente al método **BasicOperations**.

    ```csharp
     User yanhe = new User
                {
                    Id = "1",
                    UserId = "yanhe",
                    LastName = "He",
                    FirstName = "Yan",
                    Email = "yanhe@todo.com",
                    OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1000",
                    DateShipped = "08/17/2018",
                    Total = "52.49"
                }
            },
                    ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "90 W 8th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
                };
    
                await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", yanhe);
    
                User nelapin = new User
                {
                    Id = "2",
                    UserId = "nelapin",
                    LastName = "Pindakova",
                    FirstName = "Nela",
                    Email = "nelapin@todo.com",
                    Dividend = "8.50",
                    OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1001",
                    DateShipped = "08/17/2018",
                    Total = "105.89"
                }
            },
                    ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "505 NW 5th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    },
                    new ShippingPreference {
                            Priority = 2,
                            AddressLine1 = "505 NW 5th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
                    Coupons = new CouponsUsed[]
             {
                 new CouponsUsed{
                     CouponCode = "Fall2018"
                 }
             }
                };
    
                await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);
    ```

5. En el terminal integrado, escriba de nuevo el siguiente comando para ejecutar el programa a fin de garantizar su ejecución.

    ```csharp
    dotnet run
    ```

    El terminal muestra la salida siguiente, que indica que ambos registros de usuario se crearon correctamente. 

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a>Lectura de documentos

1. Para leer los documentos de la base de datos, copie el código siguiente y colóquelo al final del archivo Program.cs.

    ```csharp
    private async Task ReadUserDocument(string databaseName, string collectionName, User user)
    {
            try
            {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey("user.userId") });
            this.WriteToConsoleAndPromptToContinue("Found user {0}", user.Id);
            }
            catch (DocumentClientException de)
            {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found", user.Id);
            }
            else
            {
                throw;
            }
            }
    }
    ```

2.  Copie y pegue el código siguiente al final del método **BasicOperations**, después de la línea `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

4. Guarde el archivo Program.cs y, a continuación, en el terminal integrado, ejecute el comando siguiente.

    ```
    dotnet run
    ```
    El terminal muestra la salida siguiente, donde la salida "Found user 1" indica que se encontró el documento.

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Found user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="replace-documents"></a>Reemplazo de documentos
Azure Cosmos DB admite la sustitución de documentos JSON. En este caso, actualizaremos un registro de usuario para aplicar un cambio en su apellido.

1. Copie y pegue el método **ReplaceFamilyDocument** en el método **CreateUserDocumentIfNotExists**.

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, string LastName, User updatedUser)
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, LastName), updatedUser);
        this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", LastName);
    }
    ```

2. Copie y pegue el código siguiente al final del método **BasicOperations**, después de la línea `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe.LastName, yanhe);
    ```
    <!--TODO: need to fix this as it's giving an error-->

4. Guarde el archivo Program.cs y, a continuación, en el terminal integrado, ejecute el comando siguiente.

    ```
    dotnet run
    ```
    El terminal muestra la salida siguiente, donde la salida "Replace last name for Suh" indica que se reemplazó el documento.

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Found user 1
    Press any key to continue ...
    Replaced last name for Suh 
    End of demo, press any key to exit.
    ```

## <a name="delete-documents"></a>Eliminar documentos

1. Copie y pegue el método **DeleteUserDocument** en el método **ReplaceUserDocument**.
    
    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, string documentName)
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName), new RequestOptions { PartitionKey = new PartitionKey("User.UserId") });
        Console.WriteLine("Deleted User {0}", documentName);
    }
    ```

2. Copie y pegue el código siguiente en el método **BasicOperations** debajo de la ejecución de la segunda consulta.

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", "1");
    ```

3. Guarde el archivo Program.cs y, a continuación, en el terminal integrado, ejecute el comando siguiente.

    ```
    dotnet run
    ```

    Felicidades. Ha eliminado correctamente un documento de Azure Cosmos DB.

## <a name="summary"></a>Resumen

En esta unidad creó, reemplazó y eliminó documentos en la base de datos de Azure Cosmos DB.