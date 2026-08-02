# Enterprise Network Design with OSPF, VLAN Segmentation, Router-on-a-Stick, and Standard ACLs

## Project Overview

This project demonstrates the design, implementation, verification, and troubleshooting of a small enterprise network using Cisco Packet Tracer.

The network consists of two routers interconnected through an OSPF backbone, multiple Layer 2 switches, segmented server networks using VLANs, and inter-VLAN routing implemented through Router-on-a-Stick (ROAS).

Standard Access Control Lists (ACLs) were deployed to enforce traffic filtering policies between client and server networks while maintaining full OSPF reachability across the enterprise.

The objective of this project was not only to achieve end-to-end connectivity but also to apply structured network troubleshooting methodologies to identify and resolve Layer 2 and Layer 3 issues encountered during implementation.

# Network Objectives

- Design a multi-router enterprise network.
- Implement dynamic routing using OSPF Area 0.
- Segment the server infrastructure into multiple VLANs.
- Configure Router-on-a-Stick for Inter-VLAN routing.
- Implement IEEE 802.1Q trunking between switches and routers.
- Apply Standard Numbered and Named ACLs to enforce network security policies.
- Verify routing, VLAN communication, and ACL functionality.
- Perform systematic troubleshooting to restore connectivity when failures occur.


# Technologies Used

- Cisco Packet Tracer
- Cisco IOS
- Cisco 2911 Routers
- Cisco Catalyst 2960 Switches
- OSPF (Open Shortest Path First)
- IEEE 802.1Q Trunking
- VLAN Segmentation
- Router-on-a-Stick (ROAS)
- Standard Numbered ACLs
- Standard Named ACLs
- IPv4 Addressing
- Static Default Gateway Configuration
- Network Verification & Troubleshooting

# Network Topology

<img width="893" height="543" alt="image" src="https://github.com/user-attachments/assets/cd29baef-9277-492f-903a-2b027b67013f" />


# Network Architecture

The network consists of two routed domains connected through an OSPF backbone.

The client LANs reside behind Router R1, while Router R2 provides gateway services for multiple server VLANs using Router-on-a-Stick.

Inter-router communication is achieved through OSPF Area 0, allowing dynamic exchange of all client and server networks.

The server infrastructure is logically segmented into multiple VLANs to isolate resources while maintaining controlled inter-network communication.

# VLAN Design

| VLAN | Name | Network      |
|------|------|--------------|
|10    |SRV_1 |192.168.3.0/24|
|20    |SRV_2 |192.168.2.0/24|
|30    |SRV_3 |192.168.1.0/24|
|99    |Native VLAN|Management/Native|

# Routing Design

Dynamic routing is implemented using OSPF Area 0.

Advertised Networks include:

- Client Networks
- Server VLAN Networks
- Inter-router Transit Network

OSPF provides automatic route learning between both routers, eliminating the need for static routes and allowing scalable network expansion.

Verification commands used:

show ip route
show ip ospf neighbour
show ip protocols

# Router-on-a-Stick Implementation

Inter-VLAN routing is implemented using Router-on-a-Stick (ROAS).

Each VLAN is mapped to an individual router subinterface configured with IEEE 802.1Q encapsulation.

Example:

- GigabitEthernet0/1.10 → VLAN 10
- GigabitEthernet0/1.20 → VLAN 20
- GigabitEthernet0/1.30 → VLAN 30

Each subinterface serves as the default gateway for hosts within its corresponding VLAN.

Verification commands:

show ip interface brief
show running-config


# Switching Design

Switches were configured to provide:

- VLAN creation
- Access port assignment
- 802.1Q trunk links
- Native VLAN configuration

Trunk links carry traffic for VLANs 10, 20, 30, and Native VLAN 99 between network devices.

Verification commands:

show vlan brief

show interfaces trunk

show interfaces switchport


# Access Control Lists

Standard Access Control Lists were implemented to enforce access restrictions between client networks and server VLANs.

Policies implemented include:

- Restricting server access to authorized client hosts.
- Preventing unauthorized network communication.
- Applying ACLs outbound on Router-on-a-Stick subinterfaces following Cisco best practices for Standard ACL placement.

Verification:

show access-lists

show running-config

ping

# Verification

The following validation steps were performed after implementation.

~ OSPF adjacency successfully established

~ Dynamic routes successfully learned

~ Router-on-a-Stick operational

~ VLAN segmentation verified

~ Trunk links operational

~ Successful end-to-end connectivity

~ ACL policies validated

**Verification Commands**

show ip route

show ip ospf neighbor

show vlan brief

show interfaces trunk

show access-lists

ping

traceroute

# Troubleshooting

During implementation, end-to-end connectivity between client PCs and server networks initially failed despite correct OSPF configuration and successful route advertisement.

A structured troubleshooting methodology was followed rather than immediately modifying configurations.

The following components were systematically verified:

- OSPF neighbour adjacency
- Routing tables
- Router subinterfaces
- ACL configuration
- Trunk links
- VLAN database
- IP addressing
- Default gateways

The root cause was identified at Layer 2.

The switch interfaces connected to the servers had mistakenly been configured as **trunk ports** instead of **access ports**.

Because end devices do not participate in VLAN trunking under this design, server traffic was not being forwarded within the intended VLANs.

After reconfiguring the server-facing interfaces as access ports and assigning them to their respective VLANs, full end-to-end connectivity was restored.

This project reinforced the importance of verifying Layer 2 connectivity before assuming routing or ACL-related failures.

# Lessons Learned

Through this project, I strengthened practical understanding of:

- OSPF neighbour formation
- Dynamic routing verification
- Router-on-a-Stick deployment
- IEEE 802.1Q encapsulation
- VLAN segmentation
- Standard ACL placement
- Layer 2 versus Layer 3 troubleshooting
- Cisco IOS verification commands
- Structured fault isolation methodology

More importantly, this project reinforced the value of systematic troubleshooting rather than relying on assumptions when diagnosing network failures.

# Repository Contents

├── PacketTracer/
│   └── Enterprise_Network.pkt
│
├── Configurations/
│   ├── R1.txt
│   ├── R2.txt
│   ├── SW1.txt
│   └── SW2.txt
│
├── Topology/
│   └── topology.png
│
├── Verification/
│   ├── ospf-neighbor.png
│   ├── routing-table.png
│   ├── vlan-brief.png
│   ├── trunk-status.png
│   └── connectivity-tests.png
│
└── README.md

# Author - **Ayomide Oyekunle**

**Ayomide Oyekunle**

Computer Science Student | Aspiring Network Engineer

This project is part of my CCNA portfolio and documents the practical implementation of enterprise networking concepts using Cisco technologies.
