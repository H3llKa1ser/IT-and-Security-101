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


## Example Dockerfile

    # THIS IS A COMMENT
    # Use Ubuntu 22.04 as the base operating system of the container
    FROM ubuntu:22.04

    # Set the working directory to the root of the container
    WORKDIR / 

    # Create helloworld.txt
    RUN touch helloworld.txt

## TIP: 

Remember, the commands that you can run via the RUN instruction will depend on the operating system you use in the FROM instruction. (In this example, I have chosen Ubuntu. It’s important to remember that the operating systems used in containers are usually very minimal. I.e., don’t expect a command to be there from the start (even commands like curl, ping, etc., may need to be installed.)

## Dockerfile Optimisation

Bloated Dockerfiles are hard to read and maintain and often use a lot of unnecessary storage! For example, you can reduce the size of a docker image (and reduce build time!) using a few ways:

1) Only installing the essential packages. What’s nice about containers is that they’re practically empty from the get-go - we have complete freedom to decide what we want.

2) Removing cached files (such as APT cache or documentation installed with tools). The code within a container will only be executed once (on build!), so we don’t need to store anything for later use.

3) Using minimal base operating systems in our FROM instruction. Even though operating systems for containers such as Ubuntu are already pretty slim, consider using an even more stripped-down version (i.e. ubuntu:22.04-minimal). Or, for example, using Alpine (which can be as small as 5.59MB!).

4) Minimising the number of layers
