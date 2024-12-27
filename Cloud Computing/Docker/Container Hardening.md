# Container Hardening

## Docker Daemon

The Docker daemon  is responsible for processing requests such as managing containers and pulling or uploading images to a Docker registry. Docker can be managed remotely and is often done in CI (Continuous Integration) and CD (Continuous Development) pipelines. For example, pushing and running new code in a container on another host to check for errors.

If an attacker can interact with the Docker daemon, they can interact with the containers and images. For example, they launch their own (malicious) containers or gain access to containers running applications with sensitive information (such as databases).

The Docker daemon is not exposed to the network by default and must be manually configured. However, exposing the Docker daemon is a common practice (especially in cloud environments such as CI/CD pipelines).

Implementing secure communication and authentication methods such as those listed below are extremely important in preventing unauthorised access to the Docker daemon.

### 1) SSH

Developers can interact with other devices running Docker using SSH authentication. To do so, Docker uses contexts which can be thought of as profiles. These profiles allow developers to save and swap between configurations for other devices. For example, a developer may have one context for a device with Docker for development and another context for a device with Docker for production.

#### Note: You must have SSH access to the remote device, and your user account on the remote device must have permission to execute Docker commands.

As the developer, you will need to create the Docker context on your device.

Example:

Create the Docker context

    docker context create

    --docker host=ssh://myuser@remotehost
    --description="Development Environment" 
    development-environment-host 

Switch to our newly created context, where all Docker-related commands will now be executed on the remote host

    docker context use development-environment-host

To exit this context and, for example, use your own Docker engine, you can revert to "default" via docker context use default.

#### Note: This is not entirely secure. For example, a weak SSH password can lead to an attacker being able to authenticate. Strong password hygiene is strongly recommended. Some tips for a strong password have been included below:

1) A high amount of characters (i.e. 12-22+)

2) Special characters such as !, @, #, $

3) Capital letters and numbers placed sporadically throughout (i.e. sUp3rseCreT!PaSSw0rd!)

Docker contexts allow you to interact with the Docker daemon directly over SSH, which is a secure and encrypted way of communication.

### 2) TLS Encryption

The Docker daemon can also be interacted with using HTTP/S. This is useful if, for example, a web service or application is going to interact with Docker on a remote device.

To do this securely, we can take advantage of the cryptographic protocol TLS to encrypt the data sent between the devices. When configured in TLS mode, Docker will only accept remote commands from devices that have been signed against the device you wish to execute Docker commands remotely.

Example commands:

  On host (server)

    dockerd --tlsverify --tlscacert=myca.pem --tlscert=myserver-cert.pem --tlskey=myserver-key.pem -H=0.0.0.0:2376

  On host (client)

    docker --tlsverify --tlscacert=myca.pem --tlscert=client-cert.pem --tlskey=client-key.pem -H=SERVERIP:2376 info

  #### Note: It is important to remember that this is not guaranteed to be secure. For example, anyone with a valid certificate and private key can be a "trusted" device. 

  ### Generating a TLS certificate and key arguments table

  | Argument       | Description                                                                                                                             |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| **--tlscacert** | This argument specifies the certificate of the certificate authority. A certificate authority is a trusted entity that issues the certificates used to identify devices. |
| **--tlscert**   | This argument specifies the certificate that is used to identify the device.                                                           |
| **--tlskey**    | This argument specifies the private key that is used to decrypt the communication sent to the device.                                  |

## Control Groups

Control Groups (also known as cgroups) are a feature of the Linux kernel that facilitates restricting and prioritising the number of system resources a process can utilise.

For example, a process such as an application can be restricted to only use a certain amount of RAM or processing power or given priority over other processes. This often improves system stability and allows administrators to track system resource use better.

In the context of Docker, implementing cgroups helps achieve isolation and stability. Because cgroups can be used to determine the number of (or prioritise) resources a container uses, this helps prevent faulty or malicious containers from exhausting a system. Of course, the best mechanism is preventing this from happening, but preventing a container from bringing down a whole system is an excellent second line of defence.

This behaviour is not enabled by default on Docker and must be enabled per container when starting the container. The switches used to specify the limit of resources a container can use have been provided in the table below:

| Type of Resource | Argument                           | Example                                |
|-------------------|------------------------------------|----------------------------------------|
| **CPU**          | `--cpus` (in core count)           | `docker run -it --cpus="1" mycontainer` |
| **Memory**       | `--memory` (in k, m, g for kilobytes, megabytes or gigabytes) | `docker run -it --memory="20m" mycontainer` |

You can also update this setting once the container is running. To do so, use the docker update command, the new memory value, and the container name. For example:

    docker update --memory="40m" mycontainer

You can use the docker inspect containername command to view information about a container (including the resource limits set). If a resource limit is set to 0, this means that no resource limits have been set.

    docker inspect mycontainer

Docker uses namespaces to create isolated environments. For example, namespaces are a way of performing different actions without affecting other processes. Think of these as rooms in an office; each room serves its own individual purpose. What happens in a room in this office will not affect what happens in another office. These namespaces provide security by isolating processes from one another.

## Prevent Over-Privileged Containers

First, we need to understand what privileged containers are in this context. Privileged containers are containers that have unchecked access to the host.

The entire point of containerisation is to "isolate" a container from the host. By running Docker containers in "privileged" mode, the normal security mechanisms to isolate a container from the host are bypassed. While privileged containers can have legitimate uses, for example, running Docker-In-Docker (a container within a container) or for debugging purposes, they are extremely dangerous.

When running a Docker container in “privileged” mode, Docker will assign all possible capabilities to the container, meaning the container can do and access anything on the host (such as filesystems).

### 1) Capabilities

Capabilities are a security feature of Linux that determines what processes can and cannot do on a granular level. Traditionally, processes can either have full root privileges or no privileges at all, which can be dangerous as we may not want to allow a process to have full root privileges as it means it will have unrestricted access to the system.

Capabilities allow us to fine-tune what privileges a process has.

### Example table of some capabilities

| Capability            | Description                                                                                                             | Use Case                                                                                       |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| **CAP_NET_BIND_SERVICE** | This capability allows services to bind to ports, specifically those under 1024, which usually requires root privileges. | Allowing a web server to bind on port 80 without root access.                                 |
| **CAP_SYS_ADMIN**      | This capability provides a variety of administrative privileges, including being able to mount/unmount file systems, changing network settings, performing system reboots, shutdowns, and more. | You may find this capability in a process that automates administrative tasks. For example, modifying a user or starting/stopping a service. |
| **CAP_SYS_RESOURCE**  | This capability allows a process to modify the maximum limit of resources available. For example, a process can use more memory or bandwidth. | This capability can control the number of resources a process can consume on a granular level. This can be either increasing the amount of resources or reducing the amount of resources. |

