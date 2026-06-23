***192.168.5.0/24***
- LAN2: 64 hosts
2^7 = 128 - 2 = 126 usable hosts for lan 2:
192.168.5.0|0000000 = /25
192.168.5.0 = network 
192.168.5.1 = first usable
192.168.5.126 = last usable
192.168.5.127 = broadcast 
- LAN1: 45 hosts
192.168.5.128 = network 
192.168.5.10|000000  = /26
2^6-2= 62 usable hosts
192.168.5.129 = first usable
192.168.5.190 = last usable
192.168.5.191 = broadcast 
- LAN3: 14 hosts
192.168.5.192 = network 
192.168.5.110|00000 = /27
192.168.5.193 = first usable
2^5-2 = 30 usable hosts
192.168.5.222 = last usable
192.168.5.223 = broadcast
- LAN4: 9 hosts
192.168.5.224 = network 
192.168.5.225 = first usable
2^4 - 2 = 14 usable hosts
192.168.5.1110|0000
192.168.5.238 = last usable
192.168.5.239 = broadcast
- Point-to-point: 2 hosts
192.168.5.240 = network address
192.168.5.111100|00 = /30
192.168.5.241 = first usable (R1 g0/0)
192.168.5.242 = last usable (R2 g0/0)
192.168.5.243 = broadcast address

