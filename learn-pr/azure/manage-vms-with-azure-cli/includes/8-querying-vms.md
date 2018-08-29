Ahora que se creó una máquina virtual, podemos obtener información sobre ella a través de otros comandos.

Comencemos con `vm list`.

```azurecli
az vm list
```

Este comando devolverá _todas_ las máquinas virtuales definidas en esta suscripción. La salida se puede filtrar a un grupo de recursos específico mediante el parámetro `--resource-group`. 

## <a name="output-types"></a>Tipos de salida
Tenga en cuenta que el tipo de respuesta predeterminada para todos los comandos que hemos realizado hasta ahora es JSON. Esto es fantástico para los scripts, pero para la mayoría de las personas es más difícil de leer. Puede cambiar el estilo de salida de todas las respuestas a través de la marca `--output`. Por ejemplo, pruebe este comando en Azure Cloud Shell para ver el estilo de salida distinto.

```azurecli
az vm list --output table
```

Junto con `table`, puede especificar `json` (el valor predeterminado), `jsonc` (JSON coloreado) o `tsv` (valores separados por tablas). Pruebe algunas variaciones con el comando anterior para ver la diferencia.

## <a name="getting-the-ip-address"></a>Obtención de la dirección IP

Otro comando útil es `vm list-ip-addresses`, que enumerará las direcciones IP públicas y privadas de una máquina virtual. Si cambian o no las capturó durante la creación, puede recuperarlas en cualquier momento.

```azurecli
az vm list-ip-addresses -n SampleVM -o table
```

Esto devuelve:

```
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM          168.61.54.62         10.0.0.4
```

> [!NOTE]
> Tenga en cuenta que estamos usando una sintaxis abreviada para la marca `--output` como `-o`. La mayoría de los parámetros de los comandos de la CLI de Azure se pueden abreviar como un solo guion y una letra. Por ejemplo, `--name` se puede abreviar como `-n` y `--resource-group` como `-g`. Esto resulta útil para escribir, pero en los scripts se recomienda usar el nombre completo de la opción para mayor claridad. Consulte la documentación para más detalles sobre cada comando.

## <a name="getting-vm-details"></a>Obtención de detalles de VM

Es posible obtener información más detallada sobre una máquina virtual específica por nombre o identificador con el comando `vm show`.

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM
```

Esto devolverá un bloque JSON bastante grande con todo tipo de información sobre la máquina virtual, incluidos los dispositivos de almacenamiento conectado, las interfaces de red y todos los identificadores de objeto para los recursos a los que está conectada la máquina virtual. Nuevamente, podríamos cambiar a un formato de tabla, pero eso omite prácticamente todos los datos de interés. En su lugar, podemos volver a un lenguaje de consulta integrada de JSON llamado [JMESPath](http://jmespath.org/).

## <a name="adding-filters-to-queries-with-jmespath"></a>Incorporación de filtros a consultas con JMESPath

JMESPath es un lenguaje de consulta estándar del sector creado en torno a los objetos JSON. La consulta más sencilla consiste en especificar un _identificador_ que selecciona una clave en el objeto JSON.

Por ejemplo, dado el objeto:

```json
{
  "people": [
    {
      "name": "Fred",
      "age": 28
    },
    {
      "name": "Barney",
      "age": 25
    },
    {
      "name": "Wilma",
      "age": 27
    }
  ]
}
```

Podemos usar la consulta `people` para devolver la matriz de valores para la matriz `people`. Si solo queremos _una_ de las personas, podemos usar un indexador. Por ejemplo, `people[1]` devolvería:

```json
{
    "name": "Barney",
    "age": 25
}
```

También podemos agregar calificadores específicos que devolverían solo los objetos `Fred` y `Wilma`. 

```json
[
  {
    "name": "Fred",
    "age": 28
  },
  {
    "name": "Wilma",
    "age": 27
  }
]
```

Por último, los resultados se pueden restringir si se agrega una instrucción select: `people[?age > '25'].[name]` que devuelve solo los nombres:

```json
[
  [
    "Fred"
  ],
  [
    "Wilma"
  ]
]
```

JMESQuery tiene varias otras características de consulta interesantes. Cuando tenga tiempo, consulte el [tutorial en línea](http://jmespath.org/tutorial.html) disponible en el sitio [JMESPath.org](http://jmespath.org/).

## <a name="filtering-our-azure-cli-queries"></a>Filtrado de consultas de la CLI de Azure

Con un conocimiento básico de las consultas JMES, podemos agregar filtros a los datos devueltos por las consultas, como el comando `vm show`. Por ejemplo, podemos recuperar el nombre de usuario del administrador:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "osProfile.adminUsername"
```

Podemos obtener el tamaño asignado a la máquina virtual:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query hardwareProfile.vmSize
```

O bien, para recuperar todos los identificadores para las interfaces de red, puede usar la consulta:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id"
```

Esta técnica de consulta funcionará con cualquier comando de CLI de Azure y se puede usar para extraer elementos específicos de datos en la línea de comandos. También es útil para los scripts. Por ejemplo, puede extraer un valor de la cuenta de Azure y almacenarlo en una variable de entorno o script. Si decide usarla este modo, es un marcador útil para agregar el parámetro `--output tsv` (que se puede abreviar como `-o tsv`). Esto devolverá los resultados en valores separados por tabulaciones que solo incluyan los valores de datos con separadores de tabulación.

Como ejemplo,

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id" -o tsv
```

devuelve el texto: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`
