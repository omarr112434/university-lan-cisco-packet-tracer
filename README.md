# 🌐 University Building LAN — Cisco Packet Tracer Design & Simulation

**BUE Local & Wide Area Networks (25CSCN08I) | April 2026**

> Design, configuration, and simulation of a multi-VLAN Local Area Network for a university building using Cisco's three-layer hierarchical model. Built end-to-end in Cisco Packet Tracer 8.2 with full DHCP, DNS, HTTP, FTP, and secured wireless services.

---

## 👤 Author

| Field | Detail |
|---|---|
| **Name** | Omar Hany Saed |
| **Student ID** | 239372 |
| **University** | British University in Egypt (BUE) |
| **Module** | 25CSCN08I — Local/Wide Area Networks & Network Protocols |
| **Date** | April 2026 |

---

## 🎯 Project Overview

A complete simulation of a university building network supporting multiple departments with logical traffic separation, automatic IP addressing, internal DNS resolution, web/FTP services, and secured Wi-Fi for student devices — all built and tested in Cisco Packet Tracer.

### Key Achievements
- ✅ Three-layer hierarchical design (Core → Distribution → Access)
- ✅ Layer 3 routing across **4 VLANs** with inter-VLAN connectivity
- ✅ DHCP relay across VLANs from a centralized server
- ✅ Internal DNS service mapping `www.university.local`
- ✅ HTTP & FTP services hosted in segmented Server VLAN
- ✅ Secured wireless network using **WPA2-PSK with AES**
- ✅ Full end-to-end testing — all connectivity tests passed

---

## 🏗️ Network Architecture

### Three-Layer Hierarchical Model

| Layer | Devices | Role |
|---|---|---|
| **Core Layer** | 1× Cisco 3560-24PS (Multilayer Switch) | Inter-VLAN routing using SVIs, `ip routing` enabled |
| **Distribution Layer** | 2× Cisco 2960-24TT | Aggregation, 802.1Q trunking |
| **Access Layer** | 4× Cisco 2960-24TT | Endpoint connectivity for PCs, Servers, AP |

### VLAN Design

| VLAN ID | Department | Network | Gateway |
|---|---|---|---|
| 10 | IT_Dept | 192.168.10.0/24 | 192.168.10.1 |
| 20 | Admin_Dept | 192.168.20.0/24 | 192.168.20.1 |
| 30 | Student_WiFi | 192.168.30.0/24 | 192.168.30.1 |
| 40 | Server_Room | 192.168.40.0/24 | 192.168.40.1 |

### Server Infrastructure (VLAN 40)

| Server | IP | Service |
|---|---|---|
| DHCP-Server | 192.168.40.10 | DHCP pools for VLAN 10/20/30 |
| DNS-Server | 192.168.40.20 | A-record: `www.university.local → 192.168.40.30` |
| Web-Server | 192.168.40.30 | HTTP service |
| FTP-Server | 192.168.40.40 | File transfer (cisco/cisco) |

### Wireless Configuration

| Setting | Value |
|---|---|
| **SSID** | University-WiFi |
| **Channel** | 6 (2.4 GHz) |
| **Security** | WPA2-PSK |
| **Encryption** | AES |
| **VLAN** | 30 (Student_WiFi) |
| **Standard** | IEEE 802.11 |

---

## 🛠️ Configuration Highlights

### Core Switch — Layer 3 Routing
```cisco
hostname Core-SW
enable secret cisco123
service password-encryption
banner motd #WARNING: Authorized Access Only!#
!
ip routing
!
interface vlan 10
 ip address 192.168.10.1 255.255.255.0
 no shutdown
!
interface range fa0/1 - 2
 switchport trunk encapsulation dot1q
 switchport mode trunk
```

### VLAN Creation
```cisco
vlan 10
 name IT_Dept
vlan 20
 name Admin_Dept
vlan 30
 name Student_WiFi
vlan 40
 name Server_Room
```

---

## ✅ Testing & Verification

| Test | Result |
|---|---|
| **DHCP across VLANs** | ✓ IT-PC3 received `192.168.10.101`, Admin-PC3 received `192.168.20.104` |
| **Inter-VLAN Routing** | ✓ IT-PC1 (VLAN 10) successfully pinged Admin-PC1 (VLAN 20) — sub-1ms reply |
| **Server Reachability** | ✓ DNS server (`192.168.40.20`) reachable from VLAN 10 |
| **HTTP Service** | ✓ Web browser on IT-PC1 loaded `http://192.168.40.30` successfully |
| **WiFi Connectivity** | ✓ Student-Laptop1 connected to University-WiFi, pinged IT-PC1 with 4/4 replies (0% loss) |
| **Default Gateway** | ✓ `ping 192.168.10.1` from IT-PC1 → 4/4 replies, 0% loss |

---

## 📁 Repository Contents

| File | Description |
|---|---|
| `final_report_omar239372.pdf` | **Phase 2 Final Report** — full documentation including topology, IP scheme, configurations, and testing screenshots |
| `omar239372_complere_packet_tracer.pkt` | **Cisco Packet Tracer simulation file** — open in Packet Tracer 8.2+ to view and interact with the live network |
| `LAN-WAN__NP_Project_Coursework_Orientation.pptx` | **Project orientation presentation** — coursework overview slides |

---

## 🔧 How to Open the Simulation

1. Install **Cisco Packet Tracer 8.2** or later (free with Cisco Networking Academy account)
2. Download `omar239372_complere_packet_tracer.pkt`
3. Open it in Packet Tracer
4. Click any device → **CLI** tab to view configurations
5. Use `ping` from any PC's Command Prompt to test connectivity

---

## 💡 Reflection & Future Improvements

The most valuable lesson from this project was that small commands have huge consequences — forgetting `ip routing` on the Core-SW broke all inter-VLAN communication and took hours to diagnose. Watching pings actually work after correct configuration made networking concepts stick far better than reading textbooks alone.

**Planned improvements for future iterations:**
- 🔁 Add a redundant core switch with HSRP/VRRP for high availability
- 🛡️ Implement ACLs on the core to restrict VLAN-to-server access (least-privilege)
- 📊 Configure SNMP monitoring and syslog collection
- 🔐 Add 802.1X authentication for wired ports
- 🌍 Extend to a WAN scenario with multi-site VPN connectivity

---

## 📚 References

1. B. A. Forouzan, *Data Communications and Networking*, 5th ed. McGraw-Hill, 2013.
2. A. S. Tanenbaum & D. J. Wetherall, *Computer Networks*, 5th ed. Pearson, 2011.
3. IEEE Standards Association, *IEEE Standard for Ethernet*, IEEE Std 802.3-2018, 2018.
4. J. F. Kurose & K. W. Ross, *Computer Networking: A Top-Down Approach*, 7th ed. Pearson, 2017.
5. IEEE Standards Association, *IEEE Standard for Wireless LAN*, IEEE Std 802.11-2020, 2020.

---

## 📬 Contact

- **LinkedIn:** [linkedin.com/in/omar-hany-642aa7300](https://www.linkedin.com/in/omar-hany-642aa7300)
- **Email:** oh24237@gmail.com
- **GitHub:** [github.com/omarr112434](https://github.com/omarr112434)
