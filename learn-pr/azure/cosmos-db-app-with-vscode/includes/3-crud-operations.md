<!--TODO: explain Etag in knowledge needed-->
<!--TODO: Update to weave in the online retailer story-->


<span data-ttu-id="944ef-101">Los datos se almacenan en documentos JSON en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="944ef-101">Data is stored in JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="944ef-102">Los [documentos](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) se pueden crear, recuperar, reemplazar o eliminar en el portal, tal como se mostró en el módulo anterior, o mediante programación, como se describe en este módulo.</span><span class="sxs-lookup"><span data-stu-id="944ef-102">[Documents](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) can be created, retrieved, replaced, or deleted in the portal, as shown in the previous module, or programmatically, as described in this module.</span></span> <span data-ttu-id="944ef-103">Azure Cosmos DB proporciona el SDK de cliente para. NET, .NET Core, Java, Node.js y Python, cada uno de los cuales admite estas operaciones.</span><span class="sxs-lookup"><span data-stu-id="944ef-103">Azure Cosmos DB provides client-side SDKs for .NET, .NET Core, Java, Node.js, and Python, each of which supports these operations.</span></span> <span data-ttu-id="944ef-104">En este módulo usaremos el SDK para .NET Core para llevar a cabo operaciones CRUD (crear, recuperar, actualizar y eliminar).</span><span class="sxs-lookup"><span data-stu-id="944ef-104">In this module we'll be using the .NET Core SDK to perform CRUD (create, retrieve, update, and delete) operations.</span></span> 

