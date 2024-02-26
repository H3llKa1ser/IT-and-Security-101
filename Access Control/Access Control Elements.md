# Overview

### It can be argued that access controls are the heart of an information security program. But in the end, security all comes down to, “who can get access to organizational assets (buildings, data, systems, etc.) and what can they do when they get access?”

### Access controls are not just about restricting access to information systems and data, but also about allowing access. It is about granting the appropriate level of access to authorized personnel and processes and denying access to unauthorized functions or individuals.

### Access is based on 3 elements:

#### 1) Subjects

#### 2) Objects

#### 3) Rules

### Subjects: A subject can be defined as any entity that requests access to our assets. The entity requesting access may be a user, a client, a process or a program, for example. A subject is the initiator of a request for service; therefore, a subject is referred to as “active.”

### A subject:

#### 1) Is a user, a process, a procedure, a client (or a server), a program, a device such as an endpoint, workstation, smartphone or removable storage device with onboard firmware.

#### 2) Is active: It initiates a request for access to resources or services.

#### 3) Requests a service from an object.

#### 4) Should have a level of clearance (permissions) that relates to its ability to successfully access services or resources.

### Objects: By definition, anything that a subject attempts to access is referred to as an object. An object is a device, process, person, user, program, server, client or other entity that responds to a request for service. Whereas a subject is active in that it initiates a request for a service, an object is passive in that it takes no action until called upon by a subject. When requested, an object will respond to the request it receives, and if the request is wrong, the response will probably not be what the subject really wanted either.

### Note that by definition, objects do not contain their own access control logic. Objects are passive, not active (in access control terms), and must be protected from unauthorized access by some other layers of functionality in the system, such as the integrated identity and access management system. An object has an owner, and the owner has the right to determine who or what should be allowed access to their object. Quite often the rules of access are recorded in a rule base or access control list.

### An object:

#### 1) Is a building, a computer, a file, a database, a printer or scanner, a server, a communications resource, a block of memory, an input/output port, a person, a software task, thread or process.

#### 2) Is anything that provides service to a user.

#### 3) Is passive.

#### 4) Responds to a request.

#### 5) May have a classification.

### Rules: An access rule is an instruction developed to allow or deny access to an object by comparing the validated identity of the subject to an access control list. One example of a rule is a firewall access control list. By default, firewalls deny access from any address to any address, on any port. For a firewall to be useful, however, it needs more rules. A rule might be added to allow access from the inside network to the outside network. Here we are describing a rule that allows access to the object “outside network” by the subject having the address “inside network.” In another example, when a user (subject) attempts to access a file (object), a rule validates the level of access, if any, the user should have to that file. To do this, the rule will contain or reference a set of attributes that define what level of access has been determined to be appropriate.

### A rule can:

#### 1) Compare multiple attributes to determine appropriate access.

#### 2) Allow access to an object.

#### 3) Define how much access is allowed.

#### 4) Deny access to an object.

#### 5) Apply time-based access.
