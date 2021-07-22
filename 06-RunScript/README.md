# Run a script

Move to folder 06-RunScript

`cd 06-RunScript`

Build the image:

`docker build --tag 06myapp .`

Check your image:

`docker images`

Run your container:

`docker run --name 06myapprunning -p 8083:80 -d 06myapp:latest`

Check active containers:

`docker ps -a`

Verify the scritp:

`docker logs -f container_name`

 - --follow or -f: Follow log output

Example:

`docker logs -f 06myapprunning`

Access to your service:

`http://localhost:8083`

Delete the container:

`docker rm -fv 06myapprunning`