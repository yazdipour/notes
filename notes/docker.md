# Docker

https://github.com/wsargent/docker-cheat-sheet
https://docs.docker.com/engine/examples/dotnetcore/

## OnWindows

* https://www.dotnettips.info/post/2947/%da%a9%d8%a7%d8%b1-%d8%a8%d8%a7-docker-%d8%a8%d8%b1-%d8%b1%d9%88%db%8c-%d9%88%db%8c%d9%86%d8%af%d9%88%d8%b2-%d9%82%d8%b3%d9%85%d8%aa-%d8%a7%d9%88%d9%84-container-%da%86%db%8c%d8%b3%d8%aa
* https://www.dotnettips.info/search/label/docker#/page/1/date/desc

## Concepts

### Images

* Images are readonly templates used to create containers.
* Images are created with the docker build command.
* Images are composed of layers of other images.
* Images are stored in a Docker registry.

### Containers

* If an image is a class, then a container is an instance of a class - a runtime object.
* Containers are light weight and portable encapsulations of an environment in which to run applications.
* Containers are created from images. Inside a container, it has all the binaries and dependencies needed to run the application.

### Registries and Repositories

* A registry is where we store our images.
* You can host your own registry, or you can use Docker’s public registry which is called DockerHub.
* Inside a registry, images are stored in repositories.
* Docker repository is a collection of different docker images with the same name, that have different tags, each tag usually represents a different version of the image.

## Command

```shell
# DockerHub Auth
docker login
# List of Running images
# -a for all & exited containers
docker ps -a

# This will find the image from repo:tag (online/offline) and then create and run the container
docker run owner/repo:tag command [args] # command will run in container env
docker run busybox:1.2 echo "hello"
# -i interactive (can use shell inside container)
# -t will create pseudo-TTY
docker run -i -t busybox:1.2
# -d detached/background mode
# --rm will be remove from ps, as soon as finishing
# --name x, will name your container, by default will name sth random
# -p host_port:container_port (access via host_port)
docker run -d --rm --name xyz -p 8888:8080 busybox:1.2
# -v
docker run -p 80:80 -v /DirectPath/toProjSource:/var/www/html/ x:tag # Run Docker with float source (Update server on Code Change)
docker run [container_built_run]

# will show log all info about the container
docker inspect [container id]
# will show all the container logs
docker log [container id]
# shows all available images on the device
docker images
# to stop
docker stop [container id]

# Rename/Tag different name
docker tag [cont_id] shery/debian:tag
# Push to docker hub
docker push shery/debian:tag
# to run command inside running container/login in to container
docker -it [con_id] [bash command]
# --link 2 containers
docker run -d -op 5000:5000 --link redis [container]/dockerapp:v1
```

## Build Image

### Manually

1. First run the base image (for example debian) in intractive mode `docker run -it debian:jessie`
2. make your changes
3. `exit`
4. `docker ps -a`
5. find your container and the commit the changes to a new container
6. `docker commit [container_id] shery/debian:1.0`

### Dockerfile

* Each instruction will create a new image layer to the image.
* Instructions specify what to do when building the image.

1. Create Dockerfile
    ```Dockerfile
    FROM debian:jessie
    RUN apt install -y git && apt install -y vim
    ```
2. `docker build -t shery/debian:1.0 ./path`
    * `./path` = path to the build context.
    * When build starts, docker client would pack all the files in the build context into a tarball then transfer the tarball file to the daemon.
    * By default, docker would search for the Dockerfile in the build context path. Ca specify dockerfile path with `-f df_path`.
    * Can add `--no-cache=true` to forbid docker use your image as cache, for creating future images.

#### FROM

To specify base image

#### RUN

Can be any bash command

#### CMD

* CMD instruction specifies what command you want to run when the container starts up.
* If we don't specify CMD instruction in the Dockerfile, Docker will use the default command defined in the base image.
* **The CMD instruction doesn’t run when building the image, it only runs when the container starts up.**
* You can specify the command in either form which is preferred or in shell form.
* `CMD ["echo","hello"]`

#### COPY

`COPY srcFile_Directory tagetPath`

#### ADD

* Similar to COPY, but also allow you to download file and copy to container.
* ADD also has the ability to automatically unpack compressed files.

#### EXPOSE

### Dockerignore

Docker’s `.dockerignore` file allows you to prevent certain files from being copied into the image. You should always include a .dockerignore file when using the COPY instruction. At minimum, it should include files related to your version control system and locally installed dependencies.

```txt
# .dockerignore
Dockerfile
.dockerignore
# Node
node_modules
npm-debug.log
# ignore .git and .cache folders
.git
.cache
# JAVA - ignore all *.class files in all folders, including build root
**/*.class
# DOCS - ignore all markdown files (md) beside all README*.md other than README-secret.md
*.md
!README*.md
README-secret.md
```

### Docker Compose

