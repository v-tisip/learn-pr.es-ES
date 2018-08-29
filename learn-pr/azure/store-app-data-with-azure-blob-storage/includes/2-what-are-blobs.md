## <a name="what-are-blobs-and-how-are-they-used"></a>¿Qué son los blobs y cómo se usan?

Los blobs son "archivos para la nube". Las aplicaciones trabajan con los blobs prácticamente de la misma manera que trabajan con los archivos de un disco, para leer y escribir datos. Pero a diferencia de un archivo local, se puede acceder a los blobs desde cualquier lugar con conexión a Internet. 

Azure Blob Storage es *no estructurado*, lo que significa que no hay ninguna restricción sobre los tipos de datos que puede contener. Por ejemplo, un blob puede contener un documento PDF, una imagen JPG, un archivo JSON, contenido de vídeo, etc. Los blobs no están limitados a los formatos de archivo comunes; un blob podría contener gigabytes de datos binarios transmitidos desde un instrumento científico, un mensaje cifrado para otra aplicación o datos en un formato personalizado para una aplicación que esté desarrollando.

Los blobs no suelen ser adecuados para datos estructurados que se deben consultar con frecuencia. Tienen una latencia mayor que la memoria y el disco local, y no tienen las características de indexación que hacen que las bases de datos sean eficaces para la ejecución de consultas. Pero los blobs se suelen usar *junto* a bases de datos para almacenar datos no consultables. Por ejemplo, una aplicación con una base de datos de perfiles de usuario podría almacenar imágenes de los perfiles en blobs. Cada registro de usuario de la base de datos incluiría el nombre o la dirección URL del blob que contiene la imagen del usuario.

Los blobs se usan para almacenar datos de muchas maneras diferentes en todo tipo de aplicaciones y arquitecturas:

* Las aplicaciones que necesitan comunicar grandes cantidades de datos a través de un sistema de mensajería que solo admite mensajes pequeños pueden almacenar los datos en blobs y enviar las direcciones URL de blob en los mensajes.
* El almacenamiento de blobs se puede usar como un sistema de archivos para almacenar y compartir documentos y otros datos personales.
* Los recursos web estáticos como las imágenes se pueden almacenar en blobs y estar disponibles para descarga pública como si fueran archivos en un servidor web.
* Muchos componentes de Azure usan blobs en segundo plano. Por ejemplo, Azure Cloud Shell almacena los archivos y la configuración en blobs, y Azure Virtual Machines usa blobs para el almacenamiento en disco duro.

Algunas aplicaciones crean, actualizan y eliminan blobs de forma constante como parte de su trabajo. En otras se usa un pequeño conjunto de blobs y se modifican con poca frecuencia.

## <a name="storage-accounts-containers-and-metadata"></a>Cuentas de almacenamiento, contenedores y metadatos

En el almacenamiento de blobs, todos los blobs residen dentro de un *contenedor de blobs*. En una cuenta de almacenamiento se puede almacenar un número ilimitado de blobs en un contenedor y un número ilimitado de contenedores. Los contenedores son "planos"; solo pueden almacenar blobs, no otros contenedores.

**LISTA DE TAREAS reemplazar esta imagen por algo mejor**

![Cuentas, contenedores y blobs](../media-drafts/2-storage-container-blob.png)

Los contenedores y los blobs admiten metadatos en forma de pares de cadenas de nombre-valor. Las aplicaciones pueden usar metadatos para lo quiera: una descripción legible del contenido del blob que la aplicación va a mostrar, una cadena que la aplicación usa para determinar cómo procesar los datos del blob, etc.

> [!TIP]
> El almacenamiento de blobs no proporciona ningún mecanismo para buscar u ordenar los blobs por metadatos. Vea la sección Recursos adicionales al final de este módulo para obtener información sobre cómo usar Azure Search para lograr esto.

## <a name="the-blob-storage-api-and-client-libraries"></a>La API y las bibliotecas de cliente de Blob Storage

La API de Blob Storage se basa en REST y es compatible con las bibliotecas de cliente de muchos lenguajes populares. Permite escribir aplicaciones que crean y eliminan blobs y contenedores, cargan y descargan datos de blob, y enumeran los blobs de un contenedor.