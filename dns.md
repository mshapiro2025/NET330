# DNS

## Lecture Notes: DNS

### Network Connections Over IP

* what information is needed to connect to a server on another router?
  * MAC of default gateway (can be obtained using ARP)
  * IP of the server

### Domain Name System (DNS)

* the distributed, hierarchical naming structure for internet systems
  * root server
  * top-level-domain servers (TLD)
    * .com, .org, .edu, etc. DNS servers
  * authoritative servers
    * amazon.com, cnn.com, etc. servers
* root DNS servers are the authoritative name servers that serve the DNS root zone
  * configured as 13 named authorities, but in physical form, they are a network of hundreds of servers
* top-level domain servers are responsible for domains like .com, .net, .gov, etc.
* authoritative name servers are the servers that actually provide the answer for a query about a specific name in a zone/domain
  * ex. IP addresses for google.com hosts can be answered by the authoritative name servers for the google.com domain

### Nslookup

* can use nslookup to view the servers at each level

```
C:\> nslookup
> set type=ns
> . # will return the root server names/IPs
> edu. # will return the .edu TDP server names/IPs
> champlain.edu. # will return the champlain.edu DNS server IP
```

### DNS Resolution Techniques

* DNS has two methods of resolution:
  * iterative
  * recursive
* iterative resolution means that the server responds to the client with the name of another server that has the necessary information
* recursive resolution means that the server sends requests to other servers to find the necessary information, then returns that information to the client
  * not all servers support recursion
  * typically, local DNS servers will support recursion only for clients on its local network
    * for security and performance

### Open Resolvers and Amplification Attacks

* if a DNS server supports recursion to the outside world, it is known as an open resolver and can be used in denial of service attacks
  * DNS uses UDP, so the source address of requests can be spoofed
  * the spoofed requests use the victim's IP
  * all answers get sent to the victim
  * the requests can be "amplified": small question receives a large answer

### Resource Records

* authoritative domain servers contain "records" for the domains they are responsible for
* Resource Records contain the name-resolution information, including:
  * name (FQDN)
  * type (of record)
  * TTL (seconds that the answer can be cached)
  * value (what the FQDN resolves to- IP or other FQDN)
* Resource Record types:
  * A
    * name is the hostname
    * value is the IP
  * NS
    * name is the domain
    * value is the hostname of the authoritative name server for the domain
    * used as a routing function for queries
  * CNAME
    * name is the alias name
    * value is the canonical name
  * MX
    * name is domain name
    * value is the name of the mail server associated with this domain

### DNS Caching

* it would be efficient to make systems and name servers continually ask the same questions over and over
* DNS records include a TTL value (in seconds)
  * the expiration date put on a DNS record
* the TTL tells the recursive server or local resolver how long it should keep said record in its cache
* system and network admins have to strategically plan TTLs
  * balance query volume to server (longer TTL) and quicker propagation if a record changes (ex. a new IP) (shorter TTL)

### DNS Considerations for Network Design

* recursion
* internal and external views
* load balancing
* redundancy
* disaster planning

## Lab Notes: Small Enterprise Network

| Network Name   | VLAN ID | # of Hosts | Network Address | Subnet Mask   | Default Gateway | First Usable IP | DHCP Pool        |
| -------------- | ------- | ---------- | --------------- | ------------- | --------------- | --------------- | ---------------- |
| Default Subnet | 1       | 150        | 10.12.6.0       | 255.255.255.0 | 10.12.6.1       | 10.12.6.2       | 10.12.6.50 + 150 |
| Clinic         | 100     | 300        | 10.12.0.0       | 255.255.254.0 | 10.12.0.1       | 10.12.0.2       | 10.12.0.50 + 300 |
| Visitor        | 110     | 300        | 10.12.2.0       | 255.255.254.0 | 10.12.2.1       | 10.12.2.2       | 10.12.2.50 + 300 |
| Office         | 120     | 300        | 10.12.4.0       | 255.255.254.0 | 10.12.4.1       | 10.12.4.2       | 10.12.4.50 + 300 |
| Counseling     | 130     | 150        | 10.12.7.0       | 255.255.255.0 | 10.12.7.1       | 10.12.7.2       | 10.12.7.50 + 150 |

### Hospital Router Configuration

```
Switch> enable
Switch# config t
Switch(config)# ip routing
Switch(config)# vlan [vlan ID]
Switch(config-vlan)# name [vlan name]
Switch(config-vlan)# interface vlan 1
Switch(config-if)# no shutdown
Switch(config-if)# ip address [default gateway IP] [subnet mask]
# repeat for each VLAN
Switch(config)# interface [interfaces connected to switches]
Switch(config-if)# switchport trunk encapsulation dot1q
Switch(config-if)# switchport mode trunk
Switch(config-if)# interface vlan [vlan ID]
Switch(config-if)# ip helper-address [DHCP server IP]
```

### Switch Configuration

```
Switch> enable
Switch# config t
Switch(config)# vlan [vlan ID]
Switch(config-vlan)# name [vlan name]
Switch(config)# interface [interface connected to router]
Switch(config-if)# switchport trunk encapsulation dot1q
Switch(config-if)# switchport mode trunk
Router(config)# interface range (interface name) 0/[range x-y]
Router(config-if-range)# switchport access vlan [vlan ID]
```
