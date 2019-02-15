# Docker
https://docs.docker.com/engine/examples/dotnetcore/

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
* You can specify the command in either exec form which is preferred or in shell form.
* `CMD ["echo","hello"]`

#### COPY

`COPY srcFile_Directory tagetPath`

#### ADD

* Similar to COPY, but also allow you to download file and copy to container.
* ADD also has the ability to automatically unpack compressed files.

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