# Basic docker commands
## Pull an image from Docker Hub
```bash
# Example: pull mysql with specific version (optional)
docker pull mysql:5.7
# tag 5.7 used
# default tag is latest
```

## Create a docker container from an image
```bash
docker run -d --name myDB -p 3308:3306 -e MYSQL_ROOT_PASSWORD=password  mysql:5.7

# this command will pull the image if you haven't made a pull command
# -d option for detached mode
# --name option to name your container
# -p HOST:CONTAINER option to publish a container port to the host
# -e for environment variables (PASSWORD is mandatory with mysql)
```
A docker container is meant to run a specific process. If the process is stopped or has crashed, the container will exit.

Example:
```bash
docker run ubuntu
# this container stops immediately

docker run ubuntu sleep 10
# runs for 10 seconds
# this overrides the default docker CMD command of the image
# example CMD ["bash"]
```

### Run a command on a running container
```bash
docker exec container-name command params

# example
docker run -d --name ubuntu-box ubuntu sleep 100
docker exec ubuntu-box cat /etc/hosts
```
### Attach to a running container
```bash
docker attach ubuntu-box
# use container name or id
```
### Run in interactive mode
```bash
docker run -it ubuntu

# i - interactive mode
# t - attach to containers terminal
```

## Display information about the container
```bash
docker inspect container-name
```

## List docker images
```bash
docker images
```

## Removing docker images
```bash
docker rmi nginx
# use image name
# delete all dependent containers beforehand
```

## List docker containers
```bash
#list running containers
docker ps

#list all images
docker ps -a
```

## Remove a container
```bash
# container must be stopped before removing
docker stop container-name
docker rm container-name
```
# Advanced topics
## Volume mapping
How to persist data in a docker container on a MySQL container example?

MySQL keeps data in /var/lib/mysql inside the container.
If you delete the container the data is lost. You can map the data to a directory location on the host machine.

```bash
docker run -v /opt/datadir:/var/lib/mysql mysql
# data is now stored on the host inside /opt/datadir
```

## Log access
When using detached mode you can acces log with
```bash
docker logs container-name
```

# Docker images
To make a custom image you have to write the steps like you would do if you want to deploy an aplication manualy.

Example: Flask app (python framework)
1. get an operating system (ubuntu)
2. update apt repository
3. install dependencies using apt
4. install Python dependecies using pip
5. copy source code to a location (example: /opt)
6. run the web server (flask application)

We put this steps into a **Dockerfile**. See an example here: [Example Docker file](examples/flask-app/Dockerfile)

To build an image from a Dockerfile us:
```bash
docker build -t gferbis/example-flask-app .
# -t tag option to give your image a name
# . Docker file is in the current directory

docker history gferbis/example-flask-app
# see the cached build steps
```

You can publish your image to Dockerhub with:
```bash
docker push gferbis/example-flask-app
# -t tag name option to give your image a name
```