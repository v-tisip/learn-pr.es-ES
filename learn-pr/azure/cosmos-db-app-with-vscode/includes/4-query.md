<span data-ttu-id="d0663-101"><!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Ahora que ha creado los documentos en la aplicación, vamos a consultarlos desde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0663-101"><!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Now that you've created documents in your application, let's query them from your application.</span></span> <span data-ttu-id="d0663-102">Azure Cosmos DB usa las consultas SQL y las consultas LINQ.</span><span class="sxs-lookup"><span data-stu-id="d0663-102">Azure Cosmos DB uses SQL queries and LINQ queries.</span></span> <span data-ttu-id="d0663-103">Las consultas SQL y cómo ejecutarlas en el portal se tratan en el módulo **Add data and query data in your database** (Adición datos y datos de consulta a la base de datos).</span><span class="sxs-lookup"><span data-stu-id="d0663-103">SQL queries and how to run them in the portal is discussed in the **Add data and query data in your database** module.</span></span> 

<span data-ttu-id="d0663-104">Por tanto, esta unidad se centra en ejecutar consultas SQL y LINQ desde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d0663-104">So this unit focuses on running SQL queries and LINQ queries from your application.</span></span>

<span data-ttu-id="d0663-105">Vamos a usar los documentos de usuario que ha creado para la aplicación minorista en línea para probar estas consultas.</span><span class="sxs-lookup"><span data-stu-id="d0663-105">We'll use the user documents you've created for your online retailer application to test these queries.</span></span>

## <a name="linq-query-basics"></a><span data-ttu-id="d0663-106">Aspectos básicos de las consultas LINQ</span><span class="sxs-lookup"><span data-stu-id="d0663-106">LINQ query basics</span></span>

<span data-ttu-id="d0663-107">LINQ es un modelo de programación de .NET que expresa cálculos como consultas de secuencias de objetos.</span><span class="sxs-lookup"><span data-stu-id="d0663-107">LINQ is a .NET programming model that expresses computations as queries on streams of objects.</span></span> <span data-ttu-id="d0663-108">Puede crear un objeto **IQueryable** que consulta directamente Azure Cosmos DB, que convierte la consulta LINQ en una consulta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0663-108">You can create an **IQueryable** object that directly queries Azure Cosmos DB, which translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="d0663-109">La consulta pasa entonces al servidor de Azure Cosmos DB para recuperar un conjunto de resultados en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="d0663-109">The query is then passed to the Azure Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="d0663-110">Los resultados devueltos se deserializan en una secuencia de objetos .NET en el cliente.</span><span class="sxs-lookup"><span data-stu-id="d0663-110">The returned results are deserialized into a stream of .NET objects on the client side.</span></span> <span data-ttu-id="d0663-111">Muchos desarrolladores prefieren las consultas LINQ, ya que proporcionan un único modelo de programación coherente sobre cómo funcionan con objetos en el código de aplicación y cómo expresan la lógica de consulta que se ejecuta en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="d0663-111">Many developers prefer LINQ queries, as they provide a single consistent programming model across how they work with objects in application code and how they express query logic running in the database.</span></span>

<span data-ttu-id="d0663-112">En la tabla siguiente se muestra cómo las consultas LINQ se convierten en SQL.</span><span class="sxs-lookup"><span data-stu-id="d0663-112">The following table shows how LINQ queries are translated into SQL.</span></span>

| <span data-ttu-id="d0663-113">Expresión LINQ</span><span class="sxs-lookup"><span data-stu-id="d0663-113">LINQ expression</span></span> | <span data-ttu-id="d0663-114">Conversión de SQL</span><span class="sxs-lookup"><span data-stu-id="d0663-114">SQL translation</span></span> |
|---|---|
| `input.Select(family => family.parents[0].familyName);`| `SELECT VALUE f.parents[0].familyName FROM Families f` |
|`input.Select(family => family.children[0].grade + c); // c is an int variable` | `SELECT VALUE f.children[0].grade + c FROM Families f` |
|`input.Select(family => new { name = family.children[0].familyName, grade = family.children[0].grade + 3});`| `SELECT VALUE {"name":f.children[0].familyName, "grade": f.children[0].grade + 3 } FROM Families f`|
|`input.Where(family=> family.parents[0].familyName == "Smith");`|`SELECT * FROM Families f WHERE f.parents[0].familyName = "Smith"`|

