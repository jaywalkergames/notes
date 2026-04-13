# TCP/IP

### Transmission Control Protocol / Internet Protocol

A protocol suite that governs how data packets are transferred over the internet from one machine to another

# HTTP

### HyperText Transfer Protocol

A networking protocol that runs over TCP/IP and governs communication between web browsers and web servers

### Versions

HTTP/1.1 is the standard used for most of the web’s lifetime

HTTP/2 speeds-up transfer of information while maintaining most of HTTP/1.1’s semantics

HTTP/3 is is development and improves speed of HTTP/2 by using UDP to transport data packets instead of TCP

### How HTTP Works

1. Connection is Made

- The web browser extracts the domain name from the URL being accessed and performs a DNS lookup by sending the domain name to the local DNS and getting back the IP address of the web server hosting the domain name.
- The web browsers uses the IP address to establish a TCP connection with the web server and begins communicating with HTTP
- When the browser loads all resources from the server, the TCP connection is closed

1. Requests are Made

- HTTP Request: a message sent from the browser to the server
    - GET: request a representation of the specified resource
    - HEAD: request a response identical to GET but without the response body
    - POST: create a new resource with the contents of the message body
    - PATCH: modify an existing resource with the contents of the message body
    - PUT: replace an existing resource with the contents of the message body
    - DELETE: delete an existing resource
- HTTP Response: a message sent from the server to the browser in response to an HTTP request (often contains the requested web resource)
    - 200 (OK): standard response for a successful request
    - 301 (Moved): the resource should always be requested at a different URL
    - 302 (Found): the resource should temporarily be requested at a different URL
    - 304 (Not Modified): the resource has not been modified since the last time the resource was requested
    - 403 (Forbidden): the web browser does not have permission to access the resource
    - 404 (Not Found): the resource could not be located.
    - 500 (Internal Server Error): something unexpected happened on the web server

Request and Response Format

1. Start line: specifies the HTTP version being used, the request type and path or the response status code and phrase
2. Zero or more header fields: a keyword followed by a colon and a value specifying additional information about the request or response
3. Empty Line
4. Optional Body Message: contains data being transferred between a browser and server. A request could be form data. A response could be the requested resource.

### Browser Caching

Browsers cache requested resources on the computer’s file system to reduce the amount of network traffic required to display frequently visited webpages. Browsers use entity tags (ETags) to check if version of webpage has been modified since last cache.

### HTTPS

All HTTP traffic can be viewed by third parties using a network sniffer. HTTPS encrypts HTTP traffic between a browser and a web server.

TLS (Transport Layer Security) is used to encrypt data by using asymmetric public keys. A website wanting to use HTTPS must acquire a digital certificate that contains a public key used by TLS to encrypt data and is issued by a trusted certificate authority.

Browsers show a padlock symbol when HTTPS is used
# Web Networking

### IP Addresses

A computer’s unique address on the internet. It is typically 32 bits, divided into four 8-bit groups, each group often written as a decimal number.

### Domain Names and DNS

A name that represents an IP address. The IP address of a webpage is found by locating a domain on a DNS.

### URLs

Uniform Resource Locator is the location of a web resource on the web.

- Scheme: characters at the beginning of a URL followed by a colon ":" or a colon and double slashes "://”
- Hostname: the complete domain name following the scheme in a URL
- Path: the characters to the right of the hostname in a URL
- Query String: optional characters to the right of the question mark (?) in a URL that provide data for the web server
- Fragment: optional characters at the end of a URL that start with a hash character (#) and refer to a certain location within a webpage



`TCP` is a connection oriented stream over an IP network. It guarantees that all sent packets will reach the destination in the correct order. This imply the use of acknowledgement packets sent back to the sender, and automatic retransmission, causing additional delays and a general less efficient transmission than `UDP`.

`UDP` is a connection-less protocol. Communication is _datagram_ oriented. The integrity is guaranteed only on the single datagram. Datagrams reach destination and can arrive out of order or don't arrive at all. It is more efficient than `TCP` because it uses non _ACK_. It's generally used for real time communication, where a little percentage of packet loss rate is preferable to the overhead of a `TCP` connection.

In certain situations `UDP` is used because it allows broadcast packet transmission. This is sometimes fundamental in cases like `DHCP` protocol, because the client machine hasn't still received an `IP` address (this is the `DHCP` negotiaton protocol purpose) and there won't be any way to establish a `TCP` stream without the `IP` address itself.
