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

`docker run -d --name nombre_del_contenedor -p 8080:80 nombre_de_la_imagen`

`docker run -d --name hola -p 8080:80 apacheycentos`

(Sin la capa CMD, el contenedor inicia y muere solo)

Para ver la historia de las imágenes:

`docker history -H apacheycentos:latest`

Para ver contenedores activos:

`docker ps -a`

Para borrar contenedor:

`docker rm -fv nombre_del_contenedor`

Para eliminar la imagen:

`docker rmi [tag|nombre|id]`

Ejemplo:

`docker rmi mysql`

`docker rmi mysql apacheycentos`

Cambiar el nombre del dockerfile (si usamos un nombre diferente a “dockerfile”, lo declaramos con -f):

`docker build -t test -f my-dockerfile .`

# Docker Containers

- Listar contenedores:

`docker ps`

Listar contenedores incluyendo aquellos detenidos:

`docker ps -a`

Mapear puertos -> se expone el puerto_del_host:puerto_del_contenedor:

`docker run -d -p 8080:8080 jenkins`

`docker run -d -p 9090:8080 jenkins`

Renombrar contenedor:

`docker rename nombre_antiguo nombre_nuevo`

`docker rename hola hola2`

Detener un contenedor (no lo elimina):

`docker stop nombre_contenedor`

Iniciar un contenedor detenido:

`docker start nombre_contenedor`

Reiniciar un contenedor:

`docker restart nombre_contenedor`

(Estos comandos se usan, por ejemplo, cuando el contenedor está consumiendo mucha RAM y se requiere reiniciarlo.)

Ingresar al operativo de un contenedor:

`docker exec [-u root] -ti nombre_contenedor bash`

- ti: terminal interactive
- u: para elegir el usuario

Eliminar todos los contenedores que están corriendo:

`docker ps -q | xargs docker rm -f`

Crear variable de entorno en el contenedor (no en la imagen):

`docker run -dti -e “variable=valor” --name nombre nombre_imagen`
 
Limitar RAM:

`docker run -d -m 500mb nombre_imagen`

Limitar CPUs:

`docker run -d --cpuset-cpus 0-1 nombre_imagen`

(Asumiendo que tengo 4 CPUs, se autonombran como 0,1, 2 y 3. Con ese comando le indico que use dos CPUs, el 0 y el 1.)

Copiar archivos (para copiar archivos desde fuera del contenedor hacia dentro del contenedor):

`docker cp miarchivo nombre_contenedor:/path/to/copy/file`

y viceversa:

`docker cp nombre_contenedor:/path/file.log /path/to/copy/file`

Para convertir un contenedor en una imagen:

`docker commit nombre_contenedor nombre_imagen_resultante`

Para hacer que un contenedor se elimine automáticamente cuando se deje de utilizar:

`docker -run --rm -ti centos bash`

Cuando se sale del mismo, automáticamente se elimina. Se omite el -d para no enviarlo al fondo.

