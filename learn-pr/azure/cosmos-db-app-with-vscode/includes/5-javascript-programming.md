Con frecuencia, es necesario actualizar simultáneamente varios documentos de la base de datos. Esta unidad describe cómo crear, registrar y ejecutar procedimientos almacenados de la aplicación de consola. NET.

## <a name="create-a-stored-procedure-in-your-app"></a>Creación de un procedimiento almacenado en la aplicación

En este procedimiento almacenado, se usa OrderId, que contiene una lista de todos los elementos en el pedido, para calcular el total de un pedido. El total del pedido se calcula a partir de la suma de los artículos, menos cualquier dividendo (crédito) que tenga el cliente; además, tiene en cuenta los códigos de cupón.

1. Copie el código siguiente y péguelo al final del archivo Program.cs.

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

2. Ahora, copie el código siguiente y péguelo al final del método **BasicOperations**.

    ```
    await this.UpdateOrderTotal("Users", "WebCustomers", "5-6235");
    ```

3. Guarde el archivo Program.cs y, a continuación, en el terminal integrado, ejecute el comando siguiente.

    ```
    dotnet run
    ```

    La consola muestra el resultado siguiente.

    ```
    Order total is 90.85.
    Press any key to continue ...
    ```

## <a name="clean-up"></a>Limpieza

Si tiene previsto seguir trabajando en los módulos de esta ruta de aprendizaje, omita el proceso de limpieza o siga los pasos siguientes para eliminar los recursos de cara a evitar incurrir en cargos por uso del servicio.

1. En Azure Portal, seleccione **Grupos de recursos** en el extremo izquierdo y luego seleccione el grupo de recursos que creó.  

    Si el menú izquierdo está contraído, haga clic en el ![Botón Expandir](../media/5-javascript-programming/expand.png) para expandirlo.

   ![Métricas en Azure Portal](../media/5-javascript-programming/delete-resources-select.png)

2. En la nueva ventana, seleccione el grupo de recursos y luego haga clic en **Eliminar grupo de recursos**.

   ![Métricas en Azure Portal](../media/5-javascript-programming/delete-resources.png)

3. En la nueva ventana, escriba el nombre del grupo de recursos que quiere eliminar y, después, haga clic en **Eliminar**.

## <a name="summary"></a>Resumen

En este módulo, ha creado una aplicación de consola .NET Core que crea, actualiza y elimina los registros de usuario, consulta los usuarios mediante el uso de SQL y LINQ, y ejecuta un procedimiento almacenado para crear un total de pedido que tiene en cuenta los cupones y los dividendos de los usuarios.