# 🌐 Enterprise Multi-Area OSPF & Campus Network Infrastructure
**A Comprehensive Enterprise Networking Project | Cisco Packet Tracer**

---

## 📌 Project Overview

This project presents the design, implementation, and configuration of a scalable, resilient, and secure enterprise campus network using **Cisco Packet Tracer**.

The infrastructure consists of:

- **11 Cisco Routers**
- Layer 3 Multilayer Switches
- Layer 2 Access Switches
- Multiple LAN segments and VLANs
- Centralized DHCP and VoIP services

The primary objective is to integrate advanced routing protocols, OSPF area optimization, multi-protocol redistribution, Layer 2/3 redundancy, VoIP, and enterprise security into one comprehensive network architecture.

## 🏗️ Network Topology

### Topology Overview

*The complete topology includes multiple routing domains, campus LANs, redundant switching paths, and external network connectivity.*

---

## 🌍 Network Architecture & Routing Design

### 1. Multi-Area OSPF & LSA Optimization

The network implements five OSPF areas with different area types and routing policies.

| OSPF Area | Area Type | Network / Devices | Main Function |
|---|---|---|---|
| Area 0 | Backbone | R1, R2, R3, R4, R5 | Core transit routing and ABR connectivity |
| Area 1 | Normal | LAN a1 / R6 | Inter-area routing, Router-on-a-Stick, DHCP |
| Area 2 | Stub | LAN a2 / R3, R7, MLS-A, MLS-B | Filtering Type 5 LSAs |
| Area 3 | Totally Stub | LAN a4 / R5, R9 | Filtering Type 3, 4, and 5 LSAs |
| Area 4 | Totally NSSA | LAN a3 / R4 | External route redistribution with NSSA |

**Area 0 – Backbone**
- Provides the central transit routing infrastructure.
- Connects all Area Border Routers (ABRs).

**Area 1 – Normal Area (LAN a1)**
- Full inter-area and external route visibility.
- Router-on-a-Stick implemented on R6.
- Centralized DHCP services.
- VLAN 10: Data.
- VLAN 20: Voice.

**Area 2 – Stub Area (LAN a2)**
- Blocks Type 5 External LSAs.
- Maintains inter-area routing.
- Includes R3, R7, MLS-A, and MLS-B.
- VLAN 30: Data.
- VLAN 40: Voice.

**Area 3 – Totally Stub Area (LAN a4)**
- Configured using `area 3 stub no-summary` on R5.
- Filters Type 3, Type 4, and Type 5 LSAs.
- Relies on an injected default route: `O*IA 0.0.0.0/0`.
- Includes Router-on-a-Stick and DHCP services.
- VLAN 70: Data.
- VLAN 80: Voice.

**Area 4 – Totally NSSA (LAN a3)**
- Configured using `area 4 nssa no-summary` on R4.
- Supports external route redistribution through NSSA mechanisms.
- Optimizes external LSA propagation.
- VLAN 50: Data.
- VLAN 60: Voice.

---

### 2. Multi-Protocol Route Redistribution

The project integrates multiple routing protocols to achieve end-to-end connectivity across different routing domains.

**OSPF ↔ EIGRP (AS 100)**
- Mutual redistribution configured on R8.
- Connects the EIGRP domain through R10.
- Includes Loopback: `10.10.10.10/32`.

**OSPF ↔ RIPv2 & Static Routing**
- Integration between R11, MLS-A, MLS-B, and R8.
- Enables communication across multiple routing domains and campus networks.

Key concepts:
- Route redistribution.
- Administrative Distance.
- EIGRP metric requirements.
- Routing loop prevention.
- End-to-end reachability.

---

## 🔄 Switching, High Availability & VoIP

### 3. First-Hop Redundancy – HSRP

Configured on LAN a2 using two Multilayer Switches:

- **MLS-A:** Active Gateway for VLAN 30.
- **MLS-B:** Active Gateway for VLAN 40.
- HSRP Preemption enabled.
- Per-VLAN load balancing.
- STP Root Bridge tuning to complement gateway distribution.

### 4. Layer 2 Optimization

