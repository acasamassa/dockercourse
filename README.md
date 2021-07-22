# Docker - Images & Containers

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

