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

Access to your service:

`http://localhost:8083`

Delete the container:

`docker rm -fv 06myapprunning`