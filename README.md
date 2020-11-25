# Comandos en Docker

> Un contenedor en docker es un proceso

### Evitar escribir sudo al inicio de docker 
Si desea evitar escribir sudo al ejecutar el comando docker, agregue su nombre de usuario al grupo docker:
``` bash
sudo usermod -aG docker ${USER}
```

### Aplicar cambios
Para aplicar la nueva membresía de grupo, cierre la sesión del servidor y vuelva a iniciarla o escriba lo siguiente:
``` bash
su - ${USER}
```
Para continuar, se le solicitará ingresar la contraseña de su usuario.

### Confirmando que se agrego al grupo de docker
Confirme que ahora su usuario se agregó al grupo docker escribiendo lo siguiente:
``` bash
id -nG
```

### Nota 
Para la ejecución de los comandos en adelante, solo escriba docker porque ya es usuario del grupo docker. Si eligio no hacerlo, incluya sudo al principio de los comandos.

### Mostrar la version de Docker, con cualquiera de los siguientes comandos
``` bash
docker version
docker --version
```

### Comandos para el daemon de Docker
``` bash
systemctl status docker
systemctl start docker
systemctl enable docker
```

# Para ver los comandos disponibles en docker escriba
``` bash
docker
```

### Mostrar información de Docker
``` bash
docker info
```

### Buscar una imagen en Docker Hub, por ejemplo de postgres
``` bash
docker search postgres
```

### Buscando la imagen de ubuntu
``` bash
docker search ubuntu
```

### Descargar imagenes desde Docker Hub (repositorio de imagenes)
``` bash
docker pull image_name
```

### Ejemplo descargar la imagen publica de Postgres
``` bash
docker pull postgres
```

### Descargando la imagen de ubuntu
``` bash
docker pull ubuntu
```

### Crear una imagen desde un Dockerfile en la carpeta actual y etiquetarla
``` bash
docker build -t <<your_dockerhub_username>>/<<image_name>>:<<version>> . 
```

### Ejemplo
``` bash
docker build -t jl18/node:v1.0.0 .  
```

### Construir una imagen desde un Dockerfile con la etiqueta webserver
``` bash
docker build -t webserver .  
```

### Etiquetar una imagen en Docker
``` bash
docker tag <<image-name>> <<your_dockerhub_username>>/<<image-name>>
```

### Mostrar las imagenes descargadas o creadas con build
``` bash
docker images  
```

### Borrar una imagen por su ID
``` bash
docker image rm image-id 
```

### Eliminar una imagen por su nombre
``` bash
docker rmi image-name
```

### Eliminar todas las imagenes
``` bash
docker rmi -f $(docker images -aq)
```

### Corriendo contenedores de diferentes imagenes publicas desde Docker hub
``` bash
docker run ansible
docker run mongodb
docker run redis
docker run nodejs
```
### Correr un contenedor en modo interactivo con el comando -it
``` bash
docker run -it ubuntu
```

### Correr un contenedor en el puerto 80 para Docker Host y 8080 para la aplicacion de la imagen, -d significa modo detached
``` bash
docker run --name <<container_name>> -p 80:8080 -d <<your_dockerhub_username>>/<<image_name>>
```

### Ejemplo corriendo un contenedor de la base de datos postgres, postgres escuchara en el puerto 5432 y la entrada al contenedor sera por el puerto 6551
``` bash
docker run -d --name container_name -p 6551:5432 postgres
```

### Corriendo un contenedor del servidor de gitlab a partir de su imagen
``` bash
docker run gitlab/gitlab-ce
```

### Corriendo un contenedor apache a partir de la imagen de apache -p le asigna un puerto automaticamente
``` bash
docker run -p httpd:latest 
```

### Corriendo un contenedor de debian, el contenedor se llamara test y estará en modo detached
``` bash
docker run --name test -d -it debian
```

### Entrar en un container. Esto es en el modo -d que es detached 
``` bash
docker attach test 
```

### Muestra los contenedores corriendo
``` bash
docker ps
```

### Muestra todos los contenedores, esten o no corriendo
``` bash
docker ps -a
```

### Muestra los id de todos los contenedores
``` bash
docker ps -aq
```

### Detener todos los contenedores
``` bash
docker stop $(docker ps -aq)
```

### Eliminar todos los contenedores
``` bash
docker rm $(docker ps -aq)
```

### Eliminar todos los contenedores y volumenes
``` bash
docker rm -vf $(docker ps -aq) 
```

### exec es para ejecutar un comando en un container, dentro del contenedor ubuntu queremos ejecutar el comando cat en el archivo etc/hosts 
``` bash
docker exec ubuntu cat etc/hosts
```

### Ejecutar un contenedor en modo interactivo
``` bash
docker exec -it id-container-or-container-name
```

### Ejemplo
``` bash
docker exec -it postgres bash
su postgres
psql
psql (11.2 (Debian 11.2-1.pgdg90+1))
Type "help" for help.
postgres=#
```

### ejecutando comandos en el contenedor apache, en este caso sobreescribiendo el index.html 
``` bash
docker exec -it httpd:latest /bin/bash
ls
cd htdocs/
ls
echo "<h1>Hello world</h1>" >index.html
exit
```

### ejecutando comandos en el contenedor nginx, en este caso sobreescribiendo el index.html 
``` bash
docker exec -it nginx bash
ls
cd usr/share/nginx/html
ls
echo "<h1>Hello world</h1>" >index.html
exit
```

### Comunicando contenedores: comunicar un contenedor creado name-container con ubuntu
``` bash
docker run -it --link container-name:apache ubuntu:formacion
ping apache
```

### Muestra las redes
``` bash
docker network ls
```

### Crear una red
``` bash
docker network create red-name
``` 

### Muestra información del contenedor
``` bash
docker inspect id-container
```

### Detener un contenedor
``` bash
docker stop id-container
```

### Iniciar un contenedor
``` bash
docker start id-container
```

### Matar varios contenedores(procesos)
``` bash
docker kill id-container id-container2
```

### 
``` bash
docker logs id-container
```

### Solo muestra las primeras 300 lineas
``` bash
docker logs --tail 300 id-container
```

### Logearte a Docker Hub para subir tu imagen a un repositorio publico
``` bash
docker login
docker login -u <<your_dockerhub_username>>
```

### Subir una imagen a Docker Hub
``` bash
docker push <<your_dockerhub_username>>/<<image-name>>
```

### Deslogearte de Docker Hub
``` bash
docker logout
```
