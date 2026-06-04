OSI Model
    Open Systems Interconnection
    Created by the ISO (International Organization for Standardization)
    Functions are divided into 7 layers

IETF (Internet Engineering Task Force) defines Internet standards
	They publish them in documents called RFCs (Requests for Comments)
IEEE (Institute of Electrical and Electronics Engineers) define LAN standards

LAYERS
L7 Application
    Closest to end user
    Interacts with software (e.g. Browser)
    HTTP and HTTPS are L7 protocols
L6 Presentation
    Translates data to the appropriate format
        e.g. de-/encryption
L5 Session
    Manages and terminates connected sessions

THE TOP 3
The above create a "finished product" payload of data that will then be sent over the network.

L4 Transport, "Segment" - TCP, "Datagram" - UDP
    Adds L4 header to end of data payload
    Breaks large data into smaller pieces and reassembles them
	    Makes sure data goes to the right ports for separate applications using the network on the server/client
		    "service-to-service"
    Provides Host-to-Host communication
L3 Network, "Packet"
    Adds L3 header to the end of segment
    Connectivity between end hosts on different networks
    Provides logical addressing
    Provides path selection
    Routers operate at L3
L2 Data Link, "Frame"
    Adds L2 trailer and header to ends of Packet
    Node-to-node connectivity and data transfer
    Defines how data is formatted e.g. copper UTP
    Detects and possibly corrects L1 errors
    Uses L2 addressing, separate from L3 ip addresses
    Switches operate at L2
L1 Physical, "Bits"
    Defines physical characteristics
        voltage, transmission distance, cable specs, etc
    Digital bits are converted into electrical for wired or radio for wireless
    Cables, pin points etc


Encapsulation = Down the stack
De-encapsulation = Up the stack

Same-layer interaction = An interaction where data is encapsulated + de-encapsulated to reach the opposite layer on the recipient end
    e.g. L7 -> L7
        When a multiplayer video game has to communicate with another video game client, for instance, I guess, perhaps not really.

Protocol Data Units (PDUs)
    Payloads -> Segments -> Packets -> Frames -> Bits




TCP/IP Suite
    Developed by DARPA (Defense Advanced Research Projects Agency)

4 Application
    Maps to OSI L7 Application, L6 Presentation and L5 Session
3 Transport
    Maps to OSI L4 Transport
2 Internet
    Maps to OSI L3 Network 
1 Link
    Maps to OSI L2 Data Link and L1 Physical

[[tcpip basic topology.png]]
