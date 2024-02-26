# Open Systems Interconnection (OSI) Model

### The OSI Model was developed to establish a common way to describe the communication structure for interconnected computer systems. The OSI model serves as an abstract framework, or theoretical model, for how protocols should function in an ideal world, on ideal hardware. Thus, the OSI model has become a common conceptual reference that is used to understand the communication of various hierarchical components from software interfaces to physical hardware.

### The OSI model divides networking tasks into seven distinct layers. Each layer is responsible for performing specific tasks or operations with the goal of supporting data exchange (in other words, network communication) between two computers. The layers are interchangeably referenced by name or layer number. For example, Layer 3 is also known as the Network Layer. The layers are ordered specifically to indicate how information flows through the various levels of communication. Each layer communicates directly with the layer above and the layer below it. For example, Layer 3 communicates with both the Data Link (2) and Transport (4) layers.

### The Application, Presentation, and Session Layers (5-7) are commonly referred to simply as data. However, each layer has the potential to perform encapsulation. Encapsulation is the addition of header and possibly a footer (trailer) data by a protocol used at that layer of the OSI model. Encapsulation is particularly important when discussing Transport, Network and Data Link layers (2-4), which all generally include some form of header. At the Physical Layer (1), the data unit is converted into binary, i.e., 01010111, and sent across physical wires such as an ethernet cable.  

### It's worth mapping some common networking terminology to the OSI Model so you can see the value in the conceptual model.

### Examples:

#### 1) When someone references an image file like a JPEG or PNG, we are talking about the Presentation Layer (6). 

#### 2) When discussing logical ports such as NetBIOS, we are discussing the Session Layer (5).

#### 3) When discussing TCP/UDP, we are discussing the Transport Layer (4).

#### 4) When discussing routers sending packets, we are discussing the Network Layer (3). 

#### 5) When discussing switches, bridges or WAPs sending frames, we are discussing the Data Link Layer (2). 

### Encapsulation occurs as the data moves down the OSI model from Application to Physical. As data is encapsulated at each descending layer, the previous layer’s header, payload and footer are all treated as the next layer’s payload. The data unit size increases as we move down the conceptual model and the contents continue to encapsulate.  

### The inverse action occurs as data moves up the OSI model layers from Physical to Application. This process is known as de-encapsulation  (or decapsulation). The header and footer are used to properly interpret the data payload and are then discarded.
