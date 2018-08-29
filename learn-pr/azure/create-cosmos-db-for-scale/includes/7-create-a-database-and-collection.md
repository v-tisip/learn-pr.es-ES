Ahora que comprende cómo se usan las unidades de solicitud para determinar el rendimiento de la base de datos y cómo la clave de partición crea la estrategia de escalabilidad horizontal para la base de datos, está listo para crear la base de datos y la colección.

## <a name="creating-your-database-and-collection"></a>Creación de la colección y la base de datos

1. En Azure Portal, haga clic en **Explorador de datos** > **Nueva colección**.
    
    El área **Agregar colección** se muestra a la derecha. Puede que deba desplazarse a la derecha para verla.

    ![Hoja Agregar colección del Explorador de datos de Azure Portal](../media/5-create-a-database-and-collection/azure-cosmosdb-data-explorer.png)

2. En la página **Agregar colección**, especifique la configuración de la nueva colección.

    Configuración|Valor sugerido|DESCRIPCIÓN
    ---|---|---
    Id. de base de datos|Usuarios|Escriba *Usuarios* como nombre de la nueva base de datos. Los nombres de base de datos tiene que tener entre 1 y 255 caracteres y no pueden contener /, \\; #, ?, o un espacio al final.
    Id. de colección|WebCustomers|Escriba *WebCustomers* como nombre de la nueva colección. Los identificadores de las colecciones tienen los mismos requisitos de caracteres que los nombres de las bases de datos.
    Capacidad de almacenamiento| Ilimitado |Use el valor predeterminado de **Ilimitado**. Este valor es la capacidad de almacenamiento de la base de datos y permite que la base de datos se escale horizontalmente según sea necesario.
    Clave de partición|/UserId|UserID es una buena clave de partición para un escenario de comercio minorista en línea, así que muchas consultas giran en torno al identificador de cliente.
    Throughput|1000 RU|Cambie el rendimiento a 1000 unidades de solicitud por segundo (RU/s). 1000 es el valor de RU/s mínimo que puede establecer para permitir el escalado automático.
    
    Por ahora, no active la opción de aprovisionamiento del rendimiento de la base de datos y no agregue ninguna clave única a la colección. 
    
3. Haga clic en **OK**.

    El Explorador de datos muestra la nueva base de datos y la colección.

    ![El Explorador de datos de Azure Portal mostrando la nueva base de datos y la colección](../media/5-create-a-database-and-collection/azure-cosmos-db-new-collection.png)

## <a name="summary"></a>Resumen

En esta unidad, usó su conocimiento de las claves de partición y de las unidades de solicitud para crear una base de datos y una colección con la configuración adecuada de rendimiento y escalado para sus necesidades empresariales.