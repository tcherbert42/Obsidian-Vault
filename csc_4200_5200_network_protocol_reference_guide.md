# **CSC 4200/5200 Computer Networks - Exhaustive Reference Guide**

# **Section 0: Master Quick-Reference Matrix**
[TAGS: Key Term, Synonyms, RFC Numbers, Equation Symbols, Exam Traps, Reference]

## **Alphabetical Symbol Index**
| **Symbol** | **Meaning** | **Unit** | **Exam Trap / Watch Out** |
| :--- | :--- | :--- | :--- |
| **BDP** | Bandwidth-Delay Product | bits | Use RTT for window sizing. Convert bytes to bits. |
| **c** | Speed of light in vacuum | 3.0 × 10^8 m/s | Not the speed in fiber! |
| **cwnd** | Congestion window | bytes / segments | Sender limit; never advertised. |
| **d** | Distance | m | Convert km to m. |
| **FD** | Feasible distance (EIGRP) | cost units | Total cost via successor. |
| **G** | Offered load (ALOHA) | attempts/frame | Includes retransmissions. |
| **L** | Size of message/packet | bits | Convert bytes to bits (multiply by 8). |
| **n** | Prefix length / Seq bits | bits | n=31 has 2 usable hosts. |
| **R** | Link rate (Bandwidth) | b/s | 1 Mb/s = 10^6 b/s. |
| **RD** | Reported distance | cost units | Neighbor's advertised cost, excludes link to neighbor. |
| **RTT** | Round-trip time | s / ms | Do not halve for one-way unless symmetric is explicitly stated. |
| **rwnd** | Receive window | bytes | Flow control limit; protects receiver. |
| **S** | Throughput (ALOHA) / Window-scale | fraction / bits | Fraction of capacity, not bit rate. |
| **ssthresh** | Slow-start threshold | bytes / segments | Drops to half FlightSize on loss. |
| **W** | Window | packets / bytes | Limit: min(cwnd, rwnd). |

