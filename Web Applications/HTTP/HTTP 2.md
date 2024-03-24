# HTTP/2

### The second version of the HTTP protocol proposes several changes over the original HTTP specifications. The new protocol intends to overcome the problems inherent to HTTP/1.1 by changing the message format and how the client and server communicate. One of the significant differences is that HTTP/2 requests and responses use a completely binary protocol, unlike HTTP/1.1, which is humanly readable. This is a massive improvement over the older version since it allows any binary information to be sent in a way that is easier for machines to parse without making mistakes.

### The HTTP/2 request has the following components:

#### 1) Pseudo-headers: HTTP/2 defines some headers that start with a colon :. Those headers are the minimum required for a valid HTTP/2 request. (Example: :method, :path,etc)

#### 2) Headers: After the pseudo-headers, we have regular headers like user-agent and content-length. Note that HTTP/2 uses lowercase for header names.

#### 3) Request Body: Like in HTTP/1.1, this contains any additional information sent with the request, like POST parameters, uploaded files and other data.

### Another important change in the structure of a request that may not be obvious is that HTTP/2 establishes precise boundaries for each part of a request or response. Instead of depending on specific characters like \r\n to separate different headers or : to separate the header name from the header value like HTTP/1, HTTP/2 adds fields to track the size of each part of a request (or response).

