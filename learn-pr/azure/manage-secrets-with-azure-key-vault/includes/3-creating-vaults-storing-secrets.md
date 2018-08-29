## <a name="creating-key-vaults-for-your-applications"></a>Creación de almacenes de claves para sus aplicaciones

Un buen procedimiento es dar a cada aplicación un almacén independiente para cada entorno de aplicación que use, como desarrollo, prueba y producción. Puede ser conveniente compartir secretos entre aplicaciones, pero el impacto de que un atacante obtenga acceso de lectura a un almacén aumenta con el número de secretos del almacén.

> [!TIP]
> Si usa los mismos nombres con los secretos de distintos entornos, la única configuración específica del entorno que tiene que cambiar en su aplicación es la dirección URL del almacén.

La creación de un almacén no requiere ninguna configuración inicial. La identidad del usuario se concede automáticamente al conjunto completo de permisos de administración de secretos y puede empezar a agregar secretos inmediatamente. Una vez que tiene un almacén, para agregar y administrar secretos puede usar cualquier interfaz administrativa de Azure, como Azure Portal, la CLI de Azure y Azure PowerShell. Al configurar la aplicación para usar el almacén, deberá asignarle los permisos correctos; esto lo veremos en la siguiente unidad.

## <a name="vault-authentication-and-permissions"></a>Permisos y autenticación de almacén

La API de Azure Key Vault usa Azure Active Directory para autenticar usuarios y aplicaciones. Las directivas de acceso del almacén se basan en *acciones* y se aplican en todo el almacén. Por ejemplo, una aplicación con los permisos **Obtener** (leer valores secretos), **Lista** (enumerar los nombres de todos los secretos) y **Establecer** (crear o actualizar valores secretos) en un almacén puede crear secretos, enumerar todos los nombres de secretos y obtener y establecer todos los valores secretos de ese almacén.

*Todas* las acciones realizadas en un almacén requieren autenticación y autorización, no hay ninguna manera de conceder algún tipo de acceso anónimo.

> [!TIP]
> Al conceder acceso al almacén a desarrolladores y aplicaciones, conceda solo el conjunto mínimo de permisos necesarios. Las restricciones de permisos ayudan a evitar accidentes ocasionados por errores de código y reducen el impacto de credenciales robadas o código malintencionado insertado en la aplicación.

Normalmente, los desarrolladores solo necesitan los permisos **Obtener** y **Lista** para un almacén de entorno de desarrollo. Un desarrollador principal o jefe necesitará permisos completos para el almacén para cambiar y agregar secretos cuando sea necesario. Los permisos completos para los almacenes del entorno de producción se reservan normalmente para el personal de operaciones superior.

Para las aplicaciones, normalmente solo se requieren los permisos **Obtener**. Algunas aplicaciones pueden requerir **Lista** según cómo se implemente la aplicación. La aplicación que implementaremos en el ejercicio de este módulo requiere el permiso **Lista** debido a la técnica que usa para leer los secretos del almacén.

## <a name="exercise"></a>Ejercicio

Dadas todas las dificultades que ha estado teniendo la empresa con los secretos de aplicación, la dirección le ha pedido que cree una pequeña aplicación de inicio para mostrar a los demás desarrolladores el camino adecuado. La aplicación debe demostrar procedimientos recomendados para administrar secretos de la manera más simple y segura posible.

Para empezar, creará un almacén y almacenará un secreto.

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

Cree un grupo de recursos llamado `keyvault-exercise-group` para todos los recursos de este ejercicio. Al final de este módulo, eliminaremos este grupo de recursos para limpiar todo de una vez. Vamos a usar `eastus` como la ubicación para todo lo que hagamos en este ejercicio.

Use el terminal de Azure Cloud Shell de la derecha para ejecutar el siguiente comando de la CLI de Azure. Este comando crea el grupo de recursos en su suscripción.

```azurecli
az group create --name keyvault-exercise-group --location eastus
```

### <a name="create-the-vault-and-store-the-secret-in-it"></a>Creación del almacén y almacenamiento en él del secreto

A continuación, crearemos el almacén y almacenaremos en él el secreto.

**Los nombres de Key Vault deben ser globalmente únicos, por lo que debe elegir un nombre único**. Los nombres de almacén deben tener entre 3 y 24 caracteres y contener solo caracteres alfanuméricos y guiones.

```azurecli
az keyvault create --name <your-unique-vault-name> --resource-group keyvault-exercise-group --location eastus
```

Cuando haya terminado, verá una salida JSON que describe el nuevo almacén.

Ahora, agregue el secreto: nuestro secreto se denominará **SecretPassword** con un valor de **reindeer_flotilla**.

```azurecli
az keyvault secret set --name SecretPassword --value open_sesame --vault-name <your-unique-vault-name>
```

Anote el nombre del almacén &mdash;, pronto lo necesitará de nuevo.

En un momento escribiremos el código de nuestra aplicación, pero primero debemos saber un poco cómo vamos a autenticarla en un almacén.