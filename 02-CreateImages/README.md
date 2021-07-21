# Create images

Move to folder 02-CreateImages

`cd 02-CreateImages/`

Check dockerfile:

`cat dockerfile`

Build the image:

`docker build --tag image_name[:image_tag] path`

`docker build --tag 02myapp .`

`docker build --tag 02myapp:v1 .`

List your images:

`docker images`

Now run your first app:

 - --detach or -d: Run container in background and print container ID

 - --name: Assign a name to the container

 - --publish or -p: Publish a container's port(s) to the host



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

