RPC

Step1: Client 
		Marshal the data/Request
		Send Request to Server
Step2: Server
		Receive the Request
		Unmarshal the data/Request
		execute the function
		Marshal the data
		Send Data/Response to client
Step3:
		Wait for Response
		Unmarshal the Response/data


Why
	1. Scale
	2. Security
	3. Upgrade
	4. SDK multi-language

Blocks:
	1. Medium or Transport
		TCP/HTTP/WebSocker/Shared memory
	2. Serialization or Marshaling

HTTP/2.0 (2015 than 1.1)
	Header Compression
	Server push
	Request prioritization
	Rquest multiflexing over single TCP Connection
	Binary Frames
	Secure the Data by default (TLS)

Protoco Buffers (Binary + Schema + Data)
	Binary Serialization Format with Schema

	Scalar Value Types
	dobule/float/int32/

	Compiler

	protoc --libprotoc

GRPC
	A high performance, opensource universal RPC framework.

	unary
		Traditional (Request/Response)
	Streaming
		Server <--> Clients

	can use http tools (LoadBalancer,cUrl,postman)
	buf.build
	grpc.io

grpc-gateway (Server)
	

