# Práctica 1: Preparación de las herramientas.
## Autores: Estrella Afán de Rivera Díaz y Javier Oliva Cruz

Para comenzar, se deben instalar 2 máquinas virtuales Ubuntu server, ambas con los servicios de Apache, Mysql y Php (LAMP), siguiendo los pasos de instalación explicados en el guión.

A continuación, realizaremos los objetivos de la práctica:

**1. Conectar ambas máquinas con ssh:**

Para ello, editaremos el archivo /etc/network/interfaces, tal y como aparece en la siguiente imagen:

![img](https://github.com/estrella415/SWAP/blob/master/imagen1.jpg)

También deberemos configurar VirtualBox añadiendo un adaptador de red interna a cada máquina.

Ahora reiniciamos las máquinas y comprobamos su correcto funcionamiento con *ssh maquina2* desde la máquina1 y viceversa. 

![img](https://github.com/estrella415/SWAP/blob/master/imagen2.png)

**2. Conectar ambas máquinas con curl:**

Primero creamos un archivo html *(hola.html)* en el directorio /var/www/html. Desde otra máquina (máquina2), accederemos a este archivo mediante el comando *curl http://direccionIP-maquina1/hola.html*

![img](https://github.com/estrella415/SWAP/blob/master/imagen3.png)
