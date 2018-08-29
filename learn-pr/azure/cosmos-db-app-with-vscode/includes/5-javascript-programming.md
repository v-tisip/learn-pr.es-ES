<span data-ttu-id="e72fa-101">Con frecuencia, es necesario actualizar simultáneamente varios documentos de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="e72fa-101">Multiple documents in your database frequently need to be updated at the same time.</span></span> <span data-ttu-id="e72fa-102">Esta unidad describe cómo crear, registrar y ejecutar procedimientos almacenados de la aplicación de consola. NET.</span><span class="sxs-lookup"><span data-stu-id="e72fa-102">This unit discusses how to create, register, and run stored procedures from your .NET console application.</span></span>

## <a name="create-a-stored-procedure-in-your-app"></a><span data-ttu-id="e72fa-103">Creación de un procedimiento almacenado en la aplicación</span><span class="sxs-lookup"><span data-stu-id="e72fa-103">Create a stored procedure in your app</span></span>

<span data-ttu-id="e72fa-104">En este procedimiento almacenado, se usa OrderId, que contiene una lista de todos los elementos en el pedido, para calcular el total de un pedido.</span><span class="sxs-lookup"><span data-stu-id="e72fa-104">In this stored procedure, the OrderId, which contains a list of all the items in the order, is used to calculate an order total.</span></span> <span data-ttu-id="e72fa-105">El total del pedido se calcula a partir de la suma de los artículos, menos cualquier dividendo (crédito) que tenga el cliente; además, tiene en cuenta los códigos de cupón.</span><span class="sxs-lookup"><span data-stu-id="e72fa-105">The order total is calculated from the sum of the items in the order, less any dividend (credit) the customer has, and takes any coupon codes into account.</span></span>

1. <span data-ttu-id="e72fa-106">Copie el código siguiente y péguelo al final del archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="e72fa-106">Copy the following code and paste it into the end of the Program.cs file.</span></span>

    <!--TODO: Update sproc to take order total and check for available dividend, and use of summer coupon code, and provide updated total-->
    ```csharp
    private async Task UpdateOrderTotal(string databaseName, string collectionName, Order orderId)
    {
    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    
    
                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }
    
                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };
    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;
    
    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "ValidateDocumentAge"), document, 1920);
    }
    ```

2. <span data-ttu-id="e72fa-107">Ahora, copie el código siguiente y péguelo al final del método **BasicOperations**.</span><span class="sxs-lookup"><span data-stu-id="e72fa-107">Now copy the following code and paste it into the end of the **BasicOperations** method.</span></span>

    ```
    await this.UpdateOrderTotal("Users", "WebCustomers", "5-6235");
    ```

3. <span data-ttu-id="e72fa-108">Guarde el archivo Program.cs y, a continuación, en el terminal integrado, ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="e72fa-108">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```

    <span data-ttu-id="e72fa-109">La consola muestra el resultado siguiente.</span><span class="sxs-lookup"><span data-stu-id="e72fa-109">The console displays the following output.</span></span>

    ```
    Order total is 90.85.
    Press any key to continue ...
    ```

## <a name="clean-up"></a><span data-ttu-id="e72fa-110">Limpieza</span><span class="sxs-lookup"><span data-stu-id="e72fa-110">Clean up</span></span>

<span data-ttu-id="e72fa-111">Si tiene previsto seguir trabajando en los módulos de esta ruta de aprendizaje, omita el proceso de limpieza o siga los pasos siguientes para eliminar los recursos de cara a evitar incurrir en cargos por uso del servicio.</span><span class="sxs-lookup"><span data-stu-id="e72fa-111">If you plan to continue working on the modules in this learning path, skip the clean-up process, or else use the following steps to delete your resources to avoid incurring charges for use of the service.</span></span>

1. <span data-ttu-id="e72fa-112">En Azure Portal, seleccione **Grupos de recursos** en el extremo izquierdo y luego seleccione el grupo de recursos que creó.</span><span class="sxs-lookup"><span data-stu-id="e72fa-112">In the Azure portal, select **Resource groups** on the far left, and then select the resource group you created.</span></span>  

    <span data-ttu-id="e72fa-113">Si el menú izquierdo está contraído, haga clic en el</span><span class="sxs-lookup"><span data-stu-id="e72fa-113">If the left menu is collapsed, click</span></span> ![Botón Expandir](../media/5-javascript-programming/expand.png) <span data-ttu-id="e72fa-115">para expandirlo.</span><span class="sxs-lookup"><span data-stu-id="e72fa-115">to expand it.</span></span>

   ![Métricas en Azure Portal](../media/5-javascript-programming/delete-resources-select.png)

2. <span data-ttu-id="e72fa-117">En la nueva ventana, seleccione el grupo de recursos y luego haga clic en **Eliminar grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="e72fa-117">In the new window select the resource group, and then click **Delete resource group**.</span></span>

   ![Métricas en Azure Portal](../media/5-javascript-programming/delete-resources.png)

3. <span data-ttu-id="e72fa-119">En la nueva ventana, escriba el nombre del grupo de recursos que quiere eliminar y, después, haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="e72fa-119">In the new window, type the name of the resource group to delete, and then click **Delete**.</span></span>

## <a name="summary"></a><span data-ttu-id="e72fa-120">Resumen</span><span class="sxs-lookup"><span data-stu-id="e72fa-120">Summary</span></span>

<span data-ttu-id="e72fa-121">En este módulo, ha creado una aplicación de consola .NET Core que crea, actualiza y elimina los registros de usuario, consulta los usuarios mediante el uso de SQL y LINQ, y ejecuta un procedimiento almacenado para crear un total de pedido que tiene en cuenta los cupones y los dividendos de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e72fa-121">In this module you've created a .NET Core console application that creates, updates, and deletes user records, queries the users by using SQL and LINQ, and runs a stored procedure to create an order total that takes the users dividends and coupons into account.</span></span>