# Networking — Technical Study Notes

> **Why it is asked:** Networking questions appear in every past BMA Signals (CSE) paper and account for 30–50 marks in the technical section. OSI model, TCP/IP model, TCP vs UDP, and DHCP/ARP/DNS are the single most repeated topics.

---

## 1. OSI Model (7 Layers)

Asked as a 10-mark descriptive in multiple papers. Memorise the layer name, function, and one example protocol per layer.

```
Layer 7  Application   — User interface to network services       HTTP, FTP, DNS, SMTP
Layer 6  Presentation  — Data formatting, encryption, compression SSL/TLS, JPEG
Layer 5  Session       — Establishing, managing, terminating sessions  NetBIOS, RPC
Layer 4  Transport     — End-to-end delivery, flow/error control   TCP, UDP
Layer 3  Network       — Logical addressing, routing              IP, ICMP, ARP*
Layer 2  Data Link     — Physical addressing (MAC), framing       Ethernet, PPP
Layer 1  Physical      — Bits on the wire, cables, signals        Hubs, cables
```

*ARP operates between Layers 2 and 3 (sometimes called Layer 2.5).

**Memory aid:** "All People Seem To Need Data Processing" (top-down) or "Please Do Not Throw Sausage Pizza Away" (bottom-up).

---

## 2. TCP/IP Model (4 or 5 layers)

Asked equally often as OSI. The 4-layer version is standard; 5-layer is also acceptable.

| TCP/IP Layer (4) | TCP/IP Layer (5) | OSI equivalent |
|---|---|---|
| Application | Application | 5, 6, 7 |
| Transport | Transport | 4 |
| Internet | Network | 3 |
| Network Access | Data Link + Physical | 1, 2 |

Key protocols per layer:
- **Application:** HTTP(80), HTTPS(443), FTP(20/21), SSH(22), SMTP(25), DNS(53), DHCP(67/68), TELNET(23)
- **Transport:** TCP, UDP
- **Internet:** IP (IPv4/IPv6), ICMP, ARP, RARP
- **Network Access:** Ethernet (IEEE 802.3), Wi-Fi (IEEE 802.11)

> **Common trap from source file:** The source incorrectly lists SSH port as 222. SSH is port **22**.

---

## 3. TCP vs UDP

A guaranteed 10-mark question in almost every paper.

| Feature | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented (3-way handshake) | Connectionless |
| Reliability | Guaranteed delivery, retransmission | Best-effort, no retransmission |
| Order | In-order delivery | No ordering |
| Speed | Slower (overhead) | Faster |
| Flow control | Yes (sliding window) | No |
| Error detection | Yes (checksum + ACK) | Checksum only |
| Use cases | Web, email, file transfer | Video streaming, VoIP, DNS |
| Header size | 20 bytes minimum | 8 bytes |

**TCP 3-way handshake:**
```
Client ──SYN──────────────► Server
Client ◄─SYN-ACK─────────── Server
Client ──ACK──────────────► Server
         Connection established
```

---

## 4. ARP and RARP

| Protocol | Maps | Direction | When used |
|---|---|---|---|
| ARP (Address Resolution Protocol) | IP address → MAC address | Logical to Physical | When you know the destination IP but need its MAC to send a frame on the local network |
| RARP (Reverse ARP) | MAC address → IP address | Physical to Logical | Legacy; used by diskless workstations to get their IP; replaced by DHCP |

**How ARP works:**
1. Device A wants to send to IP `192.168.1.10` on the same subnet.
2. A broadcasts: "Who has `192.168.1.10`? Tell `192.168.1.1`."
3. The device with that IP replies with its MAC address.
4. A caches the IP→MAC mapping in its ARP cache.

---

## 5. DHCP — Four-Step Process (DORA)

A 10-mark question in the 54th paper. Know all four steps and what each message does.

```
Client            DHCP Server
  │──DHCPDISCOVER──────────►│   Broadcast: "Any DHCP server out there?"
  │◄─DHCPOFFER──────────────│   Unicast/Broadcast: "Use IP x.x.x.x, lease 24h"
  │──DHCPREQUEST────────────►│   Broadcast: "I accept the offer from server y"
  │◄─DHCPACK────────────────│   "Confirmed. IP x.x.x.x is yours."
```

