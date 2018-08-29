Antes de empezar, vamos a revisar la sintaxis de la herramienta CLI de Azure. Si ha tomado los **servicios de Azure de control con el módulo de la CLI de Azure**, sabrá que los comandos de la CLI de Azure adoptan la forma de:

```azurecli
az [command] [subcommand] [--parameter --parameter]
```

`[command]` identifica un área específica de Azure que desea controlar. Por ejemplo, puede administrar la información de suscripción con el comando `account` o bases de datos SQL con el comando `sql`. `[subcommand]` y `[--parameters]` después dependen del comando con el que está trabajando. 

Puede ver una lista de parámetros, subcomandos y parámetros escribiendo un comando parcial. Por ejemplo, si escribe `az` en la línea de comandos le proporcionará la pantalla de ayuda de nivel superior, mientras que si escribe `az vm` le proporcionará todos los subcomandos para máquinas virtuales. Este enfoque puede ser una excelente manera de explorar la herramienta CLI de Azure.

> [!NOTE]
> Vamos a usar Azure Cloud Shell hospedado en explorador para que funcione con la CLI de Azure. Si prefiere trabajar desde el equipo local, todos los comandos que trataremos también se pueden ejecutar desde la línea de comandos [instalando la CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).

## <a name="log-in-to-azure"></a>Inicio de sesión en Azure

Lo primero que hará cuando se trabaje con la CLI de Azure es iniciar sesión en su cuenta de Azure. Esto se hace en el comando `login`. Si usa Cloud Shell, habrá un botón para iniciar sesión en Azure.

```azurecli
az login
```

Este comando iniciará una ventana de explorador y le permitirá seleccionar la cuenta de Microsoft que desea usar.

## <a name="working-with-subscriptions"></a>Trabajo con suscripciones

En este módulo, vamos a trabajar en una suscripción temporal creada como un área de juegos, pero normalmente usará una suscripción de su propia cuenta. Si tiene más de una suscripción, puede obtener una lista claramente formateada de las suscripciones mediante la instrucción `az account list --output table`.

```
Name                                  CloudName    SubscriptionId                        State    IsDefault
------------------------------------  -----------  ------------------------------------  -------  -----------
Contoso Legacy Resources              AzureCloud   abc13b0c-d2c4-64b2-9ac5-2f4cb819b752  Enabled  True
Visual Studio Enterprise              AzureCloud   233aebce-23c2-4572-c056-c029449e93ed  Enabled  False
```

Tenga en cuenta que el comando también identifica la suscripción _predeterminada_ donde se aplicarán todos los comandos. Si prefiere trabajar en una suscripción diferente, puede usar el comando `az account set --subscription "[name]"`. Por ejemplo, podríamos establecer nuestra suscripción actual para que sea `Visual Studio Enterprise` en la lista anterior mediante el comando siguiente:

```azurecli
az account set --subscription "Visual Studio Enterprise"
```