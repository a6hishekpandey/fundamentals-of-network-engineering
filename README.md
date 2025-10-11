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

![WhatsApp Image 2025-10-11 at 1 11 22 PM](https://github.com/user-attachments/assets/c47c4e19-918d-49e9-87db-2daf39520651)
![WhatsApp Image 2025-10-11 at 1 11 22 PM (1)](https://github.com/user-attachments/assets/7475f8f4-d22d-4686-a7e1-b94263aa7293)
![WhatsApp Image 2025-10-11 at 1 11 23 PM](https://github.com/user-attachments/assets/58bf296b-1454-4282-81dd-54571713558f)
![WhatsApp Image 2025-10-11 at 1 11 23 PM (1)](https://github.com/user-attachments/assets/1d3c7f42-dc2d-4008-9cc8-a914cfe9fc73)
![WhatsApp Image 2025-10-11 at 1 11 23 PM (2)](https://github.com/user-attachments/assets/89e6c12f-d831-4400-869a-c0fc3eda08e4)

---

## 🌍 TCP/IP Model

A more **practical and simplified** model compared to OSI, used in real-world networking (including the Internet).

### 🧱 Layers of TCP/IP Model

| Layer | Corresponding OSI Layers | Description | Protocols |
|--------|--------------------------|--------------|--------------------|
| **4** | Application (Layers 5–7) | Handles application-level interactions like web browsing, file transfers, etc. | **HTTP**, **DNS**, **FTP**, **SMTP** |
| **3** | Transport (Layer 4) | Provides reliable or unreliable delivery between devices. | **TCP**, **UDP** |
| **2** | Internet (Layer 3) | Defines addressing, routing, and packet delivery across networks. | **IP**, **ICMP**, **ARP** |
| **1** | Network Access (Layers 1–2) | Manages how data is physically sent over the medium. | **Ethernet**, **Wi-Fi**, **PPP** |
