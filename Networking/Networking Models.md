# Networking Models

### Many different models, architectures and standards exist that provide ways to interconnect different hardware and software systems with each other for the purposes of sharing information, coordinating their activities and accomplishing joint or shared tasks.

### Computers and networks emerge from the integration of communication devices, storage devices, processing devices, security devices, input devices, output devices, operating systems, software, services, data and people.

### Translating the organization’s security needs into safe, reliable and effective network systems needs to start with a simple premise. The purpose of all communications is to exchange information and ideas between people and organizations so that they can get work done.

### Those simple goals can be re-expressed in network (and security) terms such as:

#### 1) Provide reliable, managed communications between hosts (and users)

#### 2) Isolate functions in layers

#### 3) Use packets as the basis of communication

#### 4) Standardize routing, addressing and control

#### 5) Allow layers beyond internetworking to add functionality

#### 6) Be vendor-agnostic, scalable and resilient

### In the most basic form, a network model has at least two layers:

#### 1) Upper layer: The upper layer, also known as the host or application layer, is responsible for managing the integrity of a connection and controlling the session as well as establishing, maintaining and terminating communication sessions between two computers. It is also responsible for transforming data received from the Application Layer into a format that any system can understand. And finally, it allows applications to communicate and determines whether a remote communication partner is available and accessible.

#### 2) Lower layer: The lower layer is often referred to as the media or transport layer and is responsible for receiving bits from the physical connection medium and converting them into a frame. Frames are grouped into standardized sizes. Think of frames as a bucket and the bits as water. If the buckets are sized similarly and the water is contained within the buckets, the data can be transported in a controlled manner. Route data is added to the frames of data to create packets. In other words, a destination address is added to the bucket. Once we have the buckets sorted and ready to go, the host layer takes over.
