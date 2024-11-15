# Gestión de Volúmenes con Docker

## 1. Crear volúmenes

Para crear los volúmenes volumen_datos y volumen_web, use el comando:

docker volume create volumen_datos
docker volume create volumen_web

## 2. Crear y configurar los contenedores

### Contenedor c1

He creado un contenedor llamado c1 basado en la imagen php:7.4-apache, montando el volumen volumen_web en la ruta /var/www/html dentro del contenedor:

docker run -d --name c1 -v volumen_web:/var/www/html php:7.4-apache


### Contenedor c2

He creado también un contenedor llamado c2 basado en la imagen mariadb, montando el volumen volumen_datos en la ruta /var/lib/mysql y he configurado la contraseña del usuario root como admin:

docker run -d --name c2 -v volumen_datos:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=admin mariadb

## 3. Parar y borrar el contenedor c2, y eliminar el volumen volumen_datos

### Parar el contenedor c2

Para detener el contenedor c2, he usado:

docker stop c2


### Borrar el contenedor c2

Para eliminar el contenedor c2, he usado:

docker rm c2

### Borrar el volumen volumen_datos

Una vez eliminado el contenedor, ya he podido borrar el volumen volumen_datos:

docker volume rm volumen_datos

## ![](https://github.com/rbordel2102/Despliegue/blob/master/EjerciciosDocker/07/Captura1.PNG)