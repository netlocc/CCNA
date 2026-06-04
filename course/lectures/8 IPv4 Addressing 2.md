##### IPv4 Class Tables
[[ipv4classes.png]] 
[[ipv4class_sizes_and_number_of_networks.png]]
# Extrapolating Some Important Stuff from the IPv4 Class Table
## Maximum Hosts per Network
>is determined by size of 'host portions' of IPv4 addresses
>
>(2^n where n = number of host bits, or "host portion")
>For every level of 8, multiple by 256. So

**/8 = 256**
- - 2 = 254 max hosts
**/16 = 256 x 256 = 65,536**
- - 2 = 65534 max hosts
**/24 = 256 x 256 x 256 = 16,777,216**
- - 2 = 16777214 max hosts
### Examples: Class C (/24)
the host portion is only 8 bits, therefore:
network address--->broadcast address:
x.x.x.0 /24 ---> x.x.x.255 /24
Host Portion Max = 8 bits = 2^8 = 256
Cannot use network address or broadcast address, so, 256 - 2 = 254:
- Class C Network Max. Hosts = 254
### Class B
x.x.0.0 /16 ---> x.x.255.255 /16
Host portion = 16 bits = 2^16 = 65,536
Subtract network+broadcast addresses = 65,536 - 2 = 65,534
- Class B Network Max Hosts = 65,534
### Class A
x.0.0.0 /8 ---> x.255.255.255 /8
Host portion = 24 bits = 2^24 = 16,777,216
Minus NA+BA = 16,777,214
- Class A Max Hosts = 16,777,214
## First usable address
network address + 1, eg 192.168.1.1  /24
eg 10.0.0.0/8 + 1 = 10.0.0.1/8 
## Last usable address
broadcast address -  1, eg. 192.168.1.254  /24
Last usable should lead to an interface on the router
[[IPv4firstlabusableaddress.png]]
## $ show ip interface brief (in privil. exec mode)
#### OK?:
(ip address valid?)
legacy feature, should always say "YES"
#### Method:
(how was the IP address assigned)
#### Status:
Layer 1 status
administratively down: interface disabled with 'shutdown' command
This is the default status of cisco router interface
#### Protocol:
Layer 2 status
## To Configure A Specific Interface:
These together bring you to the G0/0 interface (on R1 in this case) in global configuration mode:
>R1>                            enable
>R1#                            configure terminal
>R1(config)#               interface gigabitethernet 0/0
>$ R1(config-if)#

Using shorthand/autocomplete:
>R1>                            en
>R1#                            conf t
>R1(config)#               in g0/0  
>R1(config-if)#

To set an IP address:
```
R1(config-if)# ip address 10.255.255.254 ?
A.B.C.D    IP subnet mask

R1(config-if)# ip address 10.255.255.254 255.0.0.0
```
>Subnet mask is specified after the ip address added to indicate Class!!!!
```
R1(config-if)# no shutdown
R1(config-if)# 
*Dec  7 08:29:08.937: %LINK-3-UPDOWN: Interface GigabitEthernet 0/0, changed state to up
*Dec  7 08:29:09.938: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet 0/0, changed state to up
R1(config-if)# 
```
>This will change the result of 'show ip interface brief' to display the protocol and status columns being "up"
## R1# show interfaces [interface]
## R1# show interfaces description
You can add descriptions to 
```
int g0/0
description ## to SW1 ##
int 0/1
desc ## to SW2 ##
int g0/2
desc ## to SW3 ##
do sh int desc
```
>Interface table (w/ descriptions) command should now reflect descriptions added to the individual interfaces
## Quiz
### Find the following info using these IPs:
#### 43.109.23.12/8
Network address: 43.0.0.0
Broadcast address: 43.255.255.255
First usable address: 43.0.0.1
Last usable address: 43.255.255.254
Max number of hosts: 2^24 - 2 = 16,777,214
#### 129.221.23.13/16
Network address: 129.221.0.0
Broadcast address: 129.221.255.255
First usable address: 129.221.0.1
Last usable address: 129.221.255.254
Max number of hosts: 2^16 - 2 = 65,534
#### 209.211.3.22/24
Network address: 209.211.3.0
Broadcast address: 209.211.3.255
First usable address: 209.211.3.1
Last usable address: 209.211.3.254
Max number of hosts: 2^8 - 2 = 254
#### 2.71.209.233/8
Network address: 2.0.0.0
Broadcast address: 2.255.255.255
First usable address: 2.0.0.1
Last usable address: 2.255.255.254
Max number of hosts: 2^24 - 2 = 16,777,214
#### 155.200.201.141/16
Network address: 155.200.0.0
Broadcast address: 155.200.255.255
First usable address: 155.200.0.1
Last usable address: 155.200.255.254
Max number of hosts: 2^24 - 2 = 65,534
# 100% {]B^)

















