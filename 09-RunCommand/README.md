# Run command

Move to folder 09-RunCommand

`cd 09-RunCommand/`

Run a command in a running container:

`docker exec container_name command`

Example:

`docker run --name 09myapprunning -p 8082:80 -d 04myapp:latest`
`docker exec -u root -ti 09myapprunning bash`

- --user or -u: Username or UID
- --tty or -t: Allocate a pseudo-TTY
- --interactive or -i: Keep STDIN open even if not attached

Copy files/folders between a container and the local filesystem:

`docker cp file.log container_name:/path/to/copy/file.log`
`docker cp container_name:/path/file.log /path/to/copy/file.log`

Example:

`docker exec -u root -ti 09myapprunning bash`

`rm /usr/share/nginx/html/index.html`

`exit`

`docker cp index.html 09myapprunning:/usr/share/nginx/html/index.html`

Access to your service:

`http://localhost:8082`

Delete the container:

`docker rm -fv 09myapprunning`