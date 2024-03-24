# HTTP Pipelining

### Usually, with HTTP, one request results in one response. If the HTTP pipelining is enabled in the backend server, it will allow the simultaneous sending of two requests with the corresponding responses without waiting for each response. The only way to differentiate between two requests and a big one is by using the Content-Length header, which specifies the length in bytes of each request. The content header is an unnecessary header for most static file contents in a web application, like images or icons, since the backend server will usually not consider it.
