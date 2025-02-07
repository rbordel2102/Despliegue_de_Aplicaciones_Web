# Informe de Laboratorio 7: Apache HTTP Server y PHP

## **Ejercicio 7.2: Ejecutando Apache**

### **1. Razón para reiniciar httpd tras cambios en la configuración**

Cuando se realizan cambios en la configuración de Apache (por ejemplo, en el archivo ``httpd.conf``), es necesario reiniciar el servicio ``httpd`` para que los nuevos cambios se apliquen. Esto ocurre porque el servidor Apache solo carga su configuración durante el inicio, y no puede detectar cambios realizados en su configuración mientras está en ejecución.

### **2. Comando ps aux | grep httpd**

- El comando ``ps aux`` muestra una lista de todos los procesos en ejecución junto con información detallada sobre cada proceso. La opción ``a`` muestra procesos de otros usuarios, ``u`` incluye el nombre del usuario, y ``x`` lista los procesos que no están vinculados a una terminal.
- ``grep httpd`` filtra la salida para mostrar solo las líneas que contienen el texto *"httpd"*. 
- El símbolo ``|`` (pipe) permite canalizar la salida de un comando como entrada de otro comando. 

El comando ``ps aux | grep httpd`` muestra información sobre los procesos relacionados con Apache en ejecución.

### **3. Identificación del proceso padre de Apache (PPID)**

El comando ``ps axl | egrep "httpd|PPID"`` permite buscar el identificador de proceso padre (PPID) de Apache, mostrando las cadenas que contienen "httpd" o "PPID" en la salida de ``ps axl``.

---

## **Ejercicio 7.3: Creación de archivos HTML**

### **1. Importancia de los archivos index.htm e index.html**

Los archivos ``index.htm`` e ``index.html`` son importantes porque los servidores web los utilizan como archivos predeterminados para mostrar contenido cuando no se especifica un archivo en la URL.

### **2. Permisos y propietarios del archivo index.html**

Mediante el comando ``ls -l`` se pueden visualizar los permisos, el propietario y el grupo del archivo ``index.html``. Los permisos normalmente permiten lectura y escritura para el propietario, y solo lectura para otros usuarios.

### **3. Creación del archivo test.html**

Se crea un nuevo archivo llamado ``test.html`` con el siguiente contenido:

```html
<html>
<head><title>Página de prueba</title></head>
<body>
<h1>Prueba del servidor Apache</h1>
<p>En construcción</p>
</body>
</html>
```
Se espera que el título aparezca en la barra del navegador y el encabezado principal (``h1``) sea mostrado en grande y en negrita.

---

## **Ejercicio 7.4: Visualización de archivos HTML mediante CLI**

### **1. Diferencias entre CLI y GUI**

- **CLI (Interfaz de Línea de Comandos):** Permite a los usuarios interactuar con el sistema mediante comandos escritos. Es más rápida y eficiente para tareas repetitivas o avanzadas.
- **GUI (Interfaz Gráfica de Usuario):** Ofrece una experiencia visual donde los usuarios interactúan mediante botones e íconos. Es más intuitiva para principiantes.

### **2. Importancia de la dirección IP 127.0.0.1**

La dirección IP ``127.0.0.1`` corresponde al *localhost*, que permite que un dispositivo se comunique consigo mismo. Es utilizada para probar aplicaciones localmente.

### **3. Visualización de test.html con lynx**

Se ejecuta el comando ``lynx 127.0.0.1/test.html`` para visualizar el archivo HTML en la terminal.

---

## **Ejercicio 7.5: Creación y visualización de archivos PHP**

### **1. Funcionalidad de phpinfo()**

La función ``phpinfo();`` muestra información detallada sobre la configuración de PHP, incluyendo extensiones habilitadas, configuraciones de servidor y variables de entorno.

### **2. Visualización del archivo nse.php con lynx**

Se crea un archivo ``nse.php`` con el siguiente contenido:

```php
<?php
phpinfo(); // Test para verificar configuración PHP
?>
```
Ejecutando ``lynx 127.0.0.1/nse.php`` se verifica que la configuración de PHP esté funcionando correctamente.

---

## **Ejercicio 7.6: Edición del archivo hosts**

### **1. Configuración del archivo /etc/hosts**

Se abre el archivo ``/etc/hosts`` con un editor de texto y se añade la siguiente línea:

```
127.0.0.1 www.example.com
```
Esto permite acceder al servidor local utilizando el nombre de dominio ``www.example.com``.

### **2. Prueba de configuración**

Se ejecuta ``lynx www.example.com`` para comprobar que el servidor responde correctamente.

---
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab07_PHP_Server/Captura1.jpg)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab07_PHP_Server/Captura2.jpg)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab07_PHP_Server/Captura3.jpg)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab07_PHP_Server/Captura4.JPG)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab07_PHP_Server/Captura5.JPG)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab07_PHP_Server/Captura6.jpg)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab07_PHP_Server/Captura7.JPG)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab07_PHP_Server/Captura8.JPG)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab07_PHP_Server/Captura9.JPG)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab07_PHP_Server/Captura10.JPG)