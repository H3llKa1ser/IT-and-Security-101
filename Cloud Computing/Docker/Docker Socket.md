# Docker Socket

When you install Docker, there are two programs that get installed:

1) The Docker Client

2) The Docker Server

Docker works in a client/server model. Specifically, these two programs communicate with each other to form the Docker. Docker achieves this communication using something called a socket. Sockets are an essential feature of the operating system that allows data to be communicated. 

For example, when using a chat program, there could be two sockets:

1) A socket for storing a message that you are sending

2) A socket for storing a message that someone is sending you.

The program will interact with these two sockets to store or retrieve the data within them! A socket can either be a network connection or what is represented as a file. What's important to know about sockets is that they allow for Interprocess Communication (IPC). This simply means that processes on an operating system can communicate with each other!

In the context of Docker, the Docker Server is effectively just an API. The Docker Server uses this API to listen for requests, whereas the Docker Client uses the API to send requests.

We can interact with the Docker Server using commands like curl or an API developer tool such as Postman. 

Finally, it's important to note that because of this, the host machine running Docker can be configured to process commands sent from another device. This is an extremely dangerous vulnerability if it is not correctly configured because it means someone can remotely stop, start, and access Docker containers. Despite this, there are use cases where this feature of Docker is extremely helpful!
