En este ejercicio, va a crear y configurar un panel personalizado.

## <a name="create-a-new-dashboard"></a>Creación de un nuevo panel

1. En Azure Portal, haga clic en el botón **Nuevo panel**.

2. En el cuadro que indica **Mi panel**, cambie el nombre a **Panel del cliente**.

## <a name="add-and-configure-the-clock-tile"></a>Adición y configuración del icono de reloj

1. En la galería de iconos, arrastre y coloque el reloj en el área de trabajo. Colóquelo en la parte superior derecha del espacio disponible.

2. En la hoja Editar reloj, cambie la ubicación a **Hora del Pacífico (EE.UU. y Canadá)**.

3. En **Formato de hora**, haga clic en **24 horas**.

4. Haga clic en **Done**(Listo).

5. Repita los cuatro pasos anteriores, pero seleccione **Hora del este (EE.UU. y Canadá)**. Ahora debe tener dos relojes, uno que muestre la hora en la costa oeste y el otro en la costa este.

## <a name="resize-a-tile"></a>Cambio del tamaño de un icono

1. En el panel Galería de iconos, haga clic en **Todos los recursos** y, después, coloque el icono en la parte superior izquierda de la nueva área de trabajo del panel.

2. Haga clic sucesivamente en el icono, en los puntos suspensivos y en **6x6**.

3. Haga clic en la esquina gris de la parte inferior derecha del icono y cambie el tamaño de la baldosa a 3,5 verticalmente por 6 horizontalmente. Tenga en cuenta que cuando se quita la esquina, cambia el tamaño a 4 x 6.

4. En Galería de iconos, haga clic en el icono **Grupos de recursos** y arrástrelo al área de trabajo. Colóquelo debajo del icono **Todos los recursos**.

5. En Galería de iconos, haga clic en el icono **Service Health** y arrástrelo al área de trabajo. Colóquelo a la derecha del icono **Todos los recursos** icono.

6. Siga agregando los iconos siguientes y organícelos para que quepan:

    * Ayuda y soporte técnico
    * Tareas rápidas
    * Marketplace
    * Novedades

7. Cuando haya agregado estos iconos, haga clic en **Personalización finalizada**. Debe aparecer el **panel del cliente**.

## <a name="clone-a-dashboard"></a>Clonación de un panel

Ahora quiere crear un panel muy similar para otros clientes

1. Haga clic en el botón **Clonar**.

2. Cambie el panel de **Clonar del Panel del cliente** a **Panel de administración de Azure AD**.

3. En el icono **Grupos de recursos**, haga clic en el icono de cubo de basura para eliminar este icono.

4. Desde Galería de iconos, agregue los siguientes iconos:

    * Identidad de la organización
    * Usuarios y grupos
    * Resumen de la actividad del usuario
    * Acceso al centro de administración de Azure AD

5. Cambie la posición de los iconos según sea necesario y, después, haga clic en **Personalización finalizada**.

## <a name="share-a-dashboard"></a>Uso compartido de un panel

Ahora quiere poner este panel a disposición de otros usuarios. Para ello, realice estos pasos:

1. Asegúrese de que está seleccionado el panel de administración de Azure AD y, después, haga clic en **Compartir**.

2. En la hoja **Uso compartido y control de acceso**, asegúrese de que **Publicar en el grupo de recursos "paneles"** está seleccionado.

3. Establezca la **ubicación** a una que sea adecuada para su ubicación geográfica. Normalmente, este valor es el centro de datos más cercano.

4. Haga clic en **Publicar**, después, cierre la hoja **Uso compartido y control de acceso**.

5. Haga clic en **Panel de administración de Azure AD** y seleccione **Panel del cliente**.

6. Tenga en cuenta que en **Todos los recursos**, ha aparecido un recurso del panel compartido y que, en **Grupos de recursos**, también aparece un grupo de recursos de los paneles.

7. Repita los pasos 1 a 3 para compartir el panel del cliente.

## <a name="edit-a-dashboard-file"></a>Edición de un archivo del panel

Para mostrar cómo puede descargar y editar un archivo del panel, lleve a cabo los pasos siguientes:

1. Haga clic en **Descargar**.

2. Abra el Explorador de Windows y vaya a la carpeta de descargas.

3. Busque el archivo **Customer Dashboard.json** y haga doble clic en él.

