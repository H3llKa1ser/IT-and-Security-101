# Docker commands

### 1) Managing Docker images

Pull the latest version of an image

    docker pull IMAGE

Pull a specific version of an image

    docker pull IMAGE:22.04

List images stored on the local system

    docker image ls

Remove an image from the system

    docker image rm IMAGE:22.04

### 2) Managing containers

Run a container with an interactive shell

    docker run -it IMAGE_NAME /bin/bash

Run a container in the background

    docker run -d IMAGE_NAME

Mount a directory or file from the host operating system to a location within the container. The location these files get stored is defined in the Dockerfile

    docker run -v /host/os/directory:/container/directory IMAGE_NAME

Remove the container once the container finishes running whatever it has been instructed to do

    docker run --rm IMAGE_NAME

Bind a port on the host operating system to a port that is being exposed in the container. You would use this instruction if you are running an application or service (such as a web server) in the container and wish to access the application/service by navigating to the IP address.

    docker run -p 80:80 webserver

List running containers

    docker ps

List ALL containers

    docker ps -a

### 3) Build a Docker Image

    docker build -t IMAGE_NAME DOCKERFILE_LOCATION
