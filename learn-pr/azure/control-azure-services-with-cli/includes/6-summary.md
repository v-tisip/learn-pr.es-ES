## <a name="module-summary"></a>Resumen de módulo
En este módulo, usó los comandos de la CLI de Azure para crear un grupo de recursos e implementar una aplicación web mediante un pequeño grupo de comandos. Estos comandos se pueden combinar en un script de shell como parte de la solución de automatización.

La CLI de Azure es una buena elección para los menos familiarizados con la línea de comandos y el scripting de Azure. Su sintaxis simple y la compatibilidad multiplataforma ayudan a reducir el riesgo de errores al realizar tareas repetitivas y regulares.

## <a name="cleanup"></a>Limpieza
La ejecución de aplicaciones web genera costos en su suscripción. Quite los recursos innecesarios para evitar gastos innecesarios. La manera más sencilla de limpiar la suscripción de Azure es quitar el grupo de recursos; así, también se eliminan todos los recursos del grupo. Cuando haya terminado con este módulo, ejecute el siguiente cmdlet de Azure PowerShell:

    ```azurecli
    az group delete --resource-group popupResGroup
    ```

Cuando se le pida que confirme la eliminación, responda **Sí**. El comando puede tardar varios minutos en completarse cuando se eliminan los recursos. 