# 📘 Fundamentals of Network Engineering

## 🌐 Basic Network Properties

| Property | Description |
|-----------|--------------|
| **IP Address** | Assigned **dynamically** by your router (via DHCP). It identifies your device on the network. |
| **MAC Address** | A **permanent** hardware address embedded in your **Network Interface Card (NIC)**. Used for local identification within a network. |
| **Gateway IP** | The **IP address of your router**. It acts as a gateway to connect your local network to other networks (e.g., the internet). |

---

## 🧩 Why Do We Need a Communication Model?

A **communication model** provides a **standardized structure** for building and understanding network systems.

### 🔍 Key Reason:
To build **network-agnostic applications** — i.e., applications that can work seamlessly over **Wi-Fi**, **Ethernet**, **LTE**, or **Fiber**, **without needing separate implementations**.

> Example:  
> Imagine if every app had to be rewritten to support different network types — the complexity would be unmanageable.  
> The communication model abstracts this by defining clear **layers** and **responsibilities**.

---

## 🏗️ OSI Model (Open Systems Interconnection)

A conceptual model with **7 layers**, where each layer defines a specific function in the data communication process.

### 🔢 The 7 Layers of OSI

| Layer | Name | Description | Protocols |
|--------|------|--------------|-------------------------------|
| **7** | **Application** | Interfaces with the end user; defines how apps interact with the network. | **HTTP**, **FTP**, **gRPC**, **SMTP** |
| **6** | **Presentation** | Handles **encoding**, **encryption**, and **serialization**. | **SSL/TLS**, **JSON**, **XML**, **Base64** |
| **5** | **Session** | Manages **session establishment**, **maintenance**, and **termination** between devices. | **RPC**, **gRPC sessions** |
| **4** | **Transport** | Responsible for **end-to-end communication**, reliability, and flow control. | **TCP**, **UDP** |
| **3** | **Network** | Handles **logical addressing** and **routing** of packets. | **IP** |
| **2** | **Data Link** | Deals with **physical addressing (MAC)** and **frame transmission** within the same network. | **Ethernet**, **Wi-Fi** |
| **1** | **Physical** | Transmits **raw bits** over a physical medium like electrical signals, fiber optics, or radio waves. | **Cables**, **Radio**, **Fiber** |

---

### 🧭 Flow of Data in OSI Model


#### The OSI Layers - an Example (Sender)

- Example sending a POST request to an HTTPS webpage
- Layer 7 - **Application**
  - POST request with JSON data to HTTPS server
- Layer 6 - **Presentation**
  - Serialize JSON to flat byte strings
- Layer 5 - **Session**
  - Request to establish TCP connection/TLS
- Layer 4 - **Transport**
  - Sends SYN request target port 443
- Layer 3 - **Network**
  - SYN is placed an IP packet(s) and adds the source/dest IPs
- Layer 2 - **Data link**
  - Each packet goes into a single frame and adds the source/dest MAC addresses
- Layer 1 - **Physical**
  - Each frame becomes a string of bits which converted into either a radio signal (wifi), electric signal (ethernet), or light (fiber)

---

#### The OSI Layers - an Example (Receiver)

- Receiver computer receives the POST request the other way around
- Layer 1 - **Physical**
  - Radio, electic or light is received and converted into digital bits
- Layer 2 - **Data link**
  - The bits from Layer 1 is assembled into frames
- Layer 3 - **Network**
  - The frames from Layer 2 are assembled into IP packets
- Layer 4 - **Transport**
  - The IP packets from Layer 3 are assembled into TCP segments
  - Deals with Congestion control/flow control/retransmission in case of TCP
  - If segment is SYN we don't need to go further into more layers as we are still processing the connection request
- Layer 5 - **Session**
  - The connection session is established or identified
  - We only arrive at this layer when necessary (three way handshake is done)
- Layer 6 - **Presentation**
  - Deserialize flat byte strings back to JSON for the app to continue
- Layer 7 - **Application**
  - Application understands the JSON POST request and your express or rails request receive event is triggered

---

