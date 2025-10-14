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


## The OSI Layers - an Example (Sender)

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

## The OSI Layers - an Example (Receiver)

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

![WhatsApp Image 2025-10-11 at 1 23 17 PM (1)](https://github.com/user-attachments/assets/e81c280f-d27d-4980-9a60-354d6fd97333)

![WhatsApp Image 2025-10-11 at 1 23 16 PM](https://github.com/user-attachments/assets/d9edc136-5353-432e-9e33-d9f4f1939e9e)

![WhatsApp Image 2025-10-11 at 1 23 16 PM (1)](https://github.com/user-attachments/assets/b74b6ea2-ca1d-4f73-92ac-db15af70f749)

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
