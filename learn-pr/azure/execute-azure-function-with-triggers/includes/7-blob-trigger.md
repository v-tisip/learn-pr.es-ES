Imagine que es un fotógrafo y tiene un sitio web donde se muestran las imágenes del día. Al estar ocupado, no tiene una programación de carga coherente, pero desea notificar a los aficionados cuando carga una imagen. Decide crear una función de Azure para enviar automáticamente un tweet cada vez que carga una imagen en el contenedor de blobs de Azure Storage.

En este caso, aprenderá a crear un desencadenador de blob y le indicará que supervise una ubicación específica en el contenedor de blobs de Azure Storage.

## <a name="what-is-azure-storage"></a>¿Qué es Azure Storage?

Azure Storage es la solución de almacenamiento en la nube de Microsoft que admite todos los tipos de datos, lo que incluye blobs, colas y NoSQL. El objetivo de Azure Storage es proporcionar almacenamiento de datos, es decir:

- Alta disponibilidad
- Protección
- Escalable
- Administrado

No nos vamos a centrar en Azure Storage demasiado. En su lugar, lo usamos para crear los blobs que desencadenarán nuestra función para que se ejecute.

## <a name="what-is-azure-blob-storage"></a>¿Qué es Azure Blob Storage?

Azure Blob Storage es una solución de almacenamiento de objetos que se ha diseñado para almacenar grandes cantidades de datos no estructurados. 

Por ejemplo, Azure Blob Storage es ideal para hace cosas como:

- Almacenar archivos.
- Servir archivos.
- Streaming de audio y vídeo.
- Registrar datos.

Hay tres tipos de blobs: **blobs en bloques**, **blobs en anexos** y **blobs en páginas**. Los blobs en bloques son el tipo más frecuente. Le permiten almacenar datos binarios o de texto de forma eficaz. Los blobs en anexos son como los blobs en bloques, pero están diseñados más para operaciones de anexión como la creación de un archivo de registro que se está actualizando constantemente. Por último, los blobs en páginas están compuestos de páginas y se han diseñado para las operaciones aleatorias y frecuentes de lectura y escritura.

## <a name="what-is-a-blob-trigger"></a>¿Qué es un desencadenador de blobs?

Un desencadenador de blobs es un desencadenador que ejecuta una función cuando un archivo se carga o se actualiza en Azure Blob Storage. Para crear un desencadenador de blobs, cree una cuenta de Azure Storage y proporcione una ubicación que el desencadenador supervisa.

## <a name="how-to-create-a-blob-trigger"></a>Creación de un desencadenador de blobs

Al igual que los otros desencadenadores que hemos visto hasta ahora, crearemos un desencadenador de blobs en Azure Portal. Dentro de la función de Azure, seleccione **Desencadenador de blob** en la lista de tipos de desencadenadores predefinidos. A continuación, escriba la lógica que se ejecutará cuando se crea o actualiza un blob.

Una de las configuraciones que desea examinar es **Ruta de acceso**. **Ruta de acceso** indica al desencadenador de blobs dónde debe supervisar para comprobar si un blob se cargó o actualizó. De manera predeterminada, el valor de **Ruta de acceso** es: 

> samples-workitems/{name}

Vamos a desglosar este concepto en dos partes: *samples-workitems* y *{name}*. La primera parte, *samples-workitems*, representa el contenedor de blobs que el desencadenador supervisa. La segunda parte, *{name}*, significa que todos los tipos de archivo harán que el desencadenador invoque la función. Se invoca la función porque no hay ningún filtro. Por ejemplo, podría hacerse que el desencadenador invocara a la función solo cuando se agrega un archivo PNG utilizando una sintaxis como:

> samples-workitems/{name}.png

La última parte significativa de información con este concepto es el texto *name*. *name* representa un parámetro en la función de Azure que recibe el nombre del archivo agregado. Por ejemplo, si carga un archivo denominado *resume.txt*, mi función de Azure recibe ese valor como una cadena a través de un parámetro llamado *name*.

## <a name="summary"></a>Resumen

Un desencadenador de blobs invoca una función de Azure cuando ve actividad en una ubicación específica en la cuenta de blobs de Azure Storage. Establezca la ubicación para supervisar modificando el valor de **Ruta de acceso** en Azure Portal.
