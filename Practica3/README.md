# Práctica 3: Balanceo de carga.
## Autores: Estrella Afán de Rivera Díaz y Javier Oliva Cruz.


Los objetivos de esta prácticas son los siguientes: 

**1. Configurar una máquina e instalar el nginx como balanceador de carga.**

Primero, para instalar ngins utilizaremos los siguientes comandos:
*sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get
autoremove
sudo apt-get install nginx
sudo systemctl start nginx*

Comprobamos que funciona, tal y como se muestra en la imagen:

![img](https://github.com/estrella415/SWAP/blob/master/Practica3/1.png)

A continuación, editamos el archivo /etc/nginx/nginx.conf, comentando la línea que dice el guión (*include /etc/nginx/sites-enabled*). 
También borramos el contenido del archivo /etc/nginx/conf.d/default.conf y añadimos lo siguiente:

![img](https://github.com/estrella415/SWAP/blob/master/Practica3/6.jpeg)

Ahora, para probar su correcto funcionamiento ejecutamos *curl http://IP_maquina2* desde la nueva máquina con nginx (la máquina 3).

![img](https://github.com/estrella415/SWAP/blob/master/Practica3/2.png)

**2. Configurar una máquina e instalar el haproxy como balanceador de carga.**

**3. Someter a la granja web a una alta carga, generada con la herramienta Apache Benchmark, teniendo primero nginx y después haproxy.**
