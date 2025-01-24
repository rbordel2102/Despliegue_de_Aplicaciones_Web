# Ejercicios 4.1 a 4.5

---

## **Ejercicio 4.1: Explorando procesos actualmente en ejecución**

### Objetivo:
Identificar el número total de procesos en ejecución y describir los 10 procesos más intensivos en uso de CPU.

### Pasos:
1. Abre una terminal y ejecuta:
   ```bash
   ps aux
   ```
   Esto mostrará una lista completa de los procesos en ejecución.

2. Para identificar los procesos más intensivos en CPU, usa el comando:
   ```bash
   top
   ```
   Presiona `q` para salir de la interfaz de `top`.

3. Anota el total de procesos y los 10 más intensivos en CPU. Puedes obtener información adicional sobre un proceso usando:
   ```bash
   man <nombre_proceso>
   ```

### Descripción de los 10 procesos más intensivos en CPU
1. **systemd**
   - Administrador de servicios del sistema. Es responsable de inicializar el sistema y gestionar procesos en segundo plano.

2. **Xorg**
   - Servidor gráfico que administra la interfaz gráfica de usuario (GUI).

3. **gnome-shell**
   - Proporciona la interfaz de usuario en entornos GNOME, como ventanas y paneles.

4. **firefox**
   - Navegador web utilizado para acceder a internet.

5. **mysql**
   - Sistema de gestión de bases de datos relacional.

6. **apache2**
   - Servidor web que gestiona peticiones HTTP.

7. **vsftpd**
   - Protocolo de transferencia de archivos (FTP).

8. **docker**
   - Plataforma de contenedores que ejecuta aplicaciones en entornos aislados.

9. **python**
   - Intérprete del lenguaje de programación Python.

10. **top**
    - Herramienta de monitoreo en tiempo real de procesos.

---
   

## **Ejercicio 4.2: Explorando procesos de red**

### Objetivo:
Usar `nmap` para identificar los servicios de red en localhost y describir su propósito.

### Pasos:
1. Instala `nmap` si no está disponible:
   ```bash
   sudo apt update && sudo apt install nmap
   ```

2. Ejecuta el siguiente comando:
   ```bash
   nmap localhost
   ```

3. Lista los servicios devueltos por el comando y describe su propósito. Puedes buscar información sobre un servicio con:
   ```bash
   man <nombre_servicio>
   ```

---

## **Ejercicio 4.3: Explorando señales de UNIX**

### Objetivo:
Entender las señales disponibles en UNIX y resumir las más relevantes.

### Pasos:
1. Ejecuta el comando:
   ```bash
   kill -l
   ```
   Esto listará todas las señales disponibles en el sistema.

2. Crea una tabla con la siguiente información para las señales 1 a 9 y cinco más de tu elección (entre 10 y 31):
   - Número de la señal.
   - Nombre de la señal.
   - Breve descripción de su función.

   | Número | Nombre      | Descripción breve                                |
   |--------|-------------|-------------------------------------------------|
   | 1      | SIGHUP      | Reinicia el proceso o recarga su configuración. |
   | 2      | SIGINT      | Interrumpe el proceso desde el teclado.         |
   | 3      | SIGQUIT     | Finaliza el proceso y genera un volcado de núcleo. |
   | 4      | SIGILL      | Indica una instrucción ilegal en el programa.   |
   | 5      | SIGTRAP     | Señal para trampas de depuración.               |
   | 6      | SIGABRT     | Abortó el proceso de forma anormal.             |
   | 7      | SIGBUS      | Error de acceso a memoria.                      |
   | 8      | SIGFPE      | Error de punto flotante, como división por cero.|
   | 9      | SIGKILL     | Termina el proceso inmediatamente.              |
   | 10     | SIGUSR1     | Señal definida por el usuario 1.                |
   | 12     | SIGUSR2     | Señal definida por el usuario 2.                |
   | 13     | SIGPIPE     | Intento de escribir en un pipe sin lector.      |
   | 15     | SIGTERM     | Solicitud para terminar el proceso de forma ordenada. |
   | 19     | SIGSTOP     | Detiene el proceso, no puede ser ignorado.      |

3. Usa referencias académicas para respaldar tu descripción, si es necesario.

---

## **Ejercicio 4.4: Procesos y redes**

