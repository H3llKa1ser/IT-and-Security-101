# Docker Compose

## Definition

Docker Compose, in summary, allows multiple containers (or applications) to interact with each other when needed while running in isolation from one another.

You may have noticed a problem with Docker so far. More often than not, applications require additional services to run, which we cannot do in a single container. For example, modern - dynamic - websites use services such as databases and a web server. For now on, we will consider each application as a “microservice”.

While we can spin up multiple containers or “microservices” individually and connect them, doing so one by one is cumbersome and inefficient. Docker Compose allows us to create these “microservices” as one singular “service”. 

## Requirements

1) We need Docker Compose installed

2) We need a valid docker-compose.yml file

3) A fundamental understanding of using Docker Compose to build and manage containers.

## Docker Compose Commands Table

| Command  | Explanation                                                                                   | Example                     |
|----------|-----------------------------------------------------------------------------------------------|-----------------------------|
| **up**   | This command will (re)create/build and start the containers specified in the compose file.    | `docker-compose up`         |
| **start**| This command will start (but requires the containers already being built) the containers specified in the compose file. | `docker-compose start`      |
| **down** | This command will stop and delete the containers specified in the compose file.               | `docker-compose down`       |
| **stop** | This command will stop (not delete) the containers specified in the compose file.             | `docker-compose stop`       |
| **build**| This command will build (but will not start) the containers specified in the compose file.    | `docker-compose build`      |

## Documentation

https://docs.docker.com/compose/reference/

## Docker-compose.yml files

The formatting of a docker-compose.yml file is different to that of a Dockerfile. It is important to note that YAML requires indentation (a good practice is two spaces which must be consistent!).

## YAML file contents

| Instruction           | Explanation                                                                                                                                                          | Example                                      |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------|
| **version**           | This is placed at the top of the file and is used to identify what version of Compose the `docker-compose.yml` is written for.                                       | `'3.3'`                                      |
| **services**          | This instruction marks the beginning of the containers to be managed.                                                                                               | `services:`                                  |
| **name (replace value)** | This instruction is where you define the container and its configuration. "name" needs to be replaced with the actual name of the container, i.e., "webserver" or "database". | `webserver`                                  |
| **build**             | This instruction defines the directory containing the Dockerfile for this container/service. (You will need to use this or an image).                               | `./webserver`                                |
| **ports**             | This instruction publishes ports to the exposed ports (this depends on the image/Dockerfile).                                                                       | `'80:80'`                                    |
| **volumes**           | This instruction lists the directories that should be mounted into the container from the host operating system.                                                    | `'./home/cmnatic/webserver/:/var/www/html'` |
| **environment**       | This instruction is used to pass environment variables (not secure), i.e., passwords, usernames, timezone configurations, etc.                                      | `MYSQL_ROOT_PASSWORD=helloworld`            |
| **image**             | This instruction defines what image the container should be built with (you will need to use this or build).                                                        | `mysql:latest`                               |
| **networks**          | This instruction defines what networks the containers will be a part of. Containers can be part of multiple networks (e.g., a web server can only contact one database, but the database can contact multiple web servers). | `ecommerce`                                  |

## Documentation

https://docs.docker.com/compose/compose-file/

## Example Docker-compose.yml file

    version: '3.3'
    services:
      web:
        build: ./web
        networks:
          - ecommerce
        ports:
          - '80:80'


      database:
        image: mysql:latest
        networks:
          - ecommerce
        environment:
          - MYSQL_DATABASE=ecommerce
          - MYSQL_USERNAME=root
          - MYSQL_ROOT_PASSWORD=helloword
    
    networks:
      ecommerce:
  
