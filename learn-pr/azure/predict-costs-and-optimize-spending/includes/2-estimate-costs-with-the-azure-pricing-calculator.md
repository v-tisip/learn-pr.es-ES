Imagine que se le pidió compilar un sistema en Azure y una cotización de lo que podría costar su ejecución durante los próximos 12 meses. Ya sabe que los precios de Azure son completamente transparentes y que se le factura mensualmente solo por los servicios que usa. ¿Cómo puede obtener esa cotización sin implementar ni ejecutar esos servicios o sin calcular manualmente los precios desde las páginas de precios de los servicios de Azure? 

## <a name="introducing-the-azure-pricing-calculator"></a>Introducción a la calculadora de precios de Azure

Para facilitar la cotización por parte de los clientes, Microsoft desarrolló la **calculadora de precios de Azure**. La calculadora de precios de Azure es una herramienta gratis basada en web que permite ingresar servicios de Azure y modificar las propiedades y opciones de los servicios. Genera los costos por servicio y el costo total para tener una cotización completa.

En otra ventana o pestaña del explorador, vaya a la [calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/). En la página de la calculadora de precios, verá tres pestañas:

1. **Products.** (Productos) En esta pestaña llevará a cabo la mayor parte de la actividad. En esta pestaña se muestran todos los servicios de Azure y es donde agregará o quitará servicios para formular la cotización.
2. **Estimates.** (Cotizaciones) Esta pestaña tiene todas las cotizaciones que guardó anteriormente. Revisaremos este proceso en un momento.
3. **FAQ.** (Preguntas más frecuentes) Tal como se indica, esta pestaña contiene respuestas a algunas preguntas frecuentes.

Comencemos con la pestaña **Products** (Productos). En el lado izquierdo podrá ver la lista completa de categorías de servicio. Al hacer clic en cualquiera de las categorías se mostrarán los servicios de esa categoría. También hay un cuadro de búsqueda en el que puede buscar en todos los servicios el servicio que necesita. Si hace clic en el servicio, lo agregará a la cotización. Puede agregar un solo servicio o puede agregar todos los que necesite, incluidos múltiplos del mismo servicio (por ejemplo, varias máquinas virtuales). 

Después de agregar los servicios, querrá conocer el precio. Desplácese hacia la parte inferior de la página para ver los detalles personalizables del servicio que se aplican a los precios. En las máquinas virtuales, por ejemplo, puede seleccionar los detalles como la región, el sistema operativo y el tamaño de instancia, y todos estos factores afectarán el precio de la máquina virtual. Verá un subtotal correspondiente al servicio. Y si se desplaza más abajo, verá el total de todos los servicios que se incluyen en la cotización. Junto con el total, verá botones donde puede exportar, guardar y compartir la cotización.

## <a name="estimate-a-solution"></a>Cotización de una solución

En nuestro escenario original, imaginemos que este sistema se ejecutará en dos máquinas virtuales de Azure y se conectará a una instancia de Azure SQL Database. También queremos tener un firewall de capa 7 para garantizar que tenemos las siguientes funcionalidades de equilibrio de carga mejoradas:

![Diagrama de la arquitectura del sistema](../images/estimate-costs-architecture.png)

Podemos usar la calculadora de precios de Azure para saber cuánto costará la solución y exportar la cotización para compartirla con el equipo.

> [!NOTE]
> Asegúrese de que la calculadora esté limpia y que no se muestre nada en la cotización. Si existe algo en la cotización, haga clic en el icono de la papelera que aparece en cada elemento para restablecer la cotización.

En la pestaña **Products** (Productos) de la calculadora de precios de Azure, haga clic en estos servicios para agregarlos a la cotización:

- Virtual Machines
- Azure SQL Database
- Application Gateway

En la pestaña **Estimates** (Cotizaciones), se pueden configurar los detalles de cada uno de los servicios para obtener un cálculo concreto de los costos. Use la región **Oeste de EE. UU.** para todos los recursos.

* **Virtual Machines.** (Máquinas virtuales) Se trata de una aplicación ASP.NET, por lo que deberemos usar una máquina virtual con **SO Windows**. Esta aplicación no requiere una gran cantidad de potencia informática, por lo que seleccione el tamaño de instancia **D2v3**. Necesitaremos dos máquinas virtuales que se ejecutarán continuamente (730 horas al mes). Para estas máquinas virtuales se va a usar el almacenamiento SSD premium y requerirá un solo disco por máquina virtual de tamaño **E10**, para un total de dos discos. 

* **SQL Database.** Para la base de datos, vamos a aprovisionar un **tipo de base de datos única** a través del **modelo de núcleos virtuales**. Lo que queremos es una base de datos Gen 4 de uso general con cuatro núcleos virtuales. Necesitaremos 32 GB de almacenamiento y se retendrá un promedio de 16 GB de almacenamiento. Nuestra directiva de retención será de ocho semanas, doce meses y cinco años. 

* **Application Gateway.** Para Application Gateway, usaremos el nivel Firewall de aplicaciones web, por lo que tenemos algo de protección para el entorno. Y vamos a ir con solo dos instancias y tamaño mediano, debido a que la carga no será alta. Esperamos procesar 1 TB de datos al mes.

Si busca en la cotización, debería ver un costo resumido correspondiente a cada servicio que agregó y un total para toda la cotización. En este caso, la cotización debería rondar los **USD 1400 al mes**. Puede intentar jugar con algunas de las opciones para ver cómo aumenta o disminuye la cotización.

## <a name="share-and-save-your-estimate"></a>Compartir y guardar la cotización

Ahora tenemos una cotización para la solución. Podemos guardarla, para volver a ella más adelante y hacer los ajustes necesarios, exportarla a Excel para un mayor análisis y compartirla a través de una dirección URL. 

Para exportar la cotización, haga clic en `Export` en la parte inferior de la misma. Esto descargará la cotización en formato de Excel (**.xlsx**) e incluirá todos los servicios que agregó.

Es posible compartir la hoja de cálculo de Excel o hacer clic en el botón `Share` de la calculadora. De este modo, tendrá una dirección URL que podrá usar para compartir la cotización. Cualquier usuario con este vínculo podrá tener acceso a ella, lo que facilita compartirla con el equipo.

Si inició sesión con su cuenta de Azure, puede guardar la cotización y volver a ella más adelante. Haga clic en el botón **Guardar**. Si inició sesión, debería ver una notificación de que se guardó la cotización. Si no inició sesión, verá un mensaje que le indicará que inicie sesión para guardar la cotización. Después de guardarla, desplácese a la parte superior de la página y seleccione la pestaña **Estimates** (Cotizaciones). Ahí verá la cotización. Puede seleccionarla para usarla o eliminarla si ya no la necesita.

## <a name="summary"></a>Resumen

Pudimos llegar a una estimación de costos para un conjunto de servicios de Azure sin gastar dinero. No tuvimos que crear nada y tenemos una cotización que puede compartir completamente y en la que podemos realizar un mayor análisis y modificaciones posteriores a futuro. Puede usar esto no solo para crear cotizaciones para sistemas en los que sabe cuáles son los servicios específicos que planea usar, sino también para comparar cómo los distintos servicios pueden afectar los costos totales. Un ejemplo es Microsoft SQL Server en una máquina virtual frente a Azure SQL Database. Echemos un vistazo a cómo podemos obtener información sobre los costos de servicios que ya tenemos implementados.