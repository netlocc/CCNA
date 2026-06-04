Local Area Network
Relatively small area network, e.g. office floor, home wifi.
[[LANs.png]]

ETHERNET FRAME OVERVIEW
[[frame bytes.png]]
HEADER
    Preamble: 7 byte (56-bit)
        Alternating 1s and 0s
        10101010 * 7
        Allows devices to sync their receiver clocks
    SFD (Start Frame Delimiter): 1 byte (8-bit)
        10101011
        Marks the end of the Preamble, and the beginning of the rest of the Frame
    Destination, : 6 bytes (48 bit)
    Source  : 6 bytes (48-bit)
        Indicate the devices sending and receiving the Frame
        Consist of the destination and the source 'MAC address'
        MAC = Media Access Control
    Type/Length: 2 byte (16-bit) field
        A value of 1500 or less in this field indicates the LENGTH of the encapsulated packet (in bytes)
        1536 or GREATER in this field indicates the TYPE of the encapsulated packet (usually IPv4 or IPv6), and the length is determined via other methods
            e.g. IPv4 = 0x0800 (hexadecimal)
                        2048 (decimal)
                IPv6 = 0x86DD (hexadecimal)
                        34525 (decimal)
TRAILER
    FCS (Frame Check Sequence): 4 bytes (32 bits)
        Runs CRC algorithm over the received data to find+remove corrupted data

HEXADECIMAL
1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F

Unicast frames are forwarded to the destination address (if the devices along the way are in the address table)
UNKNOWN Unicast frames are flooded  to every network interface
MAC Addresses on the network that are learned dynamically decay after 5 minutes of inactivity

