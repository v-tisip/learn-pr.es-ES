Azure Key Vault es un *almacén de secretos*: un servicio centralizado en la nube para almacenar secretos de aplicación. Key Vault ayuda a evitar los escenarios anteriores al mantener los secretos de aplicación en una sola ubicación central y proporcionar acceso seguro, control de permisos y registro de acceso.

Un almacén individual es un recurso de Azure con su propia directiva de seguridad y configuración que se puede crear con cualquiera de las herramientas de administración de Azure estándar, como Azure Portal o la CLI de Azure. La administración del almacén y el acceso al secreto se logar a través de una API de REST. Cada almacén tiene una dirección URL única donde se hospeda su API.

> [!IMPORTANT]
> **Key Vault está diseñado para almacenar secretos de configuración de las aplicaciones de servidor.** No tiene por objeto almacenar datos que pertenezcan a los usuarios de la aplicación ni debe utilizarse en la parte del lado cliente de una aplicación. Esto se refleja en sus características de rendimiento, la API y el modelo de costos.
>
> Los datos de usuario deben almacenarse en otro lugar, como una instancia de Azure SQL Database con Cifrado de datos transparente, o una cuenta de almacenamiento con Storage Service Encryption. Los secretos que utiliza la aplicación para tener acceso a estos almacenes pueden mantenerse en Key Vault.

## <a name="what-is-a-secret-in-key-vault"></a>¿Qué es un secreto en Key Vault?

En Key Vault, un secreto es un par nombre-valor de cadenas. Los nombres de secreto deben tener entre 1 y 127 caracteres, contener solo caracteres alfanuméricos y guiones, y ser únicos en un almacén. Un valor de secreto puede ser cualquier cadena UTF-8 de hasta 25 KB de tamaño.

> [!TIP]
> Los nombres de secreto no tienen que considerarse especialmente secretos en sí mismos. Puede almacenarlos en la configuración de la aplicación si la implementación lo requiere. Lo mismo puede decirse de las direcciones URL y los nombres de almacén.

> [!NOTE]
> Key Vault admite otros dos tipos de secretos además de las cadenas, &mdash; *claves* y *certificados* &mdash;, y ofrece la funcionalidad útil específica para sus casos de uso. Este módulo no cubre estas características y se centra en cadenas secretas como contraseñas y cadenas de conexión.