* a tool for defining and running multi-container Docker apps.
* `docker-compose.yml`

```docker
version: '3'
services:
  web:
    build: .
    ports:
    - "5000:5000"
    valumes:
    - ./app:/app  #To share data between Container and host. HostDir:ContDir
    - logvolume01:/var/log
  redis:
    image: "redis:alpine"
```

* To build containers

```
$ docker-compose up [-d to run on background]
$ docker-compose down
$ docker-compose stop # Stop all
$ docker-compose logs [con_name]
$ docker-compose rm # Remove all
$ docker-compose build  # to update image
$ docker-compose ps  # to check
```

#### Example

ASP Core Sample

```shell
FROM microsoft/dotnet:latest
COPY . /app
WORKDIR /app
RUN ["dotnet", "restore"]
RUN ["dotnet", "build"]
EXPOSE 5000/tcp                     # TARGET PORT
ENTRYPOINT ["dotnet", "run", "--server.urls", "http://0.0.0.0:5000"]
```

PHP

```shell
FROM php:7.0-apache
COPY src/ /var/www/html/
EXPOSE 80
```

## Network

### Types

* Closed/None Network
  - Disconnected from network
  - `docker run --net none`
* Bridge Network (Default - docker0)
  - Default IP Range from 172.17.0.0 to 172.17.255.255
  - We can access other containers from the same bridge network
* Host/Open Network
  - Like OS Host network
  - `docker run --net host`
* Overlay Network
  - Multi-host, which is handled by kube/swarm

### Inspect Network

* `docker network ls`
* `docker network inspect [NAME]`

### Create network

`docker network create --driver [bridge/host/null] [network_name]`

### Dis/Connect two networks

So that they can ping each other from different ip range.

* `docker network connect [network_name1] [network_name2]`
* `docker network disconnect [network_name1] [network_name2]`

### Compose

```docker
version: '3'
services:
  dockerapp:
    ...
    networks:
      - xnet
  redis:
    networks:
      - xnet

networks:
  xnet:
    driver: bridge
```

Pro Sample

```docker
version: '3'
services:
  proxy:
    networks:
      - front
  app:
    networks:
      - front
      - back
  db:
    networks:
      - back

networks:
  back:
    driver: bridge
    driver_opts:
      foo: "1"
  front:
    driver: bridge
```

### Docker Machine Create command

```docker
docker-machine create --driver digitalocean --digitalocean-access-token <xxxxx> docker-app-machine
```

#### Step 1: Expose environment variables

(If you are using Windows, replace "export" with "set" command)

```docker
export DIGITALOCEAN_ACCESS_TOKEN=<YOUR_DIGITALOCEAN_TOKEN>
export DIGITALOCEAN_PRIVATE_NETWORKING=true
export DIGITALOCEAN_IMAGE=debian-8-x64
```

#### Step 2: Provision consul machine

`docker-machine create -d digitalocean consul`

#### Step 3: Display the network configuration of the consul machine

`docker-machine ssh consul ifconfig`

#### Step 4: Ping the private and public IP address of the consul machine

`ping -c 1 $(docker-machine ssh consul 'ifconfig eth0 | grep "inet addr:" | cut -d: -f2 | cut -d" " -f1')`
`ping -c 1 $(docker-machine ssh consul 'ifconfig eth1 | grep "inet addr:" | cut -d: -f2 | cut -d" " -f1')`

#### Step 5: Export the private IP to KV_IP environment variable

`export KV_IP=$(docker-machine ssh consul 'ifconfig eth1 | grep "inet addr:" | cut -d: -f2 | cut -d" " -f1')`

#### Step 6: Configure Docker client to connect to the consul machine

`eval $(docker-machine env consul)`

#### Step 7: Start the consul container in the consul machine

`docker run -d -p ${KV_IP}:8500:8500 --restart always gliderlabs/consul-server -bootstrap`

Read more:
Consul in Docker
https://hub.docker.com/r/gliderlabs/consul-server/

Bootstrap mode in Consul server
https://www.consul.io/docs/guides/bootstrapping.html

### Create Swarm master

```bash
docker-machine create -d digitalocean --swarm \
  --swarm-master \
  --swarm-discovery="consul://${KV_IP}:8500" \
  --engine-opt="cluster-store=consul://${KV_IP}:8500" \
  --engine-opt="cluster-advertise=eth1:2376" \
  master
```

### Create Swarm slave

```bash
docker-machine create \
  -d digitalocean \
  --swarm \
  --swarm-discovery="consul://${KV_IP}:8500" \
  --engine-opt="cluster-store=consul://${KV_IP}:8500" \
  --engine-opt="cluster-advertise=eth1:2376" \
  slave
```

### “Extends” keywords in Docker Compose File

* The extends keyword enables sharing of common configurations among different files or even different projects entirely
* Extending services is useful if you have several different environments that reuse a common set of configuration options