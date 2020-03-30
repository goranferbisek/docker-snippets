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
# -e for environment options (PASSWORD is mandatory with mysql)
```
A docker container is meant to run a specific process. If the process is stopped or has crashed, the container will exit.

Example:
```bash
docker run ubuntu
# this container stops immediately

docker run ubuntu sleep 10
# this runs for 10 seconds
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
