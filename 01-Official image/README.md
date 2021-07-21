# Official images

Official images are those created by software vendors. For example: Mongo, Apache, etc.

You can find them on https://hub.docker.com

To download an image:

`docker pull image_name[:version]`

Examples:

`docker pull mysql`

`docker pull mysql:latest`

`docker pull mysql:5.7`

https://hub.docker.com/_/mysql

To check your images:

`docker image`

To delete an image:

`docker rmi [name or id]`

Examples:

`docker rmi mysql`
