# networks\_01

#### Socket API

{% stepper %}
{% step %}
### socket()

Create a socket descriptor.
{% endstep %}

{% step %}
### server: bind()

Associate a socket with a local address/port.
{% endstep %}

{% step %}
### server: listen()

Mark a bound socket as accepting incoming connections.
{% endstep %}

{% step %}
### client: connect(), server: accept()

Establish a connection from client to server (`connect()`), and accept connections on the server side (`accept()`).
{% endstep %}

{% step %}
### send()/recv()

Send and receive data over a connected socket.
{% endstep %}

{% step %}
### close()

Close the socket and free associated resources.
{% endstep %}
{% endstepper %}

#### Demultiplexing

Each layer in the protocol adds its own header information. Each header will have the next layer's (upstream) protocol type, called demultiplexing keys. For example:

{% stepper %}
{% step %}
### Ethernet

Ethertype field (e.g., IP, ARP) indicates the next protocol.
{% endstep %}

{% step %}
### IP

IP protocol field indicates the transport protocol (e.g., TCP, UDP).
{% endstep %}

{% step %}
### TCP

TCP port numbers (e.g., 80 → HTTP, 53 → DNS) identify application services.
{% endstep %}
{% endstepper %}

#### Internet Reference Model

```
Application (7)   -- HTTP, RTP, DNS
-----------
Transport (4)     -- TCP, UDP
---------
Internet (3)      -- IP
--------
Link (1, 2)       -- 3G, Ethernet
```
