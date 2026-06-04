PAYLOAD (PACKET) SIZE [[payload.png]]
    64 bytes Total minimum size
    18 bytes Size of header+trailer
    46 bytes Minimum Packet size remainder
    If 46 bytes are not occupied by the packet, padding is added to create 46 bytes
        e.g. - tech enters "ping 192.168.1.1 size 36" into IOS
             - 10 bytes of padding are added to this packet before sending it out

MAC ADDRESS
6-byte (48-bit) physical address assigned to the device when it is made
AKA 'Burned-In Address' (BIA) 
Is globally unique
OUI (Organizationally Unique Identifier), first 3 bytes
Last 3 bytes unique to the device itself
Written as hexadecimal

MAC ADDRESS TABLE [[mactable.png]]
 show mac address-table
 clear mac address-table dynamic
 clear mac address-table dynamic address [MAC-address]
 clear mac address-table dynamic interface [interface id]

ARP (Address Resolution Protocol)
    0x0806 is the hexadecimal type code
ARP REQUEST
    broadcast to all hosts on the network
ARP REPLY
    unicast to original request sender

ARP TABLE [[arptable.png]]
 arp -a
    Windows, MacOS, Linux
 show arp
    IOS

FFFF.FFFF.FFFF = Broadcast MAC Address
    The destination address used to indicate that the frame should be broadcast

PING
 ping [IP-address] {size [size in bytes]}
    IOS, Windows, MacOS, Linux
measures round-trip latency
ICMP ECHO REQUEST
    unicast to a specified  IP
ICMP ECHO REPLY
    unicast reply to request

