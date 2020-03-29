# Basic docker commands
## Pull an image from Docker Hub
```bash
# Example: pull mysql with specific version (optional)
docker pull mysql:5.7
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

## Display information about hte container
```bash
docker inspect container-name
```

## List docker images
```bash
docker images
```

## List docker containers
```bash
#list running images
docker images ls

#list all images
docker images ls -a

#shorthand command
docker ps -a
```