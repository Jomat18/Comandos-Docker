# Comandos en Docker

> Un container docker es un proceso

### Mostrar la version de Docker
``` bash
docker version
```
### Ver estado y iniciar Daemon de Docker
``` bash
sudo systemctl start docker
sudo systemctl enable docker
sudo systemctl status docker
```
### Mostrar información de Docker
``` bash
docker info
```
### Logearte a Docker Hub para subir tu imagen a un repositorio

``` bash
docker login
docker login -u <<your_dockerhub_username>>
```

### Subir una imagen a Docker Hub
``` bash
docker push <<your_dockerhub_username>>/<<nodejs-image-demo>>
```

### Etiquetado en Docker
``` bash
docker tag <<nodejs-image-demo>> <<your_dockerhub_username>>/<<name-image>>
```

### Deslogearte de Docker Hub
``` bash
docker logout
```

### Mostrar los contenedores
``` bash
docker container ls  -a 
```

### Borrar un Contenedor por su id
``` bash
docker container rm id_container 
```

### Mostrar imagenes creadas
``` bash
docker images  
```

### Borrar una imagen por su ID
``` bash
docker image rm image-id 
```

### Descargar imagenes desde Docker Hub
``` bash
docker pull image_name
```

### Ejemplo descargar la imagen publica de Postgres
``` bash
docker pull postgres
```

### Buscar una imagen
``` bash
docker search postgres
```

### Crear una imagen desde el Dockerfile de la carpeta actual
``` bash
docker build -t <<your_dockerhub_username>>/<<image_name>>:<<version>> . 
```

### Ejemplo
``` bash
docker build -t jl18/node-docker:v1.0.0 .  
```

### Muestra los id todos los contenedores
``` bash
docker ps -aq
```

### Detener todos los contenedores
``` bash
docker stop $(sudo docker ps -aq)
```

### Eliminar todos los contenedores
``` bash
docker rm $(sudo docker ps -aq)
```

### Eliminar todos los contenedores y volumenes
``` bash
docker rm -vf $(sudo docker ps -a -q) 
```

### Eliminar una imagen
``` bash
docker rmi name-image 
```

### Eliminar todas las imagenes
``` bash
docker rmi -f $(sudo docker images -a -q)
```

### Correr un contenedor en el puerto 80 para Docker Host y 8080 para la aplicacion de la imagen, -d significa modo detached
``` bash
docker run --name <<container_name>> -p 80:8080 -d <<your_dockerhub_username>>/<<image_name>>
```
### Ejemplo corriendo un contenedor de la base de datos postgres, postgres escuchara en el puerto 5432 y la entrada al contenedor sera por el puerto 6551
``` bash
docker run -d --name node1 -p 6551:5432 postgres
```

### Corriendo un contenedor del servidor de gitlab a partir de su imagen
``` bash
docker run gitlab/gitlab-ce
```

### Corriendo un contenedor apache a partir de la imagen de apache -p le asigna un puerto automaticamente
``` bash
docker run -p httpd:latest 
```

### exec es para ejecutar un comando en un container
``` bash
docker exec ubuntu cat etc/hosts
```

### Ejecutar un contenedor en modo interactivo
``` bash
docker exec -it id-container
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

### Comunicando contenedores: comunicar name-container, ping apache
``` bash
docker run -it  --link name-container:apache ubuntu:version
```

### Muestra las redes
``` bash
docker network ls
```

### Crear una red
``` bash
docker network create name-red
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
docker kill id-container id-container2 ...
```

### Entrar en un container cuya terminal cerre, pero sigue corriendo. Esto es en el modo -d que es detached cuando se uso docker run
``` bash
docker attach id-container 
```

### 
``` bash
docker logs id-container
```

### Solo muestra las primeras 300 lineas
``` bash
docker logs --tail 300 id-container
```