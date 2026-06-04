Network layer review:
	Provides connectivity between hosts on DIFFERENT networks
	Provides logical addressing (IP Addresses)
	Provides path selection between source and destination


IPv4 addresses are composed of 4 sections of binary values, usually written in dotted decimal notation:
    127.0.0.1
    255.255.255.255
    192.168.1.0

IPv4 addresses are 32 bits (4 bytes) in length
11000000.10101000.00000001.11111110
192.168.1.254  /24
    /24 means the first 24 bits are the network portion of the address

IPv4 address Classes/prefix lengths [[ipv4classes.png]]
The first 4 digits of the first octet determine class by numeric range:
    0 = A             /8    0-127 (126)     <-USABLE class A range is 0-126, because 127 is for loopback addresses
                        Cisco Netmask: 255.0.0.0
                            (11111111.00000000.00000000.00000000)
    10 = B            /16   128-191
                        Cisco Netmask: 255.255.0.0
                            (11111111.11111111.00000000.00000000)
    110 = C           /24   192-223
                        Cisco Netmask: 255.255.255.0
                            (11111111.111111111.1111111.00000000)
    1110 = D                224-239         <- Multicast Addresses
    1111 = E               240-255         <- Reserved/experimental
Loopback Addresses are used to test the network stack usually to check availability
    127.0.0.0 -> 127.255.255.255


BINARY -> DECIMAL
Binary is in base-2, as in:
0           0           0           0           0           0           0           0
128         64          32          16          8           4           2           1

Therefore:
10101010 = (2+8+32+128) = 170


DECIMAL -> BINARY

Example: 221
(1) Write out the bit values for each binary digit:
128         64          32          16          8           4           2           1

(2) Subtract the largest bit value you can from your decimal value until you are left with 0:
128         64          32          16          8           4           2           1
1           1           0           1           1           1           0           1
93          29                      13          5           1                       0

Example answer: (binary) 11011101 = (decimal) 221

EX: 127
128         64          32          16          8           4           2           1
0           1           1           1           1           1           1           1
            63          31          15          7           3           1           0

EX: 207
128         64          32          16          8           4           2           1
1           1           0           0           1           1           1           1


Decipher IP Address from raw binary:
00001100.10000000.11111011.00010111
answah: 12.128.251.23/?



PRACTICE
Convert the following binary IPv4 addresses to dotted decimal notation:

    00111111.00111000.11100111.00010011 = 63.56.231.19
    11110011.01111111.01100010.00000001 = 243.127.98.1
    01101111.00000110.01011001.11000111 = 111.6.89.199
    11001111.11000110.00101111.01001100 = 207.198.47.76
    01100100.11001001.00100001.11111101 = 100.201.33.253

Convert the following dotted-decimal IPv4 addresses to binary notation:

    88.46.90.91 = 01011000.00101110.0101101.01011011
    221.234.246.163 = 11011101.11101010.11110110.10100010
    3.41.143.222 = 00000011.00101001.10001111.11011110
    10.200.231.91 = 00001010.11001000.11100111.01011011
    248.87.255.152 =    11111000.01010111.11111111.10011000

    128         64          32          16          8           4           2           1
    24                                  8           0



Prac)
10110110 = 182
1            0              1          1            0           1          1               0



147 = 10010011
1             0             0            1          0         0               1         1 
128         64          32          16          8           4           2           1


254-128 = 126
126 - 64 = 62
-32 = 30
-16 = 14
-8 = 6
-4 = 2
-2 = 0