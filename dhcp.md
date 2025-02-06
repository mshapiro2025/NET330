# DHCP

## Lecture Notes: Dynamic Host Configuration Protocol (DHCP)

* DHCP is used to automatically assign an IP address to a host
  * may include more network information as well
  * key information:
    * IP address
    * subnet mask
    * default gateway/router
    * DNS server address
* DHCP server listens for broadcasts
* employs a connectionless service model over UDP
  * server port 67
  * client port 68
* DHCP has two primary operation phases:
  * initialization: client requests, receives, and confirms an IP address
  * renewal: client asks to renew its lease of the IP address
* DHCP header key fields
  * operation code: indicates if this is a request or reply
  * hardware type: type of HW address
  * hardware length: length of HW address
  * transaction ID: random number used to pair requests and replies (since UDP is connectionless)
  * client IP address
  * offered client IP address
  * DHCP server address
  * gateway IP address
  * client hardware address (MAC address)

### DHCP Initialization

* DORA
  * discover: client attempts to discover a DHCP server
  * offer: IP lease offer from server to client
  * request: client requests to use the IP lease sent by the server
  * acknowledgement: server sends acknowledgement to client that the lease was accepted

### DHCP Renewal

* process for client to request continued use of its lease
* by default, this begins 50% of the way through the current IP lease
* client sends DHCP request packets directly to the server
* if the server responds with a DHCP acknowledgement, the IP lease is renews and its time clock restarts

### DHCP Rebinding

* if the server doesn't respond to the client's renewal requests, it goes to the rebinding phase
  * begins 87.5% of the way through the current IP lease
  * client begins sending its DHCP request packets as broadcasts to see if any DHCP server will allow them to continue using their IP
  * if a server responds, the lease is renewed and the timer restarts

### DHCP Expiration

* if no server responds before the lease ends, the lease expires and the IP is released
  * all TCP/IP communication stops
  * the client must go through the initialization process again

### DHCP Relay

* unconfigured clients have no IP configuration
  * they know nothing about the subnet, gateway, etc.
  * all they can do is broadcast
* broadcasts are layer 2 only- what if the network doesn't have a local DHCP server?
  * layer 3 devices (routers, servers) can be configured as DHCP relays
  * pick up broadcasts and forward them to the DHCP server

#### DHCP Relay on Cisco

* cisco IOS uses the "ip helper-address"
* can be assigned to a physical or VLAN interface
* if configured, grabs DHCP broadcasts seen on that interface

## Lab Notes: DHCP in Packet Tracer

### DHCP Services Config

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### DHCP Router Config

```
Router> enable
Router# config t
Router(config)# interface vlan [vlan ID]
Router(config-if)# ip helper-address [DHCP server IP]
# do for each VLAN
```
