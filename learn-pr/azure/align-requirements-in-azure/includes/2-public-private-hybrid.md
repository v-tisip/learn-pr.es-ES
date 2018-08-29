Imagine que trabaja en una empresa de asistencia sanitaria. Tiene sistemas heredados, sistemas de línea de negocio y planes futuros de nuevos sistemas. Ha oído que el uso de la informática en la nube tiene sus ventajas. ¿Cómo se elige el mejor modelo de implementación para las distintas soluciones de nube pública, privada e híbrida?

## <a name="what-is-cloud-computing"></a>¿Qué es la informática en la nube?

Informática en la nube es el aprovisionamiento de servicios y aplicaciones a petición a través de internet. Los servidores, las aplicaciones, los datos y otros recursos se ofrecen como servicio. 

Para el usuario, se abstraen los detalles de los servicios. Puede aprovisionar los recursos informáticos rápidamente y utilizar el servicio con la mínima administración. No debe considerar la informática en la nube como un centro de datos disponible a través de Internet. La informática en la nube utiliza virtualización, hardware estándar y procesos automatizados para proporcionar una experiencia de usuario de autoservicio a los clientes similar a la de una empresa de servicio público. 

Hay tres modelos de implementación para la informática en la nube: nube pública, nube privada y nube híbrida.

![Modelos de implementación](../media/2-cloud-deployment.png)

## <a name="public-cloud"></a>Nube pública

Las nubes públicas son la manera más común de implementar la informática en la nube. Los servicios se ofrecen a través de Internet pública y están disponibles para cualquiera que quiera comprarlos. Los recursos de nube, como los servidores y el almacenamiento, son propiedad de un proveedor de servicios en la nube de terceros, que los explota y los distribuye a través de Internet. Los servicios pueden ser gratuitos o venderse a petición, lo que permite a los clientes pagar solo por el uso de los ciclos de CPU, almacenamiento o ancho de banda que consumen. Microsoft Azure es un ejemplo de nube pública. 

Imagine que su empresa de asistencia sanitaria necesita un sitio web de inscripción. El sitio tiene que escalarse y tener capacidad de respuesta durante los períodos de demanda máxima de inscripciones varias veces al año. Los clientes tienen acceso al sitio desde ubicaciones globales. Puede usar la nube pública para que se escale verticalmente de forma automática a fin de satisfacer la demanda máxima de inscripciones. Cuando el tráfico del sitio sea bajo, el sitio puede reducirse verticalmente para ahorrar costos. El sitio responde a la demanda máxima y solo se pagan más recursos cuando es necesario. También puede implementar su sitio web en varias regiones geográficas para aumentar la confiabilidad y la capacidad de respuesta.

Durante el desarrollo del sitio web, los desarrolladores quieren crear varios entornos de desarrollo para acelerar el proceso de desarrollo. Los desarrolladores pueden usar la nube pública para aprovisionar rápidamente máquinas virtuales en entornos de espacio aislado para desarrollar una solución. Cuando los desarrolladores ya no necesitan un entorno, puede eliminarlo.

### <a name="why-public-cloud"></a>¿Por qué optar por la nube pública?

Las nubes públicas pueden implementarse con más rapidez que las infraestructuras locales y con una plataforma casi infinitamente escalable. Todos los empleados de una compañía pueden usar la misma aplicación desde cualquier oficina o sucursal con el dispositivo que prefieran siempre que tengan acceso a Internet. 

Ejemplos de por qué usar la nube pública:

- **Consumo de servicio a petición a través de la suscripción o según sea necesario:** El modelo a petición o de suscripción le permite pagar la parte de la CPU, el almacenamiento y otros recursos que utilice o reserve.
- **Sin inversión inicial de hardware:** No es necesario adquirir, administrar y mantener una infraestructura local de hardware y aplicaciones. El proveedor de servicios en la nube es responsable de toda la administración y el mantenimiento del sistema. 
- **Automatización:** Rápido aprovisionamiento de los recursos de infraestructura con un portal web, scripts o automáticamente. 
- **Dispersión geográfica:** Localización de los datos cerca de donde se necesitan sin tener muchos centros de datos propios.
- **Mantenimiento reducido del hardware:** El proveedor de servicios es responsable del mantenimiento del hardware.

## <a name="private-cloud"></a>Nube privada

Una nube privada consiste en recursos informáticos que determinados usuarios de una empresa u organización utilizan en exclusiva. Puede estar ubicada físicamente en el centro de datos del sitio de la organización o estar hospedada por un proveedor de servicios de terceros. El término nube privada no debe considerarse un cambio de nombre de los centros de datos locales tradicionales. Una nube privada usa la infraestructura y los servicios locales para ofrecer ventajas similares a las de la nube pública. Usa una plataforma de abstracción para proporcionar servicios *de nube* tales como clústeres de Kubernetes o un entorno de nube completa, como Azure Stack. La organización es responsable de la compra, la configuración y el mantenimiento del hardware. La comunicación entre los sistemas suele establecerse en la infraestructura de red que la empresa posee y mantiene. Por ejemplo, una red interna privada o una conexión de fibra óptica dedicada entre edificios.

