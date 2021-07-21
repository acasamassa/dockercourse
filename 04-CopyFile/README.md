# Copy file

Move to folder 04-CopyFile

`cd 04-CopyFile/`

Check dockerfile:

`cat dockerfile`

Build your image:

`docker build -t 04myapp .`

Check your image:

`docker images`

Run your container:

`docker run --name 04myapprunning -p 8082:80 -d 04myapp:latest`

Check active containers:

`docker ps -a`

Access to your service:

`http://localhost:8082`

Delete the container:

`docker rm -fv 04myapprunning`