- **D** — Discover (client → broadcast)
- **O** — Offer (server → client)
- **R** — Request (client → broadcast, confirms choice)
- **A** — Acknowledge (server → client, finalises lease)

DHCP assigns: IP address, subnet mask, default gateway, DNS server, lease duration.  
DHCP replaced RARP and eliminates manual IP configuration.

---

## 6. DNS — Domain Name System

Converts human-readable names (e.g. `www.army.mil.bd`) to IP addresses.

```
Client                 Recursive Resolver          Root Server       TLD Server (.bd)      Authoritative Server
  │──"What is IP of www.army.mil.bd?"──►│
  │                                      │──────────────►│
  │                                      │◄──"Ask .bd TLD"─
  │                                      │───────────────────────────────►│
  │                                      │◄──"Ask army.mil.bd auth"────────
  │                                      │──────────────────────────────────────────────►│
  │                                      │◄──IP: 103.x.x.x──────────────────────────────
  │◄──IP: 103.x.x.x──────────────────────│
```

DNS hierarchy: Root (`.`) → TLD (`.bd`, `.com`) → Second-level (`army.mil`) → Subdomain (`www`)

DNS uses **UDP port 53** (queries); **TCP port 53** (zone transfers / large responses).

---

## 7. Network Topologies

| Topology | Description | Advantage | Disadvantage |
|---|---|---|---|
| Bus | Single backbone cable; all devices tap in | Simple, cheap | Single point of failure; collisions |
| Ring | Devices in a closed loop; data travels one direction | Equal access; deterministic | One failure can break the ring |
| Star | All devices connect to a central hub/switch | Easy to add devices; fault isolation | Central hub is single point of failure |
| Tree | Hierarchical; star networks connected to a bus | Scalable | Complex cabling; root failure cascades |
| Mesh | Every device connected to every other | Highly fault-tolerant | Expensive; complex |

Most common in exams: Bus, Ring, Star (describe these three if asked "any three").

---

## 8. IPv4 vs IPv6

| Feature | IPv4 | IPv6 |
|---|---|---|
| Address length | 32 bits | 128 bits |
| Address format | Dotted decimal: `192.168.1.1` | Hexadecimal: `2001:db8::1` |
| Address space | ~4.3 billion | ~340 undecillion |
| Header size | 20 bytes (min) | 40 bytes (fixed) |
| NAT required? | Yes (address exhaustion) | No |
| Security | Optional (IPSec) | Built-in IPSec support |
| Broadcast | Yes | No (multicast/anycast instead) |
| Configuration | Manual or DHCP | SLAAC or DHCPv6 |

### IP Class ranges (IPv4)

| Class | First octet | Default subnet mask | Hosts per network |
|---|---|---|---|
| A | 1–126 | 255.0.0.0 | ~16.7 million |
| B | 128–191 | 255.255.0.0 | ~65,534 |
| C | 192–223 | 255.255.255.0 | 254 |
| D | 224–239 | — | Multicast |
| E | 240–255 | — | Reserved / experimental |

---

## 9. Subnetting — Finding Network, Broadcast, and Host Range

Given IP `192.168.10.2/10`:

1. CIDR `/10` → subnet mask `255.192.0.0`
2. Network address: bitwise AND of IP and mask → `192.128.0.0`
3. Broadcast: set all host bits to 1 → `192.191.255.255`
4. First host: network + 1 → `192.128.0.1`
5. Last host: broadcast − 1 → `192.191.255.254`

**Quick rule:** Hosts per subnet = 2^(32 − prefix) − 2.

---

## 10. Physical, Logical, and Port Addresses

| Type | Layer | Example | Purpose |
|---|---|---|---|
| Physical (MAC) address | Data Link (Layer 2) | `AA:BB:CC:DD:EE:FF` | Identifies a NIC on a local network |
| Logical (IP) address | Network (Layer 3) | `10.0.0.1` | Identifies a host globally; used for routing |
| Port address | Transport (Layer 4) | `80` (HTTP), `22` (SSH) | Identifies a specific process/service on a host |

Together these three addresses identify: **which machine** (MAC), **where globally** (IP), **which service** (port).

---

## 11. Switch vs Router vs Hub

| Device | Layer | Function |
|---|---|---|
| Hub | Physical (1) | Broadcasts all frames to all ports; no intelligence |
| Switch | Data Link (2) | Forwards frames using MAC address table; creates separate collision domains |
| Router | Network (3) | Routes packets between different networks using IP; separates broadcast domains |

