>> VPC Virtual Private Cloud
A secure , individual, private cloud-computing model hosted within a public cloud.

>> VPC networks connect Google Cloud resources to each other and to the internet.

	Segmenting networks
	Use Firewall rules to restrict access to resources
	Static routes to forward traffic to specific destinations
	Google VPC networks are global can have subnets in any Google Cloud region across the globe.

Bills by second
Sustained-use discounts
Committed-use discounts (1/3 y)
Spot VMs vs Preemptible & 
1. More Features <> Less
2. No Maximum runtime <> Runtime upt to 24h
3. Same pricing == Same Pricing

Compute Engine
	Machine Type
	AutoScaling-- Resilient and scalable apps

VPC Routing tables
-------------------
routing tables are built -in
No router provisioning or managing
Forward traffic from one instance to another
no external IP address required.
Firewall not required
VPC global firewall
Rules can be defined through network tags

VPCs can be belong to GCP Cloud Project
VPC peering ...establish relation between 2 vpc
Shared VPC 

Cloud Load Balancing
--------------------
Fully distributed, software-defined managed service
	HTTP(S)
	TCP
	SSL
	UDP
Provides single as well as cross-region load balancing,including automatic multi-region failover.


	Global Http(S)
	Global SSL Proxy
	Global TCP Proxy
	Regional (UDP)
	Regional internal 
	Internal Http(s) -- Proxy based L7 LB (Envoy Proxy)
	
Cloud DNS and Cloud CDN
---
8.8.8.8 Domain Name Service

Global Edge Caches -- Serves Cloud CDN

Connecting networks to Google VPC
--
1. IPSec VPN Protocol
	Uses Cloud Router to make the connection dynamic
	Lets other networks and Google VPC exchange route 
	information over the VPN using the Border Gateway Protocl (BGP)

2. Direct Peering
	Puts a router in the same public datacenter as a Google Point of Presence (POP)
	Uses a router to exchange traffic between networks
	More than 100 Google Points of presence around the world.

3. Carrier Peering
	Gives direct access from an On-premises network through a service provider's network
	Not covered by a Google Service level agreement
4. Dedicated Interconnect
	Allows for one or more direct, private connections to Google.
	Can be covered by up to 99.99% SLA.
	Connections can be backed upby a VPN
5. Partner Interconnect
	Useful if a data center is in a physical location cannot reach a Dedicated Interconnect colocation facility.
	Useful if the data needs dont' warrant an entire 10 GigaBytes per second connection
	Can be configured to support mission-critical services or applications that can tolerate some downtime.








