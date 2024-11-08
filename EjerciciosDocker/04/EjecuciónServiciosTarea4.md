# Tarea Docker: Ejecución de Servicios desde Contenedores

## Paso 1: Arrancar un contenedor web con PHP y Apache

Ejecuta el siguiente comando para iniciar un contenedor llamado web basado en la imagen php:7.3-apache, que será accesible desde tu equipo en el puerto 8181:

docker run -dit --name web -p 8181:80 php:7.3-apache

## Paso 2: Colocar el archivo index.html en el contenedor web
Creo un archivo index.html con el siguiente contenido:

<h1>HOLA SOY ROBERTO BORREGO DELGADO</h1>

Copio el archivo al directorio raíz del servicio web en el contenedor:

docker cp index.html web:/var/www/html/index.html

## Paso 3: Colocar el archivo index.php en el contenedor web
Creo un archivo index.php con el siguiente contenido:

<?php phpinfo(); ?>

Copio el archivo al directorio raíz del contenedor:

docker cp index.php web:/var/www/html/index.php

## Paso 4: Arrancar un contenedor bbdd con MariaDB
Para iniciar un contenedor bbdd usando la imagen mariadb en el puerto 3336 y configurarlo con las variables de entorno necesarias, ejecuto el siguiente comando:

docker run -dit --name bbdd -p 3336:3306 \
-e MYSQL_ROOT_PASSWORD=root \
-e MYSQL_DATABASE=prueba \
-e MYSQL_USER=invitado \
-e MYSQL_PASSWORD=invitado \
mariadb

## ![](https://github.com/rbordel2102/Despliegue/blob/master/EjerciciosDocker/04/Captura1.PNG)

## ![](https://github.com/rbordel2102/Despliegue/blob/master/EjerciciosDocker/04/Captura2.PNG)

## ![](https://github.com/rbordel2102/Despliegue/blob/master/EjerciciosDocker/04/Captura3.PNG)