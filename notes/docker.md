# Docker
https://docs.docker.com/engine/examples/dotnetcore/

## Basics

```shell
docker login						# Auth DockerHub

docker ps 							# List of Running images
docker stop (dockerID_from_ps) 		# STOP an image
docker build -t x/y ./dir  			# Build Image in x/y Repository
docker images  						# list of all available  images

docker run -p 80:5000 x/y(tag) # Run Docker (Will clone sources and then run the server)

docker run -p 80:80 -v /DirectPath/toProjSource:/var/www/html/ x/tag # Run Docker with float source (Update server on Code Change)
```

## DockerFile

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