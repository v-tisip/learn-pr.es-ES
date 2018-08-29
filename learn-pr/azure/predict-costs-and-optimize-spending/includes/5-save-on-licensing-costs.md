Las licencias son otro aspecto que puede afectar considerablemente al gasto en la nube. Veamos algunas maneras de reducir los costos de licencia.

## <a name="azure-hybrid-benefit-for-windows-server"></a>Ventaja híbrida de Azure para Windows Server

Muchos clientes han realizado una inversión en licencias de Windows Server y les gustaría reasignar esta inversión en Azure. La Ventaja híbrida de Azure ofrece a los clientes el derecho a usar estas licencias para máquinas virtuales en Azure. Esto significa que no se cobrará por la licencia de Windows Server y, en su lugar, se facturará según la tarifa de Linux. 

Para poder optar a esta ventaja, las licencias de Windows deben estar cubiertas por Software Assurance. También se aplicarán las directrices siguientes:

- Cada licencia de dos procesadores o cada conjunto de licencia de 16 núcleos tienen derecho a dos instancias de hasta ocho núcleos o a una instancia de hasta 16 núcleos. 
- Las licencias de Standard Edition solo se pueden usar una vez en el entorno local o en Azure. Esto significa que no se puede usar la misma licencia para una máquina virtual de Azure y un equipo local.
- Las ventajas de Datacenter Edition permiten el uso simultáneo de forma local y en Azure, de modo que la licencia abarcará dos equipos que ejecuten Windows. 

> [!NOTE]
> La mayoría de los clientes normalmente cuentan con licencia por núcleo, por lo que se usará ese modelo para el cálculo. Si tiene preguntas sobre qué licencias tiene, póngase en contacto con su revendedor de licencias o el equipo de cuentas de Microsoft.

La aplicación del beneficio es sencilla. Se puede activar y desactivar en cualquier momento con las máquinas virtuales existentes, o bien aplicarse durante la implementación de máquinas virtuales nuevas. La Ventaja híbrida (especialmente cuando se combina con instancias reservadas) puede proporcionar ahorros de licencia importantes.

## <a name="azure-hybrid-benefit-for-sql-server"></a>Ventaja híbrida de Azure para SQL Server

La Ventaja híbrida de Azure para SQL Server ayuda a maximizar el valor de las inversiones actuales en licencias y a acelerar el proceso de migración a la nube. Se trata de una ventaja basada en Azure que permite usar las licencias de SQL Server con Software Assurance para pagar una tarifa reducida.

Puede solicitar esta ventaja aunque el recurso de Azure esté activo, pero la tarifa se aplicará desde el momento en que la seleccione en el portal. No se emitirá ningún crédito con carácter retroactivo.

### <a name="azure-sql-database-vcore-based-options"></a>Opciones basadas en núcleos virtuales de Azure SQL Database

![Canje de la licencia de SQL Server](../images/sql-tradein-value.jpg)

Para Azure SQL Database, la Ventaja híbrida de Azure funciona del siguiente modo:

- Si tiene licencias Standard Edition por núcleo con Software Assurance activo, puede obtener un núcleo virtual en el nivel de servicio de uso general por cada núcleo de licencia que tenga en el entorno local.
- Si tiene licencias Enterprise Edition por núcleo con Software Assurance activo, puede obtener un núcleo virtual en el nivel de servicio Crítico para la empresa por cada núcleo de licencia que tenga en el entorno local. Tenga en cuenta que solo los clientes con licencias Enterprise Edition pueden optar a la Ventaja híbrida de Azure para SQL Server para el nivel de servicio Crítico para la empresa .
- Si tiene licencias Enterprise Edition altamente virtualizadas por núcleo con Software Assurance activo, puede obtener cuatro núcleos virtuales en el nivel de servicio de uso general por cada núcleo de licencia que tenga en el entorno local. Esta es una ventaja de virtualización única disponible solo en Azure SQL Database.

Para SQL Server en Azure Virtual Machines, la Ventaja híbrida de Azure funciona del siguiente modo:

- Si tiene licencias Enterprise Edition por núcleo con Software Assurance activo, puede obtener un núcleo de SQL Server Enterprise Edition en Azure Virtual Machines por cada núcleo de licencia que tenga en el entorno local.
- Si tiene licencias Standard Edition por núcleo con Software Assurance activo, puede obtener un núcleo de SQL Server Standard Edition en Azure Virtual Machines por cada núcleo de licencia que tenga en el entorno local.

Esto puede suponer un impacto significativo en el gasto de Azure con cargas de trabajo de SQL Server.

## <a name="use-devtest-subscription-offers"></a>Usar ofertas de suscripción de Desarrollo/pruebas