## <a name="run-sql-and-linq-queries"></a><span data-ttu-id="d0663-115">Ejecución de consultas SQL y LINQ</span><span class="sxs-lookup"><span data-stu-id="d0663-115">Run SQL and LINQ queries</span></span>

1. <span data-ttu-id="d0663-116">En el ejemplo siguiente se muestra cómo se podría ejecutar una consulta en SQL, LINQ o LINQ lambda a partir del código de .NET.</span><span class="sxs-lookup"><span data-stu-id="d0663-116">The following sample shows how a query could be performed in SQL, LINQ, or LINQ lambda from your .NET code.</span></span> <span data-ttu-id="d0663-117">Copie el código y agréguelo después del método **DeleteUserDocument**.</span><span class="sxs-lookup"><span data-stu-id="d0663-117">Copy the code and add it after your **DeleteUserDocument** method.</span></span>

    ```csharp
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };
    
            // Here we find the Andersen family via its LastName
            IQueryable<USer> userQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(u => u.LastName == "Sun");
    
            // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (User user in userQuery)
            {
                Console.WriteLine("\tRead {0}", user);
            }
    
            // Now execute the same query via direct SQL
            IQueryable<User> userQueryInSql = this.client.CreateDocumentQuery<User>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM User WHERE User.LastName = 'Sun'",
                    queryOptions);
    
            Console.WriteLine("Running direct SQL query...");
            foreach (User user in userQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", user);
            }
    
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }
    ```

2. <span data-ttu-id="d0663-118">Copie y pegue el código siguiente en el método **BasicOperations**, antes de la línea `await this.DeleteUserDocument("Users", "WebCustomers", "1");`.</span><span class="sxs-lookup"><span data-stu-id="d0663-118">Copy and paste the following code to your **BasicOperations** method, before the `await this.DeleteUserDocument("Users", "WebCustomers", "1");` line.</span></span>

    ```csharp
    this.ExecuteSimpleQuery("Users", "WebCustomers");
    ```

3. <span data-ttu-id="d0663-119">Guarde el archivo Program.cs y, a continuación, en el terminal integrado, ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="d0663-119">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>
    
    ```
    dotnet run
    ```

    <span data-ttu-id="d0663-120">La consola muestra el resultado siguiente.</span><span class="sxs-lookup"><span data-stu-id="d0663-120">The console displays the following output.</span></span>

    ```
    Running LINQ query...
    Running direct SQL query...
    Press any key to continue ...
    ```

    <span data-ttu-id="d0663-121">Felicidades.</span><span class="sxs-lookup"><span data-stu-id="d0663-121">Congratulations!</span></span> <span data-ttu-id="d0663-122">Ha creado correctamente la colección de usuarios de Azure Cosmos DB mediante el uso de consultas SQL y LINQ.</span><span class="sxs-lookup"><span data-stu-id="d0663-122">You have successfully your Azure Cosmos DB collection of users by using SQL and LINQ queries.</span></span>

## <a name="summary"></a><span data-ttu-id="d0663-123">Resumen</span><span class="sxs-lookup"><span data-stu-id="d0663-123">Summary</span></span>

<span data-ttu-id="d0663-124">En esta unidad ha obtenido información sobre las consultas LINQ y luego ha agregado una consulta LINQ y SQL a la aplicación para recuperar los registros de usuario.</span><span class="sxs-lookup"><span data-stu-id="d0663-124">In this unit you learned about LINQ queries, and then added a LINQ and SQL query to your application to retrieve user records.</span></span>