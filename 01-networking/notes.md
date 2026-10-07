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

Layer 2 device : Switch
Layer 3 device : Router
