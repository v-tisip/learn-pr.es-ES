El minorista en línea para el que trabaja planea expandirse a una nueva área geográfica en un futuro próximo. Esta expansión aumentará su base de clientes y el volumen de transacciones. Debe asegurarse de que la base de datos está equipada para controlar la expansión cuando sea necesario.

Tener una estrategia de partición garantiza que, cuando la base de datos necesite crecer, pueda hacerlo con facilidad y continuar con la realización de consultas y transacciones eficaces.

## <a name="what-is-a-partition-strategy"></a>¿Qué es una estrategia con particiones?

Si continúa agregando nuevos datos a un único servidor o a una sola partición, al final se quedará sin espacio. Para prepararse para esto, necesita una estrategia de particiones para **escalar horizontalmente** en lugar de verticalmente. La escalabilidad horizontal permite agregar más particiones a la base de datos a medida que la aplicación las necesita.

La estrategia de particiones y escalabilidad horizontal de Azure Cosmos DB se controla con la clave de partición, que es un valor que se define al crear una colección. Una vez establecida la clave de partición, no se puede cambiar sin volver a crear la colección, por lo que la selección de la clave de partición correcta es una decisión importante que tomar al principio del proceso de desarrollo.  

En esta unidad, obtendrá información sobre cómo elegir una clave de partición que sea adecuada para su escenario y podrá beneficiarse del escalado automático que Azure Cosmos DB puede hacer por usted.

## <a name="partition-key-basics"></a>Aspectos básicos de la clave de partición

Una clave de partición representan un valor en la base de datos que se consulta con frecuencia. Por tanto, en un escenario minorista en línea, es una buena opción usar los valores de Id. de usuario o Id. de producto como la clave de partición. El valor de Id. de usuario es una buena elección, ya que la aplicación con frecuencia necesita recuperar la configuración de personalización, el carro de la compra, el historial de pedidos y la información del perfil del usuario, entre otros datos. El valor de Id. de producto también es una buena opción, ya que la aplicación necesita consultar los niveles de inventario, los costos de envío, las opciones de color, las ubicaciones del almacenamiento y mucho más.

Una clave de partición debe tener como objetivo la distribución de operaciones en la base de datos. Desea distribuir las solicitudes con la intención de evitar particiones activas. Una partición activa es una única partición que recibe muchas más solicitudes que otras, lo que puede producir un cuello de botella del rendimiento. Por ejemplo, para la aplicación de comercio electrónico, la hora actual sería una opción poco conveniente para la clave de partición, ya que todos los datos entrantes irían a una única clave de partición. Resultarían más convenientes los valores de Id. de usuario o Id. de producto, ya que todos los usuarios de su sitio probablemente podrían agregar y actualizar su carro de la compra o la información del perfil prácticamente con la misma frecuencia, lo que distribuye las lecturas y escrituras por todas las particiones de usuario. Asimismo, las actualizaciones de los datos de productos probablemente también se distribuirán de manera más o menos uniforme, por lo que el valor de Id. de producto resultaría una buena elección como clave de partición.

Cada clave de partición tiene un espacio de almacenamiento máximo de 10 GB, que es el tamaño de una partición física en Azure Cosmos DB. Por tanto, si el registro único del Id. de usuario o del Id. de producto va a ser mayor que 10 GB, piense en usar una clave compuesta, para que cada registro sea más pequeño. Un ejemplo de clave compuesta sería UserID-date, que presentaría un aspecto como CustomerName-08072018. Este enfoque de la clave compuesta permitiría crear una partición para cada día que un usuario visite el sitio.

## <a name="best-practices"></a>Procedimientos recomendados

Cuando vaya a tratar de determinar la clave de partición correcta y la solución no sea obvia, tenga en cuenta las siguientes sugerencias.

* No tenga miedo de tener demasiadas claves de partición. Mientras más claves de partición tenga, mayor escalabilidad tendrá.

* Para determinar la mejor clave de partición para una carga de trabajo de lectura intensiva, revise las tres o cinco primeras consultas que planea usar. El valor incluido con más frecuencia en la cláusula WHERE es un buen candidato para la clave de partición.

* Para cargas de trabajo de escritura intensiva, deberá conocer las necesidades transaccionales de la carga de trabajo, porque la clave de partición es el ámbito de las transacciones de varios documentos.
