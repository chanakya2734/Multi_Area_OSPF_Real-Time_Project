# Multi_Area_OSPF_Real-Time_Project

## Project Overview

This project demonstrates the design and implementation of a Multi-Area Open Shortest Path First (OSPF) network using the GNS3 network simulation platform. The project focuses on configuring OSPF Backbone Area (Area 0), Standard Area (Area 18), NSSA Area (Area 20), route redistribution, DHCP services, and verifying end-to-end connectivity across multiple network segments.

The network consists of multiple Cisco routers interconnected through various OSPF areas, an external autonomous system, DHCP services, and end-user hosts.

---

## Objectives

- Configure and implement Multi-Area OSPF routing.
- Configure OSPF Backbone Area (Area 0).
- Configure OSPF Standard Area.
- Configure OSPF NSSA Area.
- Implement route redistribution between OSPF and external networks.
- Configure DHCP services for end-user devices.
- Verify routing tables and OSPF neighbor relationships.
- Perform end-to-end connectivity testing using Ping and Traceroute.
- Understand hierarchical OSPF network architecture.

---

## Technologies Used

- GNS3
- Cisco IOS Routers
- OSPF
- Multi-Area OSPF
- NSSA
- Route Redistribution
- DHCP
- VPCS
- Ethernet Switch
- ICMP
- Traceroute
- Solar-PuTTY

---

## Network Topology

Topology image is available in:

```
topology/Multi_Area_OSPF_Real-Time_Project_Topology.png
```

---

## Network Architecture

The network consists of:

- R1 configured as Area 0 Backbone Router and ASBR.
- R2 configured as Area 0 Router and ABR.
- R3 configured as Area 0 Router and ABR.
- R4 configured as Area 18 Router.
- R5 configured as Area 18 Router and DHCP Server.
- R6 configured as NSSA Area Router.
- R7 configured as NSSA Area Border Router.
- R8 configured as External Autonomous System Router.
- R9 configured as Remote Network Router.
- PC1 configured as DHCP Client.
- PC2 configured as End User Host.
- Switch1 providing Layer-2 connectivity.

---

## OSPF Area Design

| Area | Description |
|------|-------------|
| Area 0 | Backbone Area |
| Area 18 | Standard Area |
| Area 20 | NSSA Area |

---

## IP Addressing

### Backbone Area

| Link | Network |
|------|---------|
| R1-R2 | 192.168.12.0/24 |
| R1-R3 | 192.168.13.0/24 |
| R2-R3 | 192.168.23.0/24 |

### Area 18

| Link | Network |
|------|---------|
| R2-R4 | 192.168.24.0/24 |
| R4-R5 | 192.168.45.0/24 |
| LAN | 192.168.1.0/24 |

### NSSA Area

| Link | Network |
|------|---------|
| R3-R6 | 192.168.36.0/24 |
| R6-R7 | 192.168.67.0/24 |
| R7-R9 | 192.168.79.0/24 |

### External Network

| Link | Network |
|------|---------|
| R1-R8 | 192.168.18.0/24 |

---

## Loopback Addressing

| Router | Loopback Address |
|---------|-----------------|
| R1 | 1.1.1.1 |
| R2 | 2.2.2.2 |
| R3 | 3.3.3.3 |
| R4 | 4.4.4.4 |
| R5 | 5.5.5.5 |
| R6 | 6.6.6.6 |
| R7 | 7.7.7.7 |
| R8 | 8.8.8.8 |
| R9 | 9.9.9.9 |

---

## OSPF Configuration

### Backbone Area (Area 0)

Configured OSPF Area 0 on:

- R1
- R2
- R3

Verification performed using:

```bash
show ip ospf neighbor
show ip route
show ip protocols
```

---

### Standard Area Configuration (Area 18)

Configured OSPF Area 18 on:

- R4
- R5

Verification performed using:

```bash
show ip ospf neighbor
show ip route
```

---

### NSSA Configuration (Area 20)

Configured OSPF NSSA Area on:

- R6
- R7

Verification performed using:

```bash
show ip ospf neighbor
show ip route
```

---

## Route Redistribution

Configured redistribution between OSPF and external networks.

### Router: R1

```bash
router ospf 110
 redistribute bgp 100 subnets
```

Verification performed using:

```bash
show ip route
show running-config | section ospf
```

---

## DHCP Server Configuration

### Router: R5

Configured R5 as DHCP Server using:

```bash
ip dhcp pool SBI-BANK
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.100
 dns-server 192.168.1.101 192.168.1.102
```

Verification performed using:

```bash
show ip dhcp binding
show ip dhcp pool
```

---

## Verification

### Router Verification

Routing tables were verified on:

- R1
- R2
- R3
- R5
- R6
- R7

Verification performed using:

```bash
show ip route
show running-config | section ospf
```

---

## End-to-End Connectivity Verification

### PC1 Verification

Verified using:

```bash
ping 8.8.8.8
trace 8.8.8.8
```

Successful communication verified.

### OSPF Route Verification

Verified:

- Intra-area routes
- Inter-area routes
- NSSA routes
- External routes
- Redistributed routes

---

## Screenshots

Available in the screenshots folder:

```
OSPF_R1_Routes.png
OSPF_R2_Routes.png
 OSPF_R3_Routes.png
OSPF_R4_Routes.png
OSPF_R5_Routes.png
OSPF_R6_Routes.png
OSPF_R7_Routes.png
OSPF_R8_Routes.png
OSPF_R9_Routes.png
OSPF_PC1TOR8_Ping_Trace.png

```

---

## Project Structure

```text
Multi_Area_OSPF_Real-Time_Project

├── README.md

├── topology
│   └── Multi_Area_OSPF_Topology.png

├── screenshots
│   ├── OSPF_R1_Routes.png
│   ├── OSPF_R2_Routes.png
│   ├── OSPF_R3_Routes.png
│   ├── OSPF_R4_Routes.png
│   ├── OSPF_R5_Routes.png
│   ├── OSPF_R6_Routes.png
│   ├── OSPF_R7_Routes.png
│   ├── OSPF_R8_Routes.png
│   ├── OSPF_R9_Routes.png
│   └── OSPF_PC1TOR8_Ping_Trace.png

├── configurations
│   ├── R1_OSPF_Backbone_Configuration.txt
│   ├── R2_OSPF_Backbone_Configuration.txt
│   ├── R3_OSPF_ABR_Configuration.txt
│   ├── R4_OSPF_Area18_Configuration.txt
│   ├── R5_OSPF_DHCP_Server_Configuration.txt
│   ├── R6_OSPF_NSSA_Configuration.txt
│   ├── R7_NSSA_ABR_Configuration.txt
│   ├── R8_BGP_Redistribution_Configuration.txt
│   └── R9_External_Network_Configuration.txt

└── project_file
    └── Multi_Area_OSPF_Real-Time_Project.gns3
```

---

## Learning Outcomes

- Multi-Area OSPF Configuration
- OSPF Backbone Area Design
- OSPF Standard Area Configuration
- OSPF NSSA Configuration
- Route Redistribution
- ASBR and ABR Concepts
- DHCP Configuration
- Routing Table Analysis
- Network Troubleshooting
- Ping and Traceroute Verification
- Cisco Router Configuration
- GNS3 Network Simulation

---

## Author

**Chanakya Burugu**

Computer Science and Engineering (Networks)

Networking and Infrastructure Enthusiast
