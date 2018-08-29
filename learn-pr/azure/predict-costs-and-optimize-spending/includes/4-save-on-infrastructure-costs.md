Hemos aprendido a crear estimaciones de costos para los entornos que desea crear, visto algunas herramientas para obtener detalles sobre en qué estamos invirtiendo dinero y proyectado futuros gastos. Nuestro próximo desafío consiste en ver cómo reducir esos costos de infraestructura.

## <a name="use-reserved-instances"></a>Usar instancias reservadas

Si tiene cargas de trabajo de máquina virtual que son estáticas y predecibles por naturaleza, especialmente aquellas que se ejecutan de forma permanente, usar instancias reservadas es una manera fantástica de ahorrar hasta un 70 % de forma potencial, dependiendo del tamaño de VM.

![Ahorros en instancias reservadas](../images/savings-coins.png)

Las instancias reservadas se adquieren en plazos de uno o tres años, debiendo pagarse por adelantado la totalidad del plazo. Una vez que se adquiere, Microsoft hace coincidir la reserva con las instancias en ejecución y reduce las horas transcurridas desde la realización de la reserva. Las reservas se pueden adquirir a través de Azure Portal. Además, como las instancias reservadas son un descuento de cálculo, están disponibles tanto para las máquinas virtuales Windows como para las Linux. 

## <a name="right-size-underutilized-virtual-machines"></a>Ajustar el tamaño de las máquinas virtuales infrautilizadas

Recuerde de nuestro anterior debate que Azure Cost Management y Azure Advisor pueden recomendar que se apaguen las máquinas virtuales o se ajuste su tamaño. Ajustar el tamaño de una máquina virtual es el proceso de cambiar su tamaño para que sea el correcto. Imaginemos que tiene un servidor que se ejecuta como un controlador de dominio con el tamaño **Standard_D4sv3**, pero su máquina virtual presenta un 90 % de inactividad la mayor parte del tiempo. Al cambiar el tamaño de esta máquina virtual a **Standard_D2s_v3**, reduce su costo de proceso un 50 %. Los costos son lineales y dobles por cada tamaño mayor en la misma serie. En este caso, puede incluso beneficiarse del cambio de serie de las instancias para ir a una serie de máquinas virtuales menos costosa.

![Cambiar el tamaño de una máquina virtual](../images/vm-resize.png)

Las máquinas virtuales de tamaño grande son un gasto innecesario habitual en Azure y que tiene fácil solución. Puede cambiar el tamaño de una máquina virtual a través de Azure Portal, Azure PowerShell o la CLI de Azure.

> [!NOTE]
> Al cambiarse el tamaño de una máquina virtual, esta se detiene y, una vez cambia su tamaño, se reinicia. Esto puede tardar unos minutos dependiendo de lo significativo que sea el cambio de tamaño. Planee una interrupción o cambie su tráfico a otra instancia mientras realiza esta tarea.

## <a name="deallocate-virtual-machines-in-off-hours"></a>Desasignar máquinas virtuales en las horas de inactividad

Si tiene cargas de trabajo de máquina virtual que solo se usan durante determinados periodos de tiempo, pero las ejecuta cada hora de cada día, está perdiendo dinero. La probabilidad de que estas máquinas virtuales se apaguen es muy alta si no se usan y empiezan a realizar copias de seguridad programadas, lo que le ahorra costos de proceso mientras se desasigna la máquina virtual.

Este enfoque es una gran estrategia para los entornos de desarrollo. Muchas veces sucede que el desarrollo puede producirse solo durante las horas laborables, lo que le da la flexibilidad necesaria para desasignar estos sistemas en las horas de inactividad e impide que se acumulen sus costos de proceso. Ahora Azure tiene una [solución de automatización](https://docs.microsoft.com/azure/automation/automation-solution-vm-management) totalmente disponible para que pueda aprovecharla en su entorno.

También puede usar la característica de apagado automático en una máquina virtual para programar apagados automatizados.

![Apagado automático](../images/vm-auto-shutdown.png)

## <a name="delete-unused-virtual-machines"></a>Eliminar las máquinas virtuales sin usar 

 Tal vez suene obvio este consejo, pero si no usa un servicio, debe apagarlo. No es raro encontrar sistemas de prueba de concepto o que no son de producción que se han dejado para un proyecto que ya no es necesario. Revise su entorno con regularidad y trabaje para identificar estos sistemas. Apagar estos sistemas puede tener un beneficio multifacético, permitiéndole ahorrar en costos de infraestructura y suponiéndole, además, posibles ahorros en licencias y operaciones.

## <a name="migrate-to-paas-or-saas-services"></a>Migrar a los servicios PaaS o SaaS 

Por último, al mover cargas de trabajo a la nube, una evolución natural es empezar con servicios de infraestructura como servicio (IaaS) y, a continuación, moverlos a servicios de plataforma como servicio (PaaS) según corresponda, en un proceso iterativo.

Los servicios PaaS suelen suponer ahorros sustanciales tanto en costos de recursos como en costos operativos. El desafío consiste en que, dependiendo del tipo de servicio, se requerirán niveles de esfuerzo variables para moverse a estos servicios desde una perspectiva de tiempo y de recursos. Es posible que pueda mover fácilmente una base de datos de SQL Server a Azure SQL Database, pero puede suponer un esfuerzo considerablemente mayor mover su aplicación de varios niveles a un contenedor o arquitectura sin servidor. Es una buena práctica evaluar de forma continua la arquitectura de sus aplicaciones para determinar si se van a obtener eficiencias a través de servicios PaaS.  

Con Azure es más fácil probar estos servicios sin demasiado riesgo. Le ofrece la posibilidad de probar nuevos patrones de arquitectura de forma relativamente fácil. Dicho esto, suele ser un proceso más largo y puede que no sea útil de forma inmediata si busca resultados rápidos desde una perspectiva de ahorro de costos. Azure Architecture Center es un lugar ideal para obtener ideas con las que transformar su aplicación, así como procedimientos recomendados en una amplia gama de arquitecturas y servicios de Azure. 