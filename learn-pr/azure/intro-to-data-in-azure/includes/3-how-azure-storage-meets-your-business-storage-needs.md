Al examinar las ventajas del almacenamiento de Azure, se puede observar que ofrece las mejores opciones para almacenar su portal de aprendizaje. Ahora vamos a explorar los beneficios y opciones disponibles en el almacenamiento Azure en detalle para ver cómo se ajusta a las necesidades de su negocio.

## <a name="how-azure-storage-can-meet-your-business-storage-needs"></a>Cómo el almacenamiento de Azure puede satisfacer las necesidades de almacenamiento de su negocio

El almacenamiento Azure ofrece varias opciones que se adaptan a los tipos específicos de necesidades de almacenamiento de datos.

### <a name="azure-sql-database"></a>Azure SQL Database

**Azure SQL Database** es una sólida base de datos relacional en la nube totalmente administrada que almacena todos los datos. Puede utilizar esta característica para almacenar datos a los que se accede y se actualiza con frecuencia, como información personal y relacionada con el aprendizaje del personal. También puede migrar las bases de datos de SQL Server existentes sin cambiar las aplicaciones.

![AzureSQL](../images/Azure_SQL.png)

### <a name="azure-cosmos-db"></a>Azure Cosmos DB

Azure Cosmos DB es una característica galardonada de Azure y consiste en un servicio de base de datos distribuido globalmente. Es compatible con los datos sin esquema que ofrece la capacidad de crear aplicaciones con una gran capacidad de respuesta y *siempre activadas* para admitir los datos que cambian constantemente. Puede utilizar esta característica para almacenar datos que se actualizan y se mantienen en función de las aportaciones de usuarios de todo el mundo.

![CosmosDB](../images/Azure_cosmos_db.png)

### <a name="azure-blob-storage"></a>Azure Blob Storage

Azure Blob Storage ofrece la posibilidad de trasmitir en streaming archivos grandes de vídeo o audio directamente al explorador del usuario desde cualquier lugar del mundo. Blob Storage también se utiliza para almacenar datos para copia de seguridad y restauración, recuperación ante desastres y archivado. Azure Blob Storage puede almacenar hasta 8 TB de datos para almacenar archivos para máquinas virtuales.

![AzureBlob](../images/Azure_blob.png)

### <a name="azure-data-lake-storage-gen2"></a>Azure Data Lake Storage Gen2

Azure Data Lake Storage le permite realizar análisis sobre el uso de sus datos y preparar informes en consecuencia. Data Lake es un repositorio de gran tamaño que almacena datos estructurados y no estructurados.

**Azure Data Lake Storage Gen2** combina la escalabilidad y rentabilidad del almacenamiento de objetos con la confiabilidad y rendimiento de las funcionalidades del sistema de archivos de macrodatos.

![Data_lake_Store_concept](../images/Data_lake_store_concept.png)

### <a name="azure-files"></a>Azure Files

Azure Files ofrece recursos compartidos de archivos totalmente administrados en la nube. Las aplicaciones que se ejecutan en Azure pueden compartir archivos fácilmente entre máquinas virtuales. Se pueden usar los recursos compartidos de archivos simultáneamente en implementaciones de Windows, Linux y macOS, tanto en la nube como locales.

![Azure_Files](../images/Azure_Files.png)

### <a name="azure-queue"></a>Azure Queue

Azure Queue Storage es un servicio para almacenar grandes cantidades de mensajes a los que puede obtenerse acceso desde cualquier lugar del mundo. Un único mensaje en cola puede tener hasta 64 KB de tamaño y contener millones de mensajes.

Queue se utiliza sobre todo:

- Para crear un trabajo pendiente y pasar mensajes entre los distintos servidores web de Azure.
- Para el equilibrio de carga entre distintos servidores e infraestructura web y administrar las ráfagas de tráfico.
- Para aumentar la resistencia frente a errores de componentes cuando varios usuarios acceden a sus datos al mismo tiempo

![Azure_Queue](../images/Azure_Queue.png)

### <a name="azure-standard-storage"></a>Azure Standard Storage

Las máquinas virtuales de Azure usan los discos para almacenar un sistema operativo, aplicaciones y datos. Azure Standard Storage ofrece compatibilidad de discos confiable y de bajo coste para las máquinas virtuales que ejecutan cargas de trabajo que no son críticas. Con Standard Storage, los datos se almacenan en unidades de disco duro (HDD).

Cuando se trabaja con máquinas virtuales, se pueden usar discos SSD y HDD de almacenamiento estándar y para cargas de trabajo menos críticas, y discos SSD premium para aplicaciones de producción críticas. Los discos de Azure ofrecen durabilidad de nivel empresarial, con una tasa de error anualizada del 0 %.

![Azure_disk](../images/Azure_disks.png)

### <a name="storage-tiers"></a>Niveles de almacenamiento

El almacenamiento de Azure ofrece tres niveles de almacenamiento para el almacenamiento de objetos Blob:

1. **Nivel de almacenamiento de acceso frecuente**: esta capa de almacenamiento de Azure está optimizada para almacenar datos que se consultan con frecuencia. 
1. **Nivel de almacenamiento de acceso esporádico**: esta capa de almacenamiento de Azure está optimizada para almacenar datos a los que se accede con poca frecuencia y al menos durante 30 días.
1. **Nivel de almacenamiento de archivo**: este nivel de almacenamiento de Azure está optimizado para almacenar datos a los que raramente se accede. Estos datos se almacenan durante al menos 180 días con requisitos de latencia flexible. El almacenamiento de archivo de Azure es perfecto para almacenar versiones antiguas de los datos para que pueda recuperarlos cuando y como sea necesario para auditorías u otras actividades poco frecuentes.

![Archive_Tier](../images/Archive_Storage_Tier.png)

### <a name="azure-storage-encryptionreplication"></a>Replicación o cifrado de almacenamiento de Azure

El almacenamiento de Azure proporciona seguridad y alta disponibilidad a los datos mediante funciones de cifrado y replicación.

#### <a name="encryption-for-storage-services"></a>Cifrado de los servicios de almacenamiento

Los siguientes tipos de cifrado están disponibles para los recursos:

1. **Cifrado del servicio Azure Storage (SSE)** en reposo le ayuda a proteger sus datos con el fin de cumplir con los compromisos de cumplimiento y seguridad de su organización. Azure SSE cifra los datos antes de almacenarlos y los descifra antes de recuperar los datos. El cifrado y descifrado son transparentes para el usuario.
1. **Cifrado de cliente**, donde los datos ya están cifrados mediante las bibliotecas de cliente. Azure almacena los datos en estado cifrado en reposo, que se descifra durante la recuperación.

    Esta característica de cifrado garantiza que los datos cumplen los estándares de protección global. Es adecuada para almacenar información confidencial, como datos personales y financieros.

#### <a name="replication-for-storage-availability"></a>Replicación para disponibilidad de almacenamiento

Se configura un tipo de replicación al crear una cuenta de almacenamiento. La característica de replicación garantiza que los datos son duraderos y siempre están disponible. El almacenamiento de Azure permite replicaciones regionales y geográficas para proteger los datos contra desastres naturales y otros desastres locales, como incendios o inundaciones.
