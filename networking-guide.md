# Comprehensive Networking Guide

A complete reference for computer networking concepts, protocols, and troubleshooting.

---

## Table of Contents
1. [Introduction to Networking](#1-introduction-to-networking)
2. [Network Types](#2-network-types)
3. [The OSI Model](#3-the-osi-model-7-layers)
4. [The TCP/IP Model](#4-the-tcpip-model-4-layers)
5. [IP Addressing](#5-ip-addressing)
6. [Key Protocols](#6-key-protocols)
7. [Network Devices](#7-network-devices)
8. [MAC Addresses](#8-mac-addresses)
9. [DNS](#9-dns-domain-name-system)
10. [DHCP](#10-dhcp-dynamic-host-configuration-protocol)
11. [Network Topologies](#11-network-topologies)
12. [VLANs](#12-vlans-virtual-lans)
13. [Routing](#13-routing)
14. [Network Security](#14-network-security)
15. [Wireless Networking](#15-wireless-networking)
16. [Troubleshooting Commands](#16-network-troubleshooting-commands)
17. [NAT](#17-network-address-translation-nat)
18. [QoS](#18-quality-of-service-qos)
19. [Cloud Networking](#19-cloud-networking-concepts)
20. [Port Numbers](#20-useful-port-numbers-to-memorize)

---

## 1. Introduction to Networking

**Computer Networking** is the practice of connecting computers and other devices to share resources, exchange data, and communicate. Networks can range from small home setups to massive global infrastructures like the Internet.

### Why Networking Matters
- **Resource Sharing**: Printers, files, applications
- **Communication**: Email, video calls, messaging
- **Data Access**: Cloud storage, databases
- **Collaboration**: Real-time document editing, project management

---

## 2. Network Types

| Type | Range | Example |
|------|-------|---------|
| **PAN** (Personal Area Network) | ~10 meters | Bluetooth devices |
| **LAN** (Local Area Network) | Building/Campus | Office network |
| **MAN** (Metropolitan Area Network) | City | City-wide WiFi |
| **WAN** (Wide Area Network) | Global | The Internet |
| **WLAN** (Wireless LAN) | Building | WiFi networks |

---

## 3. The OSI Model (7 Layers)

The **Open Systems Interconnection (OSI)** model is a conceptual framework for understanding network communications.

```
┌──────────────────────────────────────��──────────────────────┐
│ Layer 7: APPLICATION                                        │
│ → User interface, HTTP, FTP, SMTP, DNS, SNMP                │
├─────────────────────────────────────────────────────────────┤
│ Layer 6: PRESENTATION                                       │
│ → Data formatting, encryption, compression (SSL/TLS, JPEG)  │
├─────────────────────────────────────────────────────────────┤
│ Layer 5: SESSION                                            │
│ → Connection management, authentication (NetBIOS, RPC)      │
├─────────────────────────────────────────────────────────────┤
│ Layer 4: TRANSPORT                                          │
│ → End-to-end delivery, reliability (TCP, UDP)               │
├───────────────────────────────────────────���─────────────────┤
│ Layer 3: NETWORK                                            │
│ → Logical addressing, routing (IP, ICMP, Routers)           │
├─────────────────────────────────────────────────────────────┤
│ Layer 2: DATA LINK                                          │
│ → Physical addressing, framing (MAC, Switches, Ethernet)    │
├─────────────────────────────────────────────────────────────┤
│ Layer 1: PHYSICAL                                           │
│ → Bits transmission, cables, signals (Hubs, Cables, NICs)   │
└─────────────────────────────────────────────────────────────┘
```

### Memory Trick
**"All People Seem To Need Data Processing"** (Top to Bottom)

---

## 4. The TCP/IP Model (4 Layers)

A more practical model used in real-world networking:

| TCP/IP Layer | OSI Equivalent | Protocols |
|--------------|----------------|-----------|
| **Application** | Layers 5-7 | HTTP, FTP, DNS, SMTP |
| **Transport** | Layer 4 | TCP, UDP |
| **Internet** | Layer 3 | IP, ICMP, ARP |
| **Network Access** | Layers 1-2 | Ethernet, WiFi |

---

## 5. IP Addressing

### IPv4 Addresses
- **Format**: 4 octets (32 bits) → `192.168.1.1`
- **Range**: 0.0.0.0 to 255.255.255.255
- **Total addresses**: ~4.3 billion

#### IP Address Classes

| Class | Range | Default Subnet | Purpose |
|-------|-------|----------------|---------|
| A | 1.0.0.0 – 126.255.255.255 | 255.0.0.0 (/8) | Large networks |
| B | 128.0.0.0 – 191.255.255.255 | 255.255.0.0 (/16) | Medium networks |
| C | 192.0.0.0 – 223.255.255.255 | 255.255.255.0 (/24) | Small networks |
| D | 224.0.0.0 – 239.255.255.255 | N/A | Multicast |
| E | 240.0.0.0 – 255.255.255.255 | N/A | Experimental |

#### Private IP Ranges (Non-routable on Internet)
```
Class A: 10.0.0.0 – 10.255.255.255
Class B: 172.16.0.0 – 172.31.255.255
Class C: 192.168.0.0 – 192.168.255.255
```

### IPv6 Addresses
- **Format**: 8 groups of 4 hex digits (128 bits)
- **Example**: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
- **Total addresses**: 340 undecillion (practically unlimited)

### Subnetting

Subnetting divides a network into smaller sub-networks.

**CIDR Notation**: `/24` means 24 bits for network, 8 bits for hosts

| CIDR | Subnet Mask | Hosts |
|------|-------------|-------|
| /24 | 255.255.255.0 | 254 |
| /25 | 255.255.255.128 | 126 |
| /26 | 255.255.255.192 | 62 |
| /27 | 255.255.255.224 | 30 |
| /28 | 255.255.255.240 | 14 |
| /30 | 255.255.255.252 | 2 |

---

## 6. Key Protocols

### Transport Layer

#### TCP (Transmission Control Protocol)
- **Connection-oriented** (3-way handshake)
- **Reliable** delivery with acknowledgments
- **Ordered** data transmission
- **Use cases**: Web browsing, email, file transfer

**TCP 3-Way Handshake:**
```
Client          Server
  │                │
  │──── SYN ──────→│
  │                │
  │←── SYN-ACK ────│
  │                │
  │──── ACK ──────→│
  │                │
  │  Connection    │
  │  Established   │
```

#### UDP (User Datagram Protocol)
- **Connectionless** (no handshake)
- **Unreliable** (no acknowledgments)
- **Faster** than TCP
- **Use cases**: Streaming, gaming, DNS queries, VoIP

### Application Layer Protocols

| Protocol | Port | Purpose |
|----------|------|---------|
| HTTP | 80 | Web pages (unencrypted) |
| HTTPS | 443 | Secure web pages |
| FTP | 20, 21 | File transfer |
| SSH | 22 | Secure shell access |
| Telnet | 23 | Remote access (insecure) |
| SMTP | 25 | Sending email |
| DNS | 53 | Domain name resolution |
| DHCP | 67, 68 | Dynamic IP assignment |
| POP3 | 110 | Retrieving email |
| IMAP | 143 | Email access |
| SNMP | 161 | Network management |
| RDP | 3389 | Remote desktop |

---

## 7. Network Devices

### Layer 1 Devices
- **Hub**: Broadcasts data to all ports (obsolete)
- **Repeater**: Amplifies signals over distance
- **Modem**: Modulates/demodulates signals

### Layer 2 Devices
- **Switch**: Forwards frames based on MAC addresses
- **Bridge**: Connects two LAN segments
- **Access Point (AP)**: Wireless connectivity

### Layer 3 Devices
- **Router**: Forwards packets between networks using IP addresses
- **Layer 3 Switch**: Switch with routing capabilities

### Other Devices
- **Firewall**: Controls traffic based on security rules
- **Load Balancer**: Distributes traffic across servers
- **Proxy Server**: Intermediary for requests
- **Gateway**: Protocol converter between networks

---

## 8. MAC Addresses

- **Format**: 48 bits (6 bytes) in hexadecimal
- **Example**: `00:1A:2B:3C:4D:5E`
- **Structure**:
  - First 3 bytes: OUI (Organizationally Unique Identifier) – manufacturer
  - Last 3 bytes: Device identifier

---

## 9. DNS (Domain Name System)

DNS translates human-readable domain names to IP addresses.

### DNS Hierarchy
```
Root (.)
    │
    ├── .com
    │   ├── google.com
    │   └── github.com
    │
    ├── .org
    │   └── wikipedia.org
    │
    └── .net
        └── example.net
```

### DNS Record Types

| Type | Purpose | Example |
|------|---------|---------|
| **A** | Maps domain to IPv4 | `example.com → 93.184.216.34` |
| **AAAA** | Maps domain to IPv6 | `example.com → 2606:2800:220:1:...` |
| **CNAME** | Alias to another domain | `www.example.com → example.com` |
| **MX** | Mail server | `example.com → mail.example.com` |
| **TXT** | Text information | SPF, DKIM records |
| **NS** | Nameserver | `example.com → ns1.example.com` |
| **PTR** | Reverse DNS | `34.216.184.93 → example.com` |

---

## 10. DHCP (Dynamic Host Configuration Protocol)

Automatically assigns IP addresses to devices.

### DORA Process
```
1. DISCOVER → Client broadcasts "I need an IP"
2. OFFER    → Server offers an available IP
3. REQUEST  → Client requests the offered IP
4. ACK      → Server acknowledges and assigns IP
```

---

## 11. Network Topologies

```
STAR                    BUS                     RING
   ┌───┐                 │                    ┌───┐
   │ A │                 │                    │ A │
   └─┬─┘              ┌──┴──┐              ┌──┴───┴──┐
     │                │     │              │         │
   ┌─┴─┐           ┌──┴┐ ┌──┴┐ ┌──┐     ┌─┴─┐     ┌─┴─┐
   │HUB│           │ A │ │ B │ │ C │     │ D │     │ B │
   └─┬─┘           └───┘ └───┘ └───┘     └─┬─┘     └─┬─┘
  ┌──┼──┐              │                   │         │
┌─┴┐┌┴─┐└─┐         ───┴───               └────┬────┘
│B ││C ││D │                                 ┌─┴─┐
└──┘└──┘└──┘                                 │ C │
                                             └───┘

MESH (Full)              TREE
┌───┐───────┌───┐           ┌───┐
│ A │       │ B │           │Root│
└─┬─┘       └─┬─┘           └─┬─┘
  │ \     / │             ┌───┴───┐
  ���  \   /  │           ┌─┴─┐   ┌─┴─┐
  │   \ /   │           │ A │   │ B │
  │    X    │           └─┬─┘   └─┬─┘
  │   / \   │          ┌──┴──┐ ┌──┴──┐
  │  /   \  │         ┌┴┐  ┌─┴┐┴┐  ┌─┴┐
└─┬─┘       └─┬─┘     │C│  │D ││E│  │F │
│ C │───────│ D │     └─┘  └──┘└─┘  └──┘
└───┘       └───┘
```

---

## 12. VLANs (Virtual LANs)

VLANs logically segment a network without physical separation.

### Benefits
- **Security**: Isolate sensitive traffic
- **Performance**: Reduce broadcast domains
- **Flexibility**: Group users by function, not location

### VLAN Tagging (802.1Q)
Adds a 4-byte tag to Ethernet frames for VLAN identification.

---

## 13. Routing

### Types of Routing
1. **Static Routing**: Manually configured routes
2. **Dynamic Routing**: Routes learned via protocols

### Routing Protocols

| Protocol | Type | Algorithm | Use Case |
|----------|------|-----------|----------|
| **RIP** | Distance Vector | Hop count | Small networks |
| **OSPF** | Link State | Dijkstra's | Enterprise |
| **EIGRP** | Hybrid | DUAL | Cisco networks |
| **BGP** | Path Vector | Path attributes | Internet backbone |

---

## 14. Network Security

### Firewalls
- **Packet Filtering**: Inspects headers
- **Stateful Inspection**: Tracks connections
- **Application Layer**: Deep packet inspection
- **Next-Gen (NGFW)**: Includes IPS, antivirus

### Common Attacks

| Attack | Description | Prevention |
|--------|-------------|------------|
| **DDoS** | Overwhelm with traffic | Rate limiting, CDN |
| **Man-in-the-Middle** | Intercept communication | Encryption, certificates |
| **ARP Spoofing** | Fake MAC addresses | Static ARP, DAI |
| **DNS Poisoning** | Redirect to malicious sites | DNSSEC |
| **Phishing** | Social engineering | User education |

### Security Protocols
- **SSL/TLS**: Encrypts web traffic
- **IPSec**: Secures IP communications
- **WPA3**: Latest WiFi security
- **802.1X**: Port-based authentication

---

## 15. Wireless Networking

### WiFi Standards (802.11)

| Standard | Frequency | Max Speed | Year |
|----------|-----------|-----------|------|
| 802.11a | 5 GHz | 54 Mbps | 1999 |
| 802.11b | 2.4 GHz | 11 Mbps | 1999 |
| 802.11g | 2.4 GHz | 54 Mbps | 2003 |
| 802.11n (WiFi 4) | 2.4/5 GHz | 600 Mbps | 2009 |
| 802.11ac (WiFi 5) | 5 GHz | 6.9 Gbps | 2013 |
| 802.11ax (WiFi 6) | 2.4/5/6 GHz | 9.6 Gbps | 2019 |
| 802.11be (WiFi 7) | 2.4/5/6 GHz | 46 Gbps | 2024 |

---

## 16. Network Troubleshooting Commands

```bash
# Connectivity testing
ping 8.8.8.8                    # Test reachability
traceroute google.com           # Trace path to destination (Linux/Mac)
tracert google.com              # Trace path (Windows)

# DNS tools
nslookup example.com            # Query DNS
dig example.com                 # Detailed DNS query (Linux/Mac)

# Network configuration
ipconfig /all                   # Windows IP config
ifconfig                        # Linux/Mac IP config (legacy)
ip addr                         # Linux IP config (modern)

# Connection information
netstat -an                     # Active connections
ss -tuln                        # Socket statistics (Linux)

# ARP table
arp -a                          # View ARP cache

# Packet capture
tcpdump -i eth0                 # Capture packets (Linux)
wireshark                       # GUI packet analyzer
```

---

## 17. Network Address Translation (NAT)

NAT translates private IPs to public IPs for Internet access.

### NAT Types
- **Static NAT**: 1:1 mapping (private to public)
- **Dynamic NAT**: Pool of public IPs
- **PAT (Port Address Translation)**: Many private IPs share one public IP using ports

---

## 18. Quality of Service (QoS)

QoS prioritizes certain traffic types for better performance.

### Traffic Classification
- **Voice**: Highest priority (low latency needed)
- **Video**: High priority
- **Business Data**: Medium priority
- **Best Effort**: Default, lowest priority

---

## 19. Cloud Networking Concepts

- **VPC (Virtual Private Cloud)**: Isolated cloud network
- **Subnet**: Segment within VPC
- **Security Groups**: Virtual firewalls
- **Load Balancer**: Distributes incoming traffic
- **CDN**: Content delivery network for caching
- **VPN**: Secure tunnel to cloud resources

---

## 20. Useful Port Numbers to Memorize

```
20, 21  → FTP
22      → SSH
23      → Telnet
25      → SMTP
53      → DNS
67, 68  → DHCP
80      → HTTP
110     → POP3
143     → IMAP
443     → HTTPS
445     → SMB
3306    → MySQL
3389    → RDP
5432    → PostgreSQL
```

---

## Quick Reference Card

### OSI Layers (Top to Bottom)
**A**pplication → **P**resentation → **S**ession → **T**ransport → **N**etwork → **D**ata Link → **P**hysical

### TCP vs UDP
| TCP | UDP |
|-----|-----|
| Reliable | Unreliable |
| Connection-oriented | Connectionless |
| Slower | Faster |
| HTTP, FTP, SSH | DNS, VoIP, Gaming |

### Private IP Ranges
- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

---

*Created: 2026-01-12*
*Author: amadou2599-png*
