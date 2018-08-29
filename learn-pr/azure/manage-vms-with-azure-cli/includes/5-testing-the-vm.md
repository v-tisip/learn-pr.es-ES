<span data-ttu-id="4c2ee-101">Cuando crea una máquina virtual, se le asigna una dirección IP pública a la que se puede acceder a través de Internet y una dirección IP privada que se utiliza en el centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c2ee-101">When you create a virtual machine, it gets assigned a public IP address that is reachable over the Internet, and a private IP address used within the Azure data center.</span></span> <span data-ttu-id="4c2ee-102">Podemos probar rápidamente que la VM de Linux está en funcionamiento mediante la herramienta `ssh`.</span><span class="sxs-lookup"><span data-stu-id="4c2ee-102">We can quickly test that the Linux VM is up and running using the `ssh` tool.</span></span> <span data-ttu-id="4c2ee-103">Recuerde que configuramos nuestro nombre de administrador en `aldis`, por lo que tenemos que especificarlo.</span><span class="sxs-lookup"><span data-stu-id="4c2ee-103">Remember that we set our admin name to `aldis`, so we have to specify that.</span></span>

```azurecli
ssh 168.61.54.62 -l aldis
```

> [!NOTE]
> <span data-ttu-id="4c2ee-104">No necesitamos una contraseña porque generamos un par de claves SSH en el proceso de creación de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4c2ee-104">We don't need a password because we generated an SSH key pair as part of the VM creation.</span></span> <span data-ttu-id="4c2ee-105">La primera vez que use el shell en la máquina virtual, le devolverá un símbolo del sistema acerca de la autenticidad del host.</span><span class="sxs-lookup"><span data-stu-id="4c2ee-105">The first time you shell into the VM, it will give you a prompt about the authenticity of the host.</span></span> 
> 
> <span data-ttu-id="4c2ee-106">Esto es porque llegamos a una dirección IP directamente en lugar de a un nombre de host.</span><span class="sxs-lookup"><span data-stu-id="4c2ee-106">This is because we are hitting an IP address directly instead of a host name.</span></span> <span data-ttu-id="4c2ee-107">Al contestar "Sí" se guardará la dirección IP como un host válido para la conexión y se permitirá que continúe la conexión.</span><span class="sxs-lookup"><span data-stu-id="4c2ee-107">Answering "yes" will save the IP as a valid host for connection and allow the connection to proceed.</span></span>

```
The authenticity of host '168.61.54.62 (168.61.54.62)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '168.61.54.62' (RSA) to the list of known hosts.
```

<span data-ttu-id="4c2ee-108">A continuación, aparecerá un shell remoto donde puede escribir los comandos de Linux.</span><span class="sxs-lookup"><span data-stu-id="4c2ee-108">Then you'll be presented with a remote shell where you can enter Linux commands.</span></span>

```
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

<span data-ttu-id="4c2ee-109">Pruebe algunos comandos como práctica y, cuando haya terminado, cierre la sesión de su cuenta (escriba `logout` o `exit` en el shell).</span><span class="sxs-lookup"><span data-stu-id="4c2ee-109">Try a few commands as practice and when you are finished, sign out of your account (type `logout` or `exit` in the shell).</span></span>