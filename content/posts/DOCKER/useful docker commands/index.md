---
title: Useful Docker Commands
date: 2020-05-09
tags: [docker]
image: "docker.jpeg"
---

This guide is a shortlist of the only docker commands you will ever need to know. I keep on forgetting them, so I'm noting them down here. <!--more-->

## Install docker
```bash
$ sudo apt install docker.io

# Do the following so that sudo is not required every time for running
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
```

## Display Docker version and info
{{<highlight bash>}}
# Check Docker version on the machine
$ docker --version

# Show summary of images/containers in the system
$ docker info
{{</highlight>}}

<!------------------------------------>

## Manage Docker images

{{<highlight bash>}}
# Run a Docker image
$ docker run hello-world

# List Docker images
$ docker image ls
$ docker image ls -a  # List all images

# Remove Docker images
$ docker image rm <image id> # Remove specified image
$ docker image rm $(docker image ls -a -q) # Remove all images
$ docker image rm $(docker images -f "dangling=true" -q) # Remove all dangling images
{{</highlight>}}

<!------------------------------------>

## Build and run Docker containers

{{<highlight bash>}}
# Create image using this directory's Dockerfile
$ docker build -t friendlyhello .  

# Run "friendlyname" mapping port 4000 of host to port 80 on container
$ docker run -p 4000:80 friendlyhello       # host-4000:container-80

# Run container in background
$ docker run -d -p 4000:80 friendlyhello    # Detached mode

# Attach a volume
# Saves db files inside container in ~/Desktop/data/db on host machine
docker run -v ~/Desktop/data/db:/data/db  mongo 

{{</highlight >}}

<!------------------------------------>

## Manage Docker containers

{{<highlight bash>}}
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
{{</highlight>}}

<!------------------------------------>

## Managing remotes

{{<highlight bash>}}
# Log in this CLI session using your Docker credentials
$ docker login             

# Tag <image> for upload to registry
$ docker tag <image hash> username/repository:tag

# Or directly tag an image when building it
$ docker build -t username/repository:tag directory/

# Upload tagged image to registry
$ docker push username/repository:tag            

# Run image from a registry
$ docker run username/repository:tag                   
{{</highlight>}}

<!------------------------------------>

## List Docker CLI commands

The commands mentioned above are just the ones that I mostly use. To know more commands run the following.

{{<highlight bash>}}
# See a list of all commands
$ docker 

# Run 'docker COMMAND --help' for more information on a command.
$ docker container --help
{{</highlight>}}
