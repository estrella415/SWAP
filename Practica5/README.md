# Práctica 5: Replicación de bases de datos MySQL.
## Autores: Estrella Afán de Rivera Díaz y Javier Oliva Cruz.


Los objetivos de esta práctica son los siguientes: 

**1. Crear una BD con al menos una tabla y algunos datos.**

Para ello usamos la interfaz de línea de comandos de MySql, e introducimos los siguientes comandos:

![img](https://github.com/estrella415/SWAP/blob/master/Practica5/1.png)

![img](https://github.com/estrella415/SWAP/blob/master/Practica5/2.png)

Con esto ya tenemos una base de datos con una tabla y varios datos.

**2. Realizar la copia de seguridad de la BD completa y copiar el archivo de copia de seguridad a la máquina secundaria.**

Para ello  usaremos la herramienta mysqldump en la máquina principal (máquina1).  
Antes de hacer la copia de seguridad debemos evitar que se acceda a la BD para cambiar nada. Para ello introducimos el comando 
*FLUSH TABLES WITH READ LOCK;* en la interfaz de MySql, para bloquear el acceso a las tablas.   
Después, introducimos el comando *mysqldump contactos -u root -p > /tmp/contactos.sql*, siendo "contactos" el nombre de la base de datos.  
A continuación, desbloqueamos las tablas con el comando *UNLOCK TABLES;* (desde MySql de nuevo).

![img](https://github.com/estrella415/SWAP/blob/master/Practica5/3.png)


Ahora copiamos el archivo .sql en el esclavo (máquina2) con la herramienta tar, como se indica al final de la siguiente imagen (a la izquierda), 
y vemos como, efectivamente, aparece en el esclavo (a la derecha):

![img](https://github.com/estrella415/SWAP/blob/master/Practica5/4.png)

Por último, importamos la BD en el esclavo con el comando *create database contactos;* (en MySql), y restauramos los datos con  
*mysql -u root -p contactos < /tmp/contactos.sql*.

![img](https://github.com/estrella415/SWAP/blob/master/Practica5/5.png)
