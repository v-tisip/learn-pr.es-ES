Los recursos de informática en la nube se proporciona a través de tres modelos de servicio distintos.

- **Infraestructura como servicio (IaaS)** proporciona la infraestructura informática instantánea que puede aprovisionar y administrar a través de Internet.
- **Plataforma como servicio (PaaS)** proporciona entornos de desarrollo e implementación listos que puede usar para brindar sus propios servicios en la nube.
- **Software como servicio (SaaS)** ofrece aplicaciones a través de Internet como un servicio basado en web.

Al elegir un modelo de servicio, considere qué parte debe ser responsable del recurso informático. Según el escenario, puede decir cuánta responsabilidad de administración compartida desea.

![Modelo de responsabilidad compartida](../media/3-shared-responsibility.png)

## <a name="iaas"></a>IaaS

Infraestructura como servicio es una infraestructura informática que se aprovisiona y administra a través de Internet. IaaS permite escalar rápidamente los recursos para satisfacer la demanda y solo pagar lo que usa. IaaS evita el gasto y la complejidad que implica comprar y administrar sus propios servidores físicos y otra estructura de centro de datos. Cada recurso se ofrece como componente de servicio independiente y *alquile* el recurso siempre que lo necesite. Como resultado, IaaS es muy flexible. Puede aprovisionar una infraestructura común como máquinas virtuales, almacenamiento, subredes virtuales, firewalls y VPN para compilar una solución. No es necesario administrar dispositivos y servidores físicos. Sin embargo, es su responsabilidad administrar directamente la configuración y administración de los componentes. Por ejemplo, configurar firewalls, actualizar sistemas operativos de máquinas virtuales, actualizar DBMS y entornos de tiempo de ejecución.

### <a name="common-scenarios"></a>Escenarios comunes 

Imaginemos que su empresa de atención médica debe ejecutar una versión especial de un software de escritorio. El software solo es compatible en una versión específica de un sistema operativo y solo se requiere un usuario y licencia. Puede crear una máquina virtual con el software necesario. El usuario puede usar Escritorio remoto para conectarse a la máquina virtual y usar el software.

Imaginemos otro escenario. Los equipos de desarrollo necesitan varios entornos de desarrollo únicos. Durante el ciclo de desarrollo, necesitan probar distintas versiones del producto. Los desarrolladores pueden aprovisionar los entornos cuando sea necesario. Cuando ya no se necesita un entorno, se puede eliminar fácilmente.

Entre los otros escenarios comunes se incluyen los siguientes:

**Hospedaje de sitios web:** si quiere mayor control del hospedaje de un sitio web, ejecutar sitios web mediante IaaS puede ser una mejor opción que el hospedaje web tradicional.

**Aplicaciones web:** IaaS proporciona toda la infraestructura para admitir aplicaciones web, incluidos los servidores de aplicaciones, web y almacenamiento, además de los recursos de red. Las organizaciones pueden implementar rápidamente aplicaciones web en IaaS y escalar y reducir la infraestructura de manera vertical cuando no es posible predecir la demanda de la aplicación.

**Almacenamiento, copia de seguridad y recuperación:** la administración de almacenamiento puede ser compleja y requerir una gran inversión de capital y personal capacitado para administrar los datos y cumplir con los requisitos legales y de cumplimiento. IaaS puede ayudar a simplificar el planeamiento, la administración, la demanda impredecible y las necesidades de almacenamiento en constante crecimiento.

**Informática de alto rendimiento:** Si tiene una carga de trabajo que requiere informática de alto rendimiento, puede ejecutarla en la nube para evitar el costo por adelantado del hardware y solo pagar el uso cuando sea necesario. 

**Análisis de macrodatos:** si tiene conjuntos de datos de gran tamaño que contienen patrones, tendencias y asociaciones potencialmente útiles, IaaS puede proporcionar la capacidad de procesamiento para extraer conjuntos de datos con el fin de buscar patrones.

### <a name="advantages"></a>Ventajas

**Elimina los gastos de capital y disminuye el costo continuo:** IaaS evita los gastos iniciales que implica la configuración y administración de un centro de datos in situ, por lo que es una opción económica para empresas emergentes y empresas que prueban ideas nuevas. Tan pronto como se decida lanzar un nuevo producto o iniciativa, la infraestructura informática necesaria puede estar lista en cuestión de minutos u horas, en lugar de días o semanas (e incluso meses) que podría tardar la configuración interna.

