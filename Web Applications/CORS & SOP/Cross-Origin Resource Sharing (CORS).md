# Cross-Origin Resource Sharing (CORS)

### Cross-Origin Resource Sharing, also known as CORS, is a mechanism that allows web applications to request resources from different domains securely. This is crucial in web security as it prevents malicious scripts on one page from obtaining access to sensitive data on another web page through the browser.

### ross-Origin Resource Sharing (CORS) is a mechanism defined by HTTP headers that allows servers to specify how resources can be requested from different origins. While the Same-Origin Policy (SOP) restricts web pages by default to making requests to the same domain, CORS enables servers to declare exceptions to this policy, allowing web pages to request resources from other domains under controlled conditions.

### CORS operates through a set of HTTP headers that the server sends as part of its response to a browser. These headers inform the browser about the server's CORS policy, such as which origins are allowed to access the resources, which HTTP methods are permitted, and whether credentials can be included with the requests. It's important to note that the server does not block or allow a request based on CORS; instead, it processes the request and includes CORS headers in the response. The browser then interprets these headers and enforces the CORS policy by granting or denying the web page's JavaScript access to the response based on the specified rules.

# CORS HTTP Headers

#### 1) Access-Control-Allow-Origin

 - This header specifies which domains are allowed to access the resources. For example, Access-Control-Allow-Origin: example.com allows only requests from example.com.

#### 2) Access-Control-Allow-Methods

 - Specifies the HTTP methods (GET, POST, etc.) that can be used during the request.

#### 3) Access-Control-Allow-Headers

 - Indicates which HTTP headers can be used during the actual request.

#### 4) Access-Control-Max-Age

 - Defines how long the results of a preflight request can be cached.

#### 5) Access-Control-Allow-Credentials

 - This header instructs the browser whether to expose the response to the frontend JavaScript code when credentials like cookies, HTTP authentication, or client-side SSL certificates are sent with the request. If Access-Control-Allow-Credentials is set to true, it allows the browser to access the response from the server when credentials are included in the request. It's important to note that when this header is used, Access-Control-Allow-Origin cannot be set to * and must specify an explicit domain to maintain security.
