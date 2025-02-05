# Laboratorio de Correo Electrónico en Linux

## Envío de Correos Electrónicos

### 1. Envío Interactivo de Correo con `mail`
Para enviar un correo electrónico a **bob** localmente, ejecuta:
```bash
mail -s testing-mail bob@localhost
```
Escribe el mensaje, presionando **[Enter]** después de cada línea, por ejemplo:
```
hola
esto es una prueba
.
```
El punto (`.`) indica el final del mensaje. Si se solicita una copia (Cc), presiona **[Enter]** para omitir.

### 2. Correo Usando `echo` y Pipe
Otra forma de enviar un mensaje:
```bash
echo "Cuerpo del correo." | mail -s "Asunto" bob@anglia.bryant
```
#### Explicación:
- Envía un correo a `bob@anglia.bryant` con el asunto "Asunto" y cuerpo "Cuerpo del correo."

### 3. Correo con Redirección de Archivo
Para enviar un mensaje desde un archivo de texto (por ejemplo, `mensaje.txt`):
```bash
mail -s "nombre-asunto" bob@localhost < mensaje.txt
```
El contenido de `mensaje.txt` será el cuerpo del correo.

---

## Ejercicio 6.1: Enviar Correo con `mail`

1. **Crear y Enviar Archivo de Mensaje:**
   - Crea un archivo de mensaje:
     ```bash
     echo "Este es el contenido del mensaje desde mensaje.txt." > mensaje.txt
     ```
   - Envíalo:
     ```bash
     mail -s "Correo de Prueba" bob@localhost < mensaje.txt
     ```

2. **Explicación del Comando:**
   ```bash
   echo "Bienvenido a Sistemas de Computación en Red" | mail -s "Hola mundo" bob@anglia.bryant -c smith@anglia.bryant -b root@anglia.bryant
   ```
#### Explicación:
- Envía un correo con el asunto **"Hola mundo"**.
- Cuerpo: *"Bienvenido a Sistemas de Computación en Red"*
- Enviado a `bob@anglia.bryant`, con una Cc a `smith@anglia.bryant` y una Bcc a `root@anglia.bryant`.

---

## Leer Correos Electrónicos
Cuando inicies sesión en Slackware, puede aparecer el mensaje “Tienes correo”. Para leer correos:
```bash
mail
```
Se listarán los mensajes no leídos. Dentro de `mail`, puedes:
- **Leer**, **Responder**, **Enviar**, **Eliminar**, **Listar** y **Guardar** mensajes. Usa `?` para ayuda.

### Ejercicio 6.2: Verificar Correo
1. Inicia sesión como **bob**:
   ```bash
   su bob
   ```
2. Ejecuta `mail` para verificar los mensajes.
3. Si no aparecen mensajes, verifica que `sendmail` esté en ejecución. De lo contrario, los correos se almacenan en `/var/spool/mqueue/` y se enviarán una vez que el demonio se inicie.

---

## Explorando el Comando `mail`
Completa lo siguiente como **bob**:

1. **Explorar Funciones de `mail`:**
   - Ejecuta `mail` y usa `?` para ver los comandos disponibles.
   - Aprende a:
     - **Leer** mensajes
     - **Responder**
     - **Enviar** o reenviar correos
     - **Eliminar** mensajes
     - **Listar** y **Guardar** mensajes

2. **Directorio de Correos:**
   - Los correos se almacenan en `/var/spool/mail/`.
   - **Implicaciones de Seguridad:** Permisos de archivo inadecuados pueden permitir que usuarios no autorizados accedan al contenido de los correos.

3. **Interacción con SMTP mediante Telnet:**
   Desde el host de Windows, conéctate al puerto 25 de la VM:
   ```bash
   telnet <IP_VM> 25
   ```
   Sigue un ejemplo de sesión:
   ```
   HELO tu_nombre
   MAIL FROM:<tu_nombre@localhost>
   RCPT TO:<bob@localhost>
   DATA
   Asunto: Asunto del Mensaje
   Cuerpo del Mensaje
   .
   QUIT
   ```
   Esto envía un correo a `bob@localhost` interactuando directamente con el servidor SMTP.

4. **Habilitar POP3:**
   - Edita `/etc/inetd.conf` para asegurarte de que POP3 no esté comentado (elimina `#`).
   - Reinicia el demonio para aplicar los cambios:
     ```bash
     /etc/rc.d/rc.inetd restart
     ```

5. **Interacción con POP3 mediante Telnet:**
   Desde el host de Windows, conéctate al puerto 110:
   ```bash
   telnet <IP_VM> 110
   ```
   Explora comandos como `USER`, `PASS`, `LIST` y `RETR` para interactuar con el servidor POP3.

6. **Puertos Utilizados:**
   - **SMTP:** Puerto **25**
   - **POP3:** Puerto **110**

---

## Ejercicio 6.4: Ejercicios Opcionales

1. **IMAP vs POP3:**
   - **IMAP (Internet Message Access Protocol):** Sincroniza mensajes directamente en el servidor, haciendo que los correos sean accesibles desde múltiples dispositivos.
   - **POP3 (Post Office Protocol 3):** Descarga mensajes al cliente y a menudo los elimina del servidor.

#### Diferencias Clave:
- IMAP es mejor para acceder a correos desde múltiples dispositivos.
- POP3 es más simple y descarga los correos localmente.

2. **PGP (Pretty Good Privacy):**
   - Una herramienta para cifrar comunicaciones por correo electrónico.
   - **Cómo Funciona:** Utiliza claves públicas y privadas. El remitente cifra el mensaje con la clave pública del destinatario, y solo el destinatario puede descifrarlo con su clave privada.

---

## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab06_Email_for_Linux/lab06-1-1.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab06_Email_for_Linux/lab06-2-1.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab06_Email_for_Linux/lab06-3-1.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab06_Email_for_Linux/lab06-3-2.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab06_Email_for_Linux/lab06-3-3.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/lab06_Email_for_Linux/lab06-3-4.png)