| Technology | Implementation |
|---|---|
| LACP EtherChannel | Port-channel 1 |
| VTP | Domain: AMRKHALED |
| PVST+ | VLAN-based spanning tree |
| Rapid PVST+ | Faster spanning-tree convergence |
| STP Root Bridge | Per-VLAN root optimization |

### 5. VoIP & Centralized DHCP

- Dedicated Data and Voice VLANs.
- DHCP Option 150 for Cisco IP Phones.
- Centralized DHCP servers.
- DHCP Relay using `ip helper-address`.
- Router-on-a-Stick.
- Separate addressing for Data and Voice networks.

---

## 🛡️ Campus Network Security Hardening

### 6. Network Security Implementation

Security mechanisms are implemented across LAN a4 and selected access-layer ports.

| Security Feature | Purpose |
|---|---|
| DHCP Snooping | Prevent unauthorized DHCP servers |
| Trusted Uplinks | Allow legitimate DHCP server responses |
| Rate Limiting | Control DHCP traffic on access ports |
| Dynamic ARP Inspection (DAI) | Protect against ARP spoofing |
| Port Security | Sticky MAC address learning |
| Maximum MAC | Maximum 2 MAC addresses |
| BPDU Guard | Protect edge ports against unexpected BPDUs |
| BPDU Filter | Control BPDU transmission where configured |
| SSHv2 | Encrypted remote management |
| Local AAA | Local authentication for device management |

---

## 🧪 Verification & Testing

The following Cisco IOS commands can be used to verify the implementation.

### OSPF Verification

```bash
show ip ospf neighbor
show ip ospf database
show ip ospf interface brief
show ip route ospf
show ip protocols
```

### Routing & Redistribution

```bash
show ip route
show ip protocols
show ip eigrp neighbors
show ip rip database
```

### Switching & Redundancy

```bash
show etherchannel summary
show interfaces trunk
show vlan brief
show spanning-tree
show standby brief
```

### Network Security

```bash
show ip dhcp snooping
show ip arp inspection
show port-security
show ip ssh
show running-config
```

### Connectivity Testing

- Inter-VLAN communication.
- Inter-area OSPF connectivity.
- OSPF and EIGRP redistribution.
- OSPF and RIP redistribution.
- Data and Voice VLAN connectivity.
- HSRP Active/Standby gateway failover.
- DHCP address assignment.
- End-to-end connectivity across campus LANs.

---

## 📂 Repository Contents

```text
Enterprise-MultiArea-OSPF/
│
├── Enterprise_MultiArea_OSPF_Final.pkz
│
├── screenshots/
│   ├── topology.png
│   ├── ospf-neighbors.png
│   ├── ospf-routing-table.png
│   ├── totally-stub-verification.png
│   ├── hsrp-status.png
│   ├── etherchannel-status.png
│   └── connectivity-tests.png
│
└── README.md
```

---

## 🎯 Skills Demonstrated

- Advanced Cisco Routing & Switching.
- Multi-Area OSPF Design and Optimization.
- OSPF LSA Types and Area Filtering.
- EIGRP and RIPv2 Configuration.
- Mutual Route Redistribution.
- HSRP and High Availability.
- VLANs, Trunking, and EtherChannel.
- Spanning Tree Optimization.
- DHCP and VoIP Integration.
- Enterprise Network Security.
- Network Troubleshooting and Verification.

---

## 🙏 Special Thanks & Appreciation

A special thank you to **Eng. Saeed** for his continuous guidance, valuable technical insights, and generous support throughout this learning journey.

His mentorship and dedication have played an important role in strengthening my networking knowledge and transforming advanced theoretical concepts into practical implementations.

I sincerely appreciate his efforts and support.

---

## 👨‍💻 Author

**Amr Abdel Khaleq (Amr Khaled)**

Network, Telecommunications & Software Engineer

- GitHub: https://github.com/amr-khaleq
- LinkedIn: https://www.linkedin.com/in/amr-abdelkhaleq/

---

⭐ If you find this project useful, feel free to explore the repository and share your feedback.

**Designed, Configured & Implemented with Cisco Packet Tracer.**
