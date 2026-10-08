#separator:semicolon
#html:false
#deck:Cybersecurity::Networking
How many layers does the OSI model have?;7
Name the 7 OSI layers from 1 to 7;Physical - Data Link - Network - Transport - Session - Presentation - Application
Mnemonic for the OSI layers 1 to 7;Please Do Not Throw Sausage Pizza Away
What is the job of Layer 1 (Physical)?;Sends raw bits over cables or radio signals
Which layer uses MAC addresses and switches?;Layer 2 - Data Link
Layer 2 delivers frames between which devices?;Devices on the same local network
Which layer routes packets between different networks?;Layer 3 - Network (IP addresses and routers)
Which layer uses TCP and UDP?;Layer 4 - Transport
TCP vs UDP?;TCP = reliable and ordered. UDP = fast with no delivery guarantee.
What is the job of Layer 5 (Session)?;Opens, maintains, and closes conversations between applications
What is the job of Layer 6 (Presentation)?;Formats, compresses, and encrypts data (for example TLS)
What is the modern name of SSL?;TLS
What does Layer 7 (Application) contain?;The protocols applications use to talk over the network, such as HTTP, DNS, and SMTP
What is the data unit called at Layer 1?;Bits
What is the data unit called at Layer 2?;Frame
What is the data unit called at Layer 3?;Packet
What is the data unit called at Layer 4?;Segment
Which device works at Layer 2?;Switch
Which device works at Layer 3?;Router

#separator:Pipe
#html:true
#tags column:3
Which device connects different networks (e.g., a LAN to the internet)?|Router|network+ 1.2
At which layer does a router work, and which address does it use?|Layer 3, IP addresses|network+ 1.2
At which layer does a standard switch work, and which address does it use?|Layer 2, MAC addresses|network+ 1.2
Switch vs router in one sentence?|A switch connects devices inside one network (MAC addresses). A router connects different networks (IP addresses).|network+ 1.2
What does PoE stand for, and what is it used for?|Power over Ethernet. It powers devices like IP phones and access points through the network cable.|network+ 1.2
What is a Layer 3 switch?|A switch with routing functionality added.|network+ 1.2
What does a traditional firewall filter on?|IP address, port, and protocol (Layers 3-4).|network+ 1.2
What makes an NGFW different from a traditional firewall?|It is application-aware (Layer 7) and can add IPS, URL filtering, and user identification.|network+ 1.2
Which encrypts traffic: the firewall or the VPN?|The VPN. Some firewalls include VPN features, but encryption is the VPN's job.|network+ 1.2
What does an IDS do?|Detects and alerts only. It is passive and receives a copy of the traffic.|network+ 1.2
What does an IPS do?|Detects and blocks attacks. It sits inline.|network+ 1.2
What does "inline" mean?|The device sits directly in the traffic path, so all traffic passes through it.|network+ 1.2
What is the downside of an inline IPS?|If it fails or gets overloaded, it can interrupt the network.|network+ 1.2
How does a passive IDS see traffic without being inline?|Through a mirrored switch port (port mirroring) or a network tap.|network+ 1.2
Which one can stop an attack before it reaches the network: IDS or IPS?|IPS|network+ 1.2
What does a load balancer do?|Distributes traffic across multiple servers so none is overloaded.|network+ 1.2
Besides spreading load, what else does a load balancer provide?|Fault tolerance: if one server fails, traffic goes to the others.|network+ 1.2
Where does a proxy sit, and what does it do?|Between the client and the server. It makes requests on the client's behalf.|network+ 1.2
Name 4 things a proxy can do.|Filter content, cache data, authenticate users, hide the client's IP address.|network+ 1.2
NAS: file-level or block-level? Which protocols?|File-level (SMB, NFS). Appears as a shared folder on the network.|network+ 1.2
SAN: file-level or block-level? Which protocols?|Block-level (Fibre Channel, iSCSI). Appears as a local disk and uses a dedicated storage network.|network+ 1.2
Which provides block-level storage: NAS or SAN?|SAN|network+ 1.2
A team needs a shared folder over the network. NAS or SAN?|NAS|network+ 1.2
What does an access point (AP) do?|Connects wireless clients to the wired network (Layer 2 bridging).|network+ 1.2
What does a wireless LAN controller (WLC) do?|Centrally configures and manages many access points.|network+ 1.2