---

## 12. Bandwidth and Latency

- **Bandwidth:** Maximum data transfer rate of a link, measured in bps (bits per second). E.g., a 100 Mbps Ethernet link.
- **Latency (delay):** Time for one packet to travel from source to destination, measured in milliseconds. Made up of propagation delay + transmission delay + queuing delay + processing delay.

High bandwidth does not mean low latency. A satellite link can have 50 Mbps bandwidth but 600 ms latency.

---

## 13. VPN (Virtual Private Network)

A VPN creates an encrypted tunnel over a public network (Internet) so remote users access a private network securely.

**Types:** Client-to-Site (remote access) and Site-to-Site (connecting two office LANs).  
**Advantages:** Encrypted, secure remote access; simulates being on local network.  
**Disadvantages:** Slower (encryption overhead); complex setup; company policy may extend to personal devices.

---

## 14. Telnet vs SSH

| Feature | Telnet | SSH |
|---|---|---|
| Port | 23 | 22 |
| Security | Plaintext (no encryption) | Encrypted |
| Use case | Legacy; avoid in production | Secure remote shell/login |

Use SSH from a remote location — Telnet sends credentials in plaintext, making it vulnerable to sniffing.

---

## Q&A Bank

### True / False

**T1.** OSI stands for Open Systems Interconnection.  
→ **True**

**T2.** TCP is a connectionless protocol.  
→ **False** (TCP is connection-oriented; UDP is connectionless.)

**T3.** UDP guarantees delivery of packets.  
→ **False** (UDP is best-effort; no acknowledgements.)

**T4.** ARP maps an IP address to a MAC address.  
→ **True**

**T5.** DHCP uses the four-step DORA process: Discover, Offer, Request, Acknowledge.  
→ **True**

**T6.** SSH operates on port 22.  
→ **True**

**T7.** A router operates at the Network layer (Layer 3) of the OSI model.  
→ **True**

**T8.** IPv6 uses 32-bit addresses.  
→ **False** (IPv6 uses 128-bit addresses; IPv4 uses 32-bit.)

**T9.** A star topology uses a central hub or switch.  
→ **True**

**T10.** DNS uses UDP port 53 for standard queries.  
→ **True**

---

### MCQ

**Q1.** The OSI layer responsible for routing is:  
(a) Data Link  (b) Transport  (c) Network  (d) Session  
→ **(c)** Network layer

**Q2.** ARP maps:  
(a) MAC → IP  (b) IP → MAC  (c) IP → port  (d) domain → IP  
→ **(b)** IP → MAC

**Q3.** Which protocol automatically assigns IP addresses to devices on a network?  
(a) ARP  (b) RARP  (c) DNS  (d) DHCP  
→ **(d)** DHCP

**Q4.** TCP uses which mechanism to establish a connection?  
(a) 2-way handshake  (b) 3-way handshake  (c) 4-way handshake  (d) No handshake  
→ **(b)** 3-way handshake (SYN, SYN-ACK, ACK)

**Q5.** Which IP class supports the largest number of hosts per network?  
(a) Class A  (b) Class B  (c) Class C  (d) Class D  
→ **(a)** Class A (~16.7 million hosts)

