### Previously we learned about Ethernet headers+trailers.
### Those are Layer 2.
### IPv4 headers are L3 headers.
## Structure
#### Version
length: 4 bits
- Identifies the version of IP used with a value
	- IPv4 = 4 (0100)
	- IPv6 = 6 (0110)
#### Internet Header Length (IHL)
length = 4 bits
- The final field of the IPv4 header (Options) is variable in length, so this field is necessary to indicate the total length of the header.
- Identifies the length of the header in 4-byte increments
- Value of 5 = 5 x 4 bytes = 20 bytes
- Min value is 5 (= 20 bytes) (only possible with an empty options field)
- Max value is 15 (15 x 4 bytes = 60 bytes)
	- These together mean that the maximum IPV4 HEADER LENGTH may only be 60 BYTES, and at minimum 20 bytes.
#### Differentiated Services Code Point (DSCP)
length = 6 bits
- Used for QoS (Quality of Service)
- Used to prioritize delay-sensitive data (streaming voice, video, etc.)
#### Explicit Congestion Notification (ECN)
length = 2 bits
- Provides end-to-end (between two endpoints) notification of network congestion **without dropping packets.***
- Optional feature that requires both endpoints, as well as the underlying netwokr infra to support it
#### Total Length field
length = 16 bits
- Indicates the total length of the packet (L3 header + L4 segment)
- Measured in bytes (not 4-byte increments like IHL)
- Min value of 20 (=IPv4 header with no encapsulated data)
- Max value of 65,535 (maximum 16-bit value)
#### Identification field
length = 16 bits
- If a packet is fragmented due to being too large, this field is used to identify which packet the fragment belongs to for reassmbly
- All fragments of the same packet will have their own IPv4 header with the same value in this field.
- Packets are fragmented if larger than the MTU (Maximum Transmission Unit)
	- MTU is usually 1500 bytes
		- This is related to the maximum size of an Ethernet frame
	- Fragments are reassmbled by the receiving host
#### Flags field
length = 3 bits
- used to control/identify fragments
- bit 0: reserved, always set to 0
- bit 1: "Don't Fragment" (DF bit), used ot indicate a packet that should not be fragmented
- bit 2: "More Fragments" (MF bit), set ot 1 if there are more fragments in the packet, set to 0 for the last fragment
	- *(unfragmented packets will always have their MF bit set to 0)*
#### Fragment Offset field
length = 13 bits
- used to indicate the position of the fragment within the original, unfragmented IP packet
- allows fragmented packets to be reassumbled even if the fragments arrive out of order
#### Time to Live field
length = 8 bits
- a router will drop a packet with a TTL of 0
- used to prevent infinite loops
- originally designed to indicate the packet's max lifetime in seconds
- in practice, indicates a hop count: each time the packet arrives at a router, the router decreases the TTL by 1
	- current reccommended TTL is 64 (max is 255)
#### Protocol field
length = 8 bits
- indicates the protocol of the encapsulated L4PDU
- value of 6: TCP
- value of 17: UDP
- value of 1: ICMP
- value of 89: OSPF (dynamic routing protocol)
	- (*"Open Shortest Path First"*)
- https://en.wikipedia.org/wiki/List_of_IP_Protocol_numbers
#### Header Checksum field
length = 16 bits
- calculated checksum used to check for errors in the IPv4 header
- when a router receives a packet, it calculates the checksum of the header and compares it to the one in this field of the header
- if they don't match, the router drops the packet
- used to check for errors only in the IPv4 header
- IP relies on the encapsulated protocol to detect errors in the encapsulated data.
- Both TCP and UDP have their own checksum fields to detect errors in the encapsulated data
#### Source/Destination IP Address fields
length = 32 bits (each)
- Source IP Address = IPv4 address of the sender of the packet
- Destination IP address = IPv4 address of the intended receiver of the packet
#### Options field (if IHL > 5)
length = 0 - 320 bits
- Rarely used.
- If the IHL field is greater than 5, it means that options are present
- [[ipv4header-options_field.png]] (beyond the scope of CCNA)

### Ping can be used with the df-bit flag to see fragmentation fail.
#### ping 192.168.1.2 size 10000
	the IPv4 header for these would show fragmentation happening
#### ping 192.168.1.2 df-bit
	the IPv4 header will have DF bit in Flags set to 1, meaning "Don't Fragment"
#### ping 192.168.1.2 size 10000 df-bit
	these two together will cause the pings to always fail since the Maximum Transmission Unit (MTU) under Ethernet is 1500b. forcing the IPv4 header to *not* fragment a 10Kb payload isn't possible, so the pings simply fail.

