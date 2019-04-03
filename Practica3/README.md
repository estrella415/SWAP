# Práctica 3: Balanceo de carga.
## Autores: Estrella Afán de Rivera Díaz y Javier Oliva Cruz.


Los objetivos de esta prácticas son los siguientes: 

**1. Configurar una máquina e instalar el nginx como balanceador de carga.**

Primero, para instalar ngins utilizaremos los siguientes comandos:  
*sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get  
autoremove  
sudo apt-get install nginx  
sudo systemctl start nginx*

Hay que tener en cuenta que en las máquinas balanceadoras, tanto con nginx como con haproxy, hay que tener **apache desinstalado o apagado.**
Comprobamos que funciona, tal y como se muestra en la imagen:

![img](https://github.com/estrella415/SWAP/blob/master/Practica3/1.png)

A continuación, editamos el archivo /etc/nginx/nginx.conf, comentando la línea que dice el guión (*include /etc/nginx/sites-enabled*).  
También borramos el contenido del archivo /etc/nginx/conf.d/default.conf y añadimos lo siguiente:

![img](https://github.com/estrella415/SWAP/blob/master/Practica3/6.jpeg)

Ahora, para probar su correcto funcionamiento ejecutamos desde las máquinas 1 o 2 (las de las sesiones anteriores): *curl http://IP_maquina3*, siendo la máquina 3 la nueva máquina con nginx.

![img](https://github.com/estrella415/SWAP/blob/master/Practica3/2.png)


**2. Configurar una máquina e instalar el haproxy como balanceador de carga.**

Primero instalamos haproxy con el siguiente comando: *sudo apt-get install haproxy*.  
Después, editamos el archivo /etc/haproxy/haproxy.cfg de forma que quede como muestra la imagen:

![img](https://github.com/estrella415/SWAP/blob/master/Practica3/3.jpeg)

A continuación, lanzamos el servicio haproxy mediante el comando: *sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg* y si todo va bien, ya podremos comenzar a hacer peticiones, por ejemplo, con curl (como hicimos con nginx).


**3. Someter a la granja web a una alta carga, generada con la herramienta Apache Benchmark, teniendo primero nginx y después haproxy.**

Para esta parte, creamos una nueva máquina desde la que lanzaremos las peticiones.  
También debemos instalar la herramienta htop en las demás (todas menos la nueva).  
Ejecutamos htop en todas ellas, y en la nueva máquina ejecutamos el comando:  
*ab -n 1000 -c 10 http://192.168.2.121/index.html*.  

En la imagen vemos cómo las máquinas se someten a una carga alta:

![img](https://github.com/estrella415/SWAP/blob/master/Practica3/5.png)
