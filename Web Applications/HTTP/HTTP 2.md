# HTTP/2

### The second version of the HTTP protocol proposes several changes over the original HTTP specifications. The new protocol intends to overcome the problems inherent to HTTP/1.1 by changing the message format and how the client and server communicate. One of the significant differences is that HTTP/2 requests and responses use a completely binary protocol, unlike HTTP/1.1, which is humanly readable. This is a massive improvement over the older version since it allows any binary information to be sent in a way that is easier for machines to parse without making mistakes.

### The HTTP/2 request has the following components:

#### 1) Pseudo-headers: HTTP/2 defines some headers that start with a colon :. Those headers are the minimum required for a valid HTTP/2 request. (Example: :method, :path,etc)

