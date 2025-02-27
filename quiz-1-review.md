---
hidden: true
---

# Quiz 1 Review

* possible security risks for DHCP
  * broadcast
  * no authentication, so DHCP clients and servers can be spoofed for MITM attacks, DoS attacks, etc.
  * rogue DHCP servers- improper configuration means potential network issues
* name four layers of hierarchical internetworking model and provide example of a device that operates at that layer
  * Cisco hierarchical internetworking model
  * distribution (multilayer switch), core (high speed chassis-based switch), border (border router), access/edge (laptop, 48-port Ethernet switch)
* when would you use PAT? when would you use static NAT?
  * static NAT is easy to configure- good for when you only need access to a few devices with static IPs and have a small number of public IPs
  * PAT is used when you have lots of hosts to map to only a single or a couple public IPs
* define and identify a primary function of each of the 4 layers of the hierarchical internetworking model
  * border
    * connect to Internet (routing/layer 3)
    * routers, border firewall, border load balancers, IPS, etc.
  * core
    * high-speed, highly redundant forwarding services to move packets between distribution-layer devices in different regions of the network
    * core switches and routers are usually the most powerful in terms of raw forwarding power
    * manage the highest-speed connections (ex. 10, 40, 100 gbps)
    * typically only perform switching
    * don't often need much configuration- just link the distribution layers to each other and the border
  * distribution
    * smart layer
    * routing, filtering (internal firewalling), QoS policies are managed at the distribution layer
    * devices also often manage individual branch-office WAN communications
    * typically handled by multi-layer/layer 3 switches (switches that route)
  * access/edge
    * end stations and servers connect to the enterprise at the access layer
    * using commodity switching platforms (switches and wireless APs)
    * also called the desktop layer because it connects client nodes (ex. workstations) to the network
    * layer 2 technology like VLANs
* list the DHCP order of operations for a new DHCP client trying to get an IP configuration and explain why the last two steps are necessary and describe
  * discover: client attempts to discover a DHCP server
  * offer: IP lease offer from server to client
  * request: client requests to use the IP lease sent by the server
  * acknowledgement: server sends acknowledgement to client that the lease was accepted
  * the last two steps are necessary because if there are multiple DHCP servers for redundancy, there needs to be a confirmation of what IP is being used for which host and prevents bad actors from taking IPs with spoofed discover packets
* identify specific addresses in a network
* true/false: NAT is exclusively for remapping a private address space into a public one
  * true
* if you have multiple routed subnets on a network but only one DHCP server, a \_ must be configured on the routers
  * relay
* by default, DHCP renewal happens at what percent of the lease time
  * 50
* port address translation is a **many-to-one** translation between IP ranges
* which of the following should be included in a DHCP server's IP pool configuration for a standard client network with expectation of internet access?
  * operation code
  * hardware type
  * hardware length
  * transaction ID
  * client IP (eventual client IP)
  * your IP (offered client IP)
  * DHCP server IP
  * default gateway IP
  * client MAC address
* subnetting
