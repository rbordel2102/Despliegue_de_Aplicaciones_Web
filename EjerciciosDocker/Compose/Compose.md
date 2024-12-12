# Instalación y Configuración de MediaWiki en Debian usando Docker Compose

Esta guía describe cómo instalar y configurar **MediaWiki** en un entorno Debian utilizando **Docker Compose**. También explica cómo crear una página de prueba y verificar la persistencia de los datos tras reiniciar los contenedores.

---

## Instalar MediaWiki

### 1. Creamos un archivo `docker-compose.yml`
Creamos un archivo `docker-compose.yml` con el siguiente contenido:

```yaml
version: '3.7'
services:
  mediawiki:
    image: mediawiki
    ports:
      - "8080:80"
    volumes:
      - ./mediawiki_data:/var/www/html
  mediawiki_db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: example
    volumes:
      - ./db_data:/var/lib/mysql
```

### 2. Iniciamos los contenedores
Con el siguiente comando:

```bash
sudo docker-compose up -d
```

Verificamos que los contenedores están en ejecución:

```bash
sudo docker-compose ps
```

### 3. Configuramos MediaWiki desde el navegador
1. Abrimos un navegador y accede a `http://localhost:8080`
2. Completa el asistente de instalación de MediaWiki.
3. Descarga el archivo `LocalSettings.php` cuando se te solicite al final de la configuración.

### 4. Copiamos el archivo `LocalSettings.php` al contenedor
1. Muevo el archivo descargado `LocalSettings.php` al directorio del proyecto donde está `docker-compose.yml`.
2. Copio el archivo al contenedor ejecutando:

```bash
sudo docker cp LocalSettings.php mediawiki:/var/www/html/
```

### 5. Crearemos una página de prueba en MediaWiki
1. Accedo nuevamente a `http://localhost:8080`.
2. Inicio sesión con el usuario administrador que configuraste.
3. Creo una página de prueba y verifica que los cambios se guardan correctamente.

---

## Verificamos la persistencia de datos

1. Reinicio los contenedores:

```bash
sudo docker-compose down
sudo docker-compose up -d
```

2. Vuelvo a acceder a `http://localhost:8080` y verifico que:
   - La página de prueba creada en el paso anterior persista.
   - Todos los datos estén intactos.

---

## ![](https://github.com/rbordel2102/Despliegue/blob/master/EjerciciosDocker/Compose/Compose.png)
