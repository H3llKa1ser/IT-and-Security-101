# Containerisation

### In computing terms, containerisation is the process of packaging an application and the necessary resources (such as libraries and packages) required into one package named a container. The process of packaging applications together makes applications considerably portable and hassle-free to run.

### Modern applications are often complex and usually depend on frameworks and libraries being installed on a device before the application can run. These dependencies can:

 - Be difficult to install depending on the environment the application is running (some operating systems might not even support them!)

 - Create difficulty for developers to diagnose and replicate faults, as it could be a problem with the application's environment - not the application itself!

 - Can often conflict with each other. For example, having multiple versions of Python to run different applications is a headache for the user, and an application may work with one version of Python and not another.

### Containerisation platforms remove this headache by packaging the dependencies together and “isolating” the application’s environment.

## (NOTE: This is not to be confused with "security isolation" in this context!

### If the device supports the containerisation engine, a user will be able to run the application and have the same behaviours.

### containerisation platforms make use of the “namespace” feature of the kernel, which is a feature used so that processes can access resources of the operating system without being able to interact with other processes.

### The isolation offered by namespaces adds a benefit of security because it means that if an application in the container is compromised, usually (unless they share the same namespace), other containers are unaffected.

### Alternatives such as virtual machines will require a whole operating system being installed to run the application (taking up large amounts of disk space and other computing resources such as CPU and RAM)

