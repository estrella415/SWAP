1. Crear una BD con al menos una tabla y algunos datos.

2. Realizar la copia de seguridad de la BD completa usando mysqldump en la
máquina principal y copiar el archivo de copia de seguridad a la máquina
secundaria.

3. Restaurar dicha copia de seguridad en la segunda máquina (clonado manual
de la BD), de forma que en ambas máquinas esté esa BD de forma idéntica.

4. Realizar la configuración maestro-esclavo de los servidores MySQL para que la
replicación de datos se realice automáticamente.