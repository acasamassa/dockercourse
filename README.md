# Docker - Images & Containers

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

