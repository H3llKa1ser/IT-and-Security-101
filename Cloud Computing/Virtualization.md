# Virtualization

### The foundation for a scalable cloud and the first step for building cloud infrastructure

### Hypervisor: A piece of software, hardware or firmware that runs virtual machines

#### 1) Type 1: Native or Bare-Metal

#### 2) Type 2: Hosted

# Types of Virtualization

### Server Virtualization: Multiple Operating Systems can run on one server

### Network Virtualization: Reproduction of a physical network in software

### Desktop Virtualization: Deploying desktops

### Application Virtualization: Applications as a managed service

### Storage Virtualization: Abstracts disks and flash drives

## Definition

### At its most basic level, virtualization is the concept of encapsulating the capabilities and features of a physical machine in a virtual environment, known as a virtual machine.

### But why is virtualization needed? For most organizations and individuals, virtualization comes from a need of the following:

#### 1) Decrease expenses:

 - Physical servers can be expensive, and virtualization can decrease the number of servers or other hardware, or even completely remove physical hardware from a company's infrastructure.

#### 2) Scale:

 -  Without properly implemented DevOps, it may be hard for a company to scale resources as server usage increases. Virtualization makes this process easier and can delegate a server's resources to virtual machines as needed based on usage.

#### 3) Efficiency:

 -  Like scaling, virtualization can also make it easier to decrease the resources allocated to a virtual machine if there is reduced usage.

# Virtualization Structure

### Virtualization is implemented using an engine-machine format, which means that a software or system creates an abstraction layer and allocates resources, while an operating system or application can then be installed on top of this virtualized environment. The operating system installed in a virtual machine is known as a guest OS, as opposed to the host OS on which the virtualization engine is running.

# Hypervisors

### A hypervisor provides the ability to create the abstraction layer between hardware and software. A hypervisor will also generally include some form of management application or software to provide an interface between the end user and the abstraction layer to create or load virtual machines.

### Hypervisors are separated into two categories that are determined by their position relative to the hardware. They can either directly create a lightweight operating system on top of the hardware that is the hypervisor or add a hypervisor as an application on top of a pre-existing operating system.

## Type 1 Hypervisors (Bare Metal Hypervisors)

 - Type 1 hypervisors, also known as bare metal hypervisors, create an abstraction layer directly between hardware and virtual machines without a common operating system between them. Instead, the hypervisor is the operating system and is often headless, with only a web-based management portal remotely accessed. These hypervisors are designed for scale and to deploy a large number of virtual machines at once. They are extremely lightweight to dedicate the most resources to virtual machines.

### Examples of Type 1 hypervisors: 

 - 1) VMWare ESXi
  
 - 2) Proxmox
  
 - 3) VMware vSphere
  
 - 4) Xen
  
 - 5) KVM
  
## Type 2 Hypervisors (Hosted Hypervisors)

 - Type 2 hypervisors, also known as hosted hypervisors, create an abstraction layer from a software application built on top of a pre-existing operating system. Unlike type 1 hypervisors, type 2 hypervisors are often managed directly from the application through a GUI. These hypervisors are often designed for end-users or individuals such as developers and are not strictly designed to run a large number of virtual machines for scale.

### Examples of Type 2 hypervisors:

 - 1) VMware Workstation
  
 - 2) VMware Fusion
  
 - 3) VirtualBox
  
 - 4) Parallels
  
 - 5) QEMU
  
## Hypervisor problems and issues

### Hypervisors work as expected for a large number of use cases but begin to encounter issues when scaling lightweight applications. Microservices give us a good example of an application architecture that encounters issues when deployed from a hypervisor. A microservice is an application structure that is broken up into smaller services that are scalable and use lightweight protocols and features. The lightweight nature of the architecture poses obvious issues to hypervisors that require a large number of virtual machines each with high resource usage.

## Containers are the current solution to the issues encountered with hypervisors at scale.


