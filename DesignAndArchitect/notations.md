Atomicity (Mutual Exclusion)
	One thread only can execute a block of code at given time or do updates on shared the data.
	Performed entirely or not executed at all.


Visibility:
	Changes done by one thread are visible to other threads.

Single Responsibility

Closed for Modifications, Open for Extentions

Vertical SCaling   Bigger Machines
	Singel point of failure
Horizontal Scaling Smaller Machines
	Redundancy
	Fault Tolerance

	Distributed (Complex)
		LoadBalancer
			RoundRobin
			Hashing
			GeoBased/CDN (static files)
Consistencey
	Strict Consistency
	Eventual Consistency
Caching
	CDN
	HardDisk
	RAM
	L1/L2/L3 CPU Cache
Domain Name Systems
	DNS Registrar (Type A Address)

Network Protocals

OSI Model - Open System Interconnection
			7 Layers (APST, NDP)
	Application Level : Human-Application interaction layer(HTTP)
	Presentation Layer: Ensures that data is in usable format and is where data encryption occurs
	Session Layer : Maintains connections and is responsible for controlling ports and sessions
	Transport Layer: Transmit data using Protocol(first protocal layers-TCP/UDP ) 

	Network Layer	- Decides Physical Path
	Data Link Layer - Defines the format of data on the network
	Physical Layer	- Transmits raw bit stream over physical medium (Copper Wire/)
TCP/IP Model: (4 Layers A-T-I-N)
	Application Layer (APS of OSI)[ HTTP/SMTP/FTP]
	Transport Layer.   (T of OSI) [TCP/UDP]
	Internet Layer 		(N of OSI) [ARP/IP/ICMP/IGMP]
	Network Access Layer (DP of OSI) [Ethernet/Frame Relay/Token Ring/ATM]

Data Transfer (APIs)
	REST API
	GraphQL
	GRPC
	WebSocket (Bi-Directional)
Data Storage
	SQL
		ACID [Atomicity/Consistency/Isolation/Durability]
	NoSQL (No Relatins/Consistency)
		[Availability,Partition Network]
	
	Replications [Leader-Follower, Leader-Leader]
	Sharding
	Partition
		CAP vs PACELC
Message Queue 
	Durability(Persistence)
	Availability
	Sharding
	Decouple(Async)






