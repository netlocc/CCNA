Both switches have an empty MAC address table, and all PCs have an empty ARP table.

1. If PC1 pings to PC3, what messages will be sent over the network, and which devices will receive them?
    PC1 ICMP ECHO REQUEST #1 -> PC3 IP
    PC1 ICMP ECHO REQUEST #1 fails because it doesn't know PC3's MAC address
    PC1 Ping process pauses
    PC1 ARP REQUEST -> FFFF.FFFF.FFFF -> PC1 -> SW1 -> PC2
                                                    SW1 -> SW2 -> PC3
                                                    SW1 -> SW2 -> PC4
    SW1 Rx PC1 ARP REQUEST, dynamically adds PC1 ARP table entry, re-broadcasts to FFFF.FFFF.FFFF
    SW2 Rx, dynamically adds SW1 ARP table entry, re-broadcasts to FFFF.FFFF.FFFF
    All hosts that do not match the IP specified by the ARP request (PC2, PC4) drop the packet
    PC3 confirms IP matches ARP request, dynamically learns PC1 IP+MAC+Interface
    ARP REPLY -> unicast to PC1 IP (sw2->sw1->pc1)
    PC1 resolves PC3's MAC address
    PC1 Ping process resumes
    PC1 ICMP ECHO REQUEST #2 -> PC3 (sw1->sw2->pc3)
    PC1 ICMP ECHO REPLY -> PC1 (sw2->sw1->pc1)
    PC1 ICMP ECHO REQUEST #3 -> PC3 (sw1->sw2->pc3)
    PC1 ICMP ECHO REPLY -> PC1 (sw2->sw1->pc1)
    PC1 ICMP ECHO REQUEST #4 -> PC3 (sw1->sw2->pc3)
    PC1 ICMP ECHO REPLY -> PC1 (sw2->sw1->pc1)
    PC1 ICMP ECHO REQUEST #5 -> PC3 (sw1->sw2->pc3)
    PC1 ICMP ECHO REPLY -> PC1 (sw2->sw1->pc1)
    PC1 Ping process complete
    
2. Send the ping and use Packet Tracer's 'simulation mode' to verify your answer.
    I was correct. One thing I'm glad to have caught is that the packets from the Ping process were put into a buffer until the ARP Reply was received as shown in simulation capture here:
        "6. The ARP process takes out and sends buffer packets waiting for this ARP reply."
            Those buffered packets happened to be the remaining 4 ICMP Echo Requests.

3. Use pings to generate network traffic and allow the switches to learn the MAC addresses of all PCs on the network.
    Since PC1 and PC3 were already in both switches' ARP table, all I had to do was use PC2 to ping PC4 to generate enough traffic for either switch to learn of their existence.

4. Use 'show' commands on the switches to identify the MAC address of each PC.
    Not sure what's going on here. it's as if the aging variable was set to <10ms, huh?? show arp returns nothing when it absolutely should, and I can only get the dynamic addresses to show up for literal split seconds in the simulations. as in, the switches are actively receiving packets by way of a ping process and show arp still is empty at times.. doesn't make sense at all.

    edit: I think I wasn't in Privileged EXEC mode, though I definitely did try it in that mode. Timing can be cruel.

5. Clear the dynamic MAC addresses from the MAC address table of each switch.
    Can't because PT is aging the tables in <10ms, but if i could it would be using the cmd "clear mac address-table dynamic" in IOS.