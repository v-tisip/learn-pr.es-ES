Su empresa ha elegido Azure Cosmos DB para satisfacer las demandas de su base de clientes y productos en expansión. Se le ha encargado la creación de la base de datos.

El primer paso es crear una cuenta de Azure Cosmos DB. 

## <a name="what-is-an-azure-cosmos-db-account"></a>¿Qué es una cuenta de Azure Cosmos DB?

La cuenta de Azure Cosmos DB es un recurso de Azure que actúa como una entidad organizativa para las bases de datos. Conecta su uso a la suscripción de Azure para fines de facturación.

Cada cuenta de Azure Cosmos DB se asocia con uno de los varios modelos de datos que Azure Cosmos DB admite, y puede crear tantas cuentas como sean necesarias. 

La API de SQL es el modelo de datos preferido si va a crear una aplicación. Si va a trabajar con tablas o gráficos o va a migrar los datos de MongoDB o Cassandra a Azure, cree cuentas adicionales y seleccione los modelos de datos relevantes.

Al crear una cuenta, elija un identificador que sea significativo para usted, ya que servirá para identificar la cuenta. Además, cree la cuenta en la región de Azure más cercana a los usuarios para minimizar la latencia entre el centro de datos y los usuarios.

Opcionalmente, puede configurar las redes virtuales y la redundancia geográfica durante la creación de la cuenta, pero esto puede hacerse más adelante. En este módulo no se habilitará dicha configuración.

## <a name="creating-an-azure-cosmos-db-account-in-the-portal"></a>Creación de una cuenta de Azure Cosmos DB en el portal

<!--TODO: Update portal link with one that routes to free Learning acct-->
1. Inicie sesión en el [Azure Portal](https://portal.azure.com/).
2. Haga clic en **Crear un recurso** > **Bases de datos** > **Azure Cosmos DB**.
   
   ![El panel de las bases de datos de Azure Portal](../media/1-introduction/create-nosql-db-databases-json-tutorial-1.png)

3. En la página **Nueva cuenta**, especifique la configuración de la nueva cuenta de Azure Cosmos DB.
 
    Configuración|Valor|DESCRIPCIÓN
    ---|---|---
    ID|*Escriba un nombre único*|Escriba un nombre único para identificar esta cuenta de Azure Cosmos DB. Como *documents.azure.com* se anexará al identificador que proporcione para crear el URI, debe usar un identificador único pero reconocible.<br><br>El identificador puede contener solo letras minúsculas, números y el carácter guion (-), y debe tener una extensión de entre 3 y 50 caracteres.
    API|SQL|La API determina el tipo de cuenta que se va a crear. Azure Cosmos DB proporciona cinco API que se adaptan a las necesidades de la aplicación: SQL (base de datos de documentos), Gremlin (base de datos de grafos), MongoDB (base de datos de documentos), Azure Table y Cassandra, y cada una de ellas requiere actualmente una cuenta independiente. <br><br>Seleccione **SQL** porque en este módulo va a crear una base de datos de documentos que es consultable mediante la sintaxis SQL y accesible con la API de SQL.|
    Subscription|*Su suscripción*|Seleccione la suscripción de Azure que quiere usar para esta cuenta de Azure Cosmos DB. 
    Grupo de recursos|Crear nuevo<br><br>*A continuación, escriba el mismo nombre único que se proporcionó anteriormente en el identificador*|Seleccione **Crear nuevo** y, después, escriba un nombre nuevo de grupo de recursos para la cuenta. Para simplificar, puede usar el mismo nombre como identificador. 
    Ubicación|*Seleccione la región más cercana a los usuarios*|Seleccione la ubicación geográfica en la que se va a hospedar la cuenta de Azure Cosmos DB. Use la ubicación más cercana a los usuarios para proporcionarles el acceso más rápido a los datos.
    Habilitar redundancia geográfica| Déjelo en blanco | Esta configuración crea una versión replicada de la base de datos en una segunda región (emparejada). Déjela en blanco por ahora, ya que la base de datos se puede replicar más tarde. 
    Redes virtuales|Disabled|Deje las redes virtuales deshabilitadas por ahora. Puede habilitarlas más tarde. 

4. Haga clic en **Create**(Crear).

    ![Página de la nueva cuenta de Azure Cosmos DB](../media/1-introduction/azure-cosmos-db-create-new-account.png)

5. La cuenta tarda unos minutos en crearse. Espere a que en el portal se muestre la notificación de que la implementación se ha realizado correctamente y luego haga clic en la notificación. 

    ![Alerta de notificación](../media/1-introduction/azure-cosmos-db-notification.png)

6. En la ventana de notificación, haga clic en **Ir al recurso**.

    ![Ir al recurso](../media/1-introduction/azure-cosmos-db-go-to-resource.png)

    En el portal se muestra la página **¡Enhorabuena! Se ha creado su cuenta de Azure Cosmos DB**.

    ![El panel de las notificaciones de Azure Portal](../media/1-introduction/azure-cosmos-db-account-created.png)

## <a name="summary"></a>Resumen

Ha creado una cuenta de Azure Cosmos DB, que es el primer paso para crear una base de datos de Azure Cosmos DB. Seleccionó la configuración adecuada para sus tipos de datos y estableció la ubicación de la cuenta para minimizar la latencia para los usuarios.
