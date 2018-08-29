Si quiere comprender lo que puede salir mal con la administración de los secretos de configuración de una aplicación, no tiene más que leer la historia de Steve, un desarrollador jefe.

Steve lleva algunas semanas desempeñando este puesto en una empresa de entrega de alimento para mascotas. Ha estado examinando los detalles de la aplicación web de la empresa, una aplicación web de .NET Core que usa una base de datos SQL Azure para almacenar la información de pedidos y API de terceros para la facturación de tarjetas de crédito y la asignación direcciones de clientes, cuando por accidente ha pegado la cadena de conexión de la base de datos de pedidos em un foro público.

Días más tarde, en contabilidad han observado que la empresa ha estado entregando muchos pedidos que nadie ha pagado. Alguien había usando la cadena de conexión para acceder a la base de datos, había manipulado mediante ingeniería inversa el esquema y había realizado pedidos sin pasar por el sitio web.

Tras darse cuenta de su error, Steve cambió a toda prisa la contraseña de la base de datos para bloquear al atacante e interrumpió el sitio web. Inició sesión directamente en el servidor de aplicaciones y cambió la configuración de la aplicación en lugar de volver a implementarla, pero el servidor seguía mostrando solicitudes con error.

Steve había olvidado que varias instancias de la aplicación se ejecutaban en distintos servidores y que solo había cambiado la configuración de una. Era necesaria una reimplementación completa, lo que suponía otros 30 minutos de inactividad.

La pérdida de una cadena de conexión de base de datos, una clave de API o una contraseña de servicio puede ser catastrófica. Posibles resultados son robo o eliminación de datos, perjuicios financieros, tiempo de inactividad de la aplicación y daños irreparable en los activos de negocio y la reputación. Por desgracia, los valores secretos con frecuencia han de implementarse en varios lugares a la vez y cambiarse en momentos inoportunos. Y hay que almacenarlos *en alguna parte*. Veamos cómo podemos hacer que todo esto sea seguro con Azure Key Vault.

## <a name="learning-objectives"></a>Objetivos de aprendizaje
> [!div class="checklist"]
> * Comprender qué tipos de información se pueden almacenar en Azure Key Vault
> * Crear un almacén de Azure Key Vault
> * Autenticarse con Azure Key Vault
> * Acceder a los secretos de una instancia de Azure KeyVault