# MySQL Server Lab 08

### Configurar MySQL
```sh
cp /etc/my-small.cnf /etc/my.cnf
mysql_install_db
chown -R mysql:mysql /var/lib/mysql
```

## Administración del servicio MySQL
### Iniciar, detener y reiniciar MySQL
```sh
/etc/rc.d/rc.mysqld start
/etc/rc.d/rc.mysqld stop
/etc/rc.d/rc.mysqld restart
```
Para verificar si MySQL está en ejecución:
```sh
ps -ef | grep mysqld
mysqladmin ping
```

## Uso básico de MySQL
Para acceder a MySQL:
```sh
mysql
```
Para ver las bases de datos disponibles:
```sql
SHOW DATABASES;
```
Para crear y eliminar bases de datos:
```sql
CREATE DATABASE database_name;
DROP DATABASE database_name;
```
Para seleccionar una base de datos:
```sql
USE database_name;
```
Para ver las tablas dentro de una base de datos:
```sql
SHOW TABLES;
```

## Ejercicio 8.1
1. Ver usuarios en MySQL:
   ```sql
   SELECT User, Host FROM mysql.user;
   ```
2. Crear, eliminar y seleccionar datos en una tabla:
   ```sql
   CREATE TABLE table_name (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(50)
   );
   DROP TABLE table_name;
   SELECT * FROM table_name;
   INSERT INTO table_name (name) VALUES ('Ejemplo');
   ```
3. Crear la base de datos `nselab` y la tabla `users`:
   ```sql
   CREATE DATABASE nselab;
   USE nselab;
   CREATE TABLE users (
       studentid INT AUTO_INCREMENT PRIMARY KEY,
       firstname VARCHAR(25),
       lastname VARCHAR(25)
   );
   INSERT INTO users (firstname, lastname) VALUES ('Joe', 'Bloggs'), ('Ashley', 'Smith');
   ```

## Ejercicio 8.2 (Opcional)
1. Crear un usuario con privilegios específicos:
   ```sql
   CREATE USER 'adminsec'@'localhost' IDENTIFIED BY 'password';
   GRANT ALL PRIVILEGES ON nselab.* TO 'adminsec'@'localhost';
   FLUSH PRIVILEGES;
   ```
2. Crear una página en PHP para mostrar los datos de la tabla `users`:
   ```php
   <?php
   $conn = new mysqli("localhost", "root", "password", "nselab");
   if ($conn->connect_error) die("Conexión fallida: " . $conn->connect_error);
   $result = $conn->query("SELECT * FROM users");
   while ($row = $result->fetch_assoc()) {
       echo "ID: " . $row["studentid"] . " - Nombre: " . $row["firstname"] . " " . $row["lastname"] . "<br>";
   }
   $conn->close();
   ?>
   
---
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab08_MySQL_Server/Captura1.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab08_MySQL_Server/Captura2.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab08_MySQL_Server/Captura3.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab08_MySQL_Server/Captura4.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab08_MySQL_Server/Captura5.png)
## ![](https://github.com/rbordel2102/Despliegue/blob/master/slack/Lab08_MySQL_Server/Captura6.png)