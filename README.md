# CompTIA Network+ (N10-009) — Beginner-Friendly Study Notes

> **Goal:** Understand the ideas, not just memorize definitions. These notes use simple explanations, everyday examples, small diagrams, and exam reminders.
>
> **Study tip:** Read one section, explain it aloud in your own words, then answer the quick-check questions without looking.

---

## Table of Contents

1. [The OSI Model](#1-the-osi-model)
2. [Networking Devices](#2-networking-devices)
3. [Important Networking Functions](#3-important-networking-functions)
4. [Cloud Networking and Design](#4-cloud-networking-and-design)
5. [Cloud Deployment and Service Models](#5-cloud-deployment-and-service-models)
6. [IP, TCP, UDP, and Ports](#6-ip-tcp-udp-and-ports)
7. [Common Ports to Memorize](#7-common-ports-to-memorize)
8. [Quick Revision Tables](#8-quick-revision-tables)
9. [Practice Questions](#9-practice-questions)
10. [Useful Linux Commands](#10-useful-linux-commands)

---

# 1. The OSI Model

## What is the OSI model?

The **OSI (Open Systems Interconnection) model** is a way to understand how data travels from one device to another over a network.

Imagine sending a parcel to a friend:

1. You prepare the item.
2. You pack it.
3. You write the delivery details.
4. A delivery company transports it.
5. Your friend receives and opens it.

Network communication also has stages. The OSI model divides those stages into **seven layers**.

### The seven layers

| Layer | Name | Easy way to remember | Main job |
|---:|---|---|---|
| 7 | Application | Application | Network services used by applications |
| 6 | Presentation | Format | Data format, encoding, encryption |
| 5 | Session | Conversation | Starts, manages, and ends communication sessions |
| 4 | Transport | Delivery | End-to-end delivery using TCP or UDP |
| 3 | Network | Route | IP addressing and routing between networks |
| 2 | Data Link | Local delivery | Frames and MAC addresses on the local link |
| 1 | Physical | Signals | Cables, connectors, radio signals, and bits |

A common memory phrase, from Layer 7 down to Layer 1:

**All People Seem To Need Data Processing**

(Application, Presentation, Session, Transport, Network, Data Link, Physical)

## Layer 7 — Application

This is the layer closest to the programs people use. It provides network services to applications.

**Examples:**
- HTTP/HTTPS — loading websites
- DNS — finding the IP address for a domain name
- SMTP — sending email
- FTP — transferring files

**Example:** When you open a website, your browser uses application-layer protocols such as HTTPS.

> Remember: The Application layer is not the browser itself. It is the network services and protocols that applications use.

## Layer 6 — Presentation

This layer is concerned with how data is represented.

Think of it as a translator or formatter. The sender and receiver need to understand the data in a compatible format.

Common responsibilities include:
- Data formatting and character encoding
- Data compression
- Encryption and decryption

**Example:** Data may be encrypted before it travels across a network and decrypted by the receiving side. TLS is commonly associated with secure application communication, although real-world protocol stacks do not always fit neatly into one OSI layer.

## Layer 5 — Session

This layer manages communication sessions between applications.

It can be understood as managing a conversation:
- Start a session.
- Keep track of the session.
- Coordinate the conversation.
- End the session.

**Example:** A system that maintains a communication session while two applications exchange information is performing a session-management function.

## Layer 4 — Transport

The Transport layer manages communication between applications running on different devices.

Its two major protocols are:

- **TCP:** reliable, connection-oriented delivery.
- **UDP:** connectionless delivery with less overhead.

It also uses **port numbers** to deliver data to the correct application.

**Data units:**
- TCP: segment
- UDP: datagram

**Example:** Your laptop may use a browser and a music app at the same time. Port numbers help the operating system deliver incoming data to the correct application.

## Layer 3 — Network

The Network layer moves packets between different networks.

Its main responsibilities include:
- Logical addressing using IP addresses
- Choosing routes between networks
- Forwarding packets through routers

**Main device:** Router  
**Data unit:** Packet  
**Common protocol:** IP

**Example:** Your laptop is on your home Wi-Fi, and a website's server is somewhere on the internet. Routers move packets across the networks between them.

## Layer 2 — Data Link

The Data Link layer handles communication over the local network link.

It uses **MAC addresses** to identify network interfaces on a local network.

**Main device:** Layer 2 switch  
**Data unit:** Frame

**Example:** Your laptop sends an Ethernet or Wi-Fi frame toward the next device on the local network.

A MAC address is commonly written as six hexadecimal pairs, such as `00:1A:2B:3C:4D:5E`.

## Layer 1 — Physical

The Physical layer carries raw bits as electrical, optical, or radio signals.

Examples:
- Ethernet cables
- Fiber-optic cables
- Wireless radio signals
- Connectors and transceivers

**Data unit:** Bits (`0` and `1`)

**Example:** When data travels through an Ethernet cable, the Physical layer is concerned with the signals that represent the bits.

## How data moves through the OSI model

When your laptop sends data, it normally moves down the layers. At the receiving device, it moves up the layers.

```text
SENDING DEVICE                         RECEIVING DEVICE

7. Application                         7. Application
6. Presentation                        6. Presentation
5. Session                             5. Session
4. Transport  → segment/datagram →     4. Transport
3. Network    → packet            →     3. Network
2. Data Link  → frame             →     2. Data Link
1. Physical   → bits              →     1. Physical
```

This process is called **encapsulation** on the sender and **decapsulation** on the receiver. Each layer adds or removes information needed for delivery.

### OSI exam reminders

- Router: primarily Layer 3.
- Layer 2 switch: primarily Layer 2.
- MAC address: Layer 2.
- IP address: Layer 3.
- TCP and UDP: Layer 4.
- Cables and signals: Layer 1.
- Real networking protocols may span or not map perfectly to one OSI layer. The model is a learning and troubleshooting framework.

### Quick check

1. Which layer uses IP addresses? **Layer 3 — Network.**
2. Which layer uses MAC addresses? **Layer 2 — Data Link.**
3. Which layer uses TCP and UDP? **Layer 4 — Transport.**
4. Which layer includes cables and radio signals? **Layer 1 — Physical.**

---

# 2. Networking Devices

Networking devices help computers communicate. Each device has a particular job.

## 2.1 Router

A **router connects different IP networks** and forwards packets toward their destination.

Think of a router as a road junction that chooses which road a vehicle should take.

**Example:** Your home router connects your home network to your internet service provider (ISP).

Key points:
- Works primarily at OSI Layer 3.
- Uses IP addresses and routing tables.
- Connects different networks.
- Can connect LANs to WANs.
- Home routers often combine routing, switching, wireless access, firewall, and NAT features in one box.

## 2.2 Switch

A **switch connects devices inside a local area network (LAN)**.

Think of a switch as an office receptionist who knows which desk belongs to each employee. It learns which MAC addresses are reachable through its ports and forwards frames accordingly.

Key points:
- A traditional Layer 2 switch works at Layer 2.
- Forwards Ethernet frames using MAC addresses.
- Commonly connects PCs, printers, servers, and access points.
- Some switches provide **Power over Ethernet (PoE)**, which can power devices such as access points and IP cameras through the network cable.

### Layer 2 switch vs Layer 3 switch

- **Layer 2 switch:** forwards frames using MAC addresses.
- **Layer 3 switch:** can also route traffic between IP networks or VLANs.

## 2.3 Firewall

A **firewall controls network traffic according to security rules**.

Think of it as a security guard at a building entrance. It checks whether traffic should be allowed or blocked.

Rules may consider:
- Source IP address
- Destination IP address
- TCP or UDP port
- Protocol
- Connection state
- Application or content, depending on the firewall

**Example:** A rule might allow HTTPS traffic to a public web server but block remote desktop connections from the internet.

### Traditional firewall vs Next-Generation Firewall (NGFW)

- A traditional firewall commonly filters using IP addresses, ports, and protocols.
- An **NGFW** can add capabilities such as application awareness, intrusion prevention, and deeper traffic inspection.

Firewalls may also support VPNs, NAT, and routing.

## 2.4 IDS and IPS

Both monitor network or system activity for suspicious behavior.

| Technology | Full name | What it does |
|---|---|---|
| IDS | Intrusion Detection System | Detects suspicious activity and alerts an administrator |
| IPS | Intrusion Prevention System | Detects suspicious activity and can block it |

**Easy memory trick:**
- **IDS = Detect and alert.**
- **IPS = Detect and prevent.**

**Example:** If traffic looks like an attack:
- An IDS sends an alert.
- An IPS may drop the suspicious traffic automatically.

## 2.5 Load Balancer

A **load balancer distributes incoming requests across multiple servers**.

Imagine a busy supermarket with several checkout counters. Instead of sending every customer to one counter, customers are distributed across available counters.

```text
                  Users
                    |
              Load Balancer
               /     |     \
          Server 1 Server 2 Server 3
```

Benefits:
- Prevents one server from becoming overloaded.
- Improves availability.
- Can direct traffic away from unhealthy servers.
- Can support fault tolerance.

Some load balancers also provide:
- **SSL/TLS offloading:** handles encryption-related work on behalf of backend servers.
- **Caching:** stores reusable content to respond faster.
- **Content switching:** selects a backend based on the requested application or content.

## 2.6 Proxy Server

A **proxy sits between a client and another server** and makes requests on the client's behalf.

Think of a proxy as a middle person. You ask the proxy for something, and the proxy contacts the destination for you.

Common uses:
- Web filtering
- Access control
- Content inspection
- Caching frequently requested content
- Logging user web access

Types:
- **Explicit proxy:** the client is configured to use the proxy.
- **Transparent proxy:** traffic is directed through the proxy without requiring the same manual client configuration.

## 2.7 NAS and SAN

Both provide shared storage, but they present storage differently.

| Feature | NAS | SAN |
|---|---|---|
| Full name | Network Attached Storage | Storage Area Network |
| Access type | File-level | Block-level |
| How it appears | Shared files/folders | Storage volumes or disks |
| Common use | Shared documents and backups | High-performance server storage |

**NAS example:** A team stores and shares files on a network storage device.

**SAN example:** A data center provides storage volumes to servers as if they were locally attached disks.

Memory tip: **NAS = files; SAN = blocks.**

## 2.8 Wireless Access Point (AP)

An **access point connects wireless devices to a wired network**.

It allows devices such as laptops and phones to join the LAN over Wi-Fi.

**Example:** Your phone connects to an office Wi-Fi access point, which bridges the wireless connection to the wired network.

A basic access point primarily performs a Layer 2 bridging function.

## 2.9 Wireless LAN Controller (WLC)

A **Wireless LAN Controller centrally manages multiple access points**.

Imagine an organization with 50 access points in different rooms. Instead of configuring every access point separately, an administrator can manage many of them from one central system.

Common functions:
- Configure access points.
- Apply wireless security settings.
- Monitor performance.
- Manage channels and power settings.
- Push configuration changes centrally.

---

# 3. Important Networking Functions

These functions help networks remain secure, fast, and available.

## 3.1 CDN — Content Delivery Network

A **CDN stores copies of content on servers located in different geographic areas**.

Why is this useful?

Imagine a website hosted in the United States. A visitor in India may experience delay if every image and video must travel from the United States.

A CDN can cache copies of that content on a server closer to the visitor.

```text
Website origin server
       /       \
 CDN India    CDN Europe
     |            |
 India users   Europe users
```

Benefits:
- Faster content delivery.
- Reduced load on the original server.
- Better performance for images, videos, and static files.
- Improved availability when configured with multiple locations.

**Remember:** CDN = content delivered from a nearby location.

## 3.2 VPN — Virtual Private Network

A **VPN creates a protected connection across another network**, often the public internet.

Think of the internet as a public road. A VPN creates an encrypted tunnel so that data traveling through that road is protected from being easily read by others.

Common uses:
- Employees securely connecting to an office network.
- Connecting two office locations.
- Protecting traffic on untrusted networks.

### Common VPN types

- **Remote-access VPN:** connects an individual user's device to an organization.
- **Site-to-site VPN:** connects two networks, such as a head office and a branch office.

A VPN gateway or concentrator handles VPN connections and encryption. It may be a dedicated device, software, or a firewall feature.

**Remember:** VPN = protected communication over another network.

## 3.3 QoS — Quality of Service

**QoS prioritizes certain types of network traffic** when network capacity is limited.

Imagine a road with:
- An ambulance
- A delivery truck
- A normal car

During a traffic jam, the ambulance should receive priority. QoS applies a similar idea to network traffic.

Example:
- Voice/video calls: high priority
- Business-critical applications: higher priority
- Large background downloads: lower priority

QoS techniques can include:
- Traffic classification
- Prioritization
- Queuing
- Traffic shaping
- Rate limiting

**Remember:** QoS = decide which traffic should receive priority.

## 3.4 TTL — Time to Live

**TTL limits how long a packet can continue traveling.** In IPv4, routers reduce the TTL value as they forward a packet.

Why is this necessary?

Imagine Router A sends a packet to Router B, but Router B sends it back to Router A. The packet could travel in a loop.

```text
Router A  →  Router B
   ↑             |
   └─────────────┘
       routing loop
```

Without a limit, the packet could keep circulating.

TTL prevents this:
1. A packet starts with a TTL value, for example 64.
2. Each router forwarding it reduces the TTL by at least 1.
3. When the TTL reaches 0, the packet is discarded.

This helps prevent packets from circulating forever.

**Important:** TTL is a hop limit in IPv4, not simply a stopwatch measuring seconds.

## 3.5 DNS — Domain Name System

DNS translates human-friendly domain names into IP addresses.

People find names easier to remember than numbers.

For example:

```text
You type:       www.example.com
                     |
                    DNS
                     |
IP address returned: 93.184.216.34
```

The browser can then use the IP address to contact the server.

Key points:
- DNS is often described as the internet's phone book.
- DNS commonly uses UDP port 53.
- TCP port 53 is also used in situations such as zone transfers and responses that require TCP.
- DNS records can be cached.
- A record's TTL controls how long a DNS answer may be cached.

Useful Linux commands:

```bash
nslookup example.com
dig example.com
```

---

# 4. Cloud Networking and Design

## 4.1 What is cloud computing?

Cloud computing means using computing resources—such as servers, storage, databases, and networking—provided over a network instead of owning and maintaining all the physical equipment yourself.

**Traditional data center:**
- Buy physical servers.
- Install them in a data center.
- Maintain power, cooling, hardware, and networking.
- Upgrade equipment when more capacity is needed.

**Cloud computing:**
- Select the resources you need.
- Deploy them through a web console, API, or command line.
- Scale resources as demand changes.
- Pay according to the provider's pricing model.

## 4.2 Important cloud characteristics

### On-demand self-service

You can create resources when you need them without waiting for someone to manually install physical hardware.

**Example:** Launch an EC2 virtual machine from the AWS console.

### Elasticity

Resources can increase or decrease as demand changes.

**Example:** An online shopping site adds server capacity during a major sale and reduces it when traffic drops.

### Scalability

A system can handle growth by adding resources or increasing capacity.

- **Vertical scaling:** make one server more powerful (more CPU or RAM).
- **Horizontal scaling:** add more servers or instances.

### Multitenancy

Multiple customers share the provider's underlying infrastructure while remaining logically separated.

**Example:** Many organizations use the same cloud provider, but each customer's resources and data are isolated through security controls.

### Virtualization

Virtualization allows multiple virtual machines to run on one physical computer.

```text
           Physical server
                 |
             Hypervisor
          /      |      \
        VM 1    VM 2    VM 3
```

A **hypervisor** creates and manages virtual machines.

### NFV — Network Functions Virtualization

NFV replaces some dedicated physical network appliances with software-based network functions.

Examples:
- Virtual router
- Virtual firewall
- Virtual load balancer

The goal is to deploy and manage network functions more flexibly.

---

# 5. Cloud Deployment and Service Models

## 5.1 Cloud deployment models

| Model | Simple meaning | Example |
|---|---|---|
| Public cloud | Cloud services offered to customers over a provider's infrastructure | AWS, Microsoft Azure, Google Cloud |
| Private cloud | Cloud infrastructure dedicated to one organization | A company's private cloud |
| Hybrid cloud | A combination of private infrastructure and public cloud | Company data center connected to AWS |

### Public cloud

A provider operates the infrastructure and offers services to many customers.

**Important:** Public cloud does not mean that your data must be publicly accessible. Access is controlled using identity, network, and security settings.

### Private cloud

Cloud infrastructure is dedicated to one organization. It may be hosted in the organization's own data center or by a service provider.

### Hybrid cloud

An organization uses both private infrastructure and public cloud services, often connecting them through VPNs or dedicated network connections.

## 5.2 Cloud service models

The three important models are **SaaS, PaaS, and IaaS**.

Think about ordering food:

- SaaS: order a ready-to-eat meal.
- PaaS: receive a prepared kitchen and ingredients; you create the dish.
- IaaS: rent the kitchen infrastructure and manage much more yourself.

| Model | Full name | What the provider gives you | What you mainly manage |
|---|---|---|---|
| SaaS | Software as a Service | A complete application | How you use it and your data/settings |
| PaaS | Platform as a Service | A platform to build and run applications | Your application and its data |
| IaaS | Infrastructure as a Service | Virtual machines, storage, and networking | Operating system, applications, and configurations |

### SaaS — Software as a Service

You use a complete application over the internet. You usually do not manage the servers or operating system.

Examples:
- Gmail
- Microsoft 365
- Salesforce

**Simple idea:** Use the software; the provider manages the platform.

### PaaS — Platform as a Service

The provider manages the underlying infrastructure and platform. Developers focus on building and deploying applications.

**Example:** A developer deploys application code to a managed application platform without managing the physical servers.

**Simple idea:** You build the application; the provider manages much of the platform.

### IaaS — Infrastructure as a Service

The provider supplies virtual infrastructure such as compute, storage, and networking. You have more control, but also more responsibility.

**Example:** Launch an AWS EC2 instance, install an operating system package, configure a web server, and manage the application.

**Simple idea:** Rent the infrastructure; manage the operating system and what runs on it.

### Easy way to remember

- **SaaS:** use an application.
- **PaaS:** build an application.
- **IaaS:** manage virtual infrastructure.

---

# 6. IP, TCP, UDP, and Ports

## 6.1 Understanding IP with a delivery example

Imagine sending a parcel:

- The **road system** is the network.
- The **delivery address** is the IP address.
- The **delivery vehicle** is IP carrying the data.
- The **room number** is the port number, which helps deliver data to the right application.

An IP address identifies a network interface so that packets can be routed to the correct destination.

IP is responsible for addressing and moving packets between networks. It does not, by itself, guarantee that the data arrives.

## 6.2 TCP — Transmission Control Protocol

TCP provides reliable, connection-oriented communication.

Think of sending an important parcel where the delivery service:
1. Establishes the delivery arrangement.
2. Tracks what was sent.
3. Notices missing items.
4. Sends missing items again.
5. Delivers data in the correct order to the application.

TCP features:
- Connection establishment and termination.
- Acknowledgments.
- Retransmission when data is lost.
- Sequencing and ordered delivery.
- Flow control.

**Common uses:** HTTPS, SSH, email protocols, and many file-transfer applications.

### TCP connection setup: three-way handshake

Before normal TCP data transfer, the endpoints typically perform a three-way handshake:

```text
Client                         Server
  | -------- SYN ------------> |
  | <------ SYN-ACK ----------- |
  | -------- ACK ------------> |
  |                             |
  |       Connection ready      |
```

- **SYN:** client asks to start a connection.
- **SYN-ACK:** server acknowledges and responds.
- **ACK:** client acknowledges the response.

## 6.3 UDP — User Datagram Protocol

UDP is connectionless and has less protocol overhead than TCP.

Think of sending a quick announcement without waiting for each person to confirm receipt.

UDP features:
- No TCP-style connection setup.
- No built-in retransmission.
- No built-in guarantee that data arrives in order.
- No TCP-style flow control.
- Low overhead and often useful for time-sensitive communication.

Common uses include:
- DNS queries
- Voice and video communication
- Online gaming
- DHCP

**Important:** UDP does not mean the application can never recover from errors. An application can implement its own reliability features if needed.

## 6.4 TCP vs UDP

| Feature | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented | Connectionless |
| Delivery guarantee | Reliable delivery mechanisms | No built-in delivery guarantee |
| Ordering | Provides ordered delivery | No built-in ordering |
| Retransmission | Yes | No built-in retransmission |
| Overhead | Higher | Lower |
| Common use | Web, SSH, email | DNS queries, voice/video, gaming |

**Exam memory tip:**
- Need reliable, ordered delivery? Think **TCP**.
- Need low overhead and can tolerate some loss? Think **UDP**.

## 6.5 What is a port number?

An IP address identifies the destination device/interface. A port number helps identify the application or service on that device.

Example:

```text
IP address:  192.168.1.20
Port:        443
Protocol:    TCP

Meaning: connect to the service listening on TCP port 443
```

Think:
- IP address = building address.
- Port number = room number inside the building.

### Port number ranges

The complete TCP and UDP port-number range is **0–65535**.

| Range | Name | Explanation |
|---|---|---|
| 0–1023 | Well-known ports | Common standard services |
| 1024–49151 | Registered ports | Registered for particular applications/services |
| 49152–65535 | Dynamic/private ports | Commonly used as temporary client-side ports |

Operating systems may use different ephemeral port ranges, so do not assume every system uses exactly the same temporary range.

### What is a socket?

A socket is an endpoint used for network communication. A connection is commonly identified by details such as:

- Source IP address
- Source port
- Destination IP address
- Destination port
- Transport protocol (TCP or UDP)

**Important:** Port numbers help applications communicate. A port number alone is not a security control. Firewalls and other security controls determine which traffic is allowed.

---

# 7. Common Ports to Memorize

These are important ports for Network+ study. Learn the service, port number, and whether it commonly uses TCP, UDP, or both.

| Port | Protocol | Service | What it is used for |
|---:|---|---|---|
| 20 | TCP | FTP Data | FTP data transfer in active mode |
| 21 | TCP | FTP Control | FTP commands and control |
| 22 | TCP | SSH | Secure remote command-line access |
| 23 | TCP | Telnet | Unencrypted remote terminal access |
| 25 | TCP | SMTP | Sending/relaying email |
| 53 | TCP/UDP | DNS | Domain name resolution |
| 67 | UDP | DHCP Server | DHCP server listens for client requests |
| 68 | UDP | DHCP Client | DHCP client receives server responses |
| 69 | UDP | TFTP | Simple file transfer |
| 80 | TCP | HTTP | Unencrypted web traffic |
| 110 | TCP | POP3 | Receiving email |
| 123 | UDP | NTP | Time synchronization |
| 143 | TCP | IMAP | Accessing and synchronizing email |
| 161 | UDP | SNMP | Network monitoring and management queries |
| 162 | UDP | SNMP Trap | SNMP notifications/traps |
| 389 | TCP/UDP | LDAP | Directory services |
| 443 | TCP | HTTPS | Secure web traffic (HTTP over TLS) |
| 445 | TCP | SMB | Windows file and printer sharing |
| 514 | UDP | Syslog | Traditional syslog messages |
| 587 | TCP | SMTP Submission | Email submission by clients |
| 636 | TCP | LDAPS | LDAP over TLS |
| 993 | TCP | IMAPS | IMAP over TLS |
| 995 | TCP | POP3S | POP3 over TLS |
| 3389 | TCP/UDP | RDP | Microsoft Remote Desktop |

> Port usage can vary by implementation and configuration. For exam preparation, learn the common default associations above.

### Port memory tips

- **22 = SSH** — secure remote login.
- **23 = Telnet** — old, unencrypted remote login.
- **53 = DNS** — name to IP address.
- **67/68 = DHCP** — automatic IP configuration.
- **80 = HTTP** — normal web traffic.
- **443 = HTTPS** — secure web traffic.
- **3389 = RDP** — remote desktop.

### Test a port from Linux

Check whether a TCP service is reachable:

```bash
nc -vz example.com 443
```

Look up DNS:

```bash
dig example.com
```

Show listening TCP/UDP sockets on your own Linux machine:

```bash
ss -tuln
```

Only test systems and services you are authorized to access.

---

# 8. Quick Revision Tables

## Devices and their main jobs

| Device | Main job | Common OSI layer |
|---|---|---|
| Router | Routes packets between IP networks | Layer 3 |
| Layer 2 switch | Forwards frames using MAC addresses | Layer 2 |
| Layer 3 switch | Switching plus IP routing | Layers 2 and 3 |
| Firewall | Allows or blocks traffic using rules | Varies; commonly Layers 3–7 |
| Access point | Connects wireless devices to a LAN | Primarily Layer 2 |
| Load balancer | Distributes requests across servers | Layers 4 and/or 7 |
| Proxy | Makes requests on behalf of clients | Commonly Layer 7 |
| IDS | Detects and alerts | Varies |
| IPS | Detects and blocks | Varies |

## Functions at a glance

| Term | Remember it as |
|---|---|
| CDN | Copies content closer to users |
| VPN | Protected tunnel across another network |
| QoS | Prioritizes important traffic |
| TTL | Limits packet lifetime/hops |
| DNS | Converts names to IP addresses |
| NAT | Translates IP addresses |
| DHCP | Automatically provides IP configuration |

## Cloud terms at a glance

| Term | Simple meaning |
|---|---|
| Elasticity | Add or remove resources as demand changes |
| Scalability | Handle growth by increasing capacity |
| Multitenancy | Multiple customers share provider infrastructure with logical isolation |
| Virtualization | Run virtual systems on physical hardware |
| Hypervisor | Creates and manages virtual machines |
| NFV | Network functions delivered as software |
| VPC | Logically isolated virtual network in a cloud |
| VPN | Encrypted connection between networks or users |
| Internet Gateway (AWS) | Enables communication between a VPC and the internet when routing and security allow it |
| NAT Gateway (AWS) | Lets private-subnet resources initiate outbound internet connections |
| VPC Endpoint (AWS) | Private connection from a VPC to supported services |

## AWS VPC concepts — beginner explanation

Since cloud networking is part of Network+ and AWS learning, here are the common AWS terms:

- **VPC:** your logically isolated network in AWS.
- **Subnet:** a smaller IP network inside the VPC. A subnet is associated with one Availability Zone.
- **Internet Gateway (IGW):** provides a path between a VPC and the internet when route tables and security rules are configured correctly.
- **Public subnet:** a subnet whose route table has a route to an Internet Gateway. A resource also needs a public IP and suitable security rules for direct internet communication.
- **Private subnet:** a subnet without a direct route to an Internet Gateway.
- **NAT Gateway:** commonly allows instances in a private subnet to start connections to the internet, while preventing unsolicited inbound connections from the internet.
- **Security Group:** stateful virtual firewall associated with resources such as network interfaces.
- **Network ACL (NACL):** stateless subnet-level traffic filter.
- **VPC Endpoint:** allows private connectivity to supported AWS services without requiring traffic to travel through the public internet.

**Important distinction:**
- Security Groups are **stateful**: return traffic for an allowed connection is automatically permitted.
- Network ACLs are **stateless**: inbound and outbound rules are evaluated separately.

---

# 9. Practice Questions

Try answering these before checking the answers.

### Questions

1. Which OSI layer is responsible for routing packets between networks?
2. Which address is used by a Layer 2 switch to forward Ethernet frames?
3. What is the main difference between an IDS and an IPS?
4. Which device distributes client requests across several servers?
5. What does a CDN do?
6. Which VPN type connects two office networks?
7. What happens when an IPv4 packet's TTL reaches zero?
8. What service translates a domain name into an IP address?
9. Which transport protocol provides reliable, ordered delivery?
10. Which transport protocol has less overhead and no built-in retransmission?
11. What is the default port commonly associated with HTTPS?
12. Which port is commonly used by SSH?
13. What is the difference between NAS and SAN?
14. What does elasticity mean in cloud computing?
15. Which cloud service model gives developers a platform to build applications?
16. In AWS, which is stateful: a Security Group or a Network ACL?

<details>
<summary><strong>Show answers</strong></summary>

1. Layer 3 — Network.
2. MAC address.
3. IDS detects and alerts; IPS can detect and block.
4. Load balancer.
5. Caches content at geographically distributed locations to deliver it closer to users.
6. Site-to-site VPN.
7. The router discards the packet.
8. DNS.
9. TCP.
10. UDP.
11. TCP port 443.
12. TCP port 22.
13. NAS provides file-level access; SAN provides block-level access.
14. Resources can be increased or decreased as demand changes.
15. PaaS.
16. Security Group. Network ACLs are stateless.

</details>

---

# 10. Useful Linux Commands

Practice these commands in your own Linux environment.

| Command | Purpose |
|---|---|
| `ip addr` | Show IP addresses on network interfaces |
| `ip route` | Show the routing table |
| `ping example.com` | Test basic reachability |
| `traceroute example.com` | Show the route toward a destination |
| `tracepath example.com` | Trace the path and discover path MTU information |
| `nslookup example.com` | Query DNS |
| `dig example.com` | Perform detailed DNS queries |
| `ss -tuln` | Show listening TCP/UDP sockets |
| `ip neigh` | Show the neighbor table (such as ARP information for IPv4) |
| `curl -I https://example.com` | Request HTTP response headers |
| `nc -vz example.com 443` | Test TCP connectivity to a port |

If a command is not installed, use your distribution's package manager to install the appropriate package.

---

## Suggested Study Order

If you are learning networking from the beginning, study in this order:

1. Understand the seven OSI layers.
2. Learn the difference between MAC addresses and IP addresses.
3. Understand what routers, switches, and firewalls do.
4. Learn DNS, DHCP, VPN, CDN, QoS, and TTL.
5. Understand IPv4, TCP, UDP, and ports.
6. Memorize common ports gradually.
7. Learn cloud concepts and AWS VPC networking.
8. Practice the Linux commands and answer the questions.

## Final Reminder

Do not try to memorize the entire document in one sitting. For each topic, ask yourself:

- **What is it?**
- **Why do we need it?**
- **How does it work?**
- **Can I give a real-world example?**

If you can explain those four things in your own words, you are building real networking understanding—not just memorizing exam answers.

These are learning notes, not the complete official CompTIA exam objectives. Use them alongside the current N10-009 objectives and practice questions.