4. En el editor de archivos, busque el texto "ClockPart".

5. En la primera aparición de ClockPart, cambie el valor anterior de rowSpan a 1.

6. En la segunda aparición de Clockpart, cambie también el valor anterior de rowSpan a 1.

7. En la segunda aparición de Clockpart, cambie el valor de Y de 2 a 1.

8. Guarde el archivo de Customer Dashboard.json y cierre el editor de código.

9. En el panel de Azure, haga clic en **Cargar**.

10. En el cuadro de diálogo **Abrir**, vaya a la carpeta de descargas y haga doble clic en **Customer Dashboard.json**.

11. Observe cómo los relojes han cambiado de tamaño a una fila de alto y el reloj inferior se ha movido una fila hacia arriba.

## <a name="select-a-shared-dashboard"></a>Selección de un panel compartido

Se ha dado cuenta de que no le gustan los relojes más pequeños y desea volver a la versión compartida anterior del Panel del cliente. Para ello, edite el archivo y cárguelo de nuevo, o acceda a la versión compartida. Para ello, realice los pasos siguientes:

1. Haga clic en la flecha abajo junto a **Panel del cliente**.

2. Haga clic en **Examinar todos los paneles**.

3. En la hoja **Todos los paneles**, en **TIPO**, seleccione **Paneles compartidos**.

4. Haga clic en **Panel del cliente**.

5. Cierre la hoja **Todos los paneles**.

6. Observe cómo los relojes han vuelto a su tamaño original.

## <a name="switch-to-full-screen"></a>Cambio a pantalla completa

1. Haga clic en la flecha abajo junto a **Panel del cliente**. Tenga en cuenta que hay otro panel del cliente, sin el símbolo de uso compartido junto a él. Haga clic en esa versión del panel del cliente y los relojes volverán a ser pequeños de nuevo.

2. Vuelva a cambiar al panel del cliente compartido.

3. Haga clic en el botón **Pantalla completa**. Observe cómo han desaparecido todos los menús y barras del explorador.

4. Haga clic en **Salir de pantalla completa** para volver a la pantalla normal.

## <a name="unshare-a-dashboard"></a>Dejar de compartir un panel

Si desea evitar que un panel en particular esté disponible para su selección, puede dejar de compartirlo. Para dejar de compartir un panel, realice los pasos siguientes:

1. Haga clic en el botón **Dejar de compartir**. Se muestra la hoja **Uso compartido y control de acceso**.

2. Haga clic en el botón **Anular publicación**.

3. En el cuadro de mensaje de confirmación, haga clic en **Aceptar**.

4. Haga clic en la flecha abajo junto a **Panel del cliente**.

5. Haga clic en **Examinar todos los paneles**.

6. En la hoja **Todos los paneles**, en **TIPO**, seleccione **Paneles compartidos**.

7. Observe que el panel del cliente ya no aparece en la lista de paneles disponibles.

8. Cierre la hoja "Todos los paneles".

## <a name="delete-a-dashboard"></a>Eliminación de un panel

1. Asegúrese de que está seleccionado Panel de administración de Azure AD.

2. Haga clic en el botón **Eliminar** .

3. En el cuadro de mensaje **Confirmación**, active la casilla para confirmar que este panel dejará de estar visible y, a continuación, haga clic en **Aceptar**.

## <a name="reset-a-dashboard"></a>Restablecimiento de un panel

1. Asegúrese de que está seleccionado Panel del cliente.

2. Haga clic en **Editar**.

3. Haga clic con el botón derecho en el área de trabajo y haga clic en **Restaurar al estado predeterminado**.

4. En el cuadro de mensaje **Restaurar al estado predeterminado**, haga clic en **Sí**.

5. Observe cómo el panel del cliente se ha restablecido a sus iconos predeterminados.

6. Haga clic en **Personalización finalizada**.

7. Haga clic en su nombre en la parte superior derecha del portal.

8. Haga clic en Cerrar sesión.

9. Cierre el explorador.

## <a name="summary"></a>Resumen

Ahora ha creado y editado paneles, los ha compartido, los ha modificado como archivos .JSON, ha dejado de compartirlos y, por último, los ha restablecido a su estado predeterminado. Ahora debería poder comprobar qué herramientas tan eficaces pueden llegar a ser los paneles y cómo puede utilizarlos para crear interfaces eficientes para diferentes roles dentro de una organización.