# Open Systems Interconnection Reference Model (OSI Model)
- Layers

## OSI Reference Model Layers
![[OSI1.png]]

## Network Devices at Each Layer
![[OSI2.png]]

### Transport Layer Considerations
Connectionless Communication
- UDP
- Considered "best effort", not guaranteed communication
Connection-Oriented Communication
- TCP
- Creates a virtual circuit for communication between two hosts providing reliable delivery
- 3-way handshake to establish virtual circuit (SYN - SYN/ACK - ACK)
- Flow control (retransmission, congestion control, data loss control)
- Windowing (number of data segments "in flight" at any given time)

### Project 802 (IEEE 802 subcommittee)
![[Proj8021.png]]
![[proj8022.png]]
## Encapsulation
1. **User information** is converted to **data** for transmission on the network.
2. **Data** is converted to **segments**, and a reliable connection is set up between transmitting and receiving hosts.
3. **Segments** are converted to **packets or datagrams**, and a logical address is placed in the header so each packed can be routed through an internetwork. A packet carries a segment of data. 
4. **Packets or datagrams** are converted to **frames** for transmission on the local network. Hardware (Ethernet) addresses are used to uniquely identify hosts on a local network segment. Frames carry packets. 
5. **Frames** are converted to **bits**, and a digital encoding and clocking scheme is used. 

# Internet Protocol
![[DODvsOSI.png]]

# IP Addressing
### IP Terminology
- Bit - one binary digit, either a 1 or a 0
- Byte - 7 or 8 bits, depending on the use of parity (Negative or positive for error correction)
- Octet - 8 bits
- Network Address - designation used in routing to send packets to a remote network - for example, 10.0.0.0, 172.16.0.0, and 192.168.10.0
- IP Address - logical address used to define a single host, consists of 32 bits (or 4 octets)
- Broadcast Address - used by applications and hosts to send information to all hosts on a network - example 255.255.255.255

### IP Adress Classes
![[IPAddclasses.png]]
### Broadcast Addresses 
- Broadcast addresses are used to send information to all of the hosts at a particular level. 
- A Layer 2 broadcast address would be FF.FF.FF.FF.FF.FF
- A Layer 3 broadcast address would be 255.255.255.255
- Unicast addresses are used to send packets to a single host.
- Multicast addresses are used by a single host to send packets to multiple hosts. 

# IPv6