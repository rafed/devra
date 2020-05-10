---
title: Advanced Docker commands
date: 2020-05-09
tags: [docker]
image: "image/docker.jpeg"
draft: true
---

<!-- USE THIS 
https://docs.docker.com/v17.06/get-started/part3/#run-your-new-load-balanced-app
 -->

## Display Docker version and info
{{< highlight bash >}}
# Check Docker version on the machine
$ docker --version

# Show summary of images/containers in the system
$ docker info
{{< / highlight >}}

<!------------------------------------>

## Manage Docker images

{{< highlight bash >}}
# Run a Docker image
$ docker run hello-world

# List Docker images
docker image ls
docker image ls -a  # List all images

# Remove Docker images
docker image rm <image id> # Remove specified image
docker image rm $(docker image ls -a -q) # Remove all images
{{< / highlight >}}

<!------------------------------------>

## Build and run Docker containers

{{< highlight bash >}}
# Create image using this directory's Dockerfile
$ docker build -t friendlyhello .  

# Run "friendlyname" mapping port 4000 to 80
$ docker run -p 4000:80 friendlyhello  
$ docker run -d -p 4000:80 friendlyhello    # In detached mode
{{< / highlight >}}

<!------------------------------------>

## Manage Docker containers

{{< highlight bash >}}
# List Docker containers
$ docker container ls           # list running containers
$ docker container ls --all     # list all containers
$ docker container ls -aq       # all in quiet mode

# Stopping & removing containers
$ docker container stop [id]  # Gracefully stop a container
$ docker container kill [id]  # Force shutdown of a container
$ docker container rm [id]    # Remove specified container
$ docker container rm $(docker container ls -a -q)  # Remove all containers

# Fetch the logs of a container
$ docker logs -f [id]

# Run a command in a running container
$ docker exec -it [id] bash   # bash is the program here
{{< / highlight >}}

<!------------------------------------>

## Managing remotes

{{< highlight bash >}}
# Log in this CLI session using your Docker credentials
$ docker login             

# Tag <image> for upload to registry
$docker tag <image> username/repository:tag

# Upload tagged image to registry
$ docker push username/repository:tag            

# Run image from a registry
$ docker run username/repository:tag                   
{{< / highlight >}}

<!------------------------------------>

## List Docker CLI commands

The commands mentioned above are just the ones that are most useful to me. To know more commands run the following.

{{< highlight bash >}}
# See list of all commands
$ docker 

# Run 'docker COMMAND --help' for more information on a command.
$ docker container --help
{{< / highlight >}}
