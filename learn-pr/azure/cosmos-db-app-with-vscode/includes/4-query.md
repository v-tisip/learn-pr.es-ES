<!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Ahora que ha creado los documentos en la aplicación, vamos a consultarlos desde la aplicación. Azure Cosmos DB usa las consultas SQL y las consultas LINQ. Las consultas SQL y cómo ejecutarlas en el portal se tratan en el módulo **Add data and query data in your database** (Adición datos y datos de consulta a la base de datos). 

Por tanto, esta unidad se centra en ejecutar consultas SQL y LINQ desde la aplicación.

Vamos a usar los documentos de usuario que ha creado para la aplicación minorista en línea para probar estas consultas.

## <a name="linq-query-basics"></a>Aspectos básicos de las consultas LINQ

LINQ es un modelo de programación de .NET que expresa cálculos como consultas de secuencias de objetos. Puede crear un objeto **IQueryable** que consulta directamente Azure Cosmos DB, que convierte la consulta LINQ en una consulta de Cosmos DB. La consulta pasa entonces al servidor de Azure Cosmos DB para recuperar un conjunto de resultados en formato JSON. Los resultados devueltos se deserializan en una secuencia de objetos .NET en el cliente. Muchos desarrolladores prefieren las consultas LINQ, ya que proporcionan un único modelo de programación coherente sobre cómo funcionan con objetos en el código de aplicación y cómo expresan la lógica de consulta que se ejecuta en la base de datos.

En la tabla siguiente se muestra cómo las consultas LINQ se convierten en SQL.

| Expresión LINQ | Conversión de SQL |
|---|---|
| `input.Select(family => family.parents[0].familyName);`| `SELECT VALUE f.parents[0].familyName FROM Families f` |
|`input.Select(family => family.children[0].grade + c); // c is an int variable` | `SELECT VALUE f.children[0].grade + c FROM Families f` |
|`input.Select(family => new { name = family.children[0].familyName, grade = family.children[0].grade + 3});`| `SELECT VALUE {"name":f.children[0].familyName, "grade": f.children[0].grade + 3 } FROM Families f`|
|`input.Where(family=> family.parents[0].familyName == "Smith");`|`SELECT * FROM Families f WHERE f.parents[0].familyName = "Smith"`|

## <a name="run-sql-and-linq-queries"></a>Ejecución de consultas SQL y LINQ

1. En el ejemplo siguiente se muestra cómo se podría ejecutar una consulta en SQL, LINQ o LINQ lambda a partir del código de .NET. Copie el código y agréguelo después del método **DeleteUserDocument**.

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

2. Copie y pegue el código siguiente en el método **BasicOperations**, antes de la línea `await this.DeleteUserDocument("Users", "WebCustomers", "1");`.

    ```csharp
    this.ExecuteSimpleQuery("Users", "WebCustomers");
    ```

3. Guarde el archivo Program.cs y, a continuación, en el terminal integrado, ejecute el comando siguiente.
    
    ```
    dotnet run
    ```

    La consola muestra el resultado siguiente.

    ```
    Running LINQ query...
    Running direct SQL query...
    Press any key to continue ...
    ```

    Felicidades. Ha creado correctamente la colección de usuarios de Azure Cosmos DB mediante el uso de consultas SQL y LINQ.

## <a name="summary"></a>Resumen

En esta unidad ha obtenido información sobre las consultas LINQ y luego ha agregado una consulta LINQ y SQL a la aplicación para recuperar los registros de usuario.