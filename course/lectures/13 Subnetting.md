[[ipv4classes.png]]
### IANA
- The IANA (Internet Assigned Numbers Authority) assigns IPv4 addresses/networks to companies based on their size.
- For example, a very large company might receive a class A or class B network, while a small company might receive a class C network
- However, this led to many wasted IP addresses
### CIDR
- The IETF introduced CIDR in 1993 to replace the 'classful' addressing system.
- With CIDR, the requirements of...
```
	Class A = /8
	Class B = /16
	Class C = /24
```
were removed.
- This allowed larger networks to be split into smaller networks, allowing greater efficiency
- These smaller networks are called 'subnetworks' or 'subnets.'
[[subnetting-cidr_notation_table.png]]
### /30 masks
- On a point-to-point interface, you can specify a /30 mask to only allow the first 2 bits of the host portion, which allows a total of 4 IPs (network, broadcast, and the 2 points themselves).
- 203.0.113.0/30
- = 203.0.113.0 through 203.0.113.3
	- (.0, .1, .2, .3)
- The remaining addresses in the 203.0.113.0/24 address block (.4 through .255) are now available to be used in other networks!
### /31 masks
- More efficient for point-to-point connections
- Mask is written as 255.255.255.254
- Only 1 host bit (2^1-2=0 usable IPs) meaning only 2 IPs total (.0 & .1)
	- These can function as the 2 points in a point-to-point connection.
- The remaining addresses in the 203.0.113.0/24 address block (.2 through .255) are now available to be used in other networks!
### /32 masks
- Written out as 255.255.255.255
- 2^0 -2 = -1 usable addresses? (Formula doesn't work)
- Only really used for static routes going directly to a host, not a network. (covered later in course)

### QUIZ
[[subnetting-first_example.png]]
Divide the 192.168.1.0/24 network into four subnets that can accommodate the number of hosts required.
- There are 45 hosts in each network
- In order to fit 45 hosts in each subnet you can use the /26 network, which contains 62 usables.
	- /26 refers to 26 network bits out of 32 total.
	- 32 - 26 = 6
	- 2^6 - 2 = 62
	- visual: [[subnetting-26_mask.png]]
The first subnet (Subnet 1) is 192.168.1.0/26. What are the remaining subnets?
HINT: Find the broadcast address of Subnet 1. The next address is the network address of Subnet 2. Repeat the process for Subnets 3 and 4.
[[subnetting-part1quiz.png]]
- A broadcast address is an IP with the host portion bits set to all 1s.
- In this case (/26) to manually solve would look like this:
32+16+8+4+2+1 = 63???
So fucking 192.168.1.63 is the broadcast address???
IDK MAN..
So that means Subnet 2 = 192.168.1.64 but like... how the fuck would I find the broadcast address of subnet 2 then? I'm so confused.
## ....
IT'S BECAUSE YOU FLIP ONE OF THE NETWORK BITS WOW JEREMY THANKS FOR TELLING ME BEFORE THE NEXT VIDEO (i would've figured it out if i wrote out the binary again but my brain kept going "but i can't set them all to 1s again!!! yes you fucking can, you move up one bit, flip that bit to 1, and all the following bits are FLIPPED BAKC TO 00000000000000000000000000 I AM SO HAPPY)
## ......
OK, so.
Subnet 2's range goes from
192.168.1.64 (network address)
(11000000.10101000.00000001.0**1***000000*)
to
192.168.1.127 (broadcast address)
(11000000.10101000.00000001.01**111111**)

Subnet 3's range:
192.168.1.128 (network address)
(11000000.10101000.00000001.**1**0000000)
to
192.168.1.191 (broadcast address)
(11000000.10101000.00000001.1**0111111**)

Subnet 4's range:
192.168.1.192 (network address)
(11000000.10101000.00000001.1**1000000**)
to
192.168.1.255
(11000000.10101000.00000001.11**111111**)

## Subnetting Trick
[[subnetting-subnetting_trick.png]]
- Adding the value of the first bit of the network portion corresponding to the CIDR-notated mask, i.e. 64 for a /26 mask, to the host portion, shows the network addresses' host portion at increments specific to that subnet size.
- /26 SN1 network address? .0
- /26 SN2 network address? .64 (0+64)
- /26 SN3 network address? .128 (64+64)
- /26 SN4 network address? .192 (128 + 64)

### Borrowed bits
- 2^x = number of subnets
- (x = number of borrowed bits)
- Borrowing 1 bit = /24->/25 = can make 2 subnets
- (If there are no borrowed bits, the max number of subnets is 1!!! Like in the case of a /16 network, class B network.)

### Identify the Subnet
What subnet does host 192.168.29.219/29 belong to?
1) Identify network/**host** bits
2) .00000|**000**
3) Find binary bits
```
91 - 64
- 32
27 - 16
11 - 8
- 4
3 - 2
1 - 1
```
- .1011|**011**
4) Change all subnet host bits to 0
- .1011|**000**
4) Evaluate 0'd host
	-  216
- Therefore, 192.168.29.219/29 belongs to the 192.168.29.216/29 subnet
### Subnets/Hosts for Class C
[[subnetting-subnet_hosts_class_C_networks.png]]
## Subnetting Class B Networks
1) You have been given the 172.16.0.0/16 network. You are asked to create 80 subnets for your company's various LANs. What prefix length should you use?
- /16 = 0 borrowed bits = 0 subnets
- find a host portion size that can do >80 subnets:
	2^8 = 256
	**2^7 = 128**
	2^6 = 64
- This means we need to borrow 7 host bits
	/16 + 7 = 23
- /23 is the prefix length we need.

2) You have been given the 172.22.0.0/16 network. You are required to divide the network into 500 separate subnets. What prefix length should you use?
- evaluate 2^x >= 500 subnets
	2^9 = 512
	/16 + 9 = 25
- /25 is the prefix length we need

3) You have been given the 172.18.0.0/16 network. Your company requires 250 subnets with the same nubmer of hosts per subnet. What prefix length should you use?
- evaluate 2^x >= 250
- 2^8 = 256
- /24

4) What subnet does host 172.25.217.192/21 belong to?
- find network/**host** bits
- 00000000.00000000.00000**000.00000000**
- 172.25.
- 217 in binary
	- ```
	  217 128
	  89 64
	  32
	  25 16
	  9 8
	  4
	  2
	  1 1
	  ```
	  - 11011001
- 192 in binary
	- ```
	  192 128
	  64 64
	  32
	  16
	  8
	  4
	  2
	  1
	  ```
  - 11000000
- /16 original host with highlighted subnet
	 = 172.25.11011**001.11000000**
- 0'd host = 110011**000.00000000**
- Evaluate
 ***172.25.216.0*** is the network address of the subnet for address 172.25.217.192/21
### Subnets/Hosts for Class C
[[subnetting-subnet_hosts_class_B_networks.png]]
### QUIZ
*You have been given the 172.30.0.0/16 network. Your company requires 100 subnets with at least 500 hosts per subnet. What prefix length should you use?*
- 2^7 = 128
- /16 + 7 = 23
**/23**