<span data-ttu-id="944ef-105">Las operaciones principales para documentos de Azure Cosmos DB forman parte de clase [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet):</span><span class="sxs-lookup"><span data-stu-id="944ef-105">The main operations for Azure Cosmos DB documents are part of the [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) class:</span></span>
* [<span data-ttu-id="944ef-106">CreateDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="944ef-106">CreateDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="944ef-107">ReadDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="944ef-107">ReadDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="944ef-108">ReplaceDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="944ef-108">ReplaceDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* <span data-ttu-id="944ef-109">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet)</span><span class="sxs-lookup"><span data-stu-id="944ef-109">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span></span> <span data-ttu-id="944ef-110">Upsert realiza una operación de crear o reemplazar en función de si el documento ya existe.</span><span class="sxs-lookup"><span data-stu-id="944ef-110">Upsert performs a create or replace operation depending on whether the document already exists.</span></span>
* [<span data-ttu-id="944ef-111">DeleteDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="944ef-111">DeleteDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

<span data-ttu-id="944ef-112">Para llevar a cabo cualquiera de estas operaciones, debe crear una clase que representa el objeto almacenado en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="944ef-112">To perform any of these operations, you need to create a class that represents the object stored in the database.</span></span> <span data-ttu-id="944ef-113">Como estamos trabajando con una base de datos de usuarios, deseará crear una clase **User** para almacenar datos principales como su nombre y UserId (que es necesario, porque es la clave de partición para habilitar el escalado horizontal) y las subclases de preferencias de envío y el historial de pedidos.</span><span class="sxs-lookup"><span data-stu-id="944ef-113">Because we're working with a database of users, you'll want to create a **User** class to store primary data such as their name and UserId (which is required, as that's the partition key to enable horizontal scaling) and subclasses for shipping preferences and order history.</span></span>

<span data-ttu-id="944ef-114">Una vez creadas esas clases para representar a los usuarios, creará nuevos documentos de usuario para cada instancia y realizará algunas operaciones CRUD sencillas en los documentos.</span><span class="sxs-lookup"><span data-stu-id="944ef-114">Once you have those classes created to represent your users, you'll create new user documents for each instance, and then we'll perform some simple CRUD operations on the documents.</span></span>

## <a name="create-documents"></a><span data-ttu-id="944ef-115">Creación de documentos</span><span class="sxs-lookup"><span data-stu-id="944ef-115">Create documents</span></span>

1. <span data-ttu-id="944ef-116">En primer lugar, cree una clase **User** que represente los objetos que va a almacenar en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="944ef-116">First, create a **User** class that represents the objects to store in Azure Cosmos DB.</span></span> <span data-ttu-id="944ef-117">También crearemos subclases **OrderHistory** y **ShippingPreference** que se usan dentro de **User**.</span><span class="sxs-lookup"><span data-stu-id="944ef-117">We will also create **OrderHistory** and **ShippingPreference** subclasses that are used within **User**.</span></span> <span data-ttu-id="944ef-118">Tenga en cuenta que los documentos deben tener una propiedad **Id** serializada como **id** en JSON.</span><span class="sxs-lookup"><span data-stu-id="944ef-118">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> 

    <span data-ttu-id="944ef-119">Para crear estas clases, copie y pegue las siguientes clases **User**, **OrderHistory** y **ShippingPreference** bajo el método **BasicOperations**.</span><span class="sxs-lookup"><span data-stu-id="944ef-119">To create these classes, copy and paste the following **User**, **OrderHistory**, **ShippingPreference** classes underneath the **BasicOperations** method.</span></span>

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

2. <span data-ttu-id="944ef-120">En el terminal integrado, escriba el siguiente comando para ejecutar el programa a fin de garantizar su ejecución.</span><span class="sxs-lookup"><span data-stu-id="944ef-120">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

3. <span data-ttu-id="944ef-121">Ahora copie y pegue la tarea **CreateUserDocumentIfNotExists** en la clase **ShippingPreference**.</span><span class="sxs-lookup"><span data-stu-id="944ef-121">Now copy and paste the **CreateUserDocumentIfNotExists** task under the **ShippingPreference** class.</span></span>

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

4. <span data-ttu-id="944ef-122">Luego agregue lo siguiente al método **BasicOperations**.</span><span class="sxs-lookup"><span data-stu-id="944ef-122">Then add the following to the **BasicOperations** method.</span></span>

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

5. <span data-ttu-id="944ef-123">En el terminal integrado, escriba de nuevo el siguiente comando para ejecutar el programa a fin de garantizar su ejecución.</span><span class="sxs-lookup"><span data-stu-id="944ef-123">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="944ef-124">El terminal muestra la salida siguiente, que indica que ambos registros de usuario se crearon correctamente.</span><span class="sxs-lookup"><span data-stu-id="944ef-124">The terminal displays the following output, indicating that both user records were successfully created.</span></span> 

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a><span data-ttu-id="944ef-125">Lectura de documentos</span><span class="sxs-lookup"><span data-stu-id="944ef-125">Read documents</span></span>

1. <span data-ttu-id="944ef-126">Para leer los documentos de la base de datos, copie el código siguiente y colóquelo al final del archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="944ef-126">To read documents from the database, copy in the following code and place it at the end of the Program.cs file.</span></span>

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

2.  <span data-ttu-id="944ef-127">Copie y pegue el código siguiente al final del método **BasicOperations**, después de la línea `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.</span><span class="sxs-lookup"><span data-stu-id="944ef-127">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

4. <span data-ttu-id="944ef-128">Guarde el archivo Program.cs y, a continuación, en el terminal integrado, ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="944ef-128">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="944ef-129">El terminal muestra la salida siguiente, donde la salida "Found user 1" indica que se encontró el documento.</span><span class="sxs-lookup"><span data-stu-id="944ef-129">The terminal displays the following output, where the output "Found user 1" indicates the document was found.</span></span>

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

## <a name="replace-documents"></a><span data-ttu-id="944ef-130">Reemplazo de documentos</span><span class="sxs-lookup"><span data-stu-id="944ef-130">Replace documents</span></span>
<span data-ttu-id="944ef-131">Azure Cosmos DB admite la sustitución de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="944ef-131">Azure Cosmos DB supports replacing JSON documents.</span></span> <span data-ttu-id="944ef-132">En este caso, actualizaremos un registro de usuario para aplicar un cambio en su apellido.</span><span class="sxs-lookup"><span data-stu-id="944ef-132">In this case, we'll update a user record to account for a change to their last name.</span></span>

1. <span data-ttu-id="944ef-133">Copie y pegue el método **ReplaceFamilyDocument** en el método **CreateUserDocumentIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="944ef-133">Copy and paste the **ReplaceFamilyDocument** method underneath your **CreateUserDocumentIfNotExists** method.</span></span>

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, string LastName, User updatedUser)
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, LastName), updatedUser);
        this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", LastName);
    }
    ```

2. <span data-ttu-id="944ef-134">Copie y pegue el código siguiente al final del método **BasicOperations**, después de la línea `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.</span><span class="sxs-lookup"><span data-stu-id="944ef-134">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe.LastName, yanhe);
    ```
    <!--TODO: need to fix this as it's giving an error-->

4. <span data-ttu-id="944ef-135">Guarde el archivo Program.cs y, a continuación, en el terminal integrado, ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="944ef-135">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="944ef-136">El terminal muestra la salida siguiente, donde la salida "Replace last name for Suh" indica que se reemplazó el documento.</span><span class="sxs-lookup"><span data-stu-id="944ef-136">The terminal displays the following output, where the output "Replaced last name for Suh" indicates the document was replaced.</span></span>

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

## <a name="delete-documents"></a><span data-ttu-id="944ef-137">Eliminar documentos</span><span class="sxs-lookup"><span data-stu-id="944ef-137">Delete documents</span></span>

1. <span data-ttu-id="944ef-138">Copie y pegue el método **DeleteUserDocument** en el método **ReplaceUserDocument**.</span><span class="sxs-lookup"><span data-stu-id="944ef-138">Copy and paste the **DeleteUserDocument** method underneath your **ReplaceUserDocument** method.</span></span>
    
    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, string documentName)
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName), new RequestOptions { PartitionKey = new PartitionKey("User.UserId") });
        Console.WriteLine("Deleted User {0}", documentName);
    }
    ```

2. <span data-ttu-id="944ef-139">Copie y pegue el código siguiente en el método **BasicOperations** debajo de la ejecución de la segunda consulta.</span><span class="sxs-lookup"><span data-stu-id="944ef-139">Copy and paste the following code to your **BasicOperations** method underneath the second query execution.</span></span>

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", "1");
    ```

3. <span data-ttu-id="944ef-140">Guarde el archivo Program.cs y, a continuación, en el terminal integrado, ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="944ef-140">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```

    <span data-ttu-id="944ef-141">Felicidades.</span><span class="sxs-lookup"><span data-stu-id="944ef-141">Congratulations!</span></span> <span data-ttu-id="944ef-142">Ha eliminado correctamente un documento de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="944ef-142">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <a name="summary"></a><span data-ttu-id="944ef-143">Resumen</span><span class="sxs-lookup"><span data-stu-id="944ef-143">Summary</span></span>

<span data-ttu-id="944ef-144">En esta unidad creó, reemplazó y eliminó documentos en la base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="944ef-144">In this unit you created, replaced, and deleted documents in your Azure Cosmos DB database.</span></span>