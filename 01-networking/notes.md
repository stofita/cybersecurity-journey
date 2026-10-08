# Networking notes

## 1.1 The OSI model
A universal reference model with 7 layers.

| # |   Layer      |                             Job                           |            Examples           |
|---|--------------|-----------------------------------------------------------|-------------------------------|
| 1 | Physical     | Sends raw bits over cables or radio signals               | Cables, Wi-Fi signals         |
| 2 | Data Link    | Delivers frames between devices on the same local network | MAC address, switch           |
| 3 | Network      | Routes packets between different networks                 | IP address, router            |
| 4 | Transport    | Delivers data between applications, using ports           | TCP (reliable), UDP (fast)    |
| 5 | Session      | Opens, maintains, and closes conversations                | Sessions                      |
| 6 | Presentation | Formats, compresses, and encrypts data                    | TLS (formerly SSL)            |
| 7 | Application  | Protocols that applications use to communicate            | HTTP, DNS, SMTP               |

Memory trick: Please Do Not Throw Sausage Pizza Away

PDU Names : L1 bits, L2 frames , L3 packets , L4 segments or datagrams

Layer 2 device : Switch .

Layer 3 device : Router .

# 1.2 Networking Devices

A data center contains many types of network equipment. Each device has a specific job and a place on the network.

## Router
- Connects **different networks** (e.g., a LAN to a WAN or the internet).
- Works at **Layer 3** and forwards packets using **IP addresses**.

## Switch
- Connects devices **inside the same network** and forwards frames using **MAC addresses** (Layer 2).
- Usually built in hardware (ASICs) with many ports.
- Often supports **PoE (Power over Ethernet)** to power devices like IP phones and access points.
- A **Layer 3 switch** adds routing functionality.

## Firewall
- Filters traffic with rules.
- **Traditional firewall:** filters by IP address, port, and protocol (Layers 3-4).
- **NGFW (Next-Generation Firewall):** application-aware (Layer 7), can also include IPS, URL filtering, and user identification.
- Many firewalls also include **VPN** features. The VPN is what encrypts traffic, not the firewall itself.

## IDS and IPS
| | IDS | IPS |
|---|---|---|
| Full name | Intrusion Detection System | Intrusion Prevention System |
| Action | **Detects** and **alerts** | **Detects** and **blocks** |
| Placement | Passive (receives a copy of traffic) | Inline (traffic passes through it) |

Both look for attacks such as exploits.

## Load Balancer
- Distributes traffic across **multiple servers** so no single server is overloaded.
- Also provides **fault tolerance**: if one server fails, traffic goes to the others.

## Proxy
- Sits **between the client and the server** and makes requests on the client's behalf.
- Can filter content, cache data, authenticate users, and hide the client's IP address.

## NAS vs SAN
| | NAS | SAN |
|---|---|---|
| Access level | **File-level** | **Block-level** |
| Protocols | SMB, NFS | Fibre Channel, iSCSI |
| Appears as | A shared folder on the network | A local disk attached to the server |
| Network | Regular network | Dedicated storage network |

## Wireless Devices
- **Access Point (AP):** connects wireless clients to the wired network (Layer 2 bridging).
- **Wireless LAN Controller (WLC):** centrally configures and manages many APs, which is easier than managing each one separately.
-