*What subnet does host 172.21.111.201/20 belong to?*
```
128
111 64
47 32
16
15 8
7 4
3 2
1 1
=
01101111
```
.01101111.?
```
201 128
73 64
32
16
9 8
4
2
1 1
=
11001001
```
.01101111.11001001
- host bits?
.0110**1111.11001001**
0'd host = network address ->
.0110**0000.00000000**
evaluate ->
.96.0
**subnet network address = 172.21.96.0/20**


*What is the <u>broadcast address</u> of the network 192.168.91.78/26 belongs to?*
```
128
78 64
32
16
14 8
6 4
2 2
1
=
01001110
```
192.168.91.01**001110**
192.168.91.01**000000**
network address = 192.168.91.64/26
192.168.91.01**111111**
**broadcast address = 192.168.91.127/26**

*You divide the 172.16.0.0/16 network into **4 subnets** of equal size. Identify the **network** and **broadcast** addresses of the **second subnet**.*
- To get 4 subnets, I need to borrow 2 bits (4 = 2^2)
- 172.16.0.0/16
- 172.16.00**000000.00000000**
- To get the network of the second subnet, I need to flip all the host bits to 1, giving me the broadcast address for subnet 1, then +1 for the network address of the second SN.
- 172.16.00**111111.11111111**
->
- SN1 broadcast address = 172.16.63.255
+1 ->
- 172.16.01**000000.00000000**
->
- SN2 network address = 172.16.64.0/18
->
- 172.16.01**111111.111111**
- **SN2 broadcast address = 172.16.127.255/18**
- **SN2 network address = 172.16.64.0/18**

*You divide the 172.30.0.0/16 network into subnets of 1000 hosts each. How many subnets are you able to make?*
- I DID THIS SHIT IN MY HEAD OMFG
- Firstly you need >1000 hosts, off the top of my head the best number here would be 1024, which is 10 bits of 1. If these are the host bits, the network portion would be 22 bits long for a prefix length of /22. Starting with a /16 network, this means we have a total of 6 borrowed bits. Number of possible subnets = 2^6 = 64 possible subnets with a max of 1022 hosts each.

## *I am become internet.*

*You divide the 165.23.10.0/24 network into subnets of 450 hosts each. How many subnets are you able to make?*

