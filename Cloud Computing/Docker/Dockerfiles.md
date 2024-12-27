# Dockerfiles 

## Definition

Dockerfiles play an essential role in Docker. Dockerfiles is a formatted text file which essentially serves as an instruction manual for what containers should do and ultimately assembles a Docker image.

You use Dockerfiles to contain the commands the container should execute when it is built. To get started with Dockerfiles, we need to know some basic syntax and instructions. Dockerfiles are formatted in the following way:

    INSTRUCTION argument

## Instructions table

| Instruction | Description                                                                                                                                  | Example                                   |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------|
| **FROM**    | This instruction sets a build stage for the container as well as setting the base image (operating system). All Dockerfiles must start with this. | `FROM ubuntu`                            |
| **RUN**     | This instruction will execute commands in the container within a new layer.                                                                 | `RUN whoami`                             |
| **COPY**    | This instruction copies files from the local system to the working directory in the container (the syntax is similar to the `cp` command).    | `COPY /home/cmnatic/myfolder/app/`       |
| **WORKDIR** | This instruction sets the working directory of the container (similar to using `cd` on Linux).                                               | `WORKDIR /` (sets to the root filesystem) |
| **CMD**     | This instruction determines what command is run when the container starts (you would use this to start a service or application).            | `CMD /bin/sh -c script.sh`               |
| **EXPOSE**  | This instruction is used to tell the person who runs the container what port they should publish when running the container.                 | `EXPOSE 80` (publish to port 80)         |


