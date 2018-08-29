Hay determinadas aplicaciones que generan un gran número de eventos de casi tantos orígenes. A menudo escuchamos el término "macrodatos" aplicado a estas situaciones y requieren una infraestructura única para controlarlas.

Imagine que trabaja para Contoso Aircraft Engines. Los motores que el empleador fabrica tiene cientos de sensores. Antes de que se pueda volar un avión cada mañana, sus motores están conectados a un arnés de prueba y se ponen a prueba. Además, los datos de vuelo almacenados en caché se transmiten cuando el avión se conecta al equipo de tierra.

Desea usar datos de sensor históricos para buscar patrones en las lecturas de sensor que indiquen que es probable que se produzca un error del motor pronto. Desea que las lecturas de sensor en tiempo real se comparen con estos patrones de error. Después, puede advertir a los usuarios prácticamente en tiempo real si un motor muestra lecturas preocupantes.

## <a name="what-is-azure-event-hubs"></a>¿Qué es Azure Event Hubs?

Azure Event Hubs es un intermediario de patrón de comunicación de publicación y suscripción, pero a diferencia de Event Grid está optimizado para un rendimiento extremadamente alto, un gran número de publicadores, seguridad y resistencia.

Mientras que Event Grid se ajusta más o menos perfectamente al patrón de publicación y suscripción, ya que simplemente administra las suscripciones y enruta las comunicaciones a los suscriptores, Event Hubs realiza bastantes servicios adicionales que de alguna manera lo hacen parecerse a un bus de servicio o a una cola de mensajes más que un simple presentador de eventos.

#### <a name="partitions"></a>Particiones ####
A medida que Event Hubs recibe las comunicaciones, las divide en particiones. Las particiones son los búferes en los que se guardan las comunicaciones. Debido a los búferes de eventos, los eventos no son completamente efímeros y un evento no se pierde simplemente porque un suscriptor está ocupado o incluso sin conexión. El suscriptor siempre puede usar el búfer "para ponerse al día". De forma predeterminada, los eventos permanecen en el búfer durante 24 horas y después expiran automáticamente.

Los búferes se denominan particiones porque los datos se dividen entre ellos. Cada centro de eventos tiene al menos dos particiones y cada partición tiene un conjunto independiente de suscriptores.

#### <a name="capture"></a>Capture ####
Event Hubs puede enviar todos los eventos inmediatamente a Azure Data Lake o Blob Storage para una persistencia permanente económica.

#### <a name="authentication"></a>Autenticación ####
Todos los publicadores se autentican y emiten un token. Esto significa que Evento Hubs puede aceptar eventos de dispositivos externos y aplicaciones móviles sin preocuparse de que datos fraudulentos procedentes de usuarios bromistas podrían arruinar nuestro análisis. 

## <a name="using-azure-event-hub"></a>Uso de Azure Event Hubs

Event Hubs es compatible con la canalización de transmisiones de eventos a otros servicios de Azure. Por ejemplo, si se usa con Stream Analytics, permite un análisis complejo de datos casi en tiempo real con la capacidad de poner varios eventos en correlación y buscar patrones. En este caso, Stream Analytics se consideraría un suscriptor.

Para nuestros motores de aviones, configuraremos nuestra arquitectura para que Event Hubs autentique las comunicaciones de nuestros motores. A continuación, haremos que use capturas para guardar todos los datos en Azure Data Lake. Más adelante podemos usar todos esos datos para volver a entrenar y mejorar nuestros modelos de aprendizaje automático. Por último, los suscriptores de Azure Stream Analytics recogerán nuestras transmisiones de eventos. Stream Analytics usará nuestro modelo de aprendizaje automático para buscar patrones en los datos de sensor que podrían indicar problemas.

Dado que tenemos varias particiones y cada motor envía todos sus datos a una sola partición, cada instancia de nuestro suscriptor de Stream Analytics solo ocuparse de un subconjunto de todos nuestros datos en lugar de filtrarlos y correlacionarlos.

## <a name="choose-event-grid-or-event-hub"></a>Elección de Event Grid o Event Hubs

Ambos admiten la semántica *Al menos una vez*.

Si necesita una infraestructura simple de publicación y suscripción de eventos con editores de confianza (por ejemplo, su propio servidor web), debe elegir Azure Event Grid.

### <a name="consider-event-hub-if"></a>Considere Event Hubs si
* Necesita admitir la autenticación de un gran número de publicadores
* Necesita guardar una transmisión de eventos a Azure Data Lake o Blob Storage
* Necesita la agregación o análisis en la transmisión de eventos
* Necesita mensajería de confianza o resistencia 