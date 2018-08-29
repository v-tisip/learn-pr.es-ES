Al diseñar una aplicación que necesita para almacenar los datos, es importante pensar en cómo la aplicación va a organizar y almacenar datos en blobs, contenedores y cuentas de almacenamiento.

## <a name="storage-accounts"></a>Cuentas de almacenamiento

Una única cuenta de almacenamiento es lo suficientemente flexible como para organizar los blobs como desee, pero debe usar cuentas de almacenamiento adicionales según sea necesario para separar los costos y controlar el acceso a los datos de forma lógica.

## <a name="containers-and-blobs"></a>Contenedores y blobs

La naturaleza de la aplicación y los datos que almacena deben impulsar la estrategia de nomenclatura y organización de contenedores y blobs.

Las aplicaciones con blobs como parte de un esquema de almacenamiento que incluye una base de datos a menudo no necesitan depender en gran medida de la organización, la nomenclatura o los metadatos para indicar algo sobre sus datos. Normalmente, esas aplicaciones utilizan identificadores como GUID como los nombres de blob y hacen referencia a estos identificadores en los registros de la base de datos. La aplicación usará la base de datos para determinar dónde se almacenan los blobs y el tipo de datos que contienen.

Otras aplicaciones pueden usar Azure Blob Storage más como algo parecido a un sistema de archivos personales, donde se usan los nombres de contenedor y blob para indicar el significado y la estructura. Los nombres de blob en estos tipos de aplicaciones a menudo se parecerán a los nombres de archivo tradicionales e incluirán extensiones de nombres de archivo como `.jpg` para indicar qué tipos de datos contienen. Usarán directorios virtuales (ver abajo) para organizar los blobs y usarán con frecuencia las etiquetas de metadatos para almacenar información sobre los blobs y contenedores.

Hay algunos conceptos clave que hay que considerar al decidir cómo organizar y almacenar blobs y contenedores.

### <a name="naming-limitations"></a>Limitaciones sobre nomenclatura

Los nombres de contenedores y blobs deben seguir una serie de reglas, como las limitaciones de longitud y las restricciones de caracteres. Vea la sección Recursos adicionales al final de este módulo para obtener información más específica sobre las reglas de nomenclatura.

### <a name="public-access-and-containers-as-security-boundaries"></a>Acceso público y contenedores como límites de seguridad

De forma predeterminada, todos los blobs requieren autenticación para acceder. Sin embargo, los contenedores individuales pueden configurarse para permitir la descarga pública de sus blobs sin autenticación. Esta característica es compatible con muchos de los casos de uso, como el hospedaje de recursos de sitio web estáticos y el uso compartido de archivos. Esto se debe a que la descarga de contenido de los blobs funciona de la misma forma que la lectura de cualquier otro tipo de datos en la Web: solo debe apuntar al explorador o a cualquier elemento que pueda realizar una solicitud GET a la dirección URL del blob.

**Imagen del contenedor público de TAREAS PENDIENTES, que muestra la dirección URL de acceso directo**

Habilitar el acceso público es importante para la escalabilidad, porque los datos descargados directamente de Blob Storage no generan ningún tráfico en la aplicación del lado servidor. Incluso si no usa de inmediato el acceso público o si usa una base de datos para controlar el acceso a los datos mediante su aplicación, planee el uso de contenedores independientes para los datos que desea que estén disponibles públicamente.

> [!CAUTION]
> Los blobs de un contenedor configurado con acceso público los puede descargar cualquier persona que conozca sus direcciones URL de almacenamiento sin ningún tipo de autenticación o auditoría. Nunca coloque datos de blob en un contenedor público si no desea compartirlos públicamente.

Además del acceso público, Azure tiene una característica de firma de acceso compartido que permite el control de permisos más específico en los contenedores. El control de acceso de precisión permite escenarios que mejoran aún más la escalabilidad, por lo que pensar en contenedores como límites de seguridad en general es una guía útil.

### <a name="blob-name-prefixes-virtual-directories"></a>Prefijos de nombres de blob (directorios virtuales)

Técnicamente, los contenedores son "planos" y no admiten cualquier tipo de anidamiento o jerarquía. Sin embargo, si asigna a los blobs nombres jerárquicos que se parecen a las rutas de acceso a archivos (como `finance/budgets/2017/q1.xls`), la operación de enumeración de la API puede filtrar los resultados de los prefijos específicos. Esto le permite navegar por la lista como si se tratara de un sistema jerárquico de archivos y carpetas.

Esta característica se denomina a menudo *directorios virtuales* porque algunas herramientas y bibliotecas cliente la usan para visualizar y acceder a Blob Storage como si fuese un sistema de archivos. La navegación en cada carpeta desencadena una llamada independiente para enumerar los blobs de dicha carpeta.

**Imagen de TAREAS PENDIENTES del explorador de almacenamiento o el portal con carpetas**

El uso de nombres similares a los nombres de archivo para los blobs es una técnica común para organizar datos de blob completos y navegar por ellos.

### <a name="blob-types"></a>Tipos de blobs

Existen tres tipos diferentes de blobs en los que puede almacenar los datos:

- Los **blobs en bloques** están compuestos por bloques de diferentes tamaños que se pueden cargar y descargar de forma independiente y en paralelo. La escritura en un blob en bloque conlleva cargar los datos en bloques y confirmarlos en el blob &mdash;; las bibliotecas cliente lo harán automáticamente.
- Los **blobs en anexos** son blobs en bloque especializados que solo permiten anexar datos nuevos (no actualizar ni eliminar los datos existentes), pero resultan muy eficaces para ello. Los blobs en anexos son ideales para escenarios como el almacenamiento de registros o el streaming de datos.
- Los **blobs en páginas** están diseñados para escenarios que conllevan lecturas y escrituras de acceso aleatorio. Los blobs en páginas se usan para almacenar archivos del disco duro virtual (VHD) utilizados por Azure Virtual Machines, pero resultan ideales para cualquier escenario que conlleve el acceso aleatorio.

Los blobs en bloques son la mejor opción para la mayoría de los escenarios que no requieren específicamente blobs en anexos o en páginas.