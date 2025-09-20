This repository contains the Cisco Packet Tracer project files for a comprehensive enterprise network design and implementation for Radeon Company Ltd., a banking and insurance firm expanding into a new four-story building in Nairobi, Kenya.

## 📜 Table of Contents
* [Project Overview](#-project-overview)
* [Network Topology](#-network-topology)
* [Key Features & Technologies](#-key-features--technologies)
* [IP Addressing Scheme](#-ip-addressing-scheme)
* [Configuration Highlights](#-configuration-highlights)
* [Software Used](#-software-used)
* [How to Use](#-how-to-use)

---

## 📝 Project Overview

Radeon Company Ltd. required a scalable, secure, and resilient network for their new four-story office. This project addresses their needs by implementing a hierarchical network that segments traffic, provides robust security, and ensures high availability. The design supports approximately 60 wired and wireless users per department, with dedicated servers for critical services.

---

## 🌐 Network Topology

The network is built on a **hierarchical model** to enhance performance, scalability, and fault tolerance.

* **Access Layer:** Consists of switches on each floor that connect directly to end-user devices (PCs, laptops, printers, IP phones) and wireless access points.
* **Distribution Layer:** Aggregates traffic from the access layer switches using a dedicated router on each floor. This layer handles inter-VLAN routing and applies network policies.
* **Core Layer:** Provides a high-speed backbone for the entire network, connecting the distribution layer routers from all floors to ensure fast and reliable communication across the enterprise.

This project implements one router on each of the four floors, which serves as the distribution layer for that specific floor, connecting upwards to a core layer for inter-floor communication.

---

## 🚀 Key Features & Technologies

This network implementation incorporates a wide range of modern networking technologies and best practices:

* **VLANs (Virtual LANs):** Each department is placed in a separate VLAN to segment the network. This enhances security by isolating broadcast domains and controlling traffic flow between departments.
* **Subnetting:** The base network address `192.168.10.0` was subnetted using a `/26` mask (`255.255.255.192`) to create appropriately sized subnets for each department, accommodating up to 62 hosts.
* **Inter-VLAN Routing:** A "Router-on-a-Stick" configuration is used on each floor's router to enable communication between different VLANs.
* **OSPF (Open Shortest Path First):** OSPF is configured as the dynamic routing protocol to allow routers to automatically learn and advertise routes, ensuring efficient and redundant data paths.
* **DHCP (Dynamic Host Configuration Protocol):** A dedicated DHCP server, located in the Server Room on the Fourth Floor, is configured to automatically assign IP addresses to all host devices, simplifying network management.
* **Network Services:** The network includes dedicated servers for essential services:
    * **HTTP Server** for web services.
    * **E-mail Server** for internal and external communication.
* **Wireless Connectivity:** Each department is equipped with a wireless network to provide seamless connectivity for mobile users.
* **Device Security:** Basic security hardening has been applied to all network devices:
    * Secure passwords for **Line Console** and **VTY** lines.
    * Warning **banner messages** for unauthorized access attempts.
    * Disabled **domain IP lookup** to prevent unwanted DNS queries.
* **Secure Remote Management:** **SSH (Secure Shell)** is configured on all routers to provide encrypted and secure remote access for network administrators.

---

## 💻 IP Addressing Scheme

The IP addressing plan is meticulously designed to support the departmental structure across the four floors.

### First Floor
| Department | Network Address | Subnet Mask | Host Range | VLAN ID |
| :--- | :--- | :--- | :--- | :--- |
| Management | `192.168.10.0` | `255.255.255.192` | `192.168.10.1 - 62` | 10 |
| Research | `192.168.10.64` | `255.255.255.192` | `192.168.10.65 - 126` | 20 |
| Human Res | `192.168.10.128`| `255.255.255.192` | `192.168.10.129 - 190`| 30 |

### Second Floor
| Department | Network Address | Subnet Mask | Host Range | VLAN ID |
| :--- | :--- | :--- | :--- | :--- |
| Marketing | `192.168.10.192`| `255.255.255.192` | `192.168.10.193 - 254`| 40 |
| Accounts | `192.168.11.0` | `255.255.255.192` | `192.168.11.1 - 62` | 50 |
| Finance | `192.168.11.64` | `255.255.255.192` | `192.168.11.65 - 126` | 60 |

### Third Floor
| Department | Network Address | Subnet Mask | Host Range | VLAN ID |
| :--- | :--- | :--- | :--- | :--- |
| Logistics | `192.168.11.128`| `255.255.255.192` | `192.168.11.129 - 190`| 70 |
| Customer | `192.168.11.192`| `255.255.255.192` | `192.168.11.193 - 254`| 80 |
| Guest | `192.168.12.0` | `255.255.255.192` | `192.168.12.1 - 62` | 90 |

### Fourth Floor
| Department | Network Address | Subnet Mask | Host Range | VLAN ID |
| :--- | :--- | :--- | :--- | :--- |
| Admin | `192.168.12.64` | `255.255.255.192` | `192.168.12.65 - 126` | 100 |
| ICT | `192.168.12.128` | `255.255.255.192` | `192.168.12.129 - 190`| 110 |
| Server Room | `192.168.12.192`| `255.255.255.192` | `192.168.12.193 - 254`| 120 |

---

## ⚙️ Configuration Highlights

Here are some sample configurations from the project.

#### VLAN Creation on a Switch
```cisco
vlan 10
 name Management
vlan 20
 name Research
vlan 30
 name Human_Resources
!
interface range FastEthernet0/1 - 5
 switchport mode access
 switchport access vlan 10
