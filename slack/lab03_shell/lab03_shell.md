# Guía Paso a Paso: Laboratorio 3 - Linux y Shell Scripting

---

## Ejercicio 3.1: Crear un Script Bash Ejecutable

1. **Crear un archivo de script:**
   - Abre un editor de texto en la terminal (vi, nano, etc.).
   - Crea un archivo llamado `test.sh` en tu directorio personal:
     ```bash
     vi ~/test.sh
     ```
   - Escribe el siguiente contenido:
     ```bash
     #!/bin/bash
     clear
     echo "Hello World"
     ```

2. **Hacer el archivo ejecutable:**
   - Cambia los permisos del archivo:
     ```bash
     chmod +x ~/test.sh
     ```

3. **Ejecutar el script:**
   - Corre el script con el comando:
     ```bash
     ./test.sh
     ```

4. **Reflexión sobre permisos:**
   - *Pregunta:* ¿Por qué es mala idea usar `chmod 777 test.sh`?
     - Respuesta: Esto da permisos de lectura, escritura y ejecución a todos los usuarios, lo que puede ser un riesgo de seguridad, ya que cualquier persona podría modificar o ejecutar el archivo de manera maliciosa.
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab03_shell/Captura1.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab03_shell/Captura2.png)
---

## Ejercicio 3.2: Crear Nuevos Usuarios

1. **Crear usuarios:**
   - Usa los siguientes comandos para crear dos nuevos usuarios:
     ```bash
     sudo useradd -d /home/bob bob
     sudo mkdir /home/bob
     sudo chown bob:bob /home/bob
     sudo passwd bob
     ```
     - Asigno la contraseña `bob` al usuario.
   - Repito los pasos anteriores para el usuario `smith` con contraseña `smith`.
   ```bash
   sudo useradd -d /home/smith smith
   sudo mkdir /home/smith
   sudo chown smith:smith /home/smith
   sudo passwd smith
     ```
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab03_shell/Captura3.png)

---

## Ejercicio 3.3: Crear un Script Ejecutable Compartido

1. **Crear un directorio público:**
   - Crea un directorio con permisos de lectura y escritura para todos los usuarios:
     ```bash
     sudo mkdir /home/ncs
     sudo chmod 777 /home/ncs
     ```

2. **Crear el script `hello.sh`:**
   - Escribe un script en `/home/ncs`:
     ```bash
     sudo nano /home/ncs/hello.sh
     ```
     Contenido:
     ```bash
     #!/bin/bash
     echo "Hello World"
     ```
   - Haz el script ejecutable:
     ```bash
     sudo chmod +x /home/ncs/hello.sh
     ```

3. **Ejecutar el script:**
   ```bash
   ./hello.sh
   ```

4. **Anotar propiedades:**
   - Usa `ls -l /home/ncs/hello.sh` para ver los permisos y la propiedad del archivo.
   - 
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab03_shell/Captura4.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab03_shell/Captura5.png)

---

## Ejercicio 3.4: Acceder a Archivos desde Diferentes Usuarios

1. **Iniciar sesión como `bob`:**
   - Usa el comando:
     ```bash
     su - bob
     ```
   - Navega a `/home/ncs` y lista el contenido:
     ```bash
     cd /home/ncs
     ls
     ```
   - Ejecuta el script `hello.sh`:
     ```bash
     ./hello.sh
     ```
   - Crea un script `bob.sh`:
     ```bash
     nano /home/ncs/bob.sh
     ```
     Contenido:
     ```bash
     #!/bin/bash
     echo "Hello this is Bob"
     ```
     - Hazlo ejecutable y ejecútalo:
       ```bash
       sudo chmod +x /home/ncs/bob.sh
       ./bob.sh
       ```

2. **Iniciar sesión como `smith`:**
   - Usa el comando:
     ```bash
     su - smith
     ```
   - Repite los pasos anteriores para verificar acceso a los scripts `hello.sh` y `bob.sh`.

## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab03_shell/Captura6.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab03_shell/Captura7.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab03_shell/Captura8.png)
---

## Ejercicio 3.5: Ejercicios Opcionales

1. **Crear un grupo `sysadmins` y asignar usuarios:**
   ```bash
   sudo groupadd sysadmins
   sudo usermod -aG sysadmins bob
   sudo usermod -aG sysadmins smith
   sudo chgrp sysadmins /home/ncs /home/ncs/hello.sh /home/ncs/bob.sh
   ```
   - Verifica si ambos usuarios pueden ejecutar los scripts.

2. **Deshabilitar el usuario `smith`:**
   ```bash
   usermod -L smith
   ```
   - Esto bloquea el acceso al usuario sin eliminarlo.

## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab03_shell/Captura9.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab03_shell/Captura10.png)
---