Las ofertas [Desarrollo/pruebas - Enterprise](https://azure.microsoft.com/offers/ms-azr-0148p/) y [Desarrollo/pruebas - Pago por uso](https://azure.microsoft.com/offers/ms-azr-0023p/) son una de las ventajas que se pueden aprovechar para ahorrar costos en los entornos que no sean de producción. Esta ventaja proporciona varios descuentos, especialmente para las cargas de trabajo de Windows, lo que elimina los gastos de licencia y solo se cobra la tarifa de Linux para las máquinas virtuales. Esto también se aplica a SQL Server y cualquier otro software de Microsoft que esté cubierto por una suscripción de Visual Studio (anteriormente conocida como MSDN). Hay algunos requisitos para esta ventaja: uno es que solo es para las cargas de trabajo que no sean de producción, y otro que los usuarios de estos entornos (excepto los evaluadores) deben estar cubiertos por una suscripción de Visual Studio. En resumen, para las cargas de trabajo que no son de producción, esto permite ahorrar en las cargas de trabajo de Windows, SQL Server y otras máquinas virtuales de Microsoft.
A continuación se muestran los detalles completos de cada oferta. Si es un cliente con un contrato Enterprise, podría aprovechar la oferta Desarrollo/pruebas - Enterprise y, si es un cliente sin un contrato Enterprise y en su lugar usa cuentas de pago por uso, podría aprovechar la oferta Desarrollo/pruebas - Pago por uso.

## <a name="bring-your-own-sql-server-license"></a>Traiga su propia licencia de SQL Server

Si es un cliente con un contrato Enterprise y ya ha invertido en licencias de SQL Server y se han liberado como parte del traslado de los recursos a Azure, puede aprovisionar imágenes **traiga su propia licencia** (BYOL) desde Azure Marketplace, lo que permite aprovechar las ventajas de estas licencias sin usar y reducir el costo de la máquina virtual de Azure. Esto siempre ha sido posible mediante el aprovisionamiento de una máquina virtual de Windows y la instalación manual de SQL Server, pero el proceso de creación se simplifica gracias al aprovechamiento de imágenes con certificación de Microsoft. Busque **BYOL** en Marketplace para encontrar estas imágenes.

![BYOL para SQL Server en Azure](../images/byol-sql-server.png)

> [!IMPORTANT]
> Se necesita una suscripción al contrato Enterprise para usar estas imágenes BYOL certificadas.

## <a name="use-sql-server-developer-edition"></a>Uso de SQL Server Developer Edition

Muchos usuarios desconocen que SQL Server Developer Edition es un producto gratuito para **uso de no producción**. Developer Edition tiene las mismas características que Enterprise Edition, pero, para las cargas de trabajo que no son de producción, se puede ahorrar considerablemente en los costos de licencia.

Busque imágenes de SQL Server Developer Edition en Azure Marketplace y úselas con fines de desarrollo o pruebas para eliminar el costo adicional de SQL Server en estos casos. 

> [!NOTE]
> Para obtener toda la información sobre las licencias, vea la [documentación de la guía de precios](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance).

## <a name="use-constrained-instance-sizes-for-database-workloads"></a>Uso de tamaños de instancia restringidos para las cargas de trabajo de base de datos 

Muchos clientes tienen requisitos elevados de memoria, almacenamiento y ancho de banda de E/S, pero recuentos de núcleos de CPU bajos. Debido a esta petición popular, Microsoft ha puesto los tamaños de máquina virtual más populares (DS, ES, GS y MS) a disposición como tamaños nuevos que restringen el número de vCPU a la mitad o un cuarto del tamaño de la máquina virtual original, manteniendo la misma memoria, almacenamiento y ancho de banda de E/S.

| Tamaño de VM | vCPU | Memoria | Discos máx. | Rendimiento de E/S máx. | Coste por año de la licencia de SQL Server Enterprise | Costo total por año (proceso + licencias) |
|---------|-------|--------|-----------|--------------------|-----------------------------------------------|---------------------------|
| Standard_DS14v2   | 16 | 112 GB | 32 | 51 200 IOPS o 768 MB/s |           |           |
| Standard_DS14-4v2 | **4**  | 112 GB | 32 | 51 200 IOPS o 768 MB/s | 75 % menos | 57 % menos |
| Standard_GS5      | 32 | 448    | 64 | 80 000 IOPS o 2 GB/s   |           |           |
| Standard_GS5-8    | **8**  | 448    | 64 | 80 000 IOPS o 2 GB/s   | 75 % menos | 42 % menos |

Dado que los productos de base de datos como SQL Server y Oracle cuentan con licencia por CPU, esto permite a los clientes reducir los costos de licencia en un 75 por ciento y seguir manteniendo el alto rendimiento que su base de datos requiere. 
