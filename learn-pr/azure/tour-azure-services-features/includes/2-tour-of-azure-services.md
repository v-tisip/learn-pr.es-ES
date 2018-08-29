Microsoft Azure es un conjunto de servicios en la nube en constante expansión que ayudan a su organización a cumplir los desafíos empresariales actuales y futuros. Azure le ofrece la libertad de crear, administrar e implementar aplicaciones en una red global masiva mediante sus herramientas y marcos favoritos. Esta sección ofrece un paseo de alto nivel por los recursos que Azure ofrece.

## <a name="azure-services"></a>Servicios de Azure

Microsoft Azure proporciona una gran variedad de servicios basados en la nube, con características que se agregan y mejoran todos los meses.

![Servicios de Azure](../images/image204.png)

Echemos un vistazo más a fondo a algunas de las características más usadas: 

- Compute
- Redes 
- Storage
- Móvil 
- Bases de datos 
- Web

### <a name="compute"></a>Compute

Los servicios Compute son una de las razones principales de por qué las compañías se cambian a la plataforma Azure. Azure proporciona una amplia gama de opciones para hospedar aplicaciones y servicios que incluyen:

- Infraestructura como servicio (**IaaS**)
- Plataforma como servicio (**PaaS**)
- Funciones como servicio (**FaaS**)

Los propios servicios son los siguientes:

|  Nombre de servicio             | Función del servicio                                                          |  Escriba     |
| -------------             | -------------                                                             | --------- |
| Virtual Machines          | Máquinas virtuales Windows o Linux hospedadas en Azure                                      | IaaS      |
| Azure Container Service   | Permite la administración de un clúster de máquinas virtuales que ejecutan servicios en contenedores    | IaaS      |
| Service Fabric            | Plataforma de sistemas distribuidos. Se ejecuta en Azure o en local                | PaaS      |
| Azure Batch               | Servicio administrado para aplicaciones informáticas de alto rendimiento y paralelas  | PaaS      |
| Cloud Services            | Servicio administrado para ejecutar aplicaciones en la nube                            | PaaS      |
| Azure Container Instances | Proporcionan contenedores sin necesidad de aprovisionar máquinas virtuales o servicios superiores      | FaaS      |
| Azure Functions           | Servicio FaaS administrado                                                      | FaaS      |

### <a name="networking"></a>Redes

La vinculación de recursos de proceso y el suministro de acceso a las aplicaciones es la función clave de la red de Azure. La funcionalidad de red de Azure incluye una gama de opciones para conectar el mundo exterior a servicios y características de los centros de datos globales de Microsoft Azure.

Las instalaciones de red de Azure tienen las siguientes características:

|  Nombre de servicio             | Función del servicio                                                                      |
| -------------             | -------------                                                                         |
| Virtual Network           | Conectar máquinas virtuales a las conexiones de red privada virtual (VPN) entrante                     |
| Load Balancer             | Equilibrar las conexiones entrantes y salientes a aplicaciones o puntos de conexión de servicio         |
| Application Gateway       | Optimizar la entrega de granja de servidores de aplicaciones y, al mismo tiempo, aumentar la seguridad de la aplicación               |
| VPN Gateway               | Acceder a redes Azure Virtual Network a través de puertas de enlace VPN de alto rendimiento                   |
| Azure DNS                 | Proporcionar respuestas DNS ultrarrápidas y disponibilidad de dominio extremadamente alta                   |
| Content Delivery Network  | Entregar contenido de gran ancho de banda a los clientes globalmente                                  |
| Azure DDoS Protection     | Proteger las aplicaciones hospedadas en Azure frente a ataques por denegación de servicio distribuido (DDoS)   |
| Traffic Manager           | Distribuir el tráfico de red entre las regiones de Azure en todo el mundo                             |
| ExpressRoute              | Conectarse a Azure a través de conexiones seguras de gran ancho de banda dedicadas                     |
| Network Watcher           | Supervisar y diagnosticar problemas de red mediante el análisis basado en escenario                     |
| Azure Firewall            | Implementar el firewall de alta seguridad y alta disponibilidad con escalabilidad ilimitada         |
| Red WAN virtual               | Crear una red de área extensa (WAN) unificada, conectando sitios locales y remotos           |

### <a name="storage"></a>Storage

