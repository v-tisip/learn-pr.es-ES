Jim administra un conjunto de máquinas virtuales de Azure que se ejecutan en nuestra infraestructura web corporativa, que incluye varios sitios web y servidores de bases de datos que se ejecutan en varias plataformas. 

Aunque Azure Portal es fácil de usar, Jim ha detectado que navegar por las distintas hojas agrega tiempo a algunas de las tareas. 

Al explorar alternativas, descubre la herramienta CLI de Azure.

Al trabajar con la CLI de Azure, Jim puede escribir scripts que comprueben el estado de los servidores, implementen una nueva configuración, abran un puerto o se conecten a una máquina virtual para cambiar un ajuste.

Tal vez, como Jim, está buscando una herramienta que le ayude a automatizar las tareas en el entorno en la nube. Vamos a mostrarle cómo usar la CLI de Azure para crear y administrar máquinas virtuales hospedadas en Azure. 

## <a name="azure-cli"></a>Azure CLI

La CLI de Azure es la herramienta de línea de comandos multiplataforma de Microsoft para administrar los recursos de Azure. Está disponible para macOS, Linux y Windows, o en el explorador con [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).

> [!IMPORTANT]
> Hay dos versiones de la herramienta CLI de Azure disponibles actualmente: CLI de Azure 1.0 y CLI de Azure 2.0. Usaremos la CLI de Azure 2.0, que es la versión más reciente y la que se recomienda a menos que se ejecuten scripts heredados escritos para 1.0. La CLI de Azure 1.0 se inicia con el comando `azure` y la CLI de Azure 2.0, con el comando `az`. 

La CLI de Azure puede ayudarle a administrar recursos de Azure, tales como máquinas virtuales y discos, desde la línea de comandos o con scripts. Empecemos a trabajar y veamos lo que puede hacer.

## <a name="learning-objectives"></a>Objetivos de aprendizaje
> [!div class="checklist"]
> * Creación de una máquina virtual de Azure con la CLI
> * Cambio de tamaño de máquinas virtuales con la CLI
> * Administración y consulta de una máquina virtual desde la línea de comandos
> * Instalación de software en una máquina virtual