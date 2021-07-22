# Commit Image

Move to folder 10-CommitImage

`cd 10-CommitImage/`

Create a new image from a container’s changes:

`docker commit container_name resulting_image_name`

Example:

`docker run --name 10myapprunning -p 8082:80 -d 04myapp:latest`

`docker exec -u root -ti 10myapprunning bash`

`rm /usr/share/nginx/html/index.html`

`exit`

`docker cp index.html 10myapprunning:/usr/share/nginx/html/index.html`

`docker commit 10myapprunning 10myapp`

`docker rm -fv 10myapprunning`

`docker run --name 10myappcommited -p 8082:80 -d 10myapp:latest`

Access to your service:

`http://localhost:8082`


Delete the container:

`docker rm -fv 10myappcommited`