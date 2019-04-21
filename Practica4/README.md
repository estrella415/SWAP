# Práctica 4: Asegurar la granja web.
## Autores: Estrella Afán de Rivera Díaz y Javier Oliva Cruz.


Los objetivos de esta práctica son los siguientes: 

**1. Instalar un certificado SSL para configurar el acceso HTTPS a los servidores.**

Para ello solo debemos activar el módulo SSL de Apache, generar los certificados y especificarle la ruta a los certificados en la 
configuración. Así pues, como root ejecutaremos:  
*a2enmod ssl  
service apache2 restart  
mkdir /etc/apache2/ssl  
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt*

Completamos los campos que se piden y, a continuación editamos el archivo /etc/apache2/sites-available/default-ssl, agregando
debajo de SSLEngine on:  
*SSLCertificateFile /etc/apache2/ssl/apache.crt  
SSLCertificateKeyFile /etc/apache2/ssl/apache.key*  
 
Por último ejecutamos:  
*a2ensite default-ssl  
service apache2 reload*

Para comprobar el correcto funcionamiento ejecutamos: *curl -k https://ipmaquina1/index.html.*  

Ahora, debemos configurar el balanceador para que también acepte este tráfico (puerto 443). Para
ello, copiamos el .crt y el .key a todas las máquinas de la granja web usando la herramienta tar, tal como se indica en la siguiente imagen:

![img](https://github.com/estrella415/SWAP/blob/master/Practica4/1.png)

(En la máquina de la derecha se ve la salida del curl y el tar a las otras máquinas, y en la máquina de la izquierda se ve el archivo tar correctamente recibido.)

Y por último, en el balanceador editamos el archivo /etc/nginx/conf.d/default.conf tal y como se muestra en la imagen:

![img](https://github.com/estrella415/SWAP/blob/master/Practica4/2.png)

Para comprobar su correcto funcionamiento, usamos la herramienta curl desde la máquina 1 y vemos que el balanceador redirige el trabajo a las dos máquinas servidoras:

![img](https://github.com/estrella415/SWAP/blob/master/Practica4/5.png)

(Donde pone m1 es la máquina 1, la otra es la máquina 2.)  


**2. Configurar las reglas del cortafuegos para proteger la granja web.**

Para comprobar el estado del cortafuegos ejecutamos: *iptables –L –n -v*.  
Para lanzar, reiniciar o parar el cortafuegos, y para salvar las reglas establecidas hasta
ese momento, ejecutaremos respectivamente:  
*service iptables start  
service iptables restart  
service iptables stop  
service iptables save*  

En esta práctica se pide configurar las reglas en una máquina servidora (máquina1) mediante un script, así que creamos un script "reglas" y añadimos las siguientes órdenes:

![img](https://github.com/estrella415/SWAP/blob/master/Practica4/4.png)

Ahora ejecutamos el script y vemos que funciona mediante el comando *iptables –L –n -v*.

![img](https://github.com/estrella415/SWAP/blob/master/Practica4/3.png)

Por último, para que este script se ejecute cada vez que arranquemos el sistema, lo movemos a la carpeta init.d:

![img](https://github.com/estrella415/SWAP/blob/master/Practica4/6.png)























