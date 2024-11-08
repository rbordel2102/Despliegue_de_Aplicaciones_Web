# Tarea Docker: Arranque y Manejo de un Contenedor

## Paso 1: Arrancar el contenedor:
docker run -dit --name ubuntu ubuntu:18.04

## Paso 2: Arrancar el contenedor y comprobar que está funcionando:
docker start ubuntu
docker ps

## Paso 3: Mostrar el archivo /etc/os-release sin entrar al contenedor:
docker exec ubuntu cat /etc/os-release

## ![](https://github.com/rbordel2102/Despliegue/blob/master/EjerciciosDocker/03/Captura1.PNG)