# HTTP Version Negotiation

### Web servers can offer the client many HTTP protocol versions in a single port. This is useful since you can't guarantee that users will have an HTTP/2-compliant browser. In this way, the server can offer the client both HTTP/1.1 and HTTP/2, and the client can select the version they want to use. This process is known as negotiation and is handled entirely by your browser. 

### The original HTTP/2 specification defined two ways to negotiate HTTP/2, depending on whether the communications were encrypted or not. The two methods used the following protocol identifiers:

#### 1) h2: Protocol used when running HTTP/2 over a TLS-encrypted channel. It relies on the Application Layer Protocol Negotiation (ALPN) mechanism of TLS to offer HTTP/2.

#### 2) h2c: HTTP/2 over cleartext channels. This would be used when encryption is not available. Since ALPN is a feature of TLS, you can't use it in cleartext channels. In this case, the client sends an initial HTTP/1.1 request with a couple of added headers to request an upgrade to HTTP/2. If the server acknowledges the additional headers, the connection is upgraded to HTTP/2.

### The h2 protocol is the usual way to implement HTTP/2 since it is considered more secure. In fact, the h2c specification is now regarded as obsolete to the point where most modern browsers don't even support it. Many server implementations, however, still support h2c for compatibility reasons, enabling a different way to smuggle requests.