165.23.10.0/24
binary + host highlight ->
10100101.00010111.00001010.**00000000**
2^8 - 2 = 254 usable addresses total
This network cannot be divided into 450 hosts each, as it has a maximum of 254 usable addresses.
If the network started with a /16 prefix, it would have way more than enough (over 65,000 more than it needs) to work, as follows:
165.23.0.0/16
binary + host highlight ->
10100101.00010111.**00000000**.**00000000**
2^16 - 2 = 65,534 usable addresses
2^9 - 2 = 510 usable addresses
10100101.00010111.**0000000|0**.**00000000**
2^7 = **64 total subnets**

## Subnetting Class A Networks
- Same exact process, just larger numbers and borrowing bits from a /8 prefix.

*PC1 has an IP address of 10.217.182.223/11*.
*Identify the following the PC1's subnet:
1) Network address: 10.192.0.0
2) Broadcast address: 10.223.255.255
3) First usable address: 10.192.0.1
4) Last usable address: 10.223.255.254
5) Number of host (usable) addresses: 2,097,150

**00001010.110**11001.10110110.11011111
0'd ->
**00001010.110**00000.00000000.00000000
decimal ->
10.192.0.0 network 
**00001010.110**11111.11111111.11111111
10.223.255.255 broadcast
## VLSM (Variable-Length Subnet Masks)
- Until now, we have practiced subnetting using FLSM(Fixed-Length Subnet Masks)
- This means that all of the subnets use the same prefix length (i.e. subnetting a class C network into 4 subnets using /26).
- VLSM (Variable-Length Subnet Masks) is the process of creating subnets of different sizes, to make your use of network addresses more efficient.
- VLSM is more complicated than FLSM, but it's easy if you follow the steps correctly.
### VLSM - Example
[[subnetting-VLSM_practice.png]]
192.168.1.0/24
We are given the above network and must divide the network into subnets to accommodate all of the hosts.
Highest number of hosts required: 110
Host bits required for =>110 hosts per subnet: 8 lol
This would use all of the available hosts, and leaves no room for actual networks. We need at least 4 network bits to accomodate the 5 networks.
### VLSM - Steps
1) Assign the largest subnet at the start of the address space.
2) Assign the second-largest subnet after it.
3) Repeat the process until all subnets have been assigned.
[[subnetting-VLSM_practice_numbered.png]]
#### Tokyo LAN A - 110 hosts
- Network address: 192.168.1.0 /25
- Broadcast add.: 192.168.1.127/25
- First usable add.: 192.168.1.1/25
- Last usable add.: 192.168.1.126/25
- Total # of usable host add.: 126
192.168.1.0/24
**192.168.1.0**1111111/25
###### Tokyo LAN A address: 192.168.1.0/25
- This takes up half of the space of the /24 (254 hosts) network, but that's not a problem, because we only have 82 hosts total to assign left.
#### Toronto LAN B - 45 hosts
- Network address: 192.168.1.128
	- Add 1 to broadcast of Tokyo LAN A to get network addy of Toronto LAN B
	- Then, find the appropriate prefix length for 45 hosts
		- 2^6-2=62 hosts and 2 borrowed bits
		- /26 prefix length
		- binary -> 11000000.10101000.00000001.10**000000**
- Broadcast address: 192.168.1.191
- First usable add.: 192.168.1.129
- Last usable:192.168.1.190
- Total # of usables: 62
###### Toronto LAN B address: 192.168.1.128/26
- Now we're at 3/4ths of the network filled, but we have room for more hosts still. (I think about 68 (minus 2x where x is # of total subnets) but i'm not sure.)
#### Toronto LAN A - 29 hosts
- Network address: 192.168.1.192  /27
- 11000000.10101000.00000001.110**00000** = /27
- Broadcast address: 192.168.1.223 /27
- First usable: 192.168.1.193 /27
- Last usable: 192.168.1.222 /27
- Total usable hosts: 30
###### Toronto LAN A address: 192.168.1.192/27
#### Tokyo LAN B - 8 hosts
- Network address: 192.168.1.224 /?
- 11000000.10101000.00000001.1110**0000** = /28 
- Broadcast address: 192.168.1.239/28
- First usable: 192.168.1.225 /28 
- Last usable:  192.168.1.238 /28
- Total usable hosts: 14
###### Tokyo LAN B address: 192.168.1.224/28
- Network address: 192.168.1.240 /?
- 11000000.10101000.00000001.111100**00** =  /30
- Broadcast address: 192.168.1.243 /30
- First usable:  192.168.1.241 /30
- Last usable:  192.168.1.242 /30
- Total usable hosts: 2
[[subnetting-VLSM_practice_complete.png]]

## Additional Practice
http://www.subnettingquestions.com/
http://subnetting.org/
https://subnettingpractice.com/

## Homework
- Do at least ONE practice question from EACH of those practice websites every day for at least one week. (probably gonna do more)