![WhatsApp Image 2025-10-18 at 5 25 08 PM](https://github.com/user-attachments/assets/7cdeb9d3-70e0-4530-ae31-6841e4d54f4a)

![WhatsApp Image 2025-10-18 at 5 25 09 PM](https://github.com/user-attachments/assets/4529581a-e45e-4339-a951-609889925990)

![WhatsApp Image 2025-10-18 at 5 25 09 PM (1)](https://github.com/user-attachments/assets/8b1841f4-a71d-4040-9601-aaf2caefdb94)

---

## 🌍 TCP/IP Model

A more **practical and simplified** model compared to OSI, used in real-world networking (including the Internet).

### 🧱 Layers of TCP/IP Model

| Layer | Corresponding OSI Layers | Description | Protocols |
|--------|--------------------------|--------------|--------------------|
| **4** | Application (Layers 5–7) | Handles application-level interactions like web browsing, file transfers, etc. | **HTTP**, **DNS**, **FTP**, **SMTP** |
| **3** | Transport (Layer 4) | Provides reliable or unreliable delivery between devices. | **TCP**, **UDP** |
| **2** | Internet (Layer 3) | Defines addressing, routing, and packet delivery across networks. | **IP** |
| **1** | Network Access (Layers 1–2) | Manages how data is physically sent over the medium. | **Ethernet**, **Wi-Fi** |

---

# 🖥️ Host-to-Host Communication (Layer 2-3 Concepts)

## 1. Message Sending Overview
- When Host A sends a message to Host B, it usually involves a request for Host B to perform some action (e.g., RPC).
- Each host's network interface card (NIC) has a **unique MAC address**.
- Host A specifies the **destination MAC address** to send the message.

## 2. MAC Addressing and Network Broadcast
- At Layer 2 (Data Link Layer), all devices on the same network **receive the message** because it's broadcast.
- Only the host with the matching MAC address **accepts and processes** the message.
- This typically happens in a **private network** or LAN environment.

## 3. Scalability Issues in Large Networks
- In networks with **millions of machines**, broadcasting messages to all hosts is inefficient.
- We need an addressing method to **eliminate unnecessary broadcast**.

## 4. IP Addressing (Layer 3) for Efficient Routing
- The **IP address** consists of two parts:
  - **Network portion:** Identifies the specific network or subnet.
  - **Host portion:** Identifies the host within that network.
- Routers use the network portion to **route packets only to the correct subnet**, reducing network traffic.
- The host portion is used to deliver the packet within the subnet.
- Even with IP addressing, **MAC addresses are still needed** at Layer 2 for final delivery.

## 5. Ports for Application-level Addressing
- A single host runs **multiple applications** simultaneously, each requiring its own communication channel.
- IP addresses identify the host, but **ports identify the specific application/service**.
- Example:
  - HTTP request on port 8080.
  - DNS request on port 53.
- Ports allow the same host to **handle multiple types of requests independently**.

---

# 🌐 Internet Protocol (IP)

## 🧩 IP Building Blocks

### 1. IP Address
- A **Layer 3** (Network Layer) property.
- Can be assigned:
  - **Statically** (manually configured)
  - **Dynamically** (via DHCP)
- Consists of:
  - **Network portion**
  - **Host portion**
- In **IPv4**, it is **32 bits (4 bytes)**.
- Example: `192.168.10.25`

---

### 2. Network vs Host Portion
- Represented as: `a.b.c.d/x`
  - `a.b.c.d` → IP address (in decimal)
  - `/x` → number of **network bits**
- The remaining bits (32 - x) represent the **host portion**.

#### 🧮 Example
`192.168.254.0/24`
- `/24` → 24 bits for **network**, 8 bits for **host**
- This means:
  - Network part → `192.168.254`
  - Host part → last octet (0–255)
  - **Usable hosts:** 2⁸ - 2 = **254**

> ⚠️ Note: We subtract 2 because one address is reserved for the *network address* and one for the *broadcast address*.

---

### 3. Subnet
A **subnet (sub-network)** is a smaller network within a larger one.  
Defined using **CIDR notation** (`/x`) or **subnet mask**.

#### Example
- `192.168.254.0/24`
- Equivalent subnet mask: `255.255.255.0`
- All IPs from `192.168.254.1` to `192.168.254.254` belong to the same subnet.

---

### 4. Subnet Mask
- Used to **determine which part of an IP address is the network portion** and which is the host portion.
- Written as:
  - Dotted decimal: `255.255.255.0`
  - Binary: `11111111.11111111.11111111.00000000`
- Example mapping:
  - `192.168.10.5/24` → Mask = `255.255.255.0`

---

### 5. CIDR Notation (`/x`)
- The `/x` **always specifies how many bits are for the network portion**.
- Remaining bits are for hosts.

#### Examples:
| CIDR | Network Bits | Host Bits | Usable Hosts | Subnet Mask |
|------|---------------|------------|---------------|--------------|
| `/8` | 8 | 24 | 16,777,214 | 255.0.0.0 |
| `/16` | 16 | 16 | 65,534 | 255.255.0.0 |
| `/24` | 24 | 8 | 254 | 255.255.255.0 |
| `/26` | 26 | 6 | 62 | 255.255.255.192 |

---

### 6. Determining If Two Devices Are on the Same Network

To check if two IPs are in the same network:

#### Step-by-step:
- Convert both IPs and subnet mask to **binary**.
- Perform **bitwise AND** (IP AND subnet mask).
- If the **results match**, both are in the same network.

#### Example:
| Device | IP | Subnet Mask | Network Address |
|---------|----|-------------|----------------|
| A | 192.168.10.5 | 255.255.255.0 | 192.168.10.0 |
| B | 192.168.10.200 | 255.255.255.0 | 192.168.10.0 |

✅ Same network → communicate directly.

| Device | IP | Subnet Mask | Network Address |
|---------|----|-------------|----------------|
| A | 192.168.10.5 | 255.255.255.0 | 192.168.10.0 |
| B | 192.168.11.5 | 255.255.255.0 | 192.168.11.0 |

❌ Different networks → communication must go through a **router (gateway)**.

---

### 7. Default Gateway
- The **gateway** (often a router) connects a local network to other networks.
- Each host in a subnet must know its **default gateway IP**.
- Communication logic:
  - If destination is in the same subnet → send directly.
  - If destination is outside the subnet → send to **gateway**.

---

### 8. Who Provides the Subnet Mask?
- In most setups, **the router provides it via DHCP**.
- DHCP automatically assigns:
  - IP address  
  - Subnet mask  
  - Default gateway  
  - DNS servers

---

# 🧾 IP Packet, ICMP & ARP

## IP Packet (IPv4)
- IP packet = **Header** + **Data**.
- **Header**
  - Minimum size: **20 bytes**.
  - Maximum size: **60 bytes** (when options are present).
  - Important header fields:
    - **TTL (Time To Live)** — decremented by each router; when TTL = 0 packet is discarded.
    - **Protocol** — indicates next-level protocol (e.g., 1 = ICMP, 6 = TCP, 17 = UDP).
    - **Source IP**, **Destination IP**
    - **Options** (if any; make header > 20 bytes)
    - **ECN** (Explicit Congestion Notification) — used for congestion signalling (requires endpoint & network support).
- **Data**
  - Maximum payload size = `65,535 − header_length`.
  - For common 20-byte header, payload max = **65,515 bytes**.

---

## ICMP (Internet Control Message Protocol)
- **Layer:** Operates with IP at Layer 3.
- **Purpose:** Provide network-layer diagnostic and control messages (e.g., Destination Unreachable, Echo Request/Reply).
- **Common uses:**
  - **ping**: uses **ICMP Echo Request** and **Echo Reply** to test reachability/latency.
- **Firewall behavior:** ICMP is often filtered/blocked or rate-limited for security reasons. If ICMP is blocked, `ping` may fail even if host is reachable.
- **No ports:** ICMP messages do not use TCP/UDP ports — they are encapsulated directly in IP.

---

## ARP (Address Resolution Protocol)
- **Purpose:** Resolve **IPv4 address → MAC address** on the local network so L2 frames can be addressed properly.
- **Basic flow (conceptual):**
  - Host A needs MAC for IP X.
  - Host A broadcasts an ARP Request: "Who has IP X? Tell MAC_A".
  - Host with IP X replies with an ARP Reply containing its MAC (unicast).
  - Host A updates its **ARP table** with the IP↔MAC mapping.
- **ARP cache:** Operating systems store mappings for a limited time to avoid repeated broadcasts.
- **Why important:** Ethernet frames require destination MAC addresses; IP addresses alone are insufficient for Layer 2 delivery.

---

# 🧩 UDP (User Datagram Protocol)

## 🔹 What is UDP?
- Layer 4 protocol  
- Addresses **processes** in a host using **ports**  
- Simple protocol for sending and receiving data  
- **No prior communication required** before transmission  
- **Stateless:** the host stores no connection information 

---

## 🔹 Multiplexing & Demultiplexing
- IP addresses only identify **target hosts**, not specific applications  
- A host may run **many applications**, each needing its own data 
- **Ports** are used to identify individual apps or processes  
- Sender side (multiplexes): 
  - Multiple applications on the same **IP address/Host** want to send data
  - UDP wraps each application’s data into its own datagram with a source and destination port
  - Each datagram is sent as a separate **IP packet** over the network    
- Receiver side (demultiplexes):
  - The host receives incoming IP packets containing UDP datagrams  
  - UDP extracts each datagram and delivers it to the **correct application** based on **destination port**

---

## 🔹 UDP Datagram Structure
- UDP Datagram = **Header + Data**
- UDP Header: 
  - Size: **8 bytes** (for IPv4)   
  - Port numbers: **16 bits each** → range **0 to 65,535**  
- The datagram is encapsulated as **data** inside an IP packet 

---

## 🔹 Limitations
- No acknowledgment (no ACKs)
- No guarantee of delivery  
- Connection-less - any host can send data without setup  
- Security risk - packets can be easily **spoofed**

---