**Mejora la continuidad empresarial y la recuperación ante desastres:** alcanzar la alta disponibilidad, continuidad empresarial y recuperación ante desastres es costoso, porque requiere una cantidad importante de tecnología y personal. Pero con el acuerdo de nivel de servicio (SLA) correcto, IaaS puede disminuir este costo y acceder a las aplicaciones y los datos como de costumbre durante un desastre o una interrupción.

**Responda rápidamente a la cambiante situación empresarial:** IaaS permite escalar verticalmente los recursos para dar cabida a los aumentos en la demanda de su aplicación (por ejemplo, durante festividades) y luego volver a reducirlos verticalmente cuando la actividad disminuye para ahorrar dinero. Como no es necesario configurar primero la infraestructura antes de desarrollar y entregar aplicaciones, puede ponerlas a disposición de los usuarios más rápido con IaaS.

**Aumente la estabilidad, confiabilidad y compatibilidad:** con IaaS, no es necesario mantener ni actualizar software ni hardware, ni tampoco solucionar problemas con los equipos. Con el acuerdo adecuado, el proveedor de servicios garantiza una infraestructura confiable y que cumple con los SLA.

## <a name="paas"></a>PaaS

Plataforma como servicio es un entorno completo de desarrollo e implementación en la nube. Con PaaS, puede compilar e implementar todo, desde aplicaciones sencillas basadas en la nube a aplicaciones empresariales sofisticadas y habilitadas para la nube. Puede adquirir los recursos de un proveedor de servicios en la nube con el método pague por uso y acceder a ellos a través de una conexión segura a Internet. Al igual que IaaS, PaaS incluye infraestructura como servidores, almacenamiento y redes. También incluye software intermedio, herramientas de desarrollo y otros servicios. PaaS admite todo el ciclo de vida de una aplicación web: compilación, prueba, implementación, administración y actualización. PaaS elimina la necesidad de administrar las licencias de software, el software intermedio y la infraestructura de los servicios. Es el usuario quien administra las aplicaciones y servicios que desarrolla y el proveedor de servicios en la nube habitualmente administra todo lo demás.

### <a name="common-scenarios"></a>Escenarios comunes

Imaginemos que su empresa de atención médica necesita un sitio web para describir un producto. Los desarrolladores quieren usar PHP. Con PaaS, los desarrolladores tienen la opción de *crear una aplicación web*. Se abstraen los detalles de la infraestructura, como la creación de una máquina virtual, la instalación de un servidor web y la instalación de software intermedio. No es necesario preocuparse de qué sistema operativo se ejecuta ni qué hardware físico se necesita. Los desarrolladores implementan los archivos del sitio web en la nube y el sitio web queda disponible en Internet.

Imaginemos otro escenario. La empresa necesita una base de datos SQL para admitir analistas de datos para un proyecto especial. No tiene infraestructura para responder a la solicitud. Puede aprovisionar rápidamente una instancia de SQL Server en la nube que cumple con las necesidades del proyecto. El analista de datos se puede conectar al servidor. La base de datos SQL Server se proporciona como servicio. Por tanto, no debe preocuparse de las actualizaciones, las revisiones de seguridad ni de optimizar el almacenamiento físico para lecturas y escrituras.

Entre los otros escenarios comunes se incluyen los siguientes:

**Marco de desarrollo:** PaaS ofrece un marco que los desarrolladores pueden usan para desarrollar o personalizar aplicaciones basadas en la nube. De una manera similar a como se crea una macro de Excel, PaaS permite que los desarrolladores creen aplicaciones a través de componentes de software integrados. Se incluyen características de la nube, como escalabilidad, alta disponibilidad y funcionalidad multiinquilino, lo que permite reducir la cantidad de codificación que deben realizar los desarrolladores.

**Análisis o inteligencia empresarial:** las herramientas de análisis que se proporcionan como servicio permiten analizar y extraer datos. Las organizaciones pueden encontrar información y patrones para predecir resultados para mejorar las previsiones, las decisiones relacionadas con el diseño de producto, las rentabilidades de las inversiones y otras decisiones empresariales.

### <a name="advantages"></a>Ventajas

Puesto que ofrece infraestructura como servicio, PaaS tiene ventajas similares a IaaS. Pero sus características adicionales, que incluyen software intermedio, herramientas de desarrollo y otras herramientas de negocios, proporcionan también otras ventajas:

**Menor tiempo de desarrollo:** las herramientas de desarrollo de PaaS pueden disminuir el tiempo de desarrollo de las aplicaciones nuevas. Los desarrolladores pueden usar componentes de aplicación codificados previamente e insertados en la plataforma, como flujo de trabajo, servicios de directorio, características de seguridad y búsqueda. Los componentes de plataforma como servicio pueden brindar al equipo de desarrollo funcionalidades nuevas sin que sea necesario agregar personal con las aptitudes necesarias.

