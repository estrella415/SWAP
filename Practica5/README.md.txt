1. Crear una BD con al menos una tabla y algunos datos.

2. Realizar la copia de seguridad de la BD completa usando mysqldump en la
m�quina principal y copiar el archivo de copia de seguridad a la m�quina
secundaria.

3. Restaurar dicha copia de seguridad en la segunda m�quina (clonado manual
de la BD), de forma que en ambas m�quinas est� esa BD de forma id�ntica.

4. Realizar la configuraci�n maestro-esclavo de los servidores MySQL para que la
replicaci�n de datos se realice autom�ticamente.