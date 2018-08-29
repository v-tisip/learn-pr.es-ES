Azure Key Vault usa **Azure Active Directory** para autenticar usuarios y aplicaciones que intentan acceder a un almacén. Para conceder acceso a la aplicación web al almacén, primero necesitamos registrar la aplicación en Azure Active Directory. El registro crea una identidad para la aplicación. Una vez que tenemos una identidad, podemos asignarle permisos para el almacén.

Las aplicaciones y los usuarios se autentican en Key Vault con un token de autenticación de Azure Active Directory. Obtener un token de Azure Active Directory requiere un secreto o certificado, porque cualquier persona que disponga de un token podría usar la identidad de la aplicación para acceder a todos los secretos del almacén.

Los secretos de la aplicación están protegidos en el almacén, pero necesitamos mantener un secreto o certificado fuera del almacén para poder acceder a ellos. Este problema se llama *problema de arranque*, y Azure tiene una solución para él.

## <a name="managed-service-identity"></a>Identidad de servicio administrada

*Managed Service Identity* (MSI) es una característica de Azure App Service que la aplicación puede usar para acceder a Key Vault y otros servicios de Azure sin tener que administrar ni un solo secreto. El uso de MSI es más fácil y seguro que administrar un secreto por su cuenta.

Al habilitar MSI, Azure activa un servicio REST de concesión de token independiente para que la aplicación lo use específicamente. Cuando la aplicación solicita un token desde el servicio de token de MSI, el servicio se pone en contacto con Azure Active Directory para obtener un token para la identidad de MSI y lo devuelve a la aplicación para usarlo con Key Vault. La parte más importante de este flujo de trabajo es la manera en que la aplicación se autentica en el servicio de token de MSI &mdash;; en lugar de requerir un secreto o certificado que necesita para administrar la configuración, la aplicación usa un secreto que Azure inserta de forma segura en su variables de entorno cuando se inicia. No es necesario administrar ni almacenar el valor de este secreto en ningún lugar. Nada fuera de la aplicación puede acceder a este secreto ni al punto de conexión del servicio de token de MSI.

MSI también registra automáticamente la aplicación en Azure Active Directory y eliminará el registro si deshabilita MSI o elimina la aplicación.

MSI está disponible en todas las ediciones de Azure Active Directory, incluida la edición gratuita incluida con una suscripción de Azure. Su uso en App Service no supone ningún costo adicional ni ninguna configuración y, además, se puede habilitar o deshabilitar en una aplicación en cualquier momento.

> [!NOTE]
> MSI no se admite actualmente para aplicaciones web con Linux o Container.

Para habilitar MSI se requiere solo un único comando de la CLI de Azure sin ninguna configuración. Lo haremos en la unidad 5 cuando configuremos una aplicación de App Service y la implementemos en Azure. No obstante, antes de eso, vamos a aplicar nuestros conocimientos sobre MSI para escribir el código para la aplicación.