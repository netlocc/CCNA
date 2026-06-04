## The Basics
RJ-45 are ethernet copper connectors
    RJ = Registered Jack

Ethernet is a collection of network protocols/standards

Bits and Bytes
    Bit = [0], [1]
        1 kilobit (Kb) = 1,000 bits
    Byte = Bit * 8
        "01110101"
## Cable Standards
UTP = Unshielded Twisted Pair
    Protects against EMI (Electromagnetic Interference)

[[copper cable standards.png]]
### Pin Pairs
10BASE-T    2 PAIRS (4 wires)
100BASE-T   2 PAIRS (4 wires)
    Routers, PCs, Firewalls
        Tx = 1 + 2
        Rx = 3 + 6
    Switches
        Tx = 3 + 6
        Rx = 1 + 2
    Straight-Through Cable
        1 -> 1
        2 -> 2
        3 -> 3
        6 -> 6
    Crossover Cable
        1 -> 3
        2 -> 6
        3 -> 1
        6 -> 2
1000BASE-T  4 PAIRS (8 wires) bi-directional
10GBASE-T   4 PAIRS (8 wires) bi-directional
    Same as above, except adding the pairs 4,5 and 7,8

Full-Duplex Connections = Data, back and forth simultaneously

(Most devices use Auto MDI-X, which uses the correct cable pins required for the device that is plugged in regardless of the type of ethernet cable inserted; if it's Switch -> Switch the device uses a Crossover configuration, etc.)
## Fiber lol
Fiber!
    SFP Transceiver = Small Form-factor Pluggable
        Tx -> Rx
        Rx -> Tx

    Multimode Fiber
        -Core diameter is wider than single-mode Fiber
        -Allows multiple angles (modes) of light waves to enter the fiberglass Core
        -Allows longer cables than UTP, but shorter cables than single-mode fiberglass
        -Cheaper than single-mode fiber (due to cheaper LED-based SFP transmitters.)

    Single-mode Fiber
        -Narrow Core
        -Single angle (mode) of light
        -Can be longer
        -More expensive

