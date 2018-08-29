## <a name="motivation"></a>Motivación
La CLI de Azure le permite escribir comandos y ejecutarlos de inmediato. Recuerde que es el objetivo general en el ejemplo de desarrollo de software es implementar nuevas compilaciones de una aplicación web para realizar pruebas. El primer paso es crear un grupo de recursos. Recuerde que el objetivo aquí es crear estos recursos mediante una instalación local de la CLI de Azure. 

Esta unidad muestra cómo usar la CLI de Azure para iniciar sesión su suscripción de Azure y crear un nuevo recurso.

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a>¿Qué recursos de Azure se pueden administrar mediante la CLI de Azure?
La CLI de Azure le permite controlar casi todos los aspectos de cualquier recurso de Azure. Puede trabajar con grupos de recursos, almacenamiento, máquinas virtuales, Azure Active Directory (Azure AD), contenedores, aprendizaje automático, etc.

Los comandos de la CLI se estructuran en grupos y subgrupos. Cada grupo representa un servicio suministrado por Azure y los subgrupos dividen comandos para estos servicios en agrupaciones lógicas. Por ejemplo, el grupo de **almacenamiento** contiene subgrupos como **cuenta**, **blob**, **almacenamiento** y **cola**.

Así pues, ¿cómo puede encontrar los comandos específicos que necesita? Una manera es usar **az find**. Por ejemplo, si desea buscar los comandos que pueden ayudarle a administrar un **blob** de almacenamiento, usaría el comando de buscar siguiente:

```bash
az find -q blob
```

Si ya conoce el nombre del comando que desea, el argumento **--help** para ese comando podría resultar más útil. Se obtiene información detallada sobre el comando y, para un grupo de comandos, una lista de los subcomandos disponibles. Por lo tanto, en nuestro ejemplo de almacenamiento, mostramos cómo puede obtener una lista de los comandos y subgrupos para administrar el almacenamiento de blobs:

```bash
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a>Creación de un recurso de Azure
La creación de un nuevo recurso de Azure normalmente consta de tres pasos: la conexión a su suscripción de Azure, la creación del recurso y la comprobación de que se creó correctamente (ver abajo).

![Pasos para crear un recurso mediante la CLI de Azure](../media-drafts/4-create-resources-overview.png)

Cada paso se corresponde con un comando de la CLI de Azure diferente.

### <a name="connect"></a>Conectar
Puesto que está trabajando con una instalación local de la CLI de Azure, tiene que autenticarse para poder ejecutar comandos de Azure usando para ello el comando **login** de la CLI de Azure. 

```bash
az login
```

La CLI de Azure normalmente iniciará el explorador predeterminado para abrir la página de inicio de sesión de Azure. Si esto no funciona, siga las instrucciones de la línea de comandos y escriba un código de autorización en [https://aka.ms/devicelogin](https://aka.ms/devicelogin).

Una vez que la sesión se inicie correctamente, estará conectado a su suscripción de Azure. 

### <a name="create"></a>Crear
A menudo, deberá crear un nuevo grupo de recursos para crear un nuevo servicio de Azure, por lo que vamos a usar grupos de recursos como ejemplo de creación de recursos de Azure desde la CLI.

El comando **group create** de la CLI de Azure crea un grupo de recursos. Debe especificar un nombre y una ubicación. El nombre debe ser único dentro de su suscripción. La ubicación determina dónde se almacenarán los metadatos para el grupo de recursos. Use cadenas como "Oeste de EE. UU.", "Europa del Norte" u "Oeste de la India" para especificar la ubicación; también puede utilizar los equivalentes de una sola palabra, como westus, northeurope o westindia. La sintaxis del núcleo es:

```bash
az group create --name <name> --location <location>
```

### <a name="verify"></a>Verify
Para muchos recursos de Azure, la CLI de Azure proporciona un subcomando **list** que le permite ver los detalles de los recursos. Por ejemplo, el comando **group list** de la CLI de Azure enumera los grupos de recursos de Azure. Esto resulta útil aquí para comprobar si la creación del grupo de recursos se completó correctamente:

```bash
az group list
```

Para obtener una vista más concisa, puede aplicar al resultado el formato de una tabla sencilla:

```bash
az group list --output table
```
