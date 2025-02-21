# Análisis del Tráfico de Red

---

## Paso a Paso

### 1. Iniciar sesión en la máquina Slackware
Inicia sesión como usuario root antes de ejecutar los comandos siguientes.

### 2. Listar Interfaces de Red
Ejecuta el siguiente comando para listar las interfaces de red disponibles en el sistema:
```sh
ifconfig | cut -c-10 | tr -d ' ' | tr -s '\n'
```
Ejemplo de salida:
```
eth0
lo
wlan0
```
Dependiendo de la configuración de red, puedes ver `eth0` o `wlan0`. Utiliza el que corresponda en los siguientes pasos.

### 3. Mostrar Direcciones IP
Para obtener detalles de una interfaz específica:
```sh
ifconfig eth0
```
Ejemplo de salida:
```
eth0      Link encap:Ethernet  HWaddr 00:1c:bf:87:25:d2
          inet addr:192.168.0.82  Bcast:192.168.3.255  Mask:255.255.252.0
```
Para extraer solo la dirección IP:
```sh
ifconfig eth0 | egrep -o "inet addr:[^ ]*" | grep -o "[0-9.]*"
```
Salida esperada:
```
192.168.0.82
```

### 4. Suplantación de Dirección MAC
Para cambiar temporalmente la dirección MAC:
```sh
ifconfig eth0 hw ether 00:1c:bf:87:25:d5
```
Nota: Este cambio dura solo hasta el próximo reinicio.

### 5. Consultas DNS
Para obtener la dirección IP de un dominio:
```sh
host google.com
```
Para listar todos los registros DNS:
```sh
nslookup google.com
```
Para agregar una entrada manual en el archivo de hosts:
```sh
echo "192.168.0.9 backupserver" >> /etc/hosts
```

### 6. Visualizar la Tabla de Enrutamiento
Para ver la tabla de enrutamiento:
```sh
route
```
Para mostrar direcciones IP en lugar de nombres de host:
```sh
route -n
```
Para definir una puerta de enlace predeterminada:
```sh
route add default gw 192.168.0.1 wlan0
```

---

## Ejercicio 9.1: Detectar Máquinas Activas en la Red
Para verificar la disponibilidad de dispositivos en la red, crea un script llamado `ping.sh`:
```sh
#!/bin/bash
# Ajusta la dirección base según tu red.
for ip in 192.168.0.{1..255}; do
    ping -c 2 $ip &> /dev/null
    if [ $? -eq 0 ]; then
        echo "$ip está activo"
    fi
done
```
Ejecuta el script:
```sh
bash ping.sh
```
Explicación:
- `ping -c 2 $ip &> /dev/null` envía 2 paquetes de prueba a cada dirección IP.
- `&> /dev/null` oculta la salida del comando para evitar sobrecarga en la terminal.
- `if [ $? -eq 0 ]` verifica si la máquina respondió al ping.

---

## Ejercicio 10.1: Información de Usuarios y Sistema
Antes de responder, reinicia la máquina y realiza algunos intentos de inicio de sesión fallidos.

1. Para ver los intentos de inicio de sesión exitosos y fallidos en las últimas 48 horas:
```sh
last
```
2. Para ver la cantidad de reinicios en las últimas 48 horas:
```sh
last reboot
```
3. Para ver intentos de inicio de sesión fallidos:
```sh
lastb
```
4. Para ver cuánto tiempo lleva encendido el sistema:
```sh
uptime
```
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab09_Network_traffic_analysis/Captura1.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab09_Network_traffic_analysis/Captura2.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab09_Network_traffic_analysis/Captura3.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab09_Network_traffic_analysis/Captura4.png)