**Desarrollo para varias plataformas:** algunos proveedores de servicio ofrecen opciones de desarrollo para varias plataformas, como equipos de escritorio, dispositivos móviles y exploradores, que permite que desarrollar aplicaciones multiplataforma sea más rápido y sencillo.

**Uso económico de herramientas sofisticadas:** un modelo de pago por uso permite que individuos u organizaciones usen sofisticadas herramientas de análisis e inteligencia empresarial y software de desarrollo sofisticado que no podrían comprar directamente.

**Compatibilidad de equipos de desarrollo distribuidos geográficamente:** como se accede por Internet al entorno de desarrollo, los equipos de desarrollo pueden trabajar conjuntamente en proyectos incluso cuando los miembros de los equipos se encuentran en ubicaciones remotas.

**Administración eficaz del ciclo de vida de la aplicación:** PaaS proporciona todas las funcionalidades necesarias para admitir todo el ciclo de vida de una aplicación web: compilación, prueba, implementación, administración y actualización dentro del mismo entorno integrado.

## <a name="saas"></a>SaaS

Software como servicio permite que los usuarios se conecten y usen aplicaciones basadas en la nube a través de Internet. Algunos ejemplos comunes son el correo electrónico, el calendario y herramientas de oficina como Microsoft Office 365. SaaS proporciona una solución de software completa que compra a través del método pago por uso en un proveedor de servicios en la nube. Lo que hace es *alquilar* el uso de una aplicación para su organización. Los usuarios se conectan al servicio a través de Internet, habitualmente con un explorador web. Toda la infraestructura subyacente, el software intermedio, el software de aplicación y los datos de aplicación se encuentran en el centro de datos del proveedor de servicios. El proveedor de servicios administra el hardware y el software y, como el acuerdo de servicio adecuado, garantizará la disponibilidad y la seguridad de la aplicación y también de los datos. SaaS permite que la organización empiece rápidamente a funcionar con una aplicación a un costo por adelantado mínimo.

Si usó un servicio de correo electrónico basado en web como Outlook, Hotmail o Yahoo! Mail, entonces ya usó un tipo de SaaS. Con estos servicios, el usuario inicia sesión en su cuenta a través de Internet, por lo general mediante un explorador web. El software de correo electrónico se encuentra en la red del proveedor de servicios y los mensajes también se almacenan ahí. Puede acceder al correo electrónico y a los mensajes almacenados desde un explorador web en cualquier equipo o dispositivo conectado a Internet.

### <a name="common-scenarios"></a>Escenarios comunes

Imaginemos que su empresa de atención médica necesita una solución de gestión de relaciones con el cliente (CRM) para su equipo de ventas. El equipo es global. Puede usar un proveedor de CRM de SaaS para implementar rápidamente una solución en el equipo de ventas de la organización.

Para el uso de la organización, puede alquilar aplicaciones de productividad, como correo electrónico, colaboración y calendario, y aplicaciones empresariales sofisticadas, como gestión de relaciones con el cliente (CRM), planeamiento de recursos empresariales (ERP) y administración de documentos. El uso de estas aplicaciones se paga por suscripción o según el nivel de uso.

### <a name="advantages"></a>Ventajas

**Obtención de acceso a aplicaciones sofisticadas:** para proporcionar aplicaciones SaaS a los usuarios, no tiene que comprar, instalar, actualizar ni mantener hardware, software intermedio ni software alguno. Con SaaS, incluso las aplicaciones empresariales sofisticadas, como ERP y CRM, son accesibles para las organizaciones que no cuentan con los recursos para comprar, implementar ni administrar la infraestructura y el software que se necesita.
Solo se paga lo que se usa. También se ahorra dinero, porque el servicio de SaaS escala y reduce verticalmente de manera automática según el nivel de uso.

**Uso de software cliente gratis:** los usuarios pueden ejecutar la mayoría de las aplicaciones SaaS directamente desde el explorador web sin tener que descargar ni instalar software. No necesita comprar ni implementar software cliente para los usuarios.

**Movilización sencilla de la fuerza de trabajo:** los usuarios pueden acceder a datos y aplicaciones de SaaS desde cualquier dispositivo móvil o equipo conectado a Internet. El proveedor de servicios se centra en la entrega del servicio a los dispositivos.

**Acceso a datos de aplicación desde cualquier lugar:** con los datos almacenados en la nube, los usuarios pueden acceder a su información desde cualquier dispositivo móvil o equipo conectado a Internet. Y cuando los datos de aplicación están almacenados en la nube, no se pierden si se produce un error en el equipo o el dispositivo de un usuario.