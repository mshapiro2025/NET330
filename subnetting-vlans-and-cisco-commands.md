# Subnetting, VLANs, and Cisco Commands

## Lecture Notes: Subnetting

### IP Place Values

* the highest value in an octet is 255

### Subnetting

* organizations are "assigned" a network address to use on the Internet
  * Champlain College has a /20 network
  * 4094 hosts- do we want them all on the same network?
* network ID can't change, but can take some host ID bits to make a subnet ID
  * subnet bits are then added to the network ID, so the subnet mask covers them
* always start with the largest subnet first
  * larger subnet boundaries are always valid for smaller ones, but smaller boundaries are not always valid for larger ones

### Private and Reserved IP Ranges

* private ranges not routable on the Internet
  * 10.0.0.0/8
  * 172.16.0.0/12
  * 192.168.0.0/16
* reserved ranges
  * 127.0.0.0/8: loopback
  * 169.254.0.0/16: link-local host only
  * 224.0.0.0/4: multicast

## Lecture Notes: VLANs

* a virtual LAN is a group of devices on one or more physical LANs that are configured to communicate as if they were on the same LAN
* VLANs define broadcast domains in a layer 2 network
  * broadcast domain: set of all devices that will receive broadcast packets from any member of the set
  * typically bounded by routers, who do not forward broadcasts
* VLANs are extremely flexible
  * can split a single switch into several separate networks
  * can merge machines on different switches into a single network
* traffic cannot pass directly between different VLANs
* to send packets between VLANs, a router or layer 3 switch is required
* VLANs are often associated with specific IP subnets
* VLANs are an implementation of VLSM
  * subnetting schemes must be carried out on physical infrastructure
  * when subnets occupy the same physical space, we can use VLANs to keep devices on separate networks, even though they're next to each other physically

### How to Configure VLANs

* define the necessary VLANs on each switch
  * choose a unique VLAN ID for each VLAN
  * ID must be consistent across all switches involved
* configure the ports on each switch- 2 possible options
  * access ports: can only be assigned to/carry traffic from a single VLAN
    * used to connect end devices to a switch
  * trunk ports: carry traffic from multiple VLANS
    * used to connect switches
    * will "tag" packets with the proper VLAN ID

### VLANs and Switch Interfaces

* when using VLANs, switchports need to be configured/defined for the appropriate VLAN

### VLSM Table

{% file src=".gitbook/assets/Correct-VLSM-Table.pdf" %}

## Lab Notes: Subnet Design

* network is 10.28.0.0/16

<table><thead><tr><th width="83">VLAN</th><th>VLAN Name</th><th>Hosts Needed</th><th>Network</th><th>Netmask</th><th>Router Address</th></tr></thead><tbody><tr><td>1</td><td>Management</td><td>250</td><td>10.28.10.0</td><td>255.255.255.0</td><td>10.28.10.1</td></tr><tr><td>100</td><td>FacStaff</td><td>200</td><td>10.28.11.0</td><td>255.255.255.0</td><td>10.28.11.1</td></tr><tr><td>110</td><td>Student1</td><td>450</td><td>10.28.8.0</td><td>255.255.254.0</td><td>10.28.8.1</td></tr><tr><td>130</td><td>StuLab1</td><td>35</td><td>10.28.12.0</td><td>255.255.255.192</td><td>10.28.12.1</td></tr><tr><td>140</td><td>StuLab2</td><td>35</td><td>10.28.12.64</td><td>255.255.255.192</td><td>10.28.12.65</td></tr><tr><td>200</td><td>StuWireless</td><td>900</td><td>10.28.0.0</td><td>255.255.252.0</td><td>10.28.0.1</td></tr><tr><td>210</td><td>FSWireless</td><td>650</td><td>10.28.4.0</td><td>255.255.252.0</td><td>10.28.4.1</td></tr></tbody></table>

