# Upload image to Docker Hub

Pre-requisite Step:
- Create your Docker hub account. 
- https://hub.docker.com/

Move to folder 05-UploadImage

`cd 05-UploadImage`

To push your image to Docker Hub, first create it following this syntax:

`docker build -t docker_hub_id/image_name:tag .`

Example:

`docker build -t acasamassapwc/dockercourse:05uploadimage .`

Then, push your image:

`docker push docker_hub_id/image_name:tag .`

Example:

`docker push acasamassapwc/dockercourse:05uploadimage`

