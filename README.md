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

- Son una instancia de ejecución de una imagen.
- Son temporales, si queremos un cambio permanente se tiene que definir en la imagen.
- Es una capa de Lectura/Escritura.
- Se pueden crear varios contenedores a partir de una sola imagen.

Listar contenedores:

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

MySql
Levantar el contenedor
docker run -d --name my-db1 -e MYSQL_ROOT_PASSWORD=12345678 mysql
Chequear el estado
docker logs -f nombre_contenedor
Localmente no vamos a encontrar el servicio de mysql asi que inspeccionamos el contenedor para encontrar la IP.
Inspeccionar el contenedor
docker inspect nombre_contenedor
Acceder al cliente de mysql
mysql -u root -h IP_del_contenedor -p12345678
De esta forma sólo se podrá acceder desde el host pero no desde otra parte de la red.
Para que se pueda acceder desde afuera, publicar el puerto:
docker run -d -p 3306:3306 --name my-db1 -e MYSQL_ROOT_PASSWORD=12345678 mysql
Mongo
Levantar un contenedor
docker run -d --name my-mongo -p 27017:27017 mongo
Chequear uso de RAM
docker stats nombre_contenedor
Usuarios
Ingresar a un contenedor eligiendo el usuario (tiene que estar declarado en la imagen)
docker exec -ti -u nombre_usuario nombre_contenedor bash
Limitar recursos
Limitar RAM
docker run -d -m 500mb nombre_imagen
Limitar CPUs
docker run -d --cpuset-cpus 0-1 nombre_imagen
Asumiendo que tengo 4 CPUs, se autonombran como 0,1, 2 y 3. Con ese comando le indico que use dos CPUs, el 0 y el 1.
Obtener cantidad de CPUs
grep model name /proc/cpuinfo | wc -l
Copiar archivos
Para copiar archivos desde fuera del contenedor hacia dentro del contenedor 
docker cp miarchivo nombre_contenedor:/path/to/copy/file
y viceversa
docker cp nombre_contenedor:/path/file.log /path/to/copy/file
Docker commit
Para convertir un contenedor en una imagen
docker commit nombre_contenedor nombre_imagen_resultante
Es probable que no tome toda la info del dockerfile original. 
No guarda la info de los volúmenes
Sobreescribir un CMD
Para editar el comando sin acceder al dockerfile
docker run -d nombre_imagen comando_al_final
Destrucción automática
Para hacer que un contenedor se elimine automáticamente cuando se deje de utilizar
docker -run --rm -ti centos bash
Cuando se sale del mismo, automáticamente se elimina. Se omite el -d para no enviarlo al fondo.
Document root
Es la jerarquía de directorios que docker crea para funcionar. Para conocer la ubicación del document root
docker info | grep -i root
Se puede cambiar la ubicación

