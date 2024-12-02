
# Dockerfile Tutorial

## 1ª Parte: Crear y subir una imagen personalizada

### Pasos:
1. **Arrancar un contenedor basado en `ubuntu:20.04`**  
   ```bash
   docker run -it ubuntu:20.04
   ```

2. **Realizar las operaciones dentro del contenedor:**
   - Actualiza los repositorios e instala las herramientas necesarias:
     ```bash
     apt update
     apt install -y nano vim inetutils-tools dnsutils
     ```
   - Crea el usuario `usuario` con contraseña `usuario`:
     ```bash
     adduser usuario
     # Sigue las instrucciones y usa "usuario" como contraseña.
     ```

3. **Salir del contenedor** (sin detenerlo) para poder realizar el commit:
   ```bash
   exit
   ```

4. **Guardar el contenedor como una nueva imagen:**
   Encuentra el ID del contenedor:
   ```bash
   docker ps -a
   ```
   Haz un commit del contenedor para crear la imagen:
   ```bash
   docker commit <ID_CONTENEDOR> rbordel/a61
   ```

5. **Subir la imagen a DockerHub:**
   - Inicia sesión en DockerHub:
     ```bash
     docker login
     ```
   - Subir la imagen:
     ```bash
     docker push rbordel/a61
     ```

---

## 2ª Parte: Construir una imagen desde un Dockerfile

### Dockerfile
El contenido del archivo `Dockerfile` debería ser similar al siguiente:

```Dockerfile
# Partimos de la imagen php:7.4-apache
FROM php:7.4-apache

# Instalar nano y git
RUN apt-get update && apt-get install -y nano git

# Crear archivos en el directorio raíz del servidor Apache
WORKDIR /var/www/html
RUN echo "HOLA SOY ROBERTO" > index.html && \
    echo "<?php phpinfo(); ?>" > info.php

# Exponer el puerto 80 para HTTP
EXPOSE 80
```

### Construir la imagen
1. Crea un directorio y guarda el `Dockerfile` dentro de él.
2. Usa el siguiente comando para construir la imagen:
   ```bash
   docker build -t rbordel/a62 .
   ```

3. **Subir la imagen a DockerHub:**
   - Inicia sesión (si no lo has hecho ya):
     ```bash
     docker login
     ```
   - Sube la imagen:
     ```bash
     docker push rbordel/a62
     ```

---

### Verificación Final
Para verificar que las imágenes están correctamente creadas y subidas:
1. Lista las imágenes locales:
   ```bash
   docker images
   ```
2. Verifica las imágenes en DockerHub iniciando sesión en tu cuenta en la web de DockerHub.


## ![](https://github.com/rbordel2102/Despliegue/blob/master/EjerciciosDocker/10/Captura1.PNG)

## ![](https://github.com/rbordel2102/Despliegue/blob/master/EjerciciosDocker/10/Captura2.PNG)

## ![](https://github.com/rbordel2102/Despliegue/blob/master/EjerciciosDocker/10/Captura3.PNG)

## ![](https://github.com/rbordel2102/Despliegue/blob/master/EjerciciosDocker/10/Captura4.PNG)

## ![](https://github.com/rbordel2102/Despliegue/blob/master/EjerciciosDocker/10/Captura5.PNG)