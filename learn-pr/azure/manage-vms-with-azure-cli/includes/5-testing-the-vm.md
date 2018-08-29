Cuando crea una máquina virtual, se le asigna una dirección IP pública a la que se puede acceder a través de Internet y una dirección IP privada que se utiliza en el centro de datos de Azure. Podemos probar rápidamente que la VM de Linux está en funcionamiento mediante la herramienta `ssh`. Recuerde que configuramos nuestro nombre de administrador en `aldis`, por lo que tenemos que especificarlo.

```azurecli
ssh 168.61.54.62 -l aldis
```

> [!NOTE]
> No necesitamos una contraseña porque generamos un par de claves SSH en el proceso de creación de la máquina virtual. La primera vez que use el shell en la máquina virtual, le devolverá un símbolo del sistema acerca de la autenticidad del host. 
> 
> Esto es porque llegamos a una dirección IP directamente en lugar de a un nombre de host. Al contestar "Sí" se guardará la dirección IP como un host válido para la conexión y se permitirá que continúe la conexión.

```
The authenticity of host '168.61.54.62 (168.61.54.62)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '168.61.54.62' (RSA) to the list of known hosts.
```

A continuación, aparecerá un shell remoto donde puede escribir los comandos de Linux.

```
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

Pruebe algunos comandos como práctica y, cuando haya terminado, cierre la sesión de su cuenta (escriba `logout` o `exit` en el shell).