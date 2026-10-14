# README

### Web Proxy

In this assignment, you will implement a simple web proxy that passes requests and data between a web client and a web server. This will give you a chance to get to know one of the most popular application protocols on the Internet — the Hypertext Transfer Protocol (HTTP) 1.0 — and give you an introduction to the Berkeley sockets API. When you're done with the assignment, you should be able to configure your web browser to use your personal proxy server as a web proxy.

### Introduction: The Hypertext Transfer Protocol

The Hypertext Transfer Protocol (HTTP) is the protocol used for communication on the web. It defines how your web browser requests resources from a web server and how the server responds. For simplicity, this assignment deals only with version 1.0 of the HTTP protocol, defined in detail in RFC 1945: http://web.archive.org/web/20080704073753/http://www.ietf.org/rfc/rfc1945.txt. You should read through this RFC and refer back to it when deciding on the behavior of your proxy.

HTTP communications happen in the form of transactions. A transaction consists of a client sending a request to a server and the server sending a response. Request and response messages share a common basic format:

* An initial line (a request or response line)
* Zero or more header lines
* A blank line (CRLF)
* An optional message body

For most common HTTP transactions, the protocol boils down to a relatively simple series of steps (important sections of RFC 1945 are in parenthesis):

1. A client creates a connection to the server.
2. The client issues a request by sending a line of text to the server. This request line consists of an HTTP method (most often GET), a request URI (like a URL), and the protocol version the client wants to use (HTTP/1.0). The message body of the initial request is typically empty. (5.1-5.2, 8.1-8.3, 10, D.1)
3. The server sends a response message, with its initial line consisting of a status line indicating if the request was successful. The status line consists of the HTTP version (HTTP/1.0), a response status code, and a reason phrase. There can be any number of header fields in the response. Following the CRLF field separator, the message body contains the data requested by the client in the event of a successful request. (6.1-6.2, 9.1-9.5, 10)
4. Once the server has returned the response to the client, it closes the connection.

It's easy to see this process in action without using a web browser. From a Unix prompt:

telnet www.yahoo.com 80

This opens a TCP connection to the server at www.yahoo.com listening on port 80 (the default HTTP port). You should see something like:

Trying 209.131.36.158... Connected to www.yahoo.com (209.131.36.158). Escape character is '^]'.

Type:

GET / HTTP/1.0

and hit enter twice. You should see:

HTTP/1.1 200 OK Date: Fri, 10 Nov 2006 20:31:19 GMT Connection: close Content-Type: text/html; charset=utf-8

Yahoo! (More HTML follows)

There may be additional header information as well (cookies, caching instructions, etc.). What you are seeing is exactly what your web browser sees when it goes to the Yahoo home page: the HTTP status line, the header fields, and the HTTP message body (the HTML).

#### HTTP Proxies

Ordinarily, HTTP is a client-server protocol. The client (usually your web browser) communicates directly with the server (the web server software). However, an intermediate entity called a proxy can be introduced. Conceptually, the proxy sits between the client and the server. Instead of sending requests directly to the server, the client sends all its requests to the proxy. The proxy opens a connection to the server, passes on the client's request, receives the reply from the server, and then sends that reply back to the client. The proxy acts like both an HTTP client (to the remote server) and an HTTP server (to the initial client).

Why use a proxy? A few reasons:

1. Performance: By saving a copy of the pages it fetches, a proxy can reduce the need to create connections to remote servers, reducing delay, especially for remote or heavily loaded servers.
2. Content Filtering and Transformation: A proxy can inspect requested URLs and selectively block domains, reformat pages (for example, strip images for a handheld device), or perform other transformations.
3. Privacy: Web servers typically log requests (including client IP, User-Agent, date/time, requested file). Using a proxy can hide personally identifiable information; requests appear to come from the proxy's IP and User-Agent.

Links:

* RFC 1945 — The Hypertext Transfer Protocol, version 1.0: http://web.archive.org/web/20080704073753/http://www.w3.org/Protocols/rfc1945/rfc1945

#### The Basics

Your first task is to build a basic web proxy capable of accepting HTTP requests, making requests to remote servers, and returning data to a client.

Do not assume your server will run on a particular IP address, or that clients will come from a pre-determined IP.

#### Listening

When your proxy starts, it must establish a socket to listen for incoming connections. The proxy should listen on the port specified from the command line and wait for incoming client connections.

Once a client has connected, the proxy should read data from the client and then check for a properly formatted HTTP request. An invalid request from the client should be answered with an appropriate error code.

#### Parsing the URL

Once the proxy sees a valid HTTP request, it will need to parse the requested URL. The proxy needs at most three pieces of information: the requested host and port, and the requested path. See the `URL (7)` manual page for more info.

#### Getting Data from the Remote Server

Once the proxy has parsed the URL, it can connect to the requested host (using the appropriate remote port, or the default of 80 if none is specified) and send an HTTP request for the requested resource. The proxy should send the HTTP request that it received from the client to the remote server.

#### Returning Data to the Client

After the response from the remote server is received, the proxy should send the response message to the client via the appropriate socket. Once the transaction is complete, the proxy should close the connection.

#### Performance and Design Considerations

* You must not use a hard-coded port number.
* You must be able to handle multiple simultaneous connections (forking, threading, etc.).
* Your proxy should not statically allocate large amounts of memory for reading requests or responses. Allocate a reasonably sized buffer and grow it to some reasonable maximum.
* You are only required to implement HTTP 1.0 methods. Additional methods specified in HTTP 1.1 should be responded to with a 501 error.
* You must support the basic HTTP 1.0 methods: GET, HEAD, and POST. Additional methods from the RFC can be implemented as an optional feature.
* You do not need to implement checking of header fields; as long as they follow the basic format specified in the RFC (section 4.2), they should be passed through unmodified.

