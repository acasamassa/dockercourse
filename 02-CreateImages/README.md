# Create images

Move to folder 02-CreateImages

`cd 02-CreateImages/`

Check dockerfile:

`cat dockerfile`

Build the image:

`docker build --tag image_name[:image_tag] path`

`docker build --tag 02myapp .`

`docker build --tag 02myapp:v1 .`   <-- Use this for the first time

List your images:

`docker images`

Now run your first app:

`docker run -d --name container_name -p host_port:container_port image_name`

 - --detach or -d: Run container in background and print container ID

 - --name: Assign a name to the container

 - --publish or -p: Publish a container's port(s) to the host

`docker run -d --name 02myapprunning -p 8080:80 02myapp`  <-- It will fail because for the tag, now run `docker build --tag 02myapp .`

To check active containers:

`docker ps -a`

 - --all or -a: Show all containers (default shows just running)

Access to your service:

`http://localhost:8080`

To check your image's history:

`docker image history image_name[:version]`

`docker image history 02myapp`

To sisplay detailed information of your image:

`docker image inspect image_name[:version]`

`docker image inspect i02myapp`

To delete a container:

`docker rm -fv container_name`

 - --force or -f: Force the removal of a running container (uses SIGKILL)
 - --volumes or -v: Remove volumes associated with the container

 Example:

`docker rm -fv 02myapprunning`




