Imagine que trabaja en una empresa que crea un conjunto de herramientas de administración de Linux. Su trabajo consiste en ayudar a posibles clientes a probar el software antes de comprarlo. Dado que el software hace cambios en el nivel de raíz del sistema operativo, decidió crear una máquina virtual Linux para cada cliente de prueba. Puede crear todas las máquinas virtuales que necesite y eliminarlas al final de la suscripción de prueba. De este modo, cada cliente empieza con una versión limpia del sistema operativo. 

Para separar estas máquinas virtuales de las máquinas virtuales que la empresa usa para las pruebas internas, creará un grupo de recursos dedicado para alojarlas. Solo necesita un grupo de recursos, por lo que usar Azure PowerShell en modo interactivo es una opción razonable para esta tarea.

## <a name="steps-to-create-a-resource-group"></a>Pasos para crear un grupo de recursos

1. Inicie PowerShell.

1. Importe el módulo en la sesión actual para que pueda acceder a los cmdlets de Azure.

   ```powershell
   Import-Module AzureRM
   ```

1. Conéctese a Azure mediante el comando que se muestra a continuación. Después de escribir el comando, autentíquese con sus credenciales de Azure.

   ```powershell
   Connect-AzureRmAccount
   ```

1. Cree un grupo de recursos.

    ```powershell
    New-AzureRmResourceGroup -Name "TrialsResourceGroup" -Location "East US"
    ```

1. Compruebe que el grupo de recursos se creó correctamente.

    ```powershell
    Get-AzureRmResource | Format-Table
    ```
Otra manera de comprobar si el grupo de recursos se creó correctamente es usar Azure Portal. Para hacerlo, inicie sesión en el portal y navegue a la sección **Grupos de recursos** (ver a continuación). El nuevo grupo de recursos debería mostrarse en la lista.

![Uso del portal para enumerar los grupos de recursos](../media-drafts/6-listing-resource-groups.png)

## <a name="summary"></a>Resumen
En este ejercicio se muestra un patrón común para una sesión interactiva de PowerShell. Usó un cmdlet estándar para importar el módulo AzureRM y después los cmdlets de Azure PowerShell para realizar una tarea específica. Ahora tiene un grupo de recursos en su suscripción y está listo para crear máquinas virtuales.