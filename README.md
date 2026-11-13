# Integrated Enterprise Network Configuration Lab

## Project Overview

This project demonstrates the design, implementation, configuration, and troubleshooting of an integrated enterprise switching network using Cisco Packet Tracer.

The network consists of one multilayer switch and three access switches connected through redundant links. It uses VLANs to segment departments, VTP to distribute VLAN information, LACP EtherChannel to aggregate physical links, SVIs for Inter-VLAN routing, and STP to prevent Layer 2 switching loops.

The project demonstrates how multiple networking technologies work together to provide an organized, scalable, and reliable network infrastructure.

## Learning Objectives

- Design and implement an enterprise network topology.
- Configure VLANs for departmental segmentation.
- Implement VTP Server and Client modes.
- Configure IEEE 802.1Q trunk links.
- Implement LACP EtherChannel between switches.
- Configure SVIs for Inter-VLAN routing.
- Enable Layer 3 routing on a multilayer switch.
- Configure STP and elect a preferred Root Bridge.
- Test EtherChannel redundancy and STP convergence.
- Perform Layer 2 and Layer 3 troubleshooting.

## Network Topology

The network contains four switches:

| Device | Model | Role |
|---|---|---|
| MLS | Cisco 3560 | Multilayer switch, VTP Server and Inter-VLAN routing |
| Green | Cisco 2960 | Access switch for VLAN 10 |
| Yellow | Cisco 2960 | Access switch for VLAN 20 |
| Purple | Cisco 2960 | Access switch for VLAN 30 |

The topology uses multiple physical connections between switches to provide redundancy and support EtherChannel.

## VLAN Configuration

| VLAN ID | VLAN Name | Department | Connected PCs |
|---|---|---|---|
| 10 | GREEN | Sales | PC0, PC1, PC6 |
| 20 | YELLOW | Marketing | PC4, PC5 |
| 30 | PURPLE | IT Support | PC2, PC3 |

## IP Addressing Plan

| PC | Switch | VLAN | IP Address | Subnet Mask | Default Gateway |
|---|---|---:|---|---|---|
| PC0 | Green | 10 | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| PC1 | Green | 10 | 192.168.10.11 | 255.255.255.0 | 192.168.10.1 |
| PC6 | Green | 10 | 192.168.10.12 | 255.255.255.0 | 192.168.10.1 |
| PC4 | Yellow | 20 | 192.168.20.10 | 255.255.255.0 | 192.168.20.1 |
| PC5 | Yellow | 20 | 192.168.20.11 | 255.255.255.0 | 192.168.20.1 |
| PC2 | Purple | 30 | 192.168.30.10 | 255.255.255.0 | 192.168.30.1 |
| PC3 | Purple | 30 | 192.168.30.11 | 255.255.255.0 | 192.168.30.1 |

## VTP Configuration

The multilayer switch operates as the VTP Server, while the three access switches operate as VTP Clients.

| Setting | Configuration |
|---|---|
| VTP Domain | NETWORKLAB |
| VTP Version | Version 2 |
| MLS | Server |
| Green | Client |
| Yellow | Client |
| Purple | Client |

VTP is used to distribute VLAN information from the central multilayer switch to the participating access switches.

## EtherChannel Configuration

LACP EtherChannel is configured to combine multiple physical connections into logical Port-Channel interfaces.

| Connection | Channel Group | Physical Interfaces |
|---|---:|---|
| MLS - Green | 1 | MLS Fa0/1-2, Green Fa0/3-4 |
| Green - Yellow | 2 | Green Fa0/1-2, Yellow Fa0/1-2 |
| Yellow - Purple | 3 | Yellow Fa0/3-4, Purple Fa0/1-2 |
| MLS - Purple | 4 | MLS Fa0/3-4, Purple Fa0/3-4 |

The EtherChannels provide increased aggregate link capacity and redundancy.

## Inter-VLAN Routing Using SVIs

The multilayer switch is configured with Switched Virtual Interfaces (SVIs) to provide default gateways for each VLAN.

| SVI | IP Address | Purpose |
|---|---|---|
| VLAN 10 | 192.168.10.1/24 | Sales Gateway |
| VLAN 20 | 192.168.20.1/24 | Marketing Gateway |
| VLAN 30 | 192.168.30.1/24 | IT Support Gateway |

IPv4 routing is enabled on the multilayer switch to allow communication between the three VLAN networks.

## Spanning Tree Protocol

STP is implemented to prevent Layer 2 switching loops in the redundant network topology.

The multilayer switch is configured as the preferred Root Bridge for VLANs 10, 20 and 30.

STP is investigated to understand:

- Root Bridge election
- Root Ports and Designated Ports
- Alternate and Blocking Ports
- Redundant link behavior
- STP topology changes following link failure

## Implementation Tasks

1. Recreate the enterprise network topology in Cisco Packet Tracer.
2. Configure VLANs 10, 20 and 30.
3. Assign end-device switch ports to the appropriate VLANs.
4. Configure VTP Server and Client modes.
5. Configure trunk links between switches.
6. Implement four LACP EtherChannels.
7. Verify Port-Channel operation and member interfaces.
8. Configure SVIs on the multilayer switch.
9. Enable IPv4 routing.
10. Configure PC IP addresses and default gateways.
11. Configure the multilayer switch as the preferred STP Root Bridge.
12. Test same-VLAN and inter-VLAN communication.
13. Investigate EtherChannel member-link failure and recovery.
14. Investigate STP topology changes and troubleshoot connectivity.

## Verification Commands

### VLAN Verification

```bash
show vlan brief
```

### VTP Verification

```bash
show vtp status
```

### Trunk Verification

```bash
show interfaces trunk
```

### EtherChannel Verification

```bash
show etherchannel summary
```

### SVI and Routing Verification

```bash
show ip interface brief
show ip route
show running-config
```

### STP Verification

```bash
show spanning-tree
show spanning-tree vlan 10
show spanning-tree vlan 20
show spanning-tree vlan 30
```

## Connectivity Testing

The following tests are used to verify network communication:

- Communication between PCs in the same VLAN.
- Communication between PCs in different VLANs.
- Connectivity to the corresponding SVI default gateways.
- Connectivity during EtherChannel member-link failure.
- Connectivity following link restoration and STP convergence.

## Technologies and Concepts

- Cisco Packet Tracer
- Cisco Catalyst 3560 and 2960 Switches
- VLAN Configuration
- VLAN Trunking Protocol (VTP)
- IEEE 802.1Q Trunking
- Link Aggregation Control Protocol (LACP)
- EtherChannel
- Switched Virtual Interfaces (SVIs)
- Inter-VLAN Routing
- Spanning Tree Protocol (STP)
- IPv4 Addressing and Subnetting
- Network Redundancy
- Layer 2 and Layer 3 Troubleshooting

## Key Learning Outcomes

- Understand enterprise network segmentation using VLANs.
- Configure and verify centralized VLAN management using VTP.
- Implement link aggregation using LACP EtherChannel.
- Configure Layer 3 SVIs for Inter-VLAN routing.
- Understand the interaction between EtherChannel and STP.
- Investigate redundant network paths and link failure recovery.
- Develop practical Cisco switching, routing, and troubleshooting skills.
