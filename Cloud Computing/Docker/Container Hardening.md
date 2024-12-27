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
