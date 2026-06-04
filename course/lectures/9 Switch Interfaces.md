## SW1#show interfaces status
#### columns:
port, name(desc), status, vlan, duplex, speed, type
#### duplex:
	auto - "automatically negotiate once connected"
	a-half - "automatically negotiated no full-duplex"
	a-full - "automatically negotiated full-duplex"
#### speed:
	auto - "auto select highest speed for both devices"
	a-100 - "automatically negotiated 100mbps"
## Configuring Interface Speed and Duplex
```
conf t
int f0/1
speed ?
[[help/options output]]
speed 100
duplex ?
[[help/options output]]
duplex full
description ## to R1 ##
```
## SW1(config)#interface range
from global config mode, you can select a range to configure several at once.
you could then type something like:
```
description ## not in use ##
shutdown
```
all the configs of each selected interface will now have those options
## Full/Half Duplex
#### Half duplex:
	The device cannot send and recieve data at the same time. If it is recieving a frame, it must wait before sending a frame.
#### Full duplex:
	The device **can** send and recieve data at the same time. It does not have to wait.
## LAN Hubs
Hubs worked like repeaters rather than switches and frames could "collide" by going to the same device?? that's fucking stupid.
To prevent this they used CSMA/CD
#### Carrier Sense Multiple Access with Collision Detection
- before sending frames, devices "listen" to the collision domain until they detect that other devices are not sending.
- If a collision does occur, the device sends a jamming signal to inform the other devices that collision happened
- each device will wait a random period of time before sending their frames again
- the process repeats
## Speed/Duplex Autonegotiation
- interfaces that can run diff speeds have default settings of speed auto and duplex auto
- interfaces advertise their capabilities to the neighboring device and they degotiate the best speed and duplex settings they are both capable of
#### if autoneg is disabled on the device connnected ot the swtich
- speed
	the switch will try to sense the speed the other device is operate at. if it fails to sense the speed, it will use the slowest supported speed (i.e. 10 Mbps on a 10/100/1000 interface)
- duplex
	If the speed is 10 or 100 Mbps, the switch will use half duplex. if the speed is 1000 Mbps or greater, it will use full duplex.
#### Duplex Mismatch = Collisions will occur
[[duplex_mismatch.png]]
If a device is manually set to <=100Mbps, but with a manual Duplex setting of Full, then connected to an autonegotiating switch, the switch's autoneg will set that interface to Half instead, which will cause a mismatch. This causes collisions to occur.
## Interface Errors
### SW1#show interfaces f0/2
##### runts
	frames that are smaller than the minimum frame size (64 bytes)
##### giants
	Frames that are larger than the maximum frame size (1518 bytes)
##### CRC
	frames that failed the CRC check in FCS
##### frame
	frames that have an incorrect format (due to an error)
##### input errors
	total of various counters, such as the above 4
##### output errors
	frames the switch tried to send, but failed due to an error
