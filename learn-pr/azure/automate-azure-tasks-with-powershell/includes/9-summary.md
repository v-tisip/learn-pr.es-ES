En este módulo, escribió un script para automatizar la creación de varias máquinas virtuales. Aunque el script era relativamente corto, puede ver las posibilidades de combinar bucles, variables y funciones de PowerShell con cmdlets de PowerShell de Azure PowerShell.

Azure PowerShell es una buena opción de automatización para los administradores con experiencia en PowerShell. También merece la pena considerar la combinación de una sintaxis limpia y un eficaz lenguaje de scripting incluso si no está familiarizado con PowerShell. Este nivel de automatización para tareas laboriosas y propensas a errores le ayudará a reducir el tiempo administrativo y aumentar la calidad.

## <a name="cleanup"></a>Limpieza
Las máquinas virtuales aprovisionadas y en ejecución generan gastos en su suscripción. Quite las máquinas virtuales innecesarias para evitar gastos innecesarios. La manera más sencilla de limpiar la suscripción de Azure es quitar el grupo de recursos asociado; así, también se eliminan todas las máquinas virtuales del grupo. Y puede hacer todo esto desde PowerShell. Cuando haya terminado, ejecute el siguiente cmdlet de PowerShell de Azure:

```powershell
Remove-AzureRmResourceGroup -Name TrialsResourceGroup
```

Cuando se le pida que confirme la eliminación, responda **Sí**. Este comando puede tardar varios minutos en completarse.