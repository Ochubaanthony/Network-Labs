# GNS3 Lab: OSPF Routing Between Two Cisco Routers

## Overview

A two-router GNS3 lab demonstrating OSPF neighbor adjacency over a point-to-point IPv4 network. The lab uses OSPF Area 0 and a /30 subnet.

## Topology

![GNS3 OSPF topology](topology/ospf-topology.png)

## Addressing

| Router | Interface | IPv4 address | Subnet mask |
|---|---|---|---|
| R1 | Ethernet0/0 | 192.168.10.1/30 | 255.255.255.252 |
| R2 | Ethernet0/0 | 192.168.10.2/30 | 255.255.255.252 |

Network: `192.168.10.0/30`  
Wildcard mask: `0.0.0.3`  
OSPF area: `0`

## Requirements

- GNS3
- Cisco IOS router images that you are licensed to use
- Two router nodes with an Ethernet0/0 interface

## Configuration

See [`configurations/R1-config.txt`](configurations/R1-config.txt) and [`configurations/R2-config.txt`](configurations/R2-config.txt).

## Verification

Run these commands on both routers:

```cisco
show ip interface brief
show ip ospf neighbor
show ip ospf
show ip route ospf
```

Expected result: the Ethernet interfaces are up/up and the routers form an OSPF adjacency in the FULL state. The OSPF process IDs (1 on R1 and 2 on R2) do not need to match; the router IDs must be unique.

## Test status

Configured and tested successfully in GNS3 by the author.

## Project files

Add the exported `.gns3` project and its required supporting files in `gns3-project/` if you want others to open the lab directly. Do not include Cisco IOS images; they are subject to licensing restrictions.