## **RFC Registry Table**
| **RFC** | **Protocol/Concept** | **Layer** | **Key Behavioral Mechanics** |
| :--- | :--- | :--- | :--- |
| **768** | UDP | Transport | 8-byte header, connectionless, checksum optional in IPv4/mandatory in IPv6. |
| **791** | IPv4 | Network | 20-60 byte header, best-effort delivery, routers may fragment. |
| **793** | TCP | Transport | Reliable, ordered byte-stream, 3-way handshake, 4-way close. |
| **826** | ARP | Link/Net | Resolves IPv4 to MAC. No authentication, vulnerable to spoofing. |
| **1071** | Internet Checksum | Net/Trans | 16-bit ones'-complement sum. Includes pseudo-header for UDP/TCP. |
| **2328** | OSPF | Network | Protocol 89. Link-state, Dijkstra, floods LSAs within areas. |
| **2644** | BCP 34 / Directed BC | Network | Mitigates Smurf. Directed broadcasts disabled by default. |
| **4271** | BGP-4 | Network | TCP 179. Path-vector, routing as policy, Longest Prefix Match dominance. |
| **4864** | NAT / IPv6 | Network | States NAT is not a security feature. Stateful filtering provides the protection. |
| **5681** | TCP Congestion Ctl | Transport | Defines Slow Start, Congestion Avoidance, Fast Retransmit, Fast Recovery. |
| **5961** | TCP Security | Transport | Challenge ACKs to prevent blind in-window RST injection attacks. |
| **6298** | TCP Timers (RTO) | Transport | Jacobson/Karels algorithm for RTO calculations. |
| **7323** | TCP Extensions | Transport | Window Scale (shift up to 14) and Timestamps (solves Karn's problem). |
| **9000+** | QUIC | Transport | UDP-based, one handshake (incorporates TLS 1.3), independent streams. |
| **9293** | TCP Standard | Transport | Consolidates RFC 793 and others into modern STD 7. |

## **Constants & Standard Timers**
* **RTO Floor**: RFC 6298 recommends a 1-second minimum. Linux (Campus VM) implements a 200 ms floor.
* **TIME_WAIT (2xMSL)**: RFC 9293 specifies MSL = 2 minutes (4 mins total). Linux defaults to 60 seconds total.
* **Ephemeral Ports**: IANA assigns 49,152–65,535. Linux uses 32,768–60,999.
* **Signal Speeds**: Vacuum/Air = $3.0 \times 10^8$ m/s. Optical Fiber = $2.0 \times 10^8$ m/s. Copper = $1.8 \times 10^8$ m/s.

---

# **Section 1: Foundations & Channel Sharing (Ch. 1 / Module 1A)**
[TAGS: 5 Problems, Circuit Switching, Packet Switching, ALOHA, S, G, Throughput, Vulnerable Period, Exam Traps]

## **Five Core Problems of Networking**
1. **Signalling**: How is information represented? (Line codes, frames).
2. **Media Access**: Who transmits on shared channels? (CSMA/CD, ALOHA).
3. **Addressing & Routing**: How does a message reach an unattached destination? (MAC, IP, routing protocols).
4. **Reliability**: How do we know it arrived intact? (FCS, ACKs, retransmissions).
5. **Access Control**: Who is permitted to use the network? (802.1X, firewalls, encryption).

## **Circuit vs. Packet Switching**
| **Feature** | **Circuit Switching** | **Packet Switching** |
| :--- | :--- | :--- |
| **Capacity** | Reserved, guaranteed, wasted if idle. | Shared, statistical multiplexing, no guarantees. |
| **Failures** | Circuit drops if a node fails. | Routes around failures (graceful degradation). |
| **Setup** | Requires setup time/signaling before data flows. | Zero setup; packets sent immediately. |

## **ALOHA Equations & Math Models**

**Formula Definitions:**
* $G$: Offered load (mean transmission attempts per frame time, including retransmissions).
* $S$: Throughput (successful frames per frame time). Fraction of capacity.

**1. Pure ALOHA**
* **Equation**: $S = G e^{-2G}$
* **Vulnerable Period**: 2 frame times.
* **Max Throughput**: $\approx 18.4\%$ at $G = 0.5$.

**2. Slotted ALOHA**
* **Equation**: $S = G e^{-G}$
* **Vulnerable Period**: 1 frame time (slot boundaries cut vulnerability in half).
* **Max Throughput**: $\approx 36.8\%$ at $G = 1.0$.

**Common Misconception & Trap Alert:**
* *Trap*: Assuming Slotted ALOHA is slightly better. *Correction*: It exactly doubles peak throughput by halving the vulnerable period.
* *Trap*: Pushing load past the peak saturates the channel. *Correction*: The channel collapses, throughput falls due to exponential collision retransmissions.

**Worked ALOHA Examples:**
* **Example 1 (Pure ALOHA at $G=0.5$)**:
  $S = 0.5 \times e^{-2(0.5)} = 0.5 \times e^{-1} = 0.5 \times 0.367879 \approx 0.1839$ (18.39%).
* **Example 2 (Slotted ALOHA at $G=1.0$)**:
  $S = 1.0 \times e^{-1.0} = 0.367879 \approx 0.3679$ (36.79%).
* **Example 3 (Pure ALOHA at $G=0.25$)**:
  $S = 0.25 \times e^{-2(0.25)} = 0.25 \times e^{-0.5} = 0.25 \times 0.60653 \approx 0.1516$ (15.16%).

---

# **Section 2: Architecture, Metrics, and Latency (Ch. 2 / Module 1B)**
[TAGS: OSI, TCP/IP, Web Request Trace, Tprop, Ttrans, Delay Breakdown, BDP, RTT, Stop-and-Wait, Window, Exam Traps]

## **Layer Models & End-to-End Argument**
* **OSI Layers**: 7 Application, 6 Presentation, 5 Session, 4 Transport, 3 Network, 2 Data Link, 1 Physical.
* **TCP/IP Layers**: Application (folds 5-7), Transport (4), Internet (3), Link (2).
* **End-to-End Argument**: Link checks only catch link damage. Router memory/software bugs require endpoints to perform final integrity checks (TCP Checksum) (Saltzer, Reed & Clark, 1984).

## **Hop-by-Hop Web Request Trace**
1. **DNS Query**: App layer, UDP to resolver. Completes before TCP starts.
2. **TCP Handshake**: Transport layer. 3-way connection setup.
3. **TLS Handshake**: Presentation layer logic over TCP.
4. **HTTP Request**: Application data sent inside TCP segment -> IP packet -> Ethernet frame.
5. **Address Changes**: IP Destination is end-to-end (unchanged). MAC Destination is hop-by-hop (rewritten by every router).

## **Delay Components & BDP Math**

**Formula Definitions:**
* $T_{total} = T_{prop} + T_{trans} + T_{proc} + T_{queue}$
* $T_{prop} = \frac{d}{v}$ ($d$: distance in meters, $v$: speed of signal in m/s).
* $T_{trans} = \frac{L}{R}$ ($L$: data length in bits, $R$: link bandwidth in b/s).
* **BDP** (Bandwidth-Delay Product) = $R \times RTT$ (gives bits in flight; sizes the TCP window).
* **Stop-and-Wait Utilization**: $U_{sw} = \frac{T_{trans}}{RTT + T_{trans}}$.
* **Window Sizing**: $W \ge \frac{RTT + T_{trans}}{T_{trans}}$.

**Common Misconception & Trap Alert:**
* *Trap*: "Bandwidth and throughput are the same." *Correction*: Bandwidth is link capacity; throughput is measured delivered rate.
* *Trap*: "Doubling bandwidth reduces latency." *Correction*: It halves $T_{trans}$ but does not touch $T_{prop}$.
* *Trap*: Using bytes instead of bits for $L$. Multiply bytes by 8!

**Worked Delay & BDP Examples:**
* **Example 1: Earth-Mars Relay (Dominated by Propagation)**
    * Distance = 225M km = $2.25 \times 10^{11}$ m. Speed in vacuum = $3.0 \times 10^8$ m/s.
    * File = 5 GB = $4.0 \times 10^{10}$ bits. Bandwidth = 100 Mb/s = $10^8$ b/s.
    * $T_{prop} = \frac{2.25 \times 10^{11}}{3.0 \times 10^8} = 750$ seconds.
    * $T_{trans} = \frac{4.0 \times 10^{10}}{10^8} = 400$ seconds. Total = 1150s.
* **Example 2: Undersea Fiber (Dominated by Transmission)**
    * Distance = 12 km = $1.2 \times 10^4$ m. Speed in fiber = $2.0 \times 10^8$ m/s.
    * File = 10 MB = $8.0 \times 10^7$ bits. Bandwidth = 50 Mb/s = $5.0 \times 10^7$ b/s.
    * $T_{prop} = \frac{1.2 \times 10^4}{2.0 \times 10^8} = 0.00006$ seconds (0.06 ms).
    * $T_{trans} = \frac{8.0 \times 10^7}{5.0 \times 10^7} = 1.6$ seconds. Total = 1.60006s.
* **Example 3: BDP Socket Buffer Sizing**
    * Link 200 Mb/s, RTT 35 ms.
    * $BDP = 2.0 \times 10^8 \text{ b/s} \times 0.035 \text{ s} = 7.0 \times 10^6 \text{ bits} = 875,000 \text{ bytes}$ (875 kB).

---

# **Section 3: Physical & Data Link Layers (Ch. 3 / Module 2)**
[TAGS: Cat 5e/6, Fiber, Line Coding, Manchester, Ethernet Frame, MAC, 802.1Q, VLAN, Spanning Tree, BPDU, CRC, Parity, ARP Spoofing, WPA]

## **Media Limits & Line Codes**
* **Twisted Pair**: Cat 6 handles 10GBASE-T to ~55m (alien crosstalk). Cat 6A handles 10GBASE-T to full 100m channel. Higher category = more bandwidth, not more distance.
* **Fiber**: 1000BASE-SX (MMF) reaches ~550m. 10GBASE-SR reaches ~400m on OM4. Single-mode removes modal dispersion.
* **Line Codes (Clock Recovery)**:
    * **Manchester (IEEE 802.3)**: Low-to-high = 1, High-to-low = 0. Overhead 100%. (G.E. Thomas is the reverse!).
    * **Block Codes**: 4B/5B and 8B/10B (25% overhead, DC balance). 64B/66B (~3% overhead, scrambling).
    * **1000BASE-T**: Uses 8B1Q4, 4D-PAM5 over 4 pairs. (Fiber gigabit uses 8B/10B).

## **Ethernet Frame & 802.1Q VLAN Tag**
* **Frame Sizes**: 64–1518 bytes. Payload is 46–1500 bytes.
* **Layout (Byte Offsets)**:
    * 0: Destination MAC (6 bytes)
    * 6: Source MAC (6 bytes)
    * 12: EtherType (2 bytes) - e.g., 0x0800 IPv4, 0x0806 ARP, 0x86DD IPv6.
    * 14: Payload (46-1500 bytes)
    * FCS (4 bytes at end): Covers Destination MAC through Payload.
* **802.1Q Shift**: Inserts 4 bytes (TPID 0x8100, TCI/VID) at offset 12. EtherType shifts to byte 16. VID is 12 bits (4094 usable VLANs).

## **Switching & Spanning Tree Protocol (STP / 802.1Q-2022)**
* **Domains**: Switches divide collision domains. Routers divide broadcast domains. Hubs divide neither.
* **STP Convergence Steps (RSTP)**:
  1. Elect Root Bridge: Lowest Bridge ID (Priority first, then MAC). Default priority is 32768.
  2. Elect Root Ports: Lowest path cost to root.
  3. Elect Designated Ports: One per segment to forward. Rest block.

## **Error Detection: Parity, Checksum, CRC**
* **Parity**: Detects odd bit flips.
* **Internet Checksum**: 16-bit ones'-complement sum.
* **CRC Guarantee**: Detects all 1-bit errors, and burst errors up to length r. FCS proves integrity, NOT authenticity.

**Worked CRC Examples (XOR Long Division):**
* **Example 1**: Message 1101011011, Gen 10011 (r=4). Append 0000 $\rightarrow$ 11010110110000.
  1. 11010 XOR 10011 = 01001. Str = 01001110110000.
  2. 10011 XOR 10011 = 00000. Str = 00000010110000.
  3. 10110 XOR 10011 = 00101. Str = 00000000101000.
  4. 10100 XOR 10011 = 00111. Str = 00000000001110. **Remainder: 1110**.
* **Example 2**: Message 101101, Gen 1101 (r=3). Append 000 $\rightarrow$ 101101000.
  1. 1011 XOR 1101 = 0110. Str = 011001000.
  2. 1100 XOR 1101 = 0001. Str = 00011000.
  3. 1100 XOR 1101 = 0001. Str = 00000100. **Remainder: 010**.
* **Example 3**: Message 100110, Gen 1011 (r=3). Append 000 $\rightarrow$ 100110000.
  1. 1001 XOR 1011 = 0010. Str = 001010000.
  2. 1010 XOR 1011 = 0001. Str = 000001000.
  3. 1000 XOR 1011 = 0011. Str = 000000011. **Remainder: 011**.

## **Layer 2 Attacks & Wi-Fi Security**
* **ARP Spoofing**: No auth on ARP. Machine-in-middle. Fix: Dynamic ARP Inspection (DAI) + DHCP Snooping.
* **MAC Flooding**: Overflows switch table to force hub-like flooding. Fix: Port Security.
* **WEP Flaws**: 1) Linear unkeyed CRC-32 (attacker flips bits and updates CRC via XOR). 2) 24-bit IV reused (keystream collision). 3) IV+Key leaks key bytes via RC4 (FMS 2001). Not dependent on key length!
* **WPA Evolution**: WPA (TKIP), WPA2 (CCMP/AES, pre-shared key doesn't separate local users), WPA3 (SAE, resists offline guess, forward secrecy).

---

# **Section 4: Network Layer & Routing (Ch. 4 / Module 3)**
[TAGS: Forwarding vs Routing, IPv4 Header, Subnetting, CIDR, VLSM, LPM, IPv6, NDP, Dijkstra, Bellman-Ford, OSPF, EIGRP, BGP, NAT, BCP 38, Route 53]

## **Forwarding vs Routing**
* **Routing**: Control plane (seconds/mins). Builds the routing table.
* **Forwarding**: Data plane (microseconds). Reads the FIB, uses Longest Prefix Match (LPM).
* **Longest Prefix Match (LPM)**: Specificity decides. Metric/protocol are strictly ignored for forwarding! 10.1.2.0/24 directly beats 10.1.0.0/16.

## **IPv4 Header & Fragmentation**
* **IPv4 Header**: 20 bytes min. IHL counts 32-bit words (e.g. IHL 7 = 28 bytes). TTL decremented every hop.
* **Fragmentation**: IPv4 routers fragment. IPv6 routers NEVER fragment (source uses ICMPv6 Packet Too Big for PMTUD). RFC 8900 calls fragmentation fragile; modern protocols avoid it.

## **Subnetting, CIDR, & VLSM Math**

**Formula Definitions:**
* Block Size = $2^{32-n}$.
* Usable Hosts = $2^{32-n} - 2$. (Exceptions: /31 has 2 usable for P2P via RFC 3021, /32 is a host route).

**Common Misconception & Trap Alert:**
* *Trap*: "Class C address." *Correction*: Classes deprecated in 1993/2006. Rely only on prefix length.
* *Trap*: Allocating subnets smallest first. *Correction*: Always allocate largest first on block boundaries.

**Worked VLSM Example:**
* From 203.0.113.0/24, allocate 100 hosts, 50 hosts, 2 P2P links.
  1. **100 hosts**: Needs 126 ($2^7-2$). $h=7$. Prefix 32-7 = /25. Range: 203.0.113.0/25 (.0 - .127).
  2. **50 hosts**: Needs 62 ($2^6-2$). $h=6$. Prefix 32-6 = /26. Range: 203.0.113.128/26 (.128 - .191).
  3. **Link 1**: Needs 2 hosts. $h=2$. Prefix 32-2 = /30. Range: 203.0.113.192/30 (.192 - .195).
  4. **Link 2**: Needs 2 hosts. Range: 203.0.113.196/30 (.196 - .199).

## **IPv6 Architecture & NDP**
* **Prefixes**: Global 2000::/3. Unique Local fc00::/7 (in practice fd00::/8). Link-Local fe80::/10. Loopback ::1/128. Multicast ff00::/8. No broadcast!
* **Multicast Structure**: ff[flags][scope]::[group]. E.g., ff02::1 (flags 0 permanent, scope 2 link-local, group 1 all-nodes).
* **NDP**: Replaces ARP. Uses ICMPv6. Target address is the Solicited-Node Multicast: ff02:0:0:0:0:1:ff00::/104 + low 24 bits.
* *Worked Ex*: Address 2001:db8::9c5:7e01. Low 24 bits: c5:7e:01. SNM = ff02::1:ffc5:7e01.

## **Routing Algorithms**
* **Distance-Vector (Bellman-Ford)**: Exchange conclusions. Vulnerable to Count-to-Infinity. Fixes: Split horizon (2-node loops only), poison reverse, hold-down.
  * **RIP**: 15 hops max (16 is infinity). Slow 30s updates.
  * **EIGRP**: Feasibility Condition: $RD_{neighbor} < FD_{router}$. (If neighbor's advertised cost is strictly less than my current best total, it guarantees no loops).
* **Link-State (Dijkstra)**: Exchange topology (LSAs). Computes shortest path tree locally.
  * **OSPF**: Protocol 89. Areas limit flooding (Area 0 backbone).
  * *Dijkstra Trace Ex*: R1 to R5. Paths: R1-R3(cost 5), R1-R2(cost 2). Next: R2-R3(cost 2). Shortest R1 to R3 is R1-R2-R3 (cost 4), beating direct link (cost 5). Shortest means lowest total cost, not fewest hops.
* **BGP (Path-Vector)**: AS_PATH loop prevention. Policy Outranks Topology (LOCAL_PREF beats distance).
  * **Prefix Hijacking**: 2008 YouTube (AS17557 announced /24 inside YouTube's /22, won via LPM). 2018 Route 53 ($150k stolen, /24 announced over /23).
  * **RPKI ROV**: Valid (Origin AS & length match), Invalid (Prefix covered, but AS wrong or length exceeds max), NotFound.

## **Network Layer Security**
* **NAT**: Not a security feature (RFC 4864). Stateful filtering provides the actual protection.
* **Spoofing**: Defeated via BCP 38 Ingress Filtering.
* **ICMP**: Blocking ICMPv6 wholesale disables IPv6 (breaks NDP and PMTUD).

---

# **Section 5: Transport Layer (Ch. 5 / Module 4)**
[TAGS: TCP, UDP, 4-Tuple, Sockets, API, Connections, States, Jacobson/Karels, RTO, Congestion Control, CUBIC, BBR, QUIC, Exam Traps]

## **UDP vs TCP & Headers**
* **4-Tuple Demultiplexing**: Server uses [Src IP, Src Port, Dst IP, Dst Port] to route segments to correct established socket. Listener uses 2-tuple.
* **UDP**: 8-byte header (Src Port, Dst Port, Length, Checksum). Pseudo-header includes IP fields to catch misdelivery.
* **TCP**: 20-60 byte header. Sequence/ACK fields count *bytes*, not messages.

## **Socket API: C vs Python**
| **C API** | **Python API** | **TCP Wire Action** |
| :--- | :--- | :--- |
| socket() | socket.socket() | None. Creates endpoint. |
| bind() | .bind() | None. Claims local port. SO_REUSEADDR bypasses TIME_WAIT lock. |
| listen() | .listen() | Enters LISTEN state. |
| connect() | .connect() | Sends SYN. Blocks until SYN-ACK processed. |
| accept() | .accept() | None. Retrieves already ESTABLISHED socket from queue. |
| send() | .send() / .sendall() | Copies data to buffer. Does NOT guarantee delivery. |
| recv() | .recv() | Returns available bytes. Returns 0 on peer's FIN. Use recv_exact loop! |
| shutdown() | .shutdown(SHUT_WR) | Sends FIN. Half-close. |

## **TCP Connection & States**
* **Handshake**: SYN (seq=X), SYN-ACK (seq=Y, ack=X+1), ACK (seq=X+1, ack=Y+1). SYN and FIN each consume 1 seq number.
* **11 States**: CLOSED, LISTEN, SYN-SENT, SYN-RECEIVED, ESTABLISHED, FIN-WAIT-1, FIN-WAIT-2, CLOSE-WAIT, CLOSING, LAST-ACK, TIME-WAIT.
* **TIME_WAIT**: Active closer waits 2xMSL to catch stray packets and ensure final ACK delivery.

## **Reliability Bounds & Timers**
* **Go-Back-N**: Window $\le 2^n - 1$. Resends everything after loss.
* **Selective Repeat**: Window $\le 2^{n-1}$. Sender and receiver buffer. Resends only the missing segment.
* **TCP Timers (RFC 6298)**:
  * $SRTT = (1-\alpha) SRTT + \alpha R$ (where $\alpha = 1/8$)
  * $RTTVAR = (1-\beta) RTTVAR + \beta |SRTT - R|$ (where $\beta = 1/4$)
  * $RTO = SRTT + \max(G, 4 \times RTTVAR)$
* **Karn's Algorithm**: Do NOT update timers using retransmitted segments (unless Timestamps option is active).

**Common Misconception & Trap Alert:**
* *Trap*: Using a fast link will speed up Stop-and-Wait. *Correction*: RTT dominates S&W. $U = d_{trans}/(RTT + d_{trans})$. Huge waste on high-BDP paths.
* *Trap*: "One send() equals one recv()." *Correction*: TCP is a byte stream. Framing logic must be manual.

**Worked RTO Trace Example (RFC 6298):**
* Given $R_1=600$ms, $R_2=680$ms, $R_3=560$ms, $G=1$ms.
  1. **Init**: $SRTT = 600$, $RTTVAR = 300$, $RTO = 600 + 4(300) = 1800$ms.
  2. **Sample 2 (680)**: $RTTVAR = (0.75 \times 300) + (0.25 \times |600-680|) = 225 + 20 = 245$ms. $SRTT = (0.875 \times 600) + (0.125 \times 680) = 525 + 85 = 610$ms. $RTO = 610 + 4(245) = 1590$ms.
  3. **Sample 3 (560)**: $RTTVAR = (0.75 \times 245) + (0.25 \times |610-560|) = 183.75 + 12.5 = 196.25$ms. $SRTT = (0.875 \times 610) + (0.125 \times 560) = 533.75 + 70 = 603.75$ms. $RTO = 603.75 + 4(196.25) = 1388.75$ms.

## **Congestion Control**
* **Window Limit**: $W \le \min(cwnd, rwnd)$.
* **Slow Start (SS)**: Double cwnd every RTT.
* **Congestion Avoidance (CA)**: Additive increase (1 MSS per RTT) when cwnd > ssthresh.
* **Loss via 3 Dup ACKs (Fast Retransmit)**: Reno cuts cwnd in half ($ssthresh = cwnd/2$), enters Fast Recovery.
* **Loss via Timeout**: Cwnd resets to 1. Slow Start restarts.
* **Algorithms**:
  * *Tahoe*: Drops to 1 on any loss.
  * *Reno*: Halves on 3 dup ACKs (Fast Recovery).
  * *Vegas*: Slows before loss based on rising RTT. Loses to Reno.
  * *CUBIC*: $W(t) = C(t-K)^3 + W_{max}$. Regains $W_{max}$ quickly, flattens out, probes aggressively. Default in Linux/Windows/macOS.
  * *BBR*: Models bottleneck capacity and min RTT. Paces traffic. (Not an RFC yet, Internet-Draft).

**Worked Congestion Window Example:**
* Round 1-5 (SS): 1, 2, 4, 8, 16, 32. (Crosses ssthresh=32).
* Round 5-9 (CA): 32, 33, 34, 35.
* Round 9: 3 Dup ACKs. $ssthresh = 35/2 = 17$. $cwnd = 17$. CA resumes.

## **Transport Attacks & QUIC**
* **SYN Floods**: Resource exhaustion. Fix: SYN Cookies (cryptographic state in seq num), breaks TCP Options.
* **Blind RST Injection**: Tears down connection. Fix: RFC 5961 Challenge ACKs requiring exact sequence match.
* **UDP Amplification**: Forged source + large reply. DNS (54x), NTP (556x), Memcached (51000x). Fix: BCP 38 Ingress Filtering.
* **QUIC (RFC 9000)**: Runs over UDP. Built-in TLS 1.3 (one combined handshake). No Head-of-Line blocking (independent streams). Connection IDs support IP migration. Protects ACKs.

---

# **Section 6: Solved Benchmark Practice Scenarios**
[TAGS: Exam Scenarios, Part B, Diagnosis, Routing, Delay, Bandwidth, Root Cause, Subnet Overlap, OSPF/RIP Convergence]

## **Scenario 1: The upload that takes all morning**
*A 45 MB file over 30 Mb/s fiber link (2400 km).*
1. **$T_{prop}$ & $T_{trans}$**:
   * $T_{prop} = (2.4 \times 10^6 \text{ m}) / (2.0 \times 10^8 \text{ m/s}) = 0.012 \text{ s} = 12 \text{ ms}$.
   * $T_{trans} = (45 \times 10^6 \times 8 \text{ bits}) / (3.0 \times 10^7 \text{ b/s}) = 3.6 \times 10^8 / 3.0 \times 10^7 = 12 \text{ seconds}$.
   * Total one-way = 12.012 s. Transmission dominates (99.9%).
2. **Stop-and-Wait (1200 byte blocks)**:
   * $RTT = 24 \text{ ms}$.
   * $d_{trans} = (1200 \times 8) / (3.0 \times 10^7) = 0.00032 \text{ s} = 0.32 \text{ ms}$.
   * Utilization = $0.32 / (24 + 0.32) = 1.32\%$.
   * Total time = 37,500 blocks $\times 0.02432 \text{ s/cycle} = 912 \text{ s}$ (15.2 minutes!).
3. **Upgrade to 60 Mb/s**:
   * New $d_{trans} = 0.16 \text{ ms}$. Cycle = 24.16 ms. Total = 906 s. Link upgrade fails because the protocol is the bottleneck, saving less than 1%.
4. **BDP / Window Sizing**:
   * $BDP_{RTT} = 3.0 \times 10^7 \text{ b/s} \times 0.024 \text{ s} = 720,000 \text{ bits} = 90,000 \text{ bytes}$.
   * Unscaled 65,535 byte TCP window limits throughput to $65535 \times 8 / 0.024 = 21.8 \text{ Mb/s}$ (73% of capacity). Window scaling with a shift of 1 is required.

## **Scenario 2: Where did the half-second go?**
*HTTPS Load. DNS=32ms, RTT=45ms, Server=18ms, Page=900kB, BW=24 Mb/s.*
1. **Exchange Sequence**: DNS Query (App/UDP) $\rightarrow$ TCP Handshake (Transport/TCP) $\rightarrow$ TLS Handshake (Presentation/TCP) $\rightarrow$ HTTP Request (App/TCP).
2. **Delay Calculation**:
   * $T_{first\_byte} = T_{DNS} + RTT_{TCP} + RTT_{TLS} + (RTT + T_{server}) = 32 + 45 + 45 + (45 + 18) = 185 \text{ ms}$.
   * $T_{rest} = L/R = (900 \times 10^3 \times 8) / 2.4 \times 10^7 = 300 \text{ ms}$.
   * Total = 185 + 300 = 485 ms.
3. **Upgrades**: Upgrading to 96 Mb/s drops $T_{rest}$ to 75ms (saves 225ms). CDN at 9ms drops $T_{first\_byte}$ to 77ms (saves 108ms). Bandwidth upgrade helps more here due to file size.
4. **Address Roles**: IP Dest names the web server and is end-to-end. MAC Dest names the gateway and is rewritten at every hop.

## **Scenario 3: The printer the staff office cannot reach**
*Subnets: Staff 192.0.2.0/25 (GW .1), Lab 192.0.2.128/26 (GW .129). Printer set to 192.0.2.140, Mask /25, GW 192.0.2.1.*
1. **Diagnosis**: Printer's /25 mask means it believes its subnet is 192.0.2.128/25 (.129 to .254). Gateway .1 is outside this subnet, making it unreachable.
2. **Lab works**: Lab hosts (.150) are inside .128/26, so they ARP directly. Printer sees .150 inside its .128/25 and ARPs back directly over the same VLAN.
3. **Staff fails**: Staff host (.20) sends to .1. Router forwards to Printer. Printer's reply to .20 evaluates as off-subnet, tries to send to GW .1, but cannot ARP for .1 on the Lab VLAN. Packet dropped.
4. **Fix**: Mask 255.255.255.192 (/26), Gateway 192.0.2.129.
5. **Growth to 75 hosts**: Needs a /25 ($126 \ge 75$). Cannot simply expand to .128/25 as it overlaps the Guest/Router links. Requires renumbering the upper block.

## **Scenario 4: The servers that vanished**
*R1 has 203.0.113.0/24 (OSPF) and stale 203.0.113.64/26 (Static to R9).*
1. **LPM Rule**: Forwarding strictly uses Longest Prefix Match. Metric/Protocol are completely ignored during forwarding.
2. **Trace**: .70 and .100 fall inside the stale /26 (range .64 - .127) and are forwarded to the dead R9 router. .20 and .200 fall to the /24 and route correctly.
3. **OSPF Rerouting (Link Failure)**: If R4-R5 fails, OSPF converges in seconds because Link-State floods the failure and Dijkstra re-runs locally with full topology. Distance-Vector (RIP) would slowly count to infinity since it lacks topological knowledge.