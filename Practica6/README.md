# Práctica 6: Servidor de disco NFS.
## Autores: Estrella Afán de Rivera Díaz y Javier Oliva Cruz.


Los objetivos de esta práctica son los siguientes: 

**1. Configurar una máquina como servidor de disco NFS y exportar una carpeta a los clientes.**

Para ello, en la máquina servidor (máquina1) instalamos las herramientas necesarias con  
*sudo apt-get install nfs-kernel-server nfs-common rpcbind*

Creamos la carpeta que vamos a compartir y le damos permisos:  
*mkdir /dat/compartida  
sudo chown nobody:nogroup /dat/compartida/  
sudo chmod -R 777 /dat/compartida/*  

Editamos el archivo /etc/exports añadiendo las máquinas clientes:

![img](https://github.com/estrella415/SWAP/blob/master/Practica6/1.png)

Y por último reiniciamos el servicio: *sudo service nfs-kernel-server restart*.

**2. Montar en las máquinas cliente la carpeta exportada por el servidor.**

Para esto, en las máquinas clientes (máquina3 y máquina5) instalamos las herramientas necesarias y creamos el punto de montaje:  
*sudo apt-get install nfs-common rpcbind  
cd /home/usuario (en mi caso: cd /home/estrella)  
mkdir carpetacliente  
chmod -R 777 carpetacliente*

Ahora podemos montar la carpeta remota en la nueva: *sudo mount ipmaquina1:/dat/compartida carpetacliente*

![img](https://github.com/estrella415/SWAP/blob/master/Practica6/2.png)

**3. Comprobar que todas las máquinas pueden acceder a los archivos almacenados en la carpeta compartida.**

Para probar que lo anterior ha funcionado, creamos un archivo en una de las máquinas cliente y vemos que las demás máquinas pueden acceder a él:

![img](https://github.com/estrella415/SWAP/blob/master/Practica6/4.png)

**4. Hacer permanente la configuración en los clientes para que monten automáticamente la carpeta compartida al arrancar el sistema.**

Para ello, editamos el archivo /etc/fstab en las máquinas clientes, añadiendo la última línea que aparece en la siguiente imagen, 
para que la carpeta compartida se monte al arrancar el sistema. Reiniciamos el sistema (reboot) y listo.

![img](https://github.com/estrella415/SWAP/blob/master/Practica6/3.png)


