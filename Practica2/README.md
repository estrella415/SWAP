# Práctica 2: Clonar la información de un sitio web.
## Autores: Estrella Afán de Rivera Díaz y Javier Oliva Cruz.


Los objetivos de esta prácticas son los siguientes: 

**1. probar el funcionamiento de la copia de archivos por ssh:**

Para ello disponemos de 2 herramientas: tar y rsync. 

Para copiar archivos con tar sólo debemos introducir este comando: *tar czf - directorio | ssh equipodestino 'cat > ~/tar.tgz'*.

Para copiar archivos con rsync, primero debemos descargarlo: *sudo apt-get install rsync*. A continuación, si queremos continuar con nuestro usuario en lugar
de con root, haremos que nuestro usuario sea el dueño de la carpeta donde residen los archivos que hay en el espacio web, 
para ello introducimos el comando: *sudo chown usuario:usuario –R /var/www*.

Por último, para copiar los archivos el comando a introducir es: *rsync -avz -e ssh ipmaquina1:/var/www/ /var/www/*. Para comprobar que se han 
copiado bien, ejecutamos *ls -la /var/www*, tal y como aparece en la siguiente imagen:

![img](https://github.com/estrella415/SWAP/blob/master/Practica2/1.png)

**2. clonado de una carpeta entre las dos máquinas:**
**3. configuración de ssh para acceder sin que solicite contraseña:**
**4. establecer una tarea en cron que se ejecute cada hora para mantener actualizado el contenido del directorio /var/www entre las dos máquinas:**