**Q6.** Consider the following C program:  
```c
m = x; n = y;
while (m != n) {
    if (m > n) m = m - n;
    else n = n - m;
}
```  
What does it compute?  
(a) x + y  (b) x mod y  (c) GCD of x and y  (d) LCM of x and y  
→ **(c)** GCD (Euclid's subtraction method)

**Q7.** Which device operates at Layer 2 of the OSI model?  
(a) Hub  (b) Router  (c) Switch  (d) Repeater  
→ **(c)** Switch

**Q8.** How many layers does the OSI model have?  
(a) 4  (b) 5  (c) 6  (d) 7  
→ **(d)** 7

---

### Descriptive Q&A

**Q.** Write the OSI model layers and briefly describe each. (10 marks)

**A.**  
The OSI (Open Systems Interconnection) model is a conceptual framework that standardises the functions of a communication system into 7 layers:

1. **Physical (Layer 1):** Transmits raw bits over a physical medium (cables, radio waves). Deals with voltage, timing, and signal encoding. Devices: hubs, repeaters.
2. **Data Link (Layer 2):** Packages bits into frames, handles MAC addressing, error detection (CRC), and flow control on a single link. Devices: switches, bridges.
3. **Network (Layer 3):** Routes packets across networks using logical (IP) addressing. Devices: routers.
4. **Transport (Layer 4):** Provides end-to-end communication; TCP offers reliable, ordered delivery; UDP offers fast, best-effort delivery.
5. **Session (Layer 5):** Manages sessions (open, maintain, close) between applications. Example: NetBIOS, RPC.
6. **Presentation (Layer 6):** Translates data formats, handles encryption/decryption and compression. Example: SSL/TLS, JPEG.
7. **Application (Layer 7):** Provides network services directly to user applications. Example: HTTP, FTP, SMTP, DNS.

---

**Q.** What is DNS? Illustrate with a diagram. (10 marks)

**A.**  
DNS (Domain Name System) is a hierarchical distributed database that translates human-readable domain names (e.g. `www.google.com`) into IP addresses (e.g. `142.250.80.36`) that computers use to communicate.

```
User types: www.google.com
     │
     ▼
  Local Cache? ─Yes─► Use cached IP
     │No
     ▼
  Recursive Resolver (ISP/router)
     │
     ├──► Root Server (.) ── "Ask .com TLD"
     │
     ├──► TLD Server (.com) ── "Ask google.com auth"
     │
     └──► Authoritative Server (google.com) ── returns IP
     │
     ▼
  IP returned to client → connection established
```

Key points:
- DNS uses **UDP port 53** (queries) / TCP port 53 (zone transfers)
- **Hierarchy:** Root → TLD → Second-level domain → Subdomain
- **Caching:** Results cached for TTL (time-to-live) to reduce lookups
- Without DNS, users would need to remember IP addresses for every website

---

**Q.** Explain the DHCP four-step process. (10 marks)

**A.**  
DHCP (Dynamic Host Configuration Protocol) automatically assigns IP addresses and network settings to devices when they join a network, replacing manual configuration.

Four steps (DORA):

1. **Discover** — The client broadcasts a `DHCPDISCOVER` message on the network, searching for any available DHCP server.
2. **Offer** — One or more DHCP servers reply with `DHCPOFFER`, proposing an IP address, subnet mask, gateway, DNS server, and lease duration.
3. **Request** — The client selects one offer and broadcasts `DHCPREQUEST` to confirm its choice (and implicitly decline other offers).
4. **Acknowledge** — The chosen server sends `DHCPACK`, confirming the IP assignment. The client configures its network interface.

```
Client    ──DISCOVER (broadcast)──►  [All DHCP servers]
Client    ◄──OFFER (IP: 10.0.0.5)──  Server A
Client    ──REQUEST (accept A)──►    [broadcast]
Client    ◄──ACK──────────────────   Server A
             IP 10.0.0.5 is yours!
```

Without DHCP, every device would need a manually assigned static IP, which is error-prone and does not scale.

---

**Q.** Differentiate between physical address, logical address, and port address. (10 marks)

**A.**  
These three address types work together to deliver data to the correct application on the correct machine:

**Physical Address (MAC address):**
- Layer 2 (Data Link)
- 48-bit address burned into a NIC; written as `AA:BB:CC:DD:EE:FF`
- Identifies a device on a *local* network segment
- Used by switches for frame forwarding

**Logical Address (IP address):**
- Layer 3 (Network)
- IPv4: 32-bit, e.g. `10.0.0.1`; IPv6: 128-bit
- Identifies a host *globally* across networks
- Used by routers for packet routing

**Port Address:**
- Layer 4 (Transport)
- 16-bit number (0–65535), e.g. port 80 = HTTP, port 22 = SSH
- Identifies a specific *process/service* on a host
- Multiple services can run on the same IP using different ports

Together: a datagram arrives at the correct machine (via IP), on the correct interface (via MAC on the LAN), and is delivered to the correct application (via port).

---

### Common Traps

| Wrong (from source) | Correct |
|---|---|
| SSH port 222 | SSH is port **22** |
| ARP at Layer 3 only | ARP operates between Layers 2 and 3 |
| SNMP listed as TCP-only | SNMP uses **UDP** (port 161); TCP is also defined but rarely used |
| `void main()` in C programs | Standard is `int main(void)` |
