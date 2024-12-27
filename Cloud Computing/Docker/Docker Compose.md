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