Imagine que trabaja en una empresa de asistencia sanitaria y tiene una aplicación que se encuentra en uso en uno de sus centros de datos. El entorno operativo no se puede replicar en la nube pública. Tiene un nuevo requisito de acceso a los datos en otro de sus centros de datos. La base de datos que contiene los datos de tiene que permanecer en el otro sitio debido al cumplimiento normativo. Este escenario es una nube privada. Tiene dos centros de datos propiedad de la organización. Podría usar una VPN en la nube pública a través de Internet para conectar los centros de datos. Pero, el escenario se consideraría una nube privada debido a que la solución es privada para la organización.

### <a name="why-private-cloud"></a>¿Por qué optar por la nube privada?

Una nube privada puede ofrecer más flexibilidad a una organización. La organización puede personalizar su entorno en la nube para satisfacer las necesidades específicas de la empresa. Puesto que los recursos no se comparten con otros usuarios, es posible tener altos niveles de seguridad y control. Además, las nubes privadas pueden proporcionar un nivel de eficiencia y escalabilidad.

Ejemplos de por qué usar la nube privada:

- **Entorno ya existente:** Entorno operativo existente que no se puede replicar en la nube pública. Una gran inversión en hardware y empleados con experiencia en soluciones. Una organización grande puede transformar sus recursos informáticos en un producto de consumo masivo.
- **Aplicaciones heredadas:** Aplicaciones heredadas críticas para la empresa que no se pueden reubicar físicamente con facilidad.
- **Seguridad y soberanía de los datos:** Las fronteras políticas y los requisitos legales pueden dictar dónde pueden existir físicamente los datos.
- **Certificación y cumplimiento normativo:** Cumplimiento de PCI o HIPAA. Centro de datos local certificado.

## <a name="hybrid-cloud"></a>Nube híbrida

Una nube híbrida es un entorno informático que combina una nube pública y una nube privada permitiendo compartir datos y aplicaciones entre ellas. Cuando las demandas de computación y procesamiento fluctúan, la informática en la nube híbrida ofrece a las empresas la posibilidad de escalar sin problemas su infraestructura local hasta la nube pública para controlar cualquier desbordamiento, sin darle a los centros de datos de terceros acceso la totalidad de los datos. Las organizaciones obtienen la flexibilidad y la potencia de computación de la nube pública para tareas informáticas básicas y no confidenciales, al tiempo que mantienen las aplicaciones y los datos críticos para la empresa en las instalaciones, de forma segura detrás de un firewall de la empresa.

El uso de una nube híbrida contribuye a eliminar la necesidad realizar gastos de capital anticipados para afrontar aumentos de demanda a corto plazo. También cuenta con la flexibilidad necesaria para administrar los recursos que son locales frente a los recursos en la nube. Las compañías solo pagan los recursos que utilizan temporalmente en lugar de tener que comprar, programar y mantener recursos y equipos adicionales que podrían permanecer inactivos durante largos períodos de tiempo. La integración generalmente se realiza a través de una VPN segura entre un proveedor en la nube como Azure y un centro de datos local.

Imagine que trabaja en una empresa de asistencia sanitaria y dispone de una aplicación en la que los clientes tienen acceso a su información médica. Un reglamento exige que los datos permanezcan en una ubicación física. El sitio web del cliente debe responder a sus muchos usuarios globales.  Como solución, la base de datos podría hospedarse en un centro de datos local y el sitio web podría hospedarse en la nube pública. Se usa una VPN entre el centro de datos local y la nube pública. Este escenario podría considerarse una nube híbrida.

### <a name="why-hybrid-cloud"></a>¿Por qué optar por la nube híbrida?

La nube híbrida permite que la organización controle y mantenga una infraestructura privada para los recursos confidenciales. También ofrece la flexibilidad para aprovechar recursos adicionales en la nube pública cuando los necesite. Con la posibilidad de escalar a la nube pública, solo se paga por la potencia de computación adicional cuando sea necesario. Asimismo, puede facilitar la transición a la nube. Se puede migrar gradualmente mediante la introducción paulatina de cargas de trabajo a lo largo del tiempo.

Ejemplos de por qué usar la nube híbrida:

- **Inversión en hardware existente:** Por motivos empresariales hay que usar el entorno operativo y el hardware actuales.
- **Requisitos normativos:** Un reglamento exige que los datos permanezcan en una ubicación física.
- **Entorno operativo único:** La nube pública no puede replicar el entorno operativo heredado.
- **Migración:**: Las cargas de trabajo se mueven a la nube a lo largo del tiempo.
