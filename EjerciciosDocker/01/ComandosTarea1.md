# Instalación de Docker en Debian

### Paso 1: Actualizar el índice de paquetes
sudo apt update

### Paso 2: Instalar paquetes necesarios para el uso de HTTPS en apt
sudo apt install apt-transport-https ca-certificates curl software-properties-common

### Paso 3: Añadir la clave GPG oficial de Docker
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

### Paso 4: Añadir el repositorio oficial de Docker a la lista de fuentes de apt
echo "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list

### Paso 5: Actualizar el índice de paquetes nuevamente para incluir el nuevo repositorio
sudo apt update

### Paso 6: Instalar Docker
sudo apt install docker-ce

### Paso 7: Configurar Docker para ejecutarse sin permisos de administrador

# Añadir tu usuario al grupo 'docker'
sudo usermod -aG docker sansanra

# Nota: Es necesario cerrar sesión y volver a iniciarla para que los cambios tengan efecto.

### Paso 8: Verificar la versión de Docker instalada
docker --version

### Paso 9: Ejecutar el contenedor de prueba "Hola Mundo"
docker run hello-world

## ![] 