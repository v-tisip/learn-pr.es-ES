Una solicitud HTTP es una operación común en la mayoría de las plataformas y dispositivos. Tanto si es una solicitud para buscar una palabra en un diccionario o para obtener la información meteorológica local, todo el tiempo enviamos solicitudes HTTP. Azure Functions nos permite crear rápidamente un fragmento de lógica que se ejecutará cuando se reciba una solicitud HTTP.  

Aquí, aprenderá a crear e invocar una función de Azure mediante un desencadenador de HTTP. También analizará algunas de las opciones de personalización que están disponibles.

## <a name="what-is-an-http-trigger"></a>¿Qué es un desencadenador de HTTP?

Un desencadenador de HTTP es un desencadenador que ejecuta una función cuando recibe una solicitud HTTP. Los desencadenadores de HTTP tienen muchas funcionalidades y personalizaciones, como por ejemplo:

- Proporcionan acceso autorizado mediante el suministro de claves.
- Restringen qué verbos HTTP se admiten.
- Devuelven datos al llamador.
- Reciben datos a través de parámetros de cadena de consulta o el cuerpo de solicitud.
- Admiten plantillas de ruta de dirección URL para modificar la dirección URL.

Cuando crea un desencadenador de HTTP, selecciona un lenguaje de programación, proporciona un nombre de desencadenador y selecciona un nivel de autorización.

## <a name="what-is-an-http-trigger-authorization-level"></a>¿Qué es un nivel de autorización de desencadenador de HTTP?

Un nivel de autorización de desencadenador de HTTP es una marca que indica si una solicitud HTTP entrante necesita una clave de API por motivos de autenticación.

Hay tres niveles de autorización:

- Función
- Anónimas
- Administración

Los niveles **Función** y **Administración** se basan en "claves". Para enviar una solicitud HTTP, debe proporcionar una clave para la autenticación. Hay dos tipos de claves: *función* y *host*. Las diferencias entre las dos claves son su ámbito. Las claves de *Función* son específicas de una función. Las claves de *Host* se aplican a todas las funciones dentro de toda la aplicación de Azure Functions. Si se establece el nivel de autorización en **Función**, se puede usar un clave de *función* o una clave de *host*. Si el nivel de autorización se establece en **Administración**, debe proporcionar una clave de *host*.

El nivel **Anónimo** significa que no se requiere autenticación. En el ejercicio, usamos este nivel.

## <a name="how-to-create-an-http-trigger"></a>Cómo crear un desencadenador de HTTP

Al igual que un desencadenador de temporizador, puede crear un desencadenador de HTTP mediante Azure Portal. Dentro de la función de Azure, seleccionará **Desencadenador de HTTP** en la lista de tipos de desencadenadores predefinidos. A continuación, escriba la lógica que quiera ejecutar y realice cualquier personalización, como restringir el uso de ciertos verbos HTTP. 

Un valor que es importante comprender es **Nombre de parámetro de solicitud**. Esta configuración es una cadena que representa el nombre del parámetro que contiene la información sobre una solicitud HTTP entrante. De forma predeterminada, el nombre del parámetro es *req*.

## <a name="how-to-invoke-an-http-trigger"></a>Cómo invocar un desencadenador de HTTP

Para invocar un desencadenador de HTTP, envíe una solicitud HTTP a la dirección URL de su función. Para obtener esta dirección URL, vaya a la página de código de la función y seleccione el vínculo **Obtener la dirección URL de la función**.

![Busque la dirección URL de la función](../media/5-function-url.png)

Una vez que tiene la dirección URL de la función, puede enviar solicitudes HTTP. Si la función recibe datos, recuerde que puede usar parámetros de cadena de consulta o proporcionar los datos a través del cuerpo de solicitud.

## <a name="summary"></a>Resumen

Un desencadenador de HTTP invoca una función de Azure cuando recibe una solicitud HTTP para su dirección URL de función. Los desencadenadores de HTTP permiten recibir datos y devolverlos al llamador.
