Imagine que trabaja en una empresa que realiza el procesamiento de datos para las cámaras de tráfico. Las secuencias de vídeo se analizan, categorizan y procesan para identificar caras y matrículas en momentos concretos. Esta información se carga después en Azure Data Lake y se genera un índice de búsqueda.

Estas secuencias de vídeo usan un intervalo de distintos códecs y resoluciones. Deberá ejecutar varios paquetes de software de su propiedad basados en Windows para llevar a cabo el procesamiento inicial y codificarlos en un formato de vídeo común. Puesto que periódicamente se publican nuevos formatos, es conveniente realizar el procesamiento de vídeo en máquinas virtuales. Después, los paquetes de su propiedad se pueden agregar y actualizar sin detener todo el sistema.

Para administrar el software de codificación en sus máquinas virtuales Windows, deberá conectarse a la interfaz de usuario.

En este módulo, aprenderá a crear una máquina virtual Windows y a conectarse a ella con el Protocolo de escritorio remoto (RDP).

## <a name="learning-objectives"></a>Objetivos de aprendizaje
> [!div class="checklist"]
> * Cree una máquina virtual Windows en Azure Portal.
> * Conozca las opciones que están disponibles para máquinas virtuales en Azure.
> * Conéctese a una máquina virtual Windows en ejecución con el uso de la conexión de Escritorio remoto de Windows.

## <a name="prerequisites"></a>Requisitos previos

- Conocimiento del entorno de Azure Cloud Services.
- Familiaridad con las máquinas virtuales.
