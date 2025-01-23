# IP Addressing

## Lecture Notes: IP Addressing

### Sending a Packet

* look up recipient address
  * DNS- convert hostname to IP
* add headers to data (encapsulate)
  * prepend bits for recipient and sender IP address to data
* send packet to network interface controller (NIC)
* transmits onto network
  * sent to local router (default gateway)
* router sends packet to next router
  * uses network part of IP address
* router uses routing table to know where to send the packet next
* ends up at local router of recipient
* router and switches send to recipient
  * uses host part of IP address and MAC address

### OSI Model

* OSI is a network protocol framework that uses 7 layers
* the 7 layers define the different stages that data must go through to travel from one device to another over a network
* physical -> datalink -> network -> transport -> session -> presentation -> application

#### Application

* the data that the computer is sending/receiving (ex. webpage)

#### Presentation

* compression, encryption, other encoding

#### Session

* session setup and teardown

#### Transport

* port numbers tell receiver what application the data is for

#### Network

* IP addresses

#### Data Link

* defines how the packets get onto the media
  * when it is safe to send
  * is the recipient ready to receive

#### Physical

* physically sending the bits over media
  * copper wires
  * fiber optic
  * radio waves

### Network Addressing

* 3 components to a computer's network address
  * network ID: first part of an IP address
  * host ID: second part of an IP address
  * MAC address: unique to every network adapter

#### IP Address

* 32-bit number
* typically displayed as four 8-bit numbers with dots in between
  * dotted decimal notation
  * each 8-bit number is called an octet
* IP address includes both the network ID and host ID
  * network ID is always at the beginning
    * variable length defined by subnet mask

### Anatomy of an IP Address

* each device on a network must be uniquely identified at the network layer
* for IPv4, a 32-bit source and destination address is contained in each packet
* devices use binary logic and work with strings of binary numbers
  * the decimal equivalent is much easier to use and remember
* to identify a route through a network, the address must be composed of two parts:
  * network portion
  * host portion
* network portion
  * some portion of the high-order bits represents the network address
  * at layer 3, we define a network as a group of hosts that have identical bit patterns in the network address portion of their addresses
* host portion
  * there are a variable number of bits that are called the host portion of the address
  * the number of bits used in this host portion determines the number of hosts that we can have within the network

### Types of Addresses in IPv4

* network address
  * a special address that refers to the network as an entity
* broadcast address
  * a special address used to send data to all hosts in a network
* host address
  * the unique address assigned to each host in a network
* network and broadcast addresses cannot be assigned to a host

### Network Address

* standard way to reference a network is the lowest address in the range
* all hosts in the network will have the same network bits
* cannot be assigned to a device
* each host bit in the address will be a 0

### Broadcast Address

* the destination address of a single packet used to communicate to all hosts in a network (the highest address in the range)
* cannot be assigned to a device
* each host bit in this address will be 1

### Host Address

* the unique address assigned to each device on the network
* assign any address between the network address and the broadcast address

### Types of Communication in IPv4

* unicast
  * the process of sending a packet from one host to an individual host
* broadcast
  * the process of sending a packet from one host to all hosts in the network
  * broadcasts are not forwarded by a router unless specifically configured to do so
* multicast
  * the process of sending a packet from one host to a selected group of hosts
  * IP range 224.0.0.0 to 239.255.255.255 reserved for multicasting
  * uses UDP
  * hosts must choose to join a multicast group on a specific network interface
  * routers send traffic to these hosts based on the routing information they have

## Lab Notes: Hardware Networking Lab

* connect blue serial console cable from console port in router

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdX0yXqh7eUlqdGURn48Cxlp3mzBt-N9HvB6_PSsivhpMgogn1FnWAdVY1Mzbs5XJXZn4JNboHWkX-w5d1NaQisoD9gWC0oXOI34R_h3HKsiOnxiojH1TxAOPFWwTqb443ONnuLYg?key=VQANE1wDgJIZ9SpaRp6oIvgl)

```
# Due to the router booting into read-only rommon mode:
rommon 1 > confreg 0x2102
rommon 2 > boot
# Router restarts, will need to restart putty session
Router> enable
Router# config t
Router (config)# do show interface
Router (config)# interface FastEthernet0/0
Router (config-if)# ip address 192.168.3.1 255.255.255.0
Router (config-if)# exit
Router (config)# interface FastEthernet0/1
Router (config-if)# ip address 192.168.1.1 255.255.255.0
Router (config)# copy run start
```

## Lab Notes: Packet Tracer Review

### Network Diagram

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc1v-Esw3sAdxsgNZNhNXQPbIu_mydDHIXTLK6hKMs8PvAzADC_tM15zEGnxJwJG0gnhwOS33zxhYkw1GqwN1q4TjehpXZwgP_HKmQeEwdMegjykOzTOmIheVxKyIm0M4TgEq49hg?key=evprcFAy_I5m5_o4BsKoA-1v)

### Router Configurations

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcOGbkZeqrzT8vZWBC1aZsDQctd9Mi1RltcuRdKz7Eb7imFWY3dY-vFYaLPt6XZE9vlGP3mQolEKnyAKYdhtQed3IISpGcA0Hhj9qrrJyA-p7T0RFW3nGBficrXF0Px872zidFg?key=evprcFAy_I5m5_o4BsKoA-1v)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeZBIT44fF61fc55b1oaIhQEKiCjxw1WpaVoTczIywY-j7DdysEv4tiZn2-adqs9DWzs6jCncMRGsk1Zgz2I_dV-69VQJBZjtdSCkNVow_BYadNiG1xA9QjdbwdO-L4mBOw7Nnl9Q?key=evprcFAy_I5m5_o4BsKoA-1v)

### Laptop Configurations

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXewjxcGRgZX1D9AmyN2hzuEhCzqgRGvU5XZANPFY1HPnHkM-1SN1JRsb0zB-BemGrR1984TcHpUuw-78n5yUfSkCL801AM3W4Z3JLUvYuwsgq-gAgu27ULzNWcHaXg7cYuIuBZ2jw?key=evprcFAy_I5m5_o4BsKoA-1v)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXespnA4qPoJvKTHxHNUXPG8MS8TZ4GOJHwAC1SYHHXdloe4PzrFt109NnmqVMWyWBBbHM0SuflPabi-tLWdGX5urxyFYwsM8vByssscxfwdiCPhCx5bhCywbwvfnM2Bk7_YT7EqBw?key=evprcFAy_I5m5_o4BsKoA-1v)

### Server Configurations

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe2BmX0ogzVyRtteZJKcKK9bFKnkAfpGerIsl9xhMq-rxgm3GP0vhwGNAP3P9QmhiAjRbjhffyrCdDgWNYTnaMCegdbFWiVCEp08q9MzqYDFy1TkyETZN-yLgwySPSmxh_HL7aAnQ?key=evprcFAy_I5m5_o4BsKoA-1v)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdG5WvRkFuEHI1AGIcgpAqFTTnYnKQk4_INtFWOSwFC7SI6TkPvt04ApN48xo03O7oWiaBSfsKwrMc7YDXfof2xI3Eo-eFkNJanwUtaD43hKChtxLrUSQFfp8oaToePM9mK7nr3ww?key=evprcFAy_I5m5_o4BsKoA-1v)