#### Testing Your Proxy

Run your proxy with:

./proxy

As a basic test, try requesting a page using telnet:

telnet localhost Trying 127.0.0.1... Connected to localhost.localdomain (127.0.0.1). Escape character is '^]'. GET http://www.google.com HTTP/1.0

If the proxy works correctly, the headers and HTML of the Google homepage should be displayed.

For a more complex test, configure your web browser to use your proxy server as its web proxy (see below).

### Configuring a Web Browser to Use a Proxy

#### A Caveat

Using your proxy with a web browser will not work 100% correctly until you have multi-threading/forking working. Browsers issue multiple HTTP requests for each URL (images, embedded content). A single-threaded proxy will likely miss some requests, resulting in missing images or other minor errors. That's OK for initial testing, but you must correctly handle multiple connections in your final submission.

#### Firefox

Version 2.0:

1. Select Tools -> Options from the menu.
2. Click on the 'Advanced' icon in the Options dialog.
3. Select the 'Network' tab, and click on 'Settings' in the 'Connections' area.
4. Select 'Manual Proxy Configuration' and enter the hostname and port where the proxy is running.

To stop using the proxy server, select 'Direct connection to the Internet' in the connection settings dialog.

**Configuring Firefox to use HTTP/1.0**

Because Firefox defaults to HTTP/1.1 and your proxy speaks HTTP/1.0, change Firefox's proxy-related configuration keys:

1. Type about:config in the title bar.
2. In the search/filter bar, type network.http.proxy
3. You should see three keys: `network.http.proxy.keepalive`, `network.http.proxy.pipelining`, and `network.http.proxy.version`.
4. Set `keepalive` to false. Set `version` to 1.0. Make sure `pipelining` is set to false.

### Socket Programming

To build your proxy you will need to learn programming sockets. The Berkeley sockets library is the standard method on Unix.

See Unix man pages (many functions in section 2) and Stevens' "Unix Network Programming" (chapters 3 and 4). Other useful sections: the client-server example system in chapter 5, and name/address conversion in chapter 9.

Links:

* Guide to Network Programming Using Sockets: http://web.archive.org/web/20080704073753/http://www.beej.us/guide/bgnet/
* An Introduction to Sockets Programming: http://web.archive.org/web/20080704073753/http://www.uwo.ca/its/doc/courses/notes/socket/
* HTTP Made Really Easy — A Practical Guide to Writing Clients and Servers: http://web.archive.org/web/20080704073753/http://www.jmarshall.com/easy/http/

#### A Note on Network Programming

Writing code that interacts with other programs on the Internet is different from writing local code. General guideline: be lenient about what you accept, but strict about what you send. Even if a client doesn't follow the spec exactly, make a best effort to process their request. Ensure anything you send conforms to published protocols. Handle minor deviations (e.g., HTTP 0.9 or 1.1 requests from clients, non-standard line terminators like '\r' instead of '\r\n') gracefully. Follow behavior specified in RFC 1945 when in doubt: http://www.ietf.org/rfc/rfc1945.txt.

#### Possible Extensions

Proxies are flexible and useful for performance boosts (caching, pre-fetching), privacy protection (anonymous proxies), content filtering/blocking, and content transformation.

Sample proxy applications:

* Anonymizer: http://web.archive.org/web/20080704073753/http://www.anonymizer.com/
* Foxy: http://web.archive.org/web/20080704073753/http://www.2-power-n.com/
* Google Web Accelerator: http://web.archive.org/web/20080704073753/http://webaccelerator.google.com/

**Content Transformation**

Content transformation is when a proxy modifies a resource retrieved from a remote server: insert/remove/change content (strip images, alter text, rotate images, etc.). After retrieving a resource, the proxy is free to change it before sending to the client.

**Caching**

Caching is a common performance enhancement. Caching proxies save copies of files retrieved from remote servers. When another request comes in for the same resource, the proxy can return the cached copy instead of creating a new connection to the remote server. This saves time and CPU, especially for distant or overloaded servers.

Caching introduces complexities: many pages are dynamically generated and shouldn't be cached. You also must decide cache timeout: too short negates benefits; too long serves outdated content.

Steps to implement caching behavior for your web proxy:

{% stepper %}
{% step %}
### Specify a timeout value

Alter your proxy so that you can specify a timeout value (probably in seconds) on the command line.
{% endstep %}

{% step %}
### Check the cache before retrieving

Alter how your proxy retrieves pages: check whether a page exists in the proxy cache before retrieving it from a remote server. If there is a valid cached copy, present that to the client instead of creating a new server connection.
{% endstep %}

{% step %}
### Implement cache expiration

Implement cache expiration. Timing need not be exact (it's okay if a page still exists in your cache after the timeout has expired), but it is not acceptable to serve a cached page after its timeout has expired.
{% endstep %}
{% endstepper %}

**Link Prefetch**

Build on caching and content transformation: link prefetching attempts to speed browsing by parsing requested pages for links and fetching linked pages in the background. Prefetched pages are stored in the cache, ready to be served without waiting for the remote server.

Because parsing and fetching links can take time, make your proxy multi-threaded if you haven't already. One thread should handle reading requests and serving pages from cache or remote servers. A separate thread should parse pages, extract HTTP links, request those links from remote servers, and add them to the cache.

**Other Possible Extensions**

* HTTP 1.1 Support
* HTTP Connection Keep-Alive
