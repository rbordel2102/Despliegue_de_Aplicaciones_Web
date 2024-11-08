# Tarea Docker: Obteniendo Información de Contenedores

Partiendo de los contenedores en ejecución de la tarea anterior, utilizo la CLI de Docker para obtener la siguiente información:

## Paso 1: Dirección IP del contenedor web

Para obtener la dirección IP del contenedor web, ejecuto el siguiente comando:

docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' web

## Paso 2: Redirección de puertos del contenedor web
Para ver cómo están mapeados los puertos del contenedor web, ejecuto el siguiente comando:

docker port web

## Paso 3: Dirección IP del contenedor bbdd
Para obtener la dirección IP del contenedor bbdd, ejecuto el siguiente comando:

docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' bbdd

## Paso 4: Redirección de puertos del contenedor bbdd
Para ver cómo están mapeados los puertos del contenedor bbdd, ejecuto el siguiente comando:

docker port bbdd

## ![](https://github.com/rbordel2102/Despliegue/blob/master/EjerciciosDocker/05/Captura1.PNG)