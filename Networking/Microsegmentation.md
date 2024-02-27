# Microsegmentation

### The toolsets of current adversaries are polymorphic in nature and allow threats to bypass static security controls. Modern cyberattacks take advantage of traditional security models to move easily between systems within a data center. Microsegmentation aids in protecting against these threats. A fundamental design requirement of microsegmentation is to understand the protection requirements for traffic within a data center and traffic to and from the internet traffic flows. 

### When organizations avoid infrastructure-centric design paradigms, they are more likely to become more efficient at service delivery in the data center and become apt at detecting and preventing advanced persistent threats. 

### Microsegmentation allows for extremely granular restrictions within the IT environment, to the point where rules can be applied to individual machines and/or users, and these rules can be as detailed and complex as desired.

### For instance, we can limit which IP addresses can communicate to a given machine, at which time of day, with which credentials, and which services those connections can utilize.

### These are logical rules, not physical rules, and do not require additional hardware or manual interaction with the device (that is, the administrator can apply the rules to various machines without having to physically touch each device or the cables connecting it to the networked environment).

### This is the ultimate end state of the defense-in-depth philosophy; no single point of access within the IT environment can lead to broader compromise.

### This is crucial in shared environments, such as the cloud, where more than one customer's data and functionality might reside on the same device(s), and where third-party personnel (administrators/technicians who work for the cloud provider, not the customer) might have physical access to the devices.

### Microsegmentation allows the organization to limit which business functions/units/offices/departments can communicate with others, in order to enforce the concept of least privilege.

### For instance, the Human Resources office probably has employee data that no other business unit should have access to, such as employee home address, salary, medical records, etc. Microsegmentation, like VLANs, can make HR its own distinct IT enclave, so that sensitive data is not available to other business entities, thus reducing the risk of exposure.

### Even in your home, microsegmentation can be used to separate computers from smart TVs, air conditioning, and smart appliances which can be connected and can have vulnerabilities.

### In modern environments, microsegmentation is available because of virtualization and software-defined networking (SDN) technologies. In the cloud, the tools for applying this strategy are often called "virtual private networks (VPN)" or "security groups".
