En este módulo, protegió la configuración del secreto de una aplicación en Azure Key Vault. El código de nuestra aplicación se autentica en el almacén con Managed Service Identity y carga automáticamente los secretos del almacén en el sistema de configuración de ASP.NET Core en el inicio.

## <a name="cleanup"></a>Limpieza

Para limpiar la suscripción de Azure, ejecute el siguiente código en Azure Cloud Shell para eliminar el grupo de recursos que contiene todos los recursos que hemos creado en este módulo.

```console
az group delete --name keyvault-exercise-group
```

Para limpiar el almacenamiento de Cloud Shell, elimine el directorio `KeyVaultDemoApp`.

## <a name="next-steps"></a>Pasos siguientes

Si se tratase de una aplicación real, ¿qué vendría a continuación?

* Colocar todos los secretos de aplicación en los almacenes. Ya no hay ninguna razón para tenerlos en archivos de configuración.
* Seguir desarrollando la aplicación. El entorno de producción está completamente configurado, por lo que no tendrá que repetir la instalación en las implementaciones futuras.
* Para admitir el desarrollo, cree un almacén de entorno de desarrollo que contenga secretos con los mismos nombres pero distintos valores. Conceda permisos al equipo de desarrollo y configure el nombre del almacén en el archivo de configuración del entorno de desarrollo de la aplicación. Cuando los desarrolladores ejecutan la aplicación localmente, `AddAzureKeyVault` detectará automáticamente las instalaciones locales de Visual Studio y la CLI de Azure y usará las credenciales de Azure configuradas en esas aplicaciones para iniciar sesión y acceder al almacén.
* Cree entornos adicionales con fines tales como pruebas de aceptación de usuario.
* Reparta los almacenes entre distintas suscripciones y/o grupos de recursos para aislarlos.
* Conceda acceso a otros almacenes de entorno a las personas adecuadas.

## <a name="further-reading"></a>Lecturas adicionales

* [Documentación de Key Vault](https://docs.microsoft.com/azure/key-vault/)
* [More about AddAzureKeyVault and its advanced options](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x) (Más información sobre AddAzureKeyVault y sus opciones avanzadas)
* [En este tutorial](https://docs.microsoft.com/azure/key-vault/key-vault-use-from-web-application) se explica cómo usar `KeyVaultClient`, incluida su autenticación manual en Azure Active Directory con un secreto de cliente en lugar de MSI.
* [MSI token service documentation](https://docs.microsoft.com/azure/app-service/app-service-managed-service-identity#using-the-rest-protocol) (Documentación del servicio de token de MSI), para implementar el flujo de trabajo de autenticación personalmente