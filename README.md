# Docker - Imágenes
 - Imágenes oficiales

Imágenes oficiales creadas por las empresas creadoras de productos como Mongo, Apache, etc. Se encuentran en https://hub.docker.com

Para descargar una imagen:

`docker pull nombre_de_la_imagen[:version]`

Ejemplos:

`docker pull mysql`

`docker pull mysql:latest`

`docker pull mysql:5.7`


 - Crear imágenes

Creamos una carpeta para las DockerFiles:

`mkdir docker-images`

Creamos un archivo dockerfile:

`nano dockerfile`

Agregamos el contenido:

```
FROM centos
RUN yum -y install httpd
CMD apachectl -DFOREGROUND
```

En Windows:

```
echo FROM centos >> Dockerfile
echo RUN yum -y install httpd >> Dockerfile
echo CMD apachectl -DFOREGROUND >> Dockerfile
```

Construimos la imagen:

`docker build --tag nombre_de_la_imagen[:tag_de_la_imagen] path_del_archivo`

`docker build --tag apacheycentos .`

`docker build --tag apacheycentos:1 .`

(Tiene que ser lo más automático posible, si no tenemos el -y, el build falla debido a que no hay confirmación)

Para ver las imágenes:

`docker images`

Para levantar el contenedor (-d para que lo haga en segundo plano, -p para definir el puerto -> puerto del server : puerto del contenedor):

`docker run -d --name nombre_del_contenedor -p 80:80 nombre_de_la_imagen`

`docker run -d --name hola -p 80:80 apacheycentos`

(Sin la capa CMD, el contenedor inicia y muere solo)

Para ver la historia de las imágenes:

`docker history -H apacheycentos:latest`

Para ver contenedores activos:

`docker ps -a`

Para borrar contenedor:

`docker rm -fv nombre_del_contenedor`




