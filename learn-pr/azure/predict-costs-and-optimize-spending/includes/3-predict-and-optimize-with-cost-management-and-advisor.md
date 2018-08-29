Aprendimos cómo se calculan los costos antes de implementar servicios en Azure, pero ¿qué sucede si ya tiene los recursos implementados? ¿Cómo puede tener visibilidad sobre los costos que ya está acumulando? Si hubiéramos implementado la solución anterior en Azure y ahora quisiéramos asegurarnos de que el tamaño de las máquinas virtuales fuese el correcto y predecir de cuánto sería nuestra factura, ¿cómo podríamos hacerlo? Echemos un vistazo a algunas herramientas en Azure que puede usar para ayudar a solucionar este problema.

## <a name="what-is-azure-advisor"></a>¿Qué es Azure Advisor? 

**Azure Advisor** es un servicio gratuito integrado en Azure que ofrece recomendaciones sobre alta disponibilidad, seguridad, rendimiento y costo. Advisor analiza los servicios implementados y busca maneras de mejorar su entorno a través de esas cuatro áreas. Nos centraremos en las recomendaciones de costo, pero le sugerimos que se dé unos momentos para revisar también las otras recomendaciones.

Advisor hace recomendaciones de costo en las áreas siguientes: 

1. **Reducción de los costos mediante la eliminación de circuitos de Azure ExpressRoute no aprovisionados.** 
    Identifica los circuitos ExpressRoute que han permanecido en el estado de proveedor de *No aprovisionado* durante más de un mes y recomienda eliminar el circuito si no piensa realizar el aprovisionamiento del circuito con el proveedor de conectividad.

2. **Compra de instancias reservadas para ahorrar dinero a través de pago por uso.** 
    Esto revisará el uso de la máquina virtual durante los últimos 30 días y determinará si podría ahorrar dinero en el futuro mediante la adquisición de instancias reservadas. Advisor le mostrará las regiones y los tamaños en los que, potencialmente, puede ahorrar más, así como el ahorro estimado que podría lograr al comprar instancias reservadas.
    
3. **Ajuste del tamaño o apagado de máquinas virtuales infrautilizadas.** 
    Esto supervisa la utilización de las máquinas virtuales durante 14 días e identifica aquellas con una utilización escasa. Se considera que una máquina virtual tiene una utilización escasa si su uso promedio de CPU es del 5 % o menos y el de la red es de 7 MB o menos durante cuatro o más días. El umbral de uso de CPU promedio se puede ajustar hasta un 20 por ciento. Mediante la identificación de estas máquinas virtuales infrautilizadas, puede decidir cambiarles el tamaño a un tipo de instancia más pequeño, lo que reduce los costos.

Echemos un vistazo a dónde puede encontrar Azure Advisor en el portal. Inicie sesión en Azure Portal en [https://portal.azure.com](https://portal.azure.com). Haga clic en **Todos los servicios** y, en la categoría **Herramientas de administración**, verá **Advisor**. También puede escribir **Advisor** en el cuadro de filtro para el filtro solo ese servicio. 

Haga clic en Advisor y se le dirigirá al panel de recomendaciones de Advisor donde podrá ver todas las recomendaciones para la suscripción. Verá un cuadro para cada categoría de recomendaciones. 

> [!NOTE]
> Es posible que no tenga ninguna recomendación relacionada con el costo en Advisor. Esto podría deberse a que las evaluaciones todavía no se completaron o simplemente porque no hay ninguna recomendación de Advisor.

![Recomendaciones de Advisor](../images/advisor-recommendations.png)

Al hacer clic en el cuadro **Costo**, irá a las recomendaciones detalladas para donde puede ver las recomendaciones que tiene Advisor.

![Recomendaciones sobre el costo de Advisor](../images/advisor-cost-recommendations.png)

Si hace clic en cualquier recomendación, irá a los detalles de esa recomendación específica. A continuación, podrá realizar una acción específica, como ajustar el tamaño de las máquinas virtuales para reducir el gasto.

![Recomendación de Advisor sobre el ajuste de tamaño de las máquinas virtuales](../images/advisor-resize-vm.png)

Estas recomendaciones son todos los lugares donde podría estar gastando dinero de manera ineficaz. Son un excelente lugar para comenzar y seguir revisitando cuando busque lugares para reducir los costos. En nuestro ejemplo, tenemos una oportunidad para ahorrar aproximadamente USD 700 al mes si tomamos estas recomendaciones. Estos ahorros se suman, así que asegúrese de revisar esto periódicamente para obtener recomendaciones a través de las cuatro áreas.

## <a name="azure-cost-management"></a>Azure Cost Management

Azure Cost Management es otra herramienta gratuita integrada Azure que se puede usar para obtener mayor información sobre dónde va su inversión en la nube. Puede ver los desgloses históricos de en qué servicios gasta su dinero y cómo se realiza el seguimiento respecto de presupuestos que haya establecido. Puede establecer presupuestos, programar informes y analizar las áreas de costo.

![Administración de costos](../images/cost-management.png)

## <a name="cloudyn"></a>Cloudyn 

Cloudyn, una subsidiaria de Microsoft, permite realizar un seguimiento de los gastos y el uso de la nube para los recursos de Azure y otros proveedores de nube, entre los que se incluyen Amazon Web Services y Google. Los sencillos informes del panel proporcionan ayuda con la asignación de costos, los contracargos y la visibilidad de los gastos. Administración de costos le ayuda a optimizar los gastos en la nube mediante la identificación de los recursos que no está aprovechando para que pueda administrarlos y ajustarlos. El uso de Azure es gratuito y hay opciones de pago para soporte técnico premium y ver datos de otras nubes. 

![Panel de administración de Cloudyn](../images/cloudyn-mgt-dash.png)

## <a name="summary"></a>Resumen

Como puede ver, hay varias herramientas disponibles sin ningún costo en Azure que puede usar para realizar un seguimiento y predecir su gasto en la nube e identificar dónde es posible que su entorno sea ineficaz desde una perspectiva del costo. Querrá asegurarse de que una práctica habitual sea revisar los informes y las recomendaciones que ponen a su disposición estas herramientas, para que puedan descubrir ahorros en su superficie de nube. Ahora echemos un vistazo a algunos procedimientos recomendados para disminuir los costos de infraestructura.
