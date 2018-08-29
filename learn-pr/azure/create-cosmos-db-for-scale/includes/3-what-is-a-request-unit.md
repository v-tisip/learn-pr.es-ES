A continuación, consideraremos los datos a través de nuestra base de datos. Esto es importante para asegurarse de que podemos administrar el volumen de transacciones para nuestras necesidades empresariales. Los requisitos de rendimiento no siempre son coherentes. Por ejemplo, puede crear un sitio web de compras que se deba escalar durante las festividades o las ofertas. Para comenzar, calcularemos los requisitos de rendimiento de la base de datos.

## <a name="what-is-database-throughput"></a>¿Qué es el rendimiento de la base de datos? 

El rendimiento de la base de datos es el número de lecturas y escrituras que la base de datos puede realizar en un solo segundo. 

Para escalar el rendimiento de manera estratégica, debe calcular las necesidades de rendimiento mediante el cálculo del número de lecturas y escrituras que debe admitir en distintos momentos y para distintos tamaños de documento. Si calcula correctamente, los usuarios seguirán satisfecho cuando se produzcan aumentos en la demanda. Si calcula de manera incorrecta, las solicitudes se pueden ver limitadas en cuanto a velocidad y las operaciones tendrán que esperar y volver a intentar ejecutarse, lo que probablemente provocará una latencia elevada e insatisfacción en los clientes.

## <a name="what-is-a-request-unit"></a>¿Qué es una unidad de solicitud?

Azure Cosmos DB mide el rendimiento con lo que se denomina una **unidad de solicitud (RU)**. El uso de la unidad de solicitud se mide por segundo, por lo que la unidad de medida es **unidades de solicitud por segundo (RU/s)**. Debe reservar el número de RU/s que desea que Azure Cosmos DB aprovisione por adelantado, para que pueda administrar la carga que se calculó, y puede escalar o reducir verticalmente las RU/s en cualquier momento para satisfacer la demanda en curso.

## <a name="request-unit-basics"></a>Conceptos básicos de unidad de solicitud

Una unidad de solicitud única, 1 RU, es equivalente al costo aproximado de realizar una solicitud GET en un documento de 1 KB con el identificador de un documento. Realizar una operación GET mediante el uso del identificador de un documento es un medio eficaz para recuperar un documento y, por tanto, el costo es pequeño. Crear, reemplazar o eliminar el mismo elemento requiere que el servicio lleve a cabo un procesamiento adicional y, por tanto, requiere más unidades de solicitud.

El número de unidades de solicitud que se usa para una operación cambia según el tamaño del documento, el número de propiedades en el documento, la operación que se realiza y algunos conceptos adicionales complejos, como la coherencia y la directiva de indexación.

En la tabla siguiente se muestra el número de unidades de solicitud que se necesita para elementos de tres tamaños diferentes (1 KB, 4 KB y 64 KB) y en dos niveles de rendimiento distintos (500 lecturas/segundo + 100 escrituras/segundo y 500 lecturas/segundo + 500 escrituras/segundo). En este ejemplo, la coherencia de datos se establece en **Sesión**, y la directiva de indexación se establece en **Ninguna**.

| Tamaño del elemento | Lecturas/segundo | Escrituras/segundo | Unidades de solicitud
| --- | --- | --- | --- |
| 1 KB | 500 | 100 | (500 * 1) + (100 * 5) = 1000 RU/s
| 1 KB | 500 | 500 | (500 * 1) + (500 * 5) = 3000 RU/s
| 4 KB | 500 | 100 | (500 * 1,3) + (100 * 7) = 1350 RU/s
| 4 KB | 500 | 500 | (500 * 1,3) + (500 * 7) = 4150 RU/s
| 64 KB | 500 | 100 | (500 * 10) + (100 * 48) = 9800 RU/s
| 64 KB | 500 | 500 | (500 * 10) + (500 * 48) = 29 000 RU/s
 
Como puede ver, cuanto mayor sea el elemento y cuantas más lecturas y escrituras se necesiten, más unidades de solicitud debe reservar. Si tiene que calcular las necesidades de rendimiento de una aplicación, Azure Cosmos DB [Capacity Planner](https://www.documentdb.com/capacityplanner) es una herramienta en línea que le permite cargar un documento JSON de ejemplo y establecer el número de operaciones que necesita completar por segundo. Luego proporciona un total estimado que se debe reservar.

## <a name="exceeding-throughput-limits"></a>Superación de los límites de rendimiento

Si no reserva unidades de solicitud suficientes e intenta leer o escribir más datos de los que permite el rendimiento aprovisionado, se limitará la velocidad de la solicitud. Cuando se limita la velocidad de una solicitud, esta se debe volver a intentar después de un intervalo especificado. Si usa el SDK .NET, la solicitud se reintentará automáticamente después de esperar el período de tiempo especificado en el encabezado retry-after.

## <a name="creating-an-account-built-to-scale"></a>Creación de una cuenta creada para escalar

Puede cambiar el número de unidades de solicitud aprovisionadas en una base de datos en cualquier momento. Por tanto, durante los períodos de gran volumen, puede escalar verticalmente para dar cabida a esas altas demandas y luego reducir el rendimiento aprovisionado durante las horas de menor actividad para reducir los costos.

Cuando crea una cuenta, puede aprovisionar un mínimo de 400 RU/s o un máximo de 250 000 RU/s en el portal. Si necesita más rendimiento, rellene una incidencia en Azure Portal. Se recomienda establecer el rendimiento inicial en 1000 RU/s para casi todas las cuentas, ya que es el valor mínimo en el que la base de datos realizará el escalado automático si necesita más de 10 GB de almacenamiento. Si establece el rendimiento inicial en cualquier valor menor que 1000 RU/s, la base de datos no podrá escalar a más de 10 GB, a menos que vuelva a aprovisionar la base de datos y proporcione una clave de partición. Las claves de partición habilitan la búsqueda rápida de datos en Azure Cosmos DB y permiten que escale automáticamente la base de datos cuando sea necesario. Las claves de partición se describen en la unidad siguiente.

## <a name="summary"></a>Resumen

Ahora ya sabe cómo calcular y examinar el rendimiento para Azure Cosmos DB mediante las unidades de solicitud. Las unidades de solicitud se pueden modificar en cualquier momento y establecerlas en 1000 RU/s cuando se crea una cuenta ayuda a garantizar que la base de datos está lista para escalar más adelante.