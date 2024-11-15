# Gestión de Imágenes con Docker

## Descargar la imagen Ubuntu:20.04 desde Docker Hub

Para descargar la imagen desde Docker Hub, usé el comando:

docker pull ubuntu:20.04

Este comando descarga la imagen Ubuntu:20.04 en la máquina.

## Obtener toda la información de esa imagen y volcarla al fichero info.txt

Para obtener información detallada sobre la imagen que he descargado, utilizo el comando docker inspect y lo paso a un archivo:

docker inspect ubuntu:20.04 > info.txt

Esto crea un archivo llamado info.txt con toda la información de la imagen.

## Instanciar esa imagen creando un contenedor llamado modulo3

Para crear un contenedor basado en la imagen Ubuntu:20.04, he utilizado el comando:

docker create --name modulo3 ubuntu:20.04

Este comando crea un contenedor llamado modulo3, pero no lo ejecuta.

## Comprobar que el contenedor modulo3 ha sido creado

Para verificar que el contenedor ha sido creado, use:

docker ps -a

Este comando lista todos los contenedores. Si el contenedor modulo3 aparece en la lista, significa que fue creado correctamente.

## Intentar borrar la imagen Ubuntu:20.04

Borro la imagen con:

docker rmi ubuntu:20.04

## ¿Has podido borrarla?

No, no he podido eliminar la imagen si está siendo utilizada por un contenedor. Docker me muestra un error indicando que la imagen está en uso.

## Realizar las operaciones necesarias para poder borrar la imagen

### 1. Detener y eliminar el contenedor asociado a la imagen:

Detenemos el contenedor si está en ejecución:


docker stop modulo3

Eliminamos el contenedor:

docker rm modulo3

### 2. Eliminar la imagen:

Una vez que no haya contenedores utilizando la imagen, podemos eliminarla:

docker rmi ubuntu:20.04

## ![](https://github.com/rbordel2102/Despliegue/blob/master/EjerciciosDocker/06/Captura1.PNG)