Azure proporciona cuatro tipos principales de servicios de almacenamiento. Estos servicios son los siguientes:

- **Azure Blob Storage**: proporciona almacenamiento para objetos muy grandes, como archivos de vídeo o mapas de bits
- **Azure File Storage**: crea recursos compartidos de archivos a los que puede acceder y administrar como un servidor de archivos
- **Azure Queue Storage**: implementa un almacén para la puesta en cola y la entrega confiable de mensajes entre aplicaciones
- **Almacenamiento de tablas de Azure**: consta de un almacén NoSLQ que hospeda datos no estructurados independientes de cualquier esquema

Cada uno de estos servicios comparte características comunes, que son:

- Durabilidad y alta disponibilidad con redundancia y la replicación.
- Seguridad mediante el cifrado automático y control de acceso basado en rol.
- Escalabilidad con un almacenamiento prácticamente ilimitado.
- Administración y control del mantenimiento y de cualquier problema crítico que pueda surgir.
- Accesibilidad desde cualquier parte del mundo a través de HTTP o HTTPS.

### <a name="mobile"></a>Móvil

Azure permite a los desarrolladores crear atractivas aplicaciones para iOS, Android y Windows rápida y fácilmente en una amplia gama de lenguajes mediante el entorno de desarrollo que prefiera. Las características que solían tardar tiempo y aumentaban el riesgo del proyecto, como la incorporación de inicio de sesión corporativo y la posterior conexión a recursos locales como SAP, Oracle, SQL Server y SharePoint, ahora se incluyen fácilmente.

Otras características de este servicio se incluyen:

- Sincronización de datos sin conexión.
- Conectividad a datos locales.
- Difusión de notificaciones push.
- Escalado automático para satisfacer las necesidades del negocio.

### <a name="databases"></a>Bases de datos

Azure proporciona varios servicios de base de datos para almacenar una gran variedad de volúmenes y tipos de datos. Y con conectividad global, los usuarios disponen de estos datos al instante.

|  Nombre de servicio             | Función del servicio                                                                                |
| -------------             | -------------                                                                                   |
| Azure Cosmos DB           | Base de datos distribuida globalmente que admite opciones NoSQL                                       |
| Azure SQL Database        | Base de datos relacional totalmente administrada con escalado automático, inteligencia integral y seguridad sólida    |
| Azure Database for MySQL  | Base de datos relacional MySQL totalmente administrada y escalable con alta disponibilidad y seguridad        |
| Base de datos de Azure para PostgreSQL   | Base de datos relacional PostgreSQL totalmente administrada y escalable con alta disponibilidad y seguridad   |
| SQL Server en máquinas virtuales         | Hospedar aplicaciones empresariales de SQL Server en la nube                                                  |
| SQL Data Warehouse        | Almacén de datos totalmente administrado con seguridad integral en todos los niveles de escala sin costo adicional    |
| Azure DB Migration Svc    | Migrar las bases de datos a la nube sin cambios de código de aplicación                            |
| Redis Cache               | Almacenar en caché datos estáticos y usados con frecuencia para reducir la latencia de los datos y las aplicaciones                    |
| Azure DB for MariaDB      | Base de datos relacional MySQL totalmente administrada y escalable con alta disponibilidad y seguridad        |

### <a name="web"></a>Web

Los servicios web en Azure incluyen las siguientes características:

- App Service: cree aplicaciones eficaces en la nube con rapidez para la Web y móviles
- Content Delivery Network: garantice una entrega de contenido segura y confiable con alcance global amplio
- Notification Hubs: envíe notificaciones push a cualquier plataforma desde cualquier back-end
- API Management: publique las API para desarrolladores, asociados y empleados de forma segura y a escala
- Azure Search: búsqueda como servicio completamente administrada
- Web Apps: cree e implemente rápidamente aplicaciones web críticas a escala
- Azure SignalR Service: agregue funcionalidades web en tiempo real con facilidad

## <a name="summary"></a>Resumen

Ahora tiene una visión general de los servicios que ofrece Azure. También ha identificado algunas de las áreas más importantes que interesarían a una empresa que esté buscando migrar a Azure para solucionar problemas relacionados con la escalabilidad y el control de cargas máximas. En la siguiente unidad, se registrará para una cuenta gratuita de Azure e iniciará sesión el portal.