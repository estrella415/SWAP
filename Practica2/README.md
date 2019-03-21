# Práctica 2: Clonar la información de un sitio web.
## Autores: Estrella Afán de Rivera Díaz y Javier Oliva Cruz.


Los objetivos de esta prácticas son los siguientes: 

**1. Probar el funcionamiento de la copia de archivos por ssh:**

Para ello disponemos de la herramienta **tar**. 

Para copiar archivos con tar sólo debemos introducir este comando: *tar czf - directorio | ssh equipodestino 'cat > ~/tar.tgz'*.

![img](https://github.com/estrella415/SWAP/blob/master/Practica2/im6.png)


**2. Clonado de una carpeta entre las dos máquinas:**

Para ello disponemos de la herramienta **rsync**. 

Para clonar archivos con rsync, primero debemos descargarlo: *sudo apt-get install rsync*. A continuación, si queremos continuar con nuestro usuario en lugar de con root, haremos que nuestro usuario sea el dueño de la carpeta donde residen los archivos que hay en el espacio web, para ello introducimos el comando: *sudo chown usuario:usuario –R /var/www*.

Por último, para clonar los archivos, el comando a introducir (en la máquina 2) es: *rsync -avz -e ssh ipmaquina1:/var/www/ /var/www/*. Para comprobar que se han copiado bien, ejecutamos *ls -la /var/www*, tal y como aparece en la siguiente imagen:

![img](https://github.com/estrella415/SWAP/blob/master/Practica2/im1.png)

**3. Configuración de ssh para acceder sin que solicite contraseña:**

Para ello, normalmente se usa autenticación con un par de claves pública-privada.

Los pasos a seguir son los siguientes:
1. En la máquina 2 generamos la clave con keygen: *ssh-keygen -b 4096 -t rsa*.
2. Copiamos la clave a la máquina 1: *ssh-copy-id maquina1*.
3. Ya podemos conectarnos a la máquina 1 sin contraseña: *ssh maquina1*.

Para ejecutar comandos, deberemos añadirlo al final del comando ssh para conectarnos: *ssh maquina1 uname -a*.

A continuación, una captura de todos estos pasos:

![img](https://github.com/estrella415/SWAP/blob/master/Practica2/im3.png)
![img](https://github.com/estrella415/SWAP/blob/master/Practica2/im4.png)


**4. Establecer una tarea en cron que se ejecute cada hora para mantener actualizado el contenido del directorio /var/www entre las dos máquinas:**

Para ello, debemos editar el archivo /etc/crontab, en el cuál cada línea está formada por los siguientes campos:  
Minuto Hora DiaDelMes Mes DiaDeLaSemana Usuario Comando.

Entonces, para que el comando se ejecute cada hora todos los días, añadimos la siguiente línea:   
0 * * * * usuario rsync -avz -e ssh ipmaquina1:/var/www/ /var/www/.

![img](https://github.com/estrella415/SWAP/blob/master/Practica2/im5.png)

