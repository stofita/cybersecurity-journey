# Networking Notes

## Contents
- [1.1 The OSI Model](#11-the-osi-model)
- [1.2.1 Networking Devices](#121-networking-devices)
- [1.2.2 Networking Functions](#122-networking-functions)
- [2.3 Introduction to IP](#23-introduction-to-ip)
- [2.4 IPv4 Addressing](#24-ipv4-addressing)
- [2.5 Binary Math](#25-binary-math)
- [2.6 IPv4 Subnet Masks](#26-ipv4-subnet-masks)
- [2.7 Classful Subnetting](#27-classful-subnetting)
- [2.8 Calculating IPv4 Subnets and Hosts](#28-calculating-ipv4-subnets-and-hosts)
- [2.9 Magic Number Subnetting](#29-magic-number-subnetting)
-  [2.10 Network Communication](#210-network-communication)
- [2.11 Other Useful Protocols](#211-other-useful-protocols)
---

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

## 1.2.1 Networking Devices

A data center contains many types of network equipment. Each device has a specific job and a place on the network.

### Router
- Connects **different networks** (e.g., a LAN to a WAN or the internet).
- Works at **Layer 3** and forwards packets using **IP addresses**.

### Switch
- Connects devices **inside the same network** and forwards frames using **MAC addresses** (Layer 2).
- Usually built in hardware (ASICs) with many ports.
- Often supports **PoE (Power over Ethernet)** to power devices like IP phones and access points.
- A **Layer 3 switch** adds routing functionality.

### Firewall
- Filters traffic with rules.
- **Traditional firewall:** filters by IP address, port, and protocol (Layers 3-4).
- **NGFW (Next-Generation Firewall):** application-aware (Layer 7), can also include IPS, URL filtering, and user identification.
- Many firewalls also include **VPN** features. The VPN is what encrypts traffic, not the firewall itself.

### IDS and IPS
| | IDS | IPS |
|---|---|---|
| Full name | Intrusion Detection System | Intrusion Prevention System |
| Action | **Detects** and **alerts** | **Detects** and **blocks** |
| Placement | Passive (receives a copy of traffic) | Inline (traffic passes through it) |

Both look for attacks such as exploits.

### Load Balancer
- Distributes traffic across **multiple servers** so no single server is overloaded.
- Also provides **fault tolerance**: if one server fails, traffic goes to the others.

### Proxy
- Sits **between the client and the server** and makes requests on the client's behalf.
- Can filter content, cache data, authenticate users, and hide the client's IP address.

### NAS vs SAN
| | NAS | SAN |
|---|---|---|
| Access level | **File-level** | **Block-level** |
| Protocols | SMB, NFS | Fibre Channel, iSCSI |
| Appears as | A shared folder on the network | A local disk attached to the server |
| Network | Regular network | Dedicated storage network |

### Wireless Devices
- **Access Point (AP):** connects wireless clients to the wired network (Layer 2 bridging).
- **Wireless LAN Controller (WLC):** centrally configures and manages many APs, which is easier than managing each one separately.

## 1.2.2 Networking Functions

A network provides several key functions: access to important data, remote access, traffic management, and protocol support.

### CDN (Content Delivery Network)
- Uses **geographically distributed servers** that cache content closer to the user, so it loads faster.
- Examples: Cloudflare, Akamai.
- Function: **access to important data**.

### VPN (Virtual Private Network)
- Creates an **encrypted tunnel** across a public network (like the internet) so data stays private.
- Function: **remote access** to a private network.

### QoS (Quality of Service)
- **Prioritizes** certain traffic (e.g., voice and video) over less sensitive traffic (e.g., downloads).
- Manages **bandwidth, delay, and packet loss**.
- Function: **traffic management**.

### TTL (Time to Live)
| | IP packet | DNS |
|---|---|---|
| Measured in | **Hops** (despite the name) | **Seconds** |
| Meaning | Each router subtracts 1. At 0, the packet is dropped. | How long a record can stay cached before it must be looked up again. |
| Purpose | Stops packets from circling forever in a **routing loop**. | Controls when cached DNS data is refreshed. |

- When doing a DNS lookup, the TTL shown is in **seconds**, not hops.
- Function: **protocol support**.

## 2.3 Introduction to IP

IP (Internet Protocol) works at **Layer 3**. It is like a **truck** that carries other protocols, such as **TCP**, **UDP**, and **ICMP**, as its payload.

### Encapsulation
Data sent over Ethernet is nested:
- The **Ethernet frame** carries an **IP packet** as its payload.
- The **IP packet** carries a **TCP segment** (or UDP datagram) as its payload.
- The TCP segment carries the **application data** (e.g., HTTP).

Ethernet Header → IP Header → TCP Header → HTTP data → Ethernet Trailer

### IP address vs port
- The **IP address** gets the packet to the right **device**.
- The **port number** (used by TCP or UDP) gets the data to the right **application** on that device.

### IPv4 sockets
A connection is identified by:

| | Server | Client |
|---|---|---|
| IP address | Server IP | Client IP |
| Protocol | TCP or UDP | Same protocol |
| Port number | Server application port | Client port |

### Port ranges
| Range | Used by |
|---|---|
| **0 - 1,023** | Servers (well-known ports, e.g., HTTP 80, HTTPS 443, DNS 53, SSH 22) |
| **1,024 - 65,535** | Clients (ephemeral ports, chosen by the OS for each connection) |

- This is a general rule, not always strict: servers can also use ports above 1,023 (e.g., 8080), and the exact client range depends on the operating system.

## 2.4 IPv4 Addressing

### Basics
- To communicate, every device needs its own **IP address**.
- IPv4 works at **OSI Layer 3**.
- An IPv4 address has **4 octets** (32 bits). Each octet is 8 bits, so its maximum value is **255**.

### Subnet mask and default gateway
- The **subnet mask** is used by a device to determine **which subnet it is on**, and whether a destination is local or not.
- If the destination is outside the local subnet, the device sends the traffic to the **default gateway** (usually the router), which allows communication outside of the local subnet.

### Special addresses
- **Loopback address:** an address that points to **yourself** (127.0.0.1, within 127.0.0.0/8). Used for testing the local network stack.
- **Reserved addresses:** set aside for **future use or testing** (e.g., **Class E**, 240.0.0.0 and above).
- **VIP (Virtual IP address):** an IP address **not tied to one specific device or interface**. Often shared by multiple servers or devices (e.g., behind a load balancer, or for redundancy) or associated with virtual machines.

### Getting an address
- **DHCP (Dynamic Host Configuration Protocol):** automatically gives a device its IP address and other IP configuration (subnet mask, default gateway, DNS server).
- **APIPA (Automatic Private IP Addressing):**
  - Used when a device **cannot reach a DHCP server**.
  - Address starts with **169.254.x.x**.
  - Can only communicate with **local devices** on the same subnet.
  - The device uses **ARP** to check that the address it picked isn't already in use.

### NAT (Network Address Translation)
- Translates a **private IP address** to a **public** one.
- Needed because there are **more devices than available IPv4 addresses**.

### 2.4 Binary Math

### How binary works
- Each **bit** is either **1** (on / active) or **0** (off / inactive).
- Each position has a value of 2ⁿ. A 1 means that value is **counted** in the total, and a 0 means it is **not**.
- An **octet** (or **byte**) has **8 bits**:

| Position | 2⁷ | 2⁶ | 2⁵ | 2⁴ | 2³ | 2² | 2¹ | 2⁰ |
|---|---|---|---|---|---|---|---|---|
| Value | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |

### Binary to decimal
Add the values of the positions that are 1.

Example: `00100010`
- 2⁵ + 2¹ = 32 + 2 = **34**

### Decimal to binary
Example: **127**
- 127 = 64 + 32 + 16 + 8 + 4 + 2 + 1
- Binary: `01111111`

### Bit vs byte
- **1 bit** = a single 0 or 1.
- **8 bits** = **1 byte** = **1 octet**.
- Maximum value of one octet: `11111111` = **255** (2⁸ - 1).

### More bits = more addresses
- **n bits** give **2ⁿ possibilities**.
- IPv4 uses 32 bits (4 octets), so it has 2³² (about 4.3 billion) possible addresses.

## 2.6 IPv4 Subnet Masks

### CIDR (Classless Inter-Domain Routing)
- A subnet mask can be written in **decimal** or in **CIDR notation**.
- The CIDR number is the **number of 1 bits** in the mask (the network bits).

| Decimal mask | CIDR |
|---|---|
| 255.0.0.0 | /8 |
| 255.255.0.0 | /16 |
| 255.255.255.0 | /24 |

- Some operating systems expect the decimal mask, others expect CIDR notation.

### Network bits and host bits
`11111111.11111111.11111111.00000000` = **255.255.255.0**
- The 1s are the **network** part (24 bits).
- The 0s are the **host** part (8 bits).
- To get the CIDR notation, **count the 1s**: here **/24**.

### Binary to decimal
`11111111.11110000.00000000.00000000`
- 11111111 = 255, 11110000 = 128 + 64 + 32 + 16 = 240
- Mask: **255.240.0.0** (/12)

### CIDR to decimal
You can also go the other way. Example: **/26**
- 26 ones: `11111111.11111111.11111111.11000000`
- 11000000 = 128 + 64 = 192
- Mask: **255.255.255.192**

You must know how to convert between binary and decimal.

## 2.7 Classful Subnetting

- Classful subnetting has **not been used since 1993**, when CIDR replaced it.
- Using CIDR as a reference, each class has a default mask:

| Class | Default mask | First bits | First octet range |
|---|---|---|---|
| **A** | /8 | `0xxx` | 0 - 127 |
| **B** | /16 | `10xx` | 128 - 191 |
| **C** | /24 | `110x` | 192 - 223 |
| **D** (multicast) | - | `1110` | 224 - 239 |
| **E** (reserved) | - | `1111` | 240 - 255 |

- **Method to identify the class:** look at the **first octet** and compare it to the ranges.

### Rules in IPv4 subnetting
- **Network address:** all **host bits are 0**.
- **Broadcast address:** the **last** IP address of the subnet, all **host bits are 1**.
- **First usable host:** one number **higher** than the network address.
- **Last usable host:** one number **lower** than the broadcast address.

### Example: 10.74.222.11
- First octet is 10, so it is **Class A**. Network part: `10`, host part: `74.222.11`.
- Subnet mask: **255.0.0.0**
- Network address: **10.0.0.0**
- First usable host: **10.0.0.1**
- Broadcast address: **10.255.255.255**
- Last usable host: **10.255.255.254**

## 2.8 Calculating IPv4 Subnets and Hosts

### Why subnet?
- One large network is inefficient: more broadcast traffic, wasted addresses, and harder to manage. **Subnetting** splits it into smaller networks.
- **VLSM (Variable Length Subnet Masking)** lets admins define their own masks, so each subnet can have a different size and fewer addresses are wasted.
- A subnet is like **borrowing bits** from the host portion.

### The three parts of an address
| Part | Meaning |
|---|---|
| **Network bits** | Default for the class (e.g., Class A = 8) |
| **Subnet bits** | Bits **borrowed** from the host portion |
| **Host bits** | The bits that remain for hosts |

Network + subnet + host = **32 bits**.

### Formulas
- **Number of subnets** = 2^(subnet bits)
- **Hosts per subnet** = 2^(host bits) - 2
  - The 2 removed are the **network address** and the **broadcast address**.

### Example: 10.1.1.0/24
- Class A, so network bits = **8**
- /24 means 24 mask bits, so subnet bits = 24 - 8 = **16**
- Host bits = 32 - 24 = **8**

`11111111.11111111.11111111.00000000` = 255.255.255.0

| Network | Subnet | Host |
|---|---|---|
| 8 bits | 16 bits | 8 bits |

- Total subnets = 2¹⁶ = **65,536**
- Hosts per subnet = 2⁸ - 2 = **254**

## 2.9 Magic Number Subnetting

### Why
- Calculating a subnet usually means converting decimal to binary, which takes a lot of time.
- The **magic number** method is a faster shortcut. A chart helps to memorize the mask values.

### CIDR to decimal chart
| Octet 2 | Octet 3 | Octet 4 | Decimal |
|---|---|---|---|
| /9 | /17 | /25 | 128 |
| /10 | /18 | /26 | 192 |
| /11 | /19 | /27 | 224 |
| /12 | /20 | /28 | 240 |
| /13 | /21 | /29 | 248 |
| /14 | /22 | /30 | 252 |
| /15 | /23 | /31 | 254 |
| /16 | /24 | /32 | 255 |

- Normal subnets don't use **/31** and **/32** because they don't leave room for hosts (/31 is a special case for point-to-point links).

### Method
1. Have the subnet mask in **decimal**.
2. Identify the **interesting octet**: the octet whose mask value is not 255 or 0.
3. Calculate the **magic number** = **256 - interesting octet**. It is the size of each subnet block.
4. Find the **host range**: blocks start at multiples of the magic number (0, 16, 32, ...). Find the block that contains the IP's value in the interesting octet.
5. Identify the **subnet ID** (network address) and the **broadcast address**.

### Rules for each octet
| Mask value | Subnet ID | Broadcast |
|---|---|---|
| **255** | Copy the IP octet | Same as subnet ID |
| **0** | Write **0** | Write **255** |
| Anything else (interesting octet) | Start of the block | Subnet ID + magic number - 1 |

- **First host** = subnet ID + 1
- **Last host** = broadcast - 1

### Example 1: 165.245.77.14, mask 255.255.240.0
| | Octet 1 | Octet 2 | Octet 3 | Octet 4 |
|---|---|---|---|---|
| Mask | 255 | 255 | 240 | 0 |
| IP | 165 | 245 | 77 | 14 |
| Subnet ID | 165 | 245 | 64 | 0 |
| Broadcast | 165 | 245 | 79 | 255 |

- Interesting octet: 3rd (240)
- Magic number: 256 - 240 = **16**
- Blocks: 0, 16, 32, 48, 64, 80... The value 77 is between 64 and 79, so the block starts at **64**.
- Subnet ID: **165.245.64.0**
- Broadcast: 64 + 16 - 1 = 79, so **165.245.79.255**
- First host: **165.245.64.1**
- Last host: **165.245.79.254**

### Example 2 (using the chart): 172.16.242.133/27
- /27 is in the **octet 4** column, so the mask is **255.255.255.224** and the interesting octet is the 4th.
- Magic number: 256 - 224 = **32**
- Blocks: 0, 32, 64, 96, 128, 160... The value 133 is in the block starting at **128**.
- Subnet ID: **172.16.242.128**
- Broadcast: 128 + 32 - 1 = 159, so **172.16.242.159**
- First host: 128 + 1 = **172.16.242.129**
- Last host: 159 - 1 = **172.16.242.158**

## 2.10 Network Communication

How data is sent from one station to others:

| Type | Direction | Description |
|---|---|---|
| **Unicast** | One to one | Transfers data from station A to station B |
| **Multicast** | One to many (a group) | Sends from one station to a group of stations that joined, simultaneously |
| **Anycast** | One to the nearest of many | Several devices share the same IP address, and the data goes to the closest one |
| **Broadcast** | One to all | Sends data to everyone on the local network at once |

- Multicast addresses are **Class D** (224.0.0.0 - 239.255.255.255).
- IPv6 does not have broadcast.

## 2.11 Other Useful Protocols

### ICMP (Internet Control Message Protocol)
- Used by network devices to send **error messages and diagnostic information**.
- Examples: **ping** (echo request/reply), **traceroute**, "destination unreachable".
- It is carried inside IP and does not use ports.

### GRE (Generic Routing Encapsulation)
- A **tunneling** protocol: it encapsulates one packet inside another to send it across a network.
- It does **not encrypt** the data. It is often combined with IPsec.

### VPN (Virtual Private Network)
- Encrypts data across a public network.
- **Site-to-site:** connects two whole networks (e.g., two offices).
- Remote access (client-to-site) connects a single user to a network.

### IPsec
- Used to **encrypt and secure** traffic at the network layer (Layer 3).
- Needs **IKE (Internet Key Exchange)** to set up the connection:
  - **Phase I:** the two sides authenticate and create a secure channel.
  - **Phase II:** they negotiate the IPsec parameters used to protect the data.

| Protocol | What it does |
|---|---|
| **AH** (Authentication Header) | **Hashing**: verifies who sent the data and that it wasn't changed. No encryption. |
| **ESP** (Encapsulating Security Payload) | **Encryption** + authentication |

### Modes
- **Transport mode:** the original IP header is **not encrypted**; only the data is protected.
  - IP Header → IPsec Header → Data → IPsec Trailer
- **Tunnel mode:** the **whole original packet** is protected inside a new packet. Commonly used for site-to-site VPNs.
  - New IP Header → IPsec Header → Original IP Header → Data → IPsec Trailer
