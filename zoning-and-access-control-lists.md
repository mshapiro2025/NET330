# Zoning and Access Control Lists

## Lecture Notes: Network Zoning, Segmentation, and Isolation for Security

### Reasons for Segmentation

* reduce size of broadcast domains
* restrict unnecessary traffic crossing long distance and/or slow links
* conserve public IP addresses with an organized NAT implementation
* security

### Security and Network Segmentation

* principle of least privilege
  * providing network access to servers/services introduces risk, so we should access to only those remote systems that need it&#x20;

### Network-Based Defenses: Access Control

* how is the system connected to the network?
  * not connected to any network (standalone)
    * the best defense, obviously
  * on a private network (not the Internet)
    * highly secure environments (military, utility grid, etc.) may run separate networks
  * on the Internet
* use network connections and routing devices to control access to a system
* NAT
  * using private IPs internally and translating to "public" IPs when communicating on the Internet
  * private IPs
    * 10.0.0.0
    * 192.168.0.0
    * 172.16.0.0
  * organizations use private IPs on the local network
  * router translates private to public IPs and keeps track of translation in a table
* routers
  * devices that route traffic between different networks
  * can create routing rule to control which networks can communicate
  * can create Access Control Lists to drop certain types of traffic
    * spoofed addresses
    * certain protocols
* firewalls
  * device that controls traffic in and out of a network based on a ruleset
  * layer 4 firewalls
    * rules based on layer 3:
      * IP addresses of both internal and external computers
    * and layer 4 (port numbers):
      * ex. port 80, 443, 3389
  * layer 7 (application) firewalls
    * newer firewalls
    * can inspect the entire packet, including the data
    * can set rules on layers 3 and 4 plus:
      * info in the data such as URLs
      * particular applications, regardless of ports
    * ex.&#x20;
      * allow HTTP but block Facebook

### Network Defense Techniques

* technical solutions
  * NAT
  * ACLs
  * firewalls
* planning/layout solutions
  * network zoning

### Network Zoning

* designing networks to improve security by:
  * placing systems with similar security requirements in "zones" protected by firewalls
  * these requirements include:
    * services they run
    * who accesses them
    * who manages them
    * operational criticality
    * data they store/process
    * regulatory requirements
* asset-based as opposed to perimeter approach to network traffic flow policy

### Network Zoning Goals

* place all datacenter servers behind hardware firewalls
* simplify rulesets as much as possible
  * administrative access
  * services
  * user access
* quicker troubleshooting and incident response
* improve intrusion prevention and monitoring
* defense in depth

### Firewall Contexts

* firewall contexts can be viewed as "virtual" firewalls on the same hardware
* reasons for configuring separate contexts include:
  * simplify rule sets while maintaining security requirements
  * isolate systems according to security requirements
  * comply with policy and regulatory controls for isolation, monitoring, and logging
* planned contexts:
  * PCI: systems processing credit cards
  * HIPAA: systems processing/storing Protected Health Info
  * ITS: systems administered exclusively by central IT team
  * general: systems administered by central IT, other IT, and/or vendors
  * management: systems used to manage network devices, building control, or other embedded devices

### VLAN Groups

* grouping of VLANs within a context
* can include:
  * DMZ
    * directly accessible by internal and/or external users
  * production
    * only directly accessible by admins and load balancers
  * dev/non-prod
    * firewall rule update testing
    * allows different inbound/outbound, and back-end rules
    * policy requirement and best practice
    * minimal impact for admins

### Access Lists on Cisco

* two types:
  * standard
    * apply to source IP address or network only
    * layer 3
  * extended
    * apply to source and destination IP address and/or network
    * can also create rule for TCP ports
    * layer 3 and 4
* creating access lists is a two-step process
  * in global config mode, use ip access-list command to create list
  * apply list to interface with ip access-group command
    * interface config mode
    * specify in or out
    * does list apply to packets entering interface (in) or leaving interface (out)
* standard: ip access-list standard \[name of list]
  * permit/deny \[IP address] \[wildcard mask]
* extended: ip access-list extended \[name of list]
  * permit/deny \[protocol] \[source IP] \[wildcard mask] \[destination IP] \[wildcard mask] \[port?]
* additional notes
  * rules applied in order from top to bottom
  * deny all is applied by default
    * must add permit any at the end of list if appropriate
  * regular ACLs cannot be reordered- must delete and recreate if the order is messed up
