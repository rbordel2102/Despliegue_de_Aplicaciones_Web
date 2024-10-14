# Configuración de DNS en Debian con Bind9

Este documento describe los pasos para instalar y configurar un servidor DNS en Debian utilizando Bind9. Además, mostraremos cómo configurar una zona directa e inversa para el dominio `ejemplo.com` y se comprueba su funcionamiento.

## 1. Instalación de Bind9

Actualizamos el sistema e instalamos Bind9:

```bash
sudo apt update
sudo apt install bind9 bind9utils bind9-doc
```

## 2. Configuración de IP fija

Editamos el archivo `/etc/network/interfaces` para configurar una IP estática:

```bash
sudo nano /etc/network/interfaces
```

Añadimos la configuración:

```bash
auto eth0
iface eth0 inet static
    address 192.168.1.10
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 192.168.1.10
```

## 3. Configuración de `named.conf.options`

Editamos el archivo `/etc/bind/named.conf.options`:

```bash
sudo nano /etc/bind/named.conf.options
```

Añadimos las opciones para las búsquedas directas e inversas:

```bash
options {
    directory "/var/cache/bind";

    allow-query { 192.168.1.0/24; };

    forwarders {
        8.8.8.8;
        8.8.4.4;
    };

    dnssec-validation auto;

    listen-on { 192.168.1.10; };
    listen-on-v6 { none; };
};
```

## 4. Configuración de la zona directa e inversa

### Zona directa (`/etc/bind/db.ejemplo.com`):

```bash
sudo nano /etc/bind/db.ejemplo.com
```

Añadimos el siguiente contenido:

```bash
$TTL 604800
@   IN  SOA ns.ejemplo.com. admin.ejemplo.com. (
            1         ; Serial
            604800     ; Refresh
            86400      ; Retry
            2419200    ; Expire
            604800 )   ; Negative Cache TTL

@   IN  NS  ns.ejemplo.com.
ns  IN  A   192.168.1.10
www IN  A   192.168.1.10
```

### Zona inversa (`/etc/bind/db.192`):

```bash
sudo nano /etc/bind/db.192
```

Añadimos el siguiente contenido:

```bash
$TTL 604800
@   IN  SOA ns.ejemplo.com. admin.ejemplo.com. (
            1         ; Serial
            604800     ; Refresh
            86400      ; Retry
            2419200    ; Expire
            604800 )   ; Negative Cache TTL

@   IN  NS  ns.ejemplo.com.
10  IN  PTR ns.ejemplo.com.
```

## 5. Configuración de `named.conf.local`

Editamos el archivo `/etc/bind/named.conf.local`:

```bash
sudo nano /etc/bind/named.conf.local
```

Añadimos las referencias a las zonas directa e inversa:

```bash
zone "ejemplo.com" {
    type master;
    file "/etc/bind/db.ejemplo.com";
};

zone "1.168.192.in-addr.arpa" {
    type master;
    file "/etc/bind/db.192";
};
```

## 6. Configuración de `/etc/resolv.conf`

Editamos el archivo `/etc/resolv.conf` para apuntar al servidor DNS:

```bash
sudo nano /etc/resolv.conf
```

Añadimos el siguiente contenido:

```bash
nameserver 192.168.1.10
```

## 7. Reiniciar Bind9 y comprobar configuración

Reiniciamos el servicio Bind9:

```bash
sudo systemctl restart bind9
sudo systemctl enable bind9
```

Verificamos que no haya errores de configuración:

```bash
sudo named-checkconf
sudo named-checkzone ejemplo.com /etc/bind/db.ejemplo.com
```

## 8. Comprobación de resolución de nombres

Usamos los comandos `nslookup`, `host` o `dig` para verificar que el DNS está funcionando correctamente:

```bash
nslookup www.ejemplo.com
host www.ejemplo.com
dig www.ejemplo.com
```

La zona directa está configurada correctamente, y vemos la IP `192.168.1.10` en la salida de estos comandos.

---

¡Con esto, el servidor DNS esta configurado y funcionando!
