# 0. Model a Single-Server Web Stack

## *0. Server*

A server may be a physical machine or a virtual machine. It runs an operating system and is commonly hosted in a data center. The server is the machine itself, while the web server, application server, application code and database are services or software running on that machine.

## *1. DNS and A Record*

DNS translates the domain name `www.foobar.com` into an IP address so that the user can reach the server. In this scenario, the `www` record is an A record because it maps the domain name to the IPv4 address `8.8.8.8`.

## *2. Component Roles*

The web server (Nginx) receives HTTP requests and forwards them to the application layer. The application server runs the application, while the application code contains the logic used to process requests and generate responses. The database stores and retrieves the application's data.

## *3. Network Communication*

The user and the server communicate across a network using the TCP/IP protocol suite. TCP/IP provides the networking rules that allow requests to travel from the client to the server and responses to return to the client.

## *4. LAMP*

LAMP stands for Linux, Apache, MySQL and PHP. This design is LAMP-like because it combines a Linux-based server with a web server, application layer and database, but it is not a literal LAMP stack because it uses Nginx instead of Apache and does not require PHP.

## *5. Limitations*

The single server is a single point of failure because if it becomes unavailable, every service in the application becomes unavailable. Maintenance on this server can also cause downtime because there is no redundant server to handle requests. Finally, the capacity of one server is limited, so incresed traffic can eventually exceed its CPU, memory, network or other available resources.

# 1. Add Redundancy and Traffic Distribution

## *0. Load Balancer and Redundant Paths*

The load balancer was added to distribute incoming requests across multiple web and application paths. The two redundant paths improve availability and can increase capacity because traffic can be handled by more than one path.

## *1. Active-Active and Active-Passive*

The two application paths operate in an actice-active design because both paths can receive and process requests at the same time. In an active-passive design, one path handles traffic while the other remains on standby until it is needed.

## *2. Load Distribution Method*

Round robin is a load-distribution method that sends incoming requests to available servers in sequence. For example, one request can be sent to the first path, the next request to the second path and then the process repeats.

## *3. Database Primary, Replica and Replication*

The database primary handles writable data operations. The database replica receives copies of data from the primary through the replication flow and does not accept writes in this design. Replication alone does not provide automatic failover or guarantee database write availability.

## *4. Remaining SPOFs*

The load balancer remains a single point of failure because this design contains only one load balancer. The writable database primary is also a SPOF because its failure can prevent new writes even though a replica exists.

## *5. Missing Security and Monitoring Controls*

This design does not include HTTPS, firewalls or monitoring. Without these controls, communication security, network protection and operational visibility remain limitations.

## *6. Cost of Redundancy*

Redundancy can improve availability and increase capacity by providing multiple application paths. However, additional servers and components increase infrastructure costs and operational complexity.

# 2. Add Protection and Observability

## *0. Firewall*

A firewall filters network traffic according to defined security policies and helps restrict unwanted or unauthorized connections. It does not encrypt traffic, replace application security or guarantee that every attack is prevented.

## *1. HTTPS*

HTTPS is used to protect data in transit between the user and the infrastructure by providing encryption and helping protect the confidentiality and integrity of the connection. It also uses TLS to authenticate the server.

## *2. Monitoring and Metrics*

Monitoring clients or agents collect operational data and metrics from infrastructure services and send this information to a monitoring system. In this design, the monitoring system receives one-way metric flows from the load balancer, web servers, application servers and the database primary.

## *3. QPS Metrics*

QPS means Queries Per Second and measures how many queries or requests a service handles each second. Monitoring QPS can help detect sudden traffic changes and identify when capacity requirements may be increasing.

## *4. TLS Termination*

If TLS terminates at the load balancer, the connection between the user and the load balancer is encrypted. However, the internal hop can remain unencrypted unless encryption is continued between internal components.

## *5. Writable Database Primary*

The database primary remains a write-availability risk because it is the only component in this design that accepts writes. If the primary fails, the replica cannot automatically guarantee that new writes remain available.

## *6. Collocated Services*

When web, application and database services are collocated, they are more difficult to scale and maintain independently. Resource usage and maintenance on one service can affect the others because they share the same infrastructure.

# 3. Separate Tiers and Remove the Load-Balancer SPOF

## *0.Comparison with the Single-Server Design*

Unlike the single-server design, this architecture separates the web, application and database services into distinct tiers and uses redundant instances. This reduces the dependence on one machine and removes the load balancer as a single point of failure at a conceptual level through a redundant load-balancer pair.

## *1. Independent Scaling*

Separated tiers can be scaled independently because each tier has its own resources and instances. For example, additional web or application servers can be added without necessarily increasing the number of database servers.

## *2. Maintenance Isolation*

Separating the tiers can reduce the impact of maintenance on unrelated components. Work on one tier can be performed without requiring every service in the infrastructure to be maintained or restarted at the same time.

## *3. Evidence-Based Sizing*

The number of instances should be based on measured demand, expected growth, failure tolerance and a justified safety margin. Instances should not simply be copied from a diagram or increased without evidence because unnecessary infrastructure increases cost and operational complexity.

## *4. Remaining Limitations

A database write-availability risk relains because the design does not define automatic database failover. The separated architecture also has higher infrastructure costs and greater operational complexity than the single-server design.
