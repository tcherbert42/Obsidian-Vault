##### Types of Networks (Naming Classification)
LAN (Local Area Network), PAN (Personal Area Network), CAN (Campus Area Network), MAN (Municipal/Metropolitan Area Network)

LAN - connects a group of hosts in a localized geographic location, such as an office building, workgroup, or home office. Don't have a perfect rule of size, but generally exist under one security organization. 

PAN - Connects a group of devices associated with an individual using a protocol such as Bluetooth or IP. CarPlay, Wireless Key Fob, etc. 
- Like LANs these networks will interact with larger networks to pass data and information. 

WAN (Wide Area Network) - connects multiple network elements over a large geographic area generally using telecommunication circuits. Such large networks generally involve a grouping of LANs connected by routers. 
- The Internet is considered an example of a WAN. 

#### What Kind of stuff is networked 
- Short answer: almost everything
- Our society is the most digitally-connected to date. 
- We generally speak of hosts (workstations, servers, data collection terminals) as part of a network. A host can now be an actuator, meter, sensor, information display, personal digital assistants, tablets, watches, etc.
- Other networking elements which we will talk about soon are switches, routers, packet shapers, firewalls, etc. 

# Network Architectures 
Peer to Peer Networks
- Popular in early PC network designs
- No central agent providing coordination
- Works only in small networks
- The broadcast storm required to share information would saturate larger networks
Client-Server Networks
- Most common format for modern networks (especially in business)
- Central servers provide core time, addressing, directory, name service, storage, and logistical services
- Clients may be advised or totally controlled by central service providers

## Network Topologies
### Bus Network Topology
- Old style networking, very popular with small LANs in the 80s and early 90s
- Relied on an interconnected chain of cable, absolutely no fault tolerance.
- All hosts are connected via a single cable

### Star Network Topology
- More popular
- Requires more physical media
- A cable can fail and only take down the host connected to that cable, not the entire network.. increased fault tolerance. 
- Increased scalability over bus topology

### Ring Network Topology
- Ring networks (sometimes referred to as token ring networks) were popular on early generation networks - especially IBM.
- These networks were considered beneficial for heavy loads where bandwidth consistency was important

### Mesh Network Topology
- Mesh networks are very fault tolerant
- Hosts have multiple network connections. In the case of a full mesh, each host has a direct connection to all the other hosts.
- The internet is an excellent example of a mesh network topology

### Point-to-X Topology
- Point to Point topologies are exactly what they sound like. These topologies provide a direct connection between two network devices. (e.g. a switch to a router)
- Point to Multipoint topologies connect one network device to multiple network devices. Consider a company with branch offices. The company would have a primary router at the main office with links to routers at each branch office. 

### Hybrid Topologies
- You guessed it, this is a combination of two or more of the topologies that we have previously discussed. 
- Almost every mature technology configuration will introduce multiple approaches which include features most beneficial to a specific problem. 

#### Final Thoughts 
- As implied in our discussion of hybrid topologies, various techniques may be used depending on the need of that grouping. 
- A network backbone may look more like a bus topology using star and mesh topology features to provide capacity and fault tolerance. 
- Each network segment which extends from the network backbone will have a configuration to address the needs of the hosts operating within that space. Remember our discussion of wireless mesh networks. 
- 