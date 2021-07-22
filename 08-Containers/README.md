# Docker Containers

To check active containers:

`docker ps -a`

 - --all or -a: Show all containers (default shows just running)

To run containers:

`docker run -d --name container_name -p host_port:container_port image_name`

 - --detach or -d: Run container in background and print container ID

 - --name: Assign a name to the container

 - --publish or -p: Publish a container's port(s) to the host

Example:

`docker run -d --name 02myapprunning -p 8080:80 02myapp:latest`

Rename a container:

`docker rename container_name new_container_name`

`docker rename 02myapprunning 02myapprunningrenamed`

Stop running containers (not delete):

`docker stop container_name`

Start stopped containers:

`docker start container_name`

Restart one or more containers:

`docker restart container_name`

To delete a container:

`docker rm -fv 02myapprunningrenamed`