# CORS

CORS stands for **Cross-Origin Resource Sharing**. It's a mechanism that allows browsers to make [requests](http_requests.md) across different origins and domains. It basically allows a service running on one domain to request different resources, like data or scripts, from a different domain.

By default, browsers would block such request for security reasons. This is typically known as **same-origin policy**. This means, that communication through such requests would only be allowed inside the same domain.

CORS adds a layer of control to these types of requests, allowing to specify which origins are permitted to request resources.