### Objetivo:
Habilitar y deshabilitar servicios de red y comprender las diferencias entre `telnet`, `sftp` y `ssh`.

### Pasos:
1. **Habilitar `ftp` y `telnet`:**
   - Edita el archivo de configuración de `inetd`:
     ```bash
     sudo nano /etc/inetd.conf
     ```
   - Busca las líneas correspondientes a `ftp` y `telnet`. Si están comentadas (precedidas por `#`), elimínales el `#` para habilitarlas.

     Ejemplo:
     ```plaintext
     #ftp  stream  tcp  nowait  root  /usr/sbin/tcpd  in.ftpd
     #telnet stream  tcp  nowait  root  /usr/sbin/tcpd  in.telnetd
     ```
     Cambia a:
     ```plaintext
     ftp  stream  tcp  nowait  root  /usr/sbin/tcpd  in.ftpd
     telnet stream  tcp  nowait  root  /usr/sbin/tcpd  in.telnetd
     ```

2. **Instala los paquetes necesarios:**
   - Asegúrate de que los paquetes de los servicios están instalados. Usa los siguientes comandos para instalar `vsftpd` (para FTP) y `telnetd` (para Telnet):
     ```bash
     sudo apt update
     sudo apt install vsftpd telnetd
     ```

3. **Reinicia el daemon `inetd`:**
   - Reinicia `inetd` para que lea los cambios en el archivo de configuración:
     ```bash
     sudo systemctl restart inetd
     ```

4. **Verifica que los servicios están habilitados:**
   - Para probar `ftp`, ejecuta:
     ```bash
     ftp localhost
     ```
   - Para probar `telnet`, ejecuta:
     ```bash
     telnet localhost
     ```

5. **Inicia sesión con el usuario `bob`:**
   - Ingresa las credenciales del usuario `bob` (creado en ejercicios anteriores).
   - En FTP, puedes usar comandos como cargar, descargar, borrar y renombrar archivos.

6. **Deshabilitar `ftp`:**
   - Repite el paso 1 y comenta la línea de `ftp` en `/etc/inetd.conf`.
   - Reinicia `inetd` y verifica que `ftp` ya no esté habilitado.

7. **Responde a las preguntas:**
   - **¿Qué son `sftp` y `ssh`?**
     - `sftp` (Secure File Transfer Protocol) es un protocolo para transferir archivos de manera segura mediante SSH, cifrando la comunicación.
     - `ssh` (Secure Shell) es un protocolo que permite acceder a una máquina de forma remota y segura, utilizando cifrado para proteger la sesión.
   
   - **¿Por qué se desaconseja usar `telnet` en entornos reales?**
     - `telnet` transmite la información, incluidas las credenciales, en texto plano, lo que lo hace vulnerable a intercepciones y ataques. Por esta razón, se prefiere usar `ssh` en su lugar.

---

## **Ejercicio 4.5: Ejercicios opcionales**

### Objetivo:
Realizar tareas adicionales relacionadas con daemons y procesos.

### Pasos:
1. **Reiniciar `inetd` con un solo comando:**
   ```bash
   sudo kill -HUP $(pidof inetd)
   ```

2. **Usar `ftp` como root:**
   - Intenta iniciar sesión como root usando `ftp` y evalúa si es una buena práctica. Considera los riesgos de seguridad asociados.
   - **Respuesta:** No es una buena práctica usar `ftp` como root, ya que este protocolo no cifra las credenciales ni los datos transferidos, exponiendo al sistema a riesgos de seguridad. En su lugar, se recomienda usar `sftp` o `scp`.

3. **Pruebas desde Windows:**
   - Desde una máquina Windows, usa herramientas como `Command Prompt` o `PowerShell` para conectarte vía `ftp` y `telnet` al servidor Debian.
   - Comandos:
     ```
     ftp <ip_debian>
     telnet <ip_debian>
     ```

## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab04_demons/Captura1.PNG)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab04_demons/Captura2.PNG)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab04_demons/Captura3.PNG)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab04_demons/Captura4.1.PNG)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab04_demons/Captura4.2.PNG)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab04_demons/Captura4.3.PNG)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab04_demons/Captura4.4.PNG)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab04_demons/Captura5.PNG)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab04_demons/Captura5.1.PNG)
