## 1. Crear la carpeta y el fichero index.html
Creo una carpeta llamada saludo:
mkdir saludo
Dentro de esta carpeta, creo un archivo index.html con el siguiente contenido:
<h1>HOLA SOY ROBERTO BORREGO</h1>

## 2. Arrancar los contenedores con Bind Mounts
Arranco el contenedor c1:

docker run -d --name c1 -v $(pwd)/saludo:/var/www/html -p 8181:80 php:7.4-apache

Esto mapea la carpeta local saludo al directorio /var/www/html del contenedor y redirige el puerto 80 del contenedor al puerto 8181.

Arranco el contenedor c2:

docker run -d --name c2 -v $(pwd)/saludo:/var/www/html -p 8282:80 php:7.4-apache

Esto hace lo mismo, pero redirige el puerto 80 al 8282.

## ![](https://github.com/rbordel2102/Despliegue/blob/master/EjerciciosDocker/08/Captura1.PNG)

## ![](https://github.com/rbordel2102/Despliegue/blob/master/EjerciciosDocker/08/Captura2.PNG)
