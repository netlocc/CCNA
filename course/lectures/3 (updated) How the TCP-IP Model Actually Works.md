Protocol - a set of rules defining how data should be communicated between devices over a network.
	The "languages" that computers use to communicate
Standard- an agreed upon spec that describes how procotonls and tech shouldwork
	vendor-neutral standards allow iPads to talk to Androids, for instance.

the DoD's ARPA created ARPANET.
the first internet.
lol

TCP 1974
and
IP 1974

Fully sdwapped to TCP/IP on Jan 1 1983

IEEE Institute of Electrical and Electronics Engineers
Ethernet 802.3
Wifi 802.11

IETF (Internet Engineering Task Force)
	TCP, IP, UDP, HTTP, DNS, etc
		publishes standards in documents called RFCs (requests for comments)\


Layered models
	networks do different jobs to move data

Stack
	Application layer
	Transport Layer
	Internet Layer
	Link Layer


"Sending a Letter" Example
your house -> road -> post office a -> road -> PO B -> road -> bob's house

 Layer 1 Physical
 Complex signals and transcievers and recievers and all that shit, cables, Network Interface Cards, all kinds of shit bru

Layer 2 Local Network Layer
provides "hop-to-hop" delivery of messages on a local network
	a hop is one step along the path between two devices,
		from router to host or next router or host in the path
uses MAC (Media Access Control) addresses to identify interfaces
	(as opposed to IP address, on the network layer)
Ethernet
Wifi
are the Most common layer 2 protocols

Layer 3: The Internet Layer
	provides end-to-end delivery between hosts
		it's not concerned with host-to-host delivery
	keeps destination and source addresses intact for reference
	

Layer 4: Transport Layer
	provides end-to-end communication between application processes
	which service should receive the message
		also called "process-to-process" "or "service-toservce"
	uses port numbers to identify the processes on each host
	runs mainly on the communicating hosts
	routers operate on layer 3, not layer 4
	protocols at this layer:
		UDP (User Datagram Protocol): simple and efficient
		TCP (Transmission Control Protocol): more robust features beyond basic message addressing

Layer 5: Application Layer          (also called layer 7)
	where network communcations meet applications
		defines how apps rpocess, format, send and interpret data
			for browsing the web (http/https)
			transferring files (ftp, tftp)
			sending/receiving mail (smtp, pop3, imap)
	network infrastructure devices don't care about application layer details
		they just move messages across thenetwork
		only the communicating hosts do



Encapsulation/Decapsulation
PDUs: L4 headers are composed of segments (TCP) and datagrams (UDP)
L3 = packet
L2 = frame
payload is what's being carried inside that PDU:
	the payload of a frame is a packet
	the payload of a packet is a segment
	the payload of a segment is the raw application data being transmitted.

adjacent layer interaction
	every layer is serviced by the layer below and provides a service to the above

same layer interaction
	layers interacting with the "same layer" of another device
		application -> application
			network -> network
				physical -> physical
