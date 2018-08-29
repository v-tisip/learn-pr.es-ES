En este ejercicio, continuará con el ejemplo de una empresa que crea herramientas administrativas con Linux. Recuerde que tiene previsto usar máquinas virtuales Linux para permitir que los clientes potenciales prueben el software. Tiene un grupo de recursos listo y ahora es el momento de crear las máquinas virtuales.

Su empresa ha pagado por un stand en la gran feria de Linux. Planea habilitar un área de demostración que contiene tres terminales, cada una de ellas conectada a una máquina virtual Linux independiente. Al final de cada día, desea eliminar las máquinas virtuales y volver a crearlas, para empezar de cero cada mañana. Crear las máquinas virtuales manualmente después de trabajar cuando está cansado sería una tarea propensa a errores. Desea escribir un script de PowerShell para automatizar el proceso de creación de máquinas virtuales.

## <a name="write-a-script-that-creates-virtual-machines"></a>Escritura de un script que crea máquinas virtuales

Siga estos pasos para escribir el script:

1. Cree un archivo de texto llamado **ConferenceDailyReset.ps1**.

2. Capture el parámetro en una variable:

    ```powershell
    param([string]$resourceGroup)
    ```

3. Autentíquese con sus credenciales en Azure:

    ```powershell
    Connect-AzureRmAccount
    ```

4. Pida un nombre de usuario y una contraseña para la cuenta de administrador de la máquina virtual y capture el resultado en una variable:

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

5. Cree un bucle que se ejecute tres veces:

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

6. En el cuerpo del bucle, cree un nombre para cada máquina virtual y almacénelo en una variable:

    ```powershell
    $vmName = "ConferenceDemo" + $i
    ```

7. A continuación, cree una máquina virtual con la variable `$vmName`:

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" 
   ```

8. Guarde el archivo.

Este es el aspecto que debería tener el script completado:

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

Connect-AzureRmAccount

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i

    New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a>Ejecución del script

Inicie PowerShell y cambie al directorio donde guardó el archivo de script. Para ejecutar el script, ejecute el siguiente comando:

```powershell
.\ConferenceDailyReset.ps1 TrialsResourceGroup
```

El script puede tardar unos minutos en completarse. Cuando haya finalizado, compruebe que se ejecutó correctamente:

1. En un explorador, inicie sesión en Azure Portal.
2. En el panel de navegación de la izquierda, haga clic en **Grupos de recursos**.
3. En la lista de grupos de recursos, haga clic en **TrialsResourceGroup**. En la lista de recursos, debería ver las máquinas virtuales recién creadas y sus recursos asociados.

## <a name="summary"></a>Resumen
Escribió un script que automatizó la creación de tres máquinas virtuales en el grupo de recursos indicado por un parámetro de script. El script es corto y sencillo pero automatiza un proceso que tardaría mucho tiempo en completar manualmente en Azure Portal.