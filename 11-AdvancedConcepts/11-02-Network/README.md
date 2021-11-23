# Docker - Network

Every installation of the Docker Engine automatically includes three default networks. 

You can list them:

`docker network ls`

Inspect a network:

`docker network inspect bridge`

Build your image:

`docker build -t 11-02myapp .`

Containers on the same network can connect each other through IP but no through container's name.

Example:

`docker run --name 11-02myapprunningA -p 8086:80 -d  11-02myapp:latest`
`docker run --name 11-02myapprunningB -p 8087:80 -d  11-02myapp:latest`

Find B container's IP

`docker inspect 11-02myapprunningB`

Try to ping B from A:

`docker exec 11-02myapprunningA bash -c “ping ip_containerB”`

`docker exec 11-02myapprunningA bash -c “ping 172.17.0.3”`

Try to ping B from A through container's name: 

`docker exec 11-02myapprunningA bash -c “ping 11-02myapprunningB”`

Clean up:

`docker rm -fv 11-02myapprunningA 11-02myapprunningB`

User-defined network: You can create a network using a Docker network driver or an external network driver plugin.

To create a network:

`docker network create [network_name]`

`docker network create mynet`

You can list:

`docker network ls`

Inspect a network:

`docker network inspect mynet`

To define parameters:

`docker network create -d [driver_name] --subnet [network/mask] --gateway [network_gateway] [network_name]`

`docker network create -d bridge --subnet 172.20.0.0/24 --gateway 172.20.0.1 mynet2`

You can list:

`docker network ls`

Inspect a network:

`docker network inspect mynet2`

Assign a network to a container:

`docker run -d --network [network_name] [image_name]`

`docker run --name 11-02myapprunningA -p 8086:80 -d --network mynet 11-02myapp:latest`

`docker run --name 11-02myapprunningB -p 8087:80 -d --network mynet 11-02myapp:latest`

Try to ping B from A through container's name: 

`docker exec 11-02myapprunningA bash -c “ping 11-02myapprunningB”`

Add (not replace) a network to a container:

`docker network connect [network_name] [container_name]`

`docker network connect mynet2 11-02myapprunningA`

Check:

`docker inspect 11-02myapprunningA`

Disconnect a network:

`docker network disconnect [network_name] [container_name]`

`docker network disconnect mynet 11-02myapprunningA`

Check:

`docker inspect 11-02myapprunningA`

Clean up:

`docker rm -fv 11-02myapprunningA 11-02myapprunningB`

To delete a network:

`docker network rm [network_name]`

`docker network rm mynet mynet2`
