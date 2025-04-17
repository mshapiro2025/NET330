# Load Balancing

## Lecture Notes: Server Load Balancing

### Load Balancing Concepts

* distribution of workload across multiple computing resources
* can load-balance many resources including:
  * network links
  * computers/servers
  * CPUs
  * disk drives

### Why Load-Balance?

* efficiency
  * optimize resource use
* performance
  * maximize throughput
  * improve performance
* availability
  * minimize overload of single resource
  * increase availability through redundancy
* elasticity
  * grow services based on demand
* security
  * resource isolation and protection
  * supports "zoning" efforts

### Network vs. Server Load Balancing

* network load balancing
  * balance traffic across network links
  * handled with routing and other network protocols
  * provides redundancy
  * provides link selection based on criteria (bandwidth, load, cost)
* server/service load balancing (SLB)
  * providing a single service using multiple servers on the back end
  * highly customizable and widely-used in modern enterprises
  * performance, security, elasticity, redundancy are all popular reasons

### Layer 3 SLB

* what operates at layer 3?
  * IP addresses
* layer 3 SLB only uses the IP addresses of different servers
* DNS round robin is an example of layer 3 SLB
  * multiple A records for the same hostname
  * queries yield different answers so different servers are contacted
  * sometimes nslookup on the same hostname receives different responses (ex. google.com)

### Layer 4 SLB

* what operates at layer 4?
  * TCP and UDP ports
* layer 4 SLB usually uses dedicated load-balancer systems
* load balancers host virtual IPs (ex. front ends) with the IP and port that end users use to access a server
* the load balancer then brokers the connection with a server in the backend/pool

### Layer 7 Load Balancing

* layer 7 load balancing does full packet inspection
  * make decisions based on URLs, headers, and/or content and other tags/metadata

### SLB and Security

* zoning
  * load balancers allow backend servers to be protected behind firewalls on private VLANs
  * end users don't connect directly to the server, but have to pass through the load balancer
  * reduces exposed attack surface on the backend servers
* DoS and other protections
  * advanced load-balancers can offer protections against resource exhaustion of servers and other DoS techniques
  * layer 7 inspection allows for integration with application firewalls (ex. filter out/block bad web requests)

### SLB and TLS/SSL

* SSL/TLS offload
  * many load-balancers provide SSL/TLS "offload"
  * the LB device handles the cryptographic functions and then communicates to the backend servers without encryption
  * why?
    * SSL/TLS can be processor intensive
    * allows servers to focus on their primary services
    * LBs can have optimized hardware modules to handle encryption quickly
    * minimal risk if the link between LB and servers are physically secured

### SLB Service Monitoring

* load balancers can also monitor servers/services to make sure they are still running
* if a server/service goes down, it will be removed from the pool
* this monitoring can include:
  * simple IP, TCP, or UDP connectivity
  * particular protocol response
  * presence of a certain resource (web page) or successful completion of a transaction
    * ensures service is not just up, but working correctly

### Common Load Balancing Issues

* access logging
  * does a backend server know the IP address of the client/source?
    * no, the source IP is changed to that of the load balancer
    * creates issues for troubleshooting and incident response when we need to identify the true source of a particular action
  * options include:
    * for HTTP, create the X-Forwarded-For header that adds the original source IP to the request
    * for other protocols, extensive logging is needed on the load balancer that correlates with the backend server logs
* session persistence
  * some applications require the server to store information for the user, but if the user is directed to other servers, that information is lost
    * session persistence
      * directing a client's requests to the same backend server for the duration of a session
    * types
      * simple (address affinity/sticky) persistence based on IP addresses
      * cookie: uses an HTTP cookie set by the load balancer and stored on the client
      * SSL: uses SSL session IP (when SSL is passing through the load balancer)

### SLB Software and Devices

* F5 and NetScaler are two of the most popular vendors
  * make hardware appliances used in many data centers
  * also have virtual appliances that perform the same function as the hardware appliance but run on an organization's hypervisor
* NGINX and HAProxy are open-source software load balancers
  * also very popular and used by some of the most active websites
  * software-based and run on high performance server hardware
