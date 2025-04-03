# FABRIC

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| FABRIC | media_leaf | C160064-001B101A | 10.176.142.83/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-001B201A | 10.176.142.84/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-002B101A | 10.176.142.102/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-002B201A | 10.176.142.103/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-003B101A | 10.176.136.154/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-003B201A | 10.176.136.155/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-004B101A | 10.176.136.185/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-004B201A | 10.176.136.186/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-005B101A | 10.176.136.218/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-005B201A | 10.176.136.219/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-006B101A | 10.176.136.250/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-006B201A | 10.176.136.251/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-007B101A | 10.176.137.26/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-007B201A | 10.176.137.27/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-008B101A | 10.176.137.58/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-008B201A | 10.176.137.59/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-009B101A | 10.176.137.90/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-009B201A | 10.176.137.91/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-010B101A | 10.176.137.122/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-010B201A | 10.176.137.123/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-013B101A | 10.176.142.116/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-013B102A | 10.176.142.133/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-013B201A | 10.176.142.117/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-013B202A | 10.176.142.134/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-014B101A | 10.176.142.148/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-014B102A | 10.176.142.164/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-014B201A | 10.176.142.149/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-014B202A | 10.176.142.165/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-015B101A | 10.176.142.187/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-015B102A | 10.176.142.189/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-015B103A | 10.176.142.191/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-015B201A | 10.176.142.188/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-015B202A | 10.176.142.190/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-015B203A | 10.176.142.192/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-016B101A | 10.176.142.215/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-016B102A | 10.176.142.231/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-016B201A | 10.176.142.216/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-016B202A | 10.176.142.232/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-017B101A | 10.176.142.248/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-017B201A | 10.176.142.249/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_spine | C160064-037B100A | 10.176.143.139/27 | 7808R3 | Provisioned | HNN23076021 |
| FABRIC | media_leaf | C160064-037B101A | 10.176.143.141/27 | 7289R3A | Provisioned | JPA2423A0HM |
| FABRIC | media_leaf | C160064-037B102A | 10.176.143.170/27 | 7289R3A | Provisioned | JPA2403A1WC |
| FABRIC | media_leaf | C160064-037B103A | 10.166.80.10/27 | 7289R3A | Provisioned | JPA2401A3GM |
| FABRIC | media_leaf | C160064-037B104A | 10.166.80.44/27 | 7289R3A | Provisioned | JPA2401A3W6 |
| FABRIC | media_leaf | C160064-037B105A | 10.166.80.6/27 | 7280SR3 | Provisioned | JPA2416P3JC |
| FABRIC | media_leaf | C160064-037B106A | 10.166.80.40/27 | 7280SR3 | Provisioned | JPA2416P1VH |
| FABRIC | media_spine | C160064-037B200A | 10.176.143.168/27 | 7808R3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-037B201A | 10.176.143.143/27 | 7289R3A | Provisioned | JPA2423A0HG |
| FABRIC | media_leaf | C160064-037B202A | 10.176.143.172/27 | 7289R3A | Provisioned | JPA2401A3W3 |
| FABRIC | media_leaf | C160064-037B203A | 10.166.80.12/27 | 7289R3A | Provisioned | JPA2402A092 |
| FABRIC | media_leaf | C160064-037B204A | 10.166.80.46/27 | 7289R3A | Provisioned | JPA2401A3W5 |
| FABRIC | media_leaf | C160064-037B205A | 10.166.80.7/27 | 7280SR3 | Provisioned | JPA2416P3K9 |
| FABRIC | media_leaf | C160064-037B206A | 10.166.80.41/27 | 7280SR3 | Provisioned | JPA2416P3GF |
| FABRIC | ptp_leaf | C160064-037B370A | 10.176.143.137/27 | 7280SR3 | Provisioned | JPA2416P3HN |
| FABRIC | ptp_leaf | C160064-037B371A | 10.176.143.166/27 | 7280SR3 | Provisioned | JPA2416P3JA |
| FABRIC | border_leaf | C160064-037B380A | 10.176.143.138/27 | 7280CR3 | Provisioned | JPA2409P23Z |
| FABRIC | border_leaf | C160064-037B381A | 10.176.143.167/27 | 7280CR3 | Provisioned | JPA2409P250 |
| FABRIC | media_leaf | C160064-046B101A | 10.176.141.119/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-046B201A | 10.176.141.120/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-049B101A | 10.176.141.167/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-049B201A | 10.176.141.168/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-050B101A | 10.176.143.86/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-050B201A | 10.176.143.87/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-051B101A | 10.176.143.100/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-051B102A | 10.176.143.118/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-051B201A | 10.176.143.101/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-051B202A | 10.176.143.119/28 | 7289R3A | Provisioned | NA |
| FABRIC | media_leaf | C160064-056B101A | 10.176.142.21/28 | 7280SR3 | Provisioned | NA |
| FABRIC | media_leaf | C160064-056B201A | 10.176.142.22/28 | 7280SR3 | Provisioned | NA |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| media_leaf | C160064-001B101A | Ethernet2/1/1 | media_spine | C160064-037B100A | Ethernet6/23/1 |
| media_leaf | C160064-001B101A | Ethernet2/2/1 | media_spine | C160064-037B100A | Ethernet7/23/1 |
| media_leaf | C160064-001B201A | Ethernet2/1/1 | media_spine | C160064-037B200A | Ethernet6/23/1 |
| media_leaf | C160064-001B201A | Ethernet2/2/1 | media_spine | C160064-037B200A | Ethernet7/23/1 |
| media_leaf | C160064-002B101A | Ethernet2/1/1 | media_spine | C160064-037B100A | Ethernet6/21/1 |
| media_leaf | C160064-002B101A | Ethernet2/2/1 | media_spine | C160064-037B100A | Ethernet7/21/1 |
| media_leaf | C160064-002B101A | Ethernet2/3/1 | media_spine | C160064-037B100A | Ethernet6/22/1 |
| media_leaf | C160064-002B101A | Ethernet2/4/1 | media_spine | C160064-037B100A | Ethernet7/22/1 |
| media_leaf | C160064-002B101A | Ethernet3/1/1 | media_spine | C160064-037B100A | Ethernet6/24/1 |
| media_leaf | C160064-002B201A | Ethernet2/1/1 | media_spine | C160064-037B200A | Ethernet6/21/1 |
| media_leaf | C160064-002B201A | Ethernet2/2/1 | media_spine | C160064-037B200A | Ethernet7/21/1 |
| media_leaf | C160064-002B201A | Ethernet2/3/1 | media_spine | C160064-037B200A | Ethernet6/22/1 |
| media_leaf | C160064-002B201A | Ethernet2/4/1 | media_spine | C160064-037B200A | Ethernet7/22/1 |
| media_leaf | C160064-002B201A | Ethernet3/1/1 | media_spine | C160064-037B200A | Ethernet6/24/1 |
| media_leaf | C160064-003B101A | Ethernet2/1/1 | media_spine | C160064-037B100A | Ethernet6/20/1 |
| media_leaf | C160064-003B101A | Ethernet2/2/1 | media_spine | C160064-037B100A | Ethernet7/20/1 |
| media_leaf | C160064-003B201A | Ethernet2/1/1 | media_spine | C160064-037B200A | Ethernet6/20/1 |
| media_leaf | C160064-003B201A | Ethernet2/2/1 | media_spine | C160064-037B200A | Ethernet7/20/1 |
| media_leaf | C160064-004B101A | Ethernet53/1 | media_spine | C160064-037B100A | Ethernet3/33/1 |
| media_leaf | C160064-004B101A | Ethernet54/1 | media_spine | C160064-037B100A | Ethernet4/32/4 |
| media_leaf | C160064-004B101A | Ethernet55/1 | media_spine | C160064-037B100A | Ethernet5/33/4 |
| media_leaf | C160064-004B101A | Ethernet56/1 | media_spine | C160064-037B100A | Ethernet3/32/4 |
| media_leaf | C160064-004B201A | Ethernet53/1 | media_spine | C160064-037B200A | Ethernet3/33/1 |
| media_leaf | C160064-004B201A | Ethernet54/1 | media_spine | C160064-037B200A | Ethernet4/32/4 |
| media_leaf | C160064-004B201A | Ethernet55/1 | media_spine | C160064-037B200A | Ethernet5/33/4 |
| media_leaf | C160064-004B201A | Ethernet56/1 | media_spine | C160064-037B200A | Ethernet3/32/4 |
| media_leaf | C160064-005B101A | Ethernet2/1/1 | media_spine | C160064-037B100A | Ethernet6/19/1 |
| media_leaf | C160064-005B101A | Ethernet2/2/1 | media_spine | C160064-037B100A | Ethernet7/19/1 |
| media_leaf | C160064-005B201A | Ethernet2/1/1 | media_spine | C160064-037B200A | Ethernet6/19/1 |
| media_leaf | C160064-005B201A | Ethernet2/2/1 | media_spine | C160064-037B200A | Ethernet7/19/1 |
| media_leaf | C160064-006B101A | Ethernet53/1 | media_spine | C160064-037B100A | Ethernet5/34/2 |
| media_leaf | C160064-006B101A | Ethernet54/1 | media_spine | C160064-037B100A | Ethernet3/33/2 |
| media_leaf | C160064-006B101A | Ethernet55/1 | media_spine | C160064-037B100A | Ethernet4/33/1 |
| media_leaf | C160064-006B101A | Ethernet56/1 | media_spine | C160064-037B100A | Ethernet5/34/1 |
| media_leaf | C160064-006B201A | Ethernet53/1 | media_spine | C160064-037B200A | Ethernet5/34/2 |
| media_leaf | C160064-006B201A | Ethernet54/1 | media_spine | C160064-037B200A | Ethernet3/33/2 |
| media_leaf | C160064-006B201A | Ethernet55/1 | media_spine | C160064-037B200A | Ethernet4/33/1 |
| media_leaf | C160064-006B201A | Ethernet56/1 | media_spine | C160064-037B200A | Ethernet5/34/1 |
| media_leaf | C160064-007B101A | Ethernet2/1/1 | media_spine | C160064-037B100A | Ethernet6/18/1 |
| media_leaf | C160064-007B101A | Ethernet2/2/1 | media_spine | C160064-037B100A | Ethernet7/18/1 |
| media_leaf | C160064-007B201A | Ethernet2/1/1 | media_spine | C160064-037B200A | Ethernet6/18/1 |
| media_leaf | C160064-007B201A | Ethernet2/2/1 | media_spine | C160064-037B200A | Ethernet7/18/1 |
| media_leaf | C160064-008B101A | Ethernet53/1 | media_spine | C160064-037B100A | Ethernet4/33/3 |
| media_leaf | C160064-008B101A | Ethernet54/1 | media_spine | C160064-037B100A | Ethernet5/34/3 |
| media_leaf | C160064-008B101A | Ethernet55/1 | media_spine | C160064-037B100A | Ethernet3/33/3 |
| media_leaf | C160064-008B101A | Ethernet56/1 | media_spine | C160064-037B100A | Ethernet4/33/2 |
| media_leaf | C160064-008B201A | Ethernet53/1 | media_spine | C160064-037B200A | Ethernet4/33/3 |
| media_leaf | C160064-008B201A | Ethernet54/1 | media_spine | C160064-037B200A | Ethernet5/34/3 |
| media_leaf | C160064-008B201A | Ethernet55/1 | media_spine | C160064-037B200A | Ethernet3/33/3 |
| media_leaf | C160064-008B201A | Ethernet56/1 | media_spine | C160064-037B200A | Ethernet4/33/2 |
| media_leaf | C160064-009B101A | Ethernet2/1/1 | media_spine | C160064-037B100A | Ethernet6/17/1 |
| media_leaf | C160064-009B101A | Ethernet2/2/1 | media_spine | C160064-037B100A | Ethernet7/17/1 |
| media_leaf | C160064-009B201A | Ethernet2/1/1 | media_spine | C160064-037B200A | Ethernet6/17/1 |
| media_leaf | C160064-009B201A | Ethernet2/2/1 | media_spine | C160064-037B200A | Ethernet7/17/1 |
| media_leaf | C160064-010B101A | Ethernet53/1 | media_spine | C160064-037B100A | Ethernet3/34/4 |
| media_leaf | C160064-010B101A | Ethernet54/1 | media_spine | C160064-037B100A | Ethernet4/33/4 |
| media_leaf | C160064-010B101A | Ethernet55/1 | media_spine | C160064-037B100A | Ethernet5/34/4 |
| media_leaf | C160064-010B101A | Ethernet56/1 | media_spine | C160064-037B100A | Ethernet3/34/3 |
| media_leaf | C160064-010B201A | Ethernet53/1 | media_spine | C160064-037B200A | Ethernet3/34/4 |
| media_leaf | C160064-010B201A | Ethernet54/1 | media_spine | C160064-037B200A | Ethernet4/33/4 |
| media_leaf | C160064-010B201A | Ethernet55/1 | media_spine | C160064-037B200A | Ethernet5/34/4 |
| media_leaf | C160064-010B201A | Ethernet56/1 | media_spine | C160064-037B200A | Ethernet3/34/3 |
| media_leaf | C160064-013B101A | Ethernet55/1 | media_spine | C160064-037B100A | Ethernet4/35/1 |
| media_leaf | C160064-013B101A | Ethernet56/1 | media_spine | C160064-037B100A | Ethernet5/35/1 |
| media_leaf | C160064-013B102A | Ethernet2/1/1 | media_spine | C160064-037B100A | Ethernet6/16/1 |
| media_leaf | C160064-013B102A | Ethernet2/2/1 | media_spine | C160064-037B100A | Ethernet7/16/1 |
| media_leaf | C160064-013B201A | Ethernet55/1 | media_spine | C160064-037B200A | Ethernet4/35/1 |
| media_leaf | C160064-013B201A | Ethernet56/1 | media_spine | C160064-037B200A | Ethernet5/35/1 |
| media_leaf | C160064-013B202A | Ethernet2/1/1 | media_spine | C160064-037B200A | Ethernet6/16/1 |
| media_leaf | C160064-013B202A | Ethernet2/2/1 | media_spine | C160064-037B200A | Ethernet7/16/1 |
| media_leaf | C160064-014B101A | Ethernet55/1 | media_spine | C160064-037B100A | Ethernet5/35/2 |
| media_leaf | C160064-014B101A | Ethernet56/1 | media_spine | C160064-037B100A | Ethernet3/35/1 |
| media_leaf | C160064-014B102A | Ethernet53/1 | media_spine | C160064-037B100A | Ethernet4/35/3 |
| media_leaf | C160064-014B102A | Ethernet54/1 | media_spine | C160064-037B100A | Ethernet5/35/3 |
| media_leaf | C160064-014B102A | Ethernet55/1 | media_spine | C160064-037B100A | Ethernet3/35/2 |
| media_leaf | C160064-014B102A | Ethernet56/1 | media_spine | C160064-037B100A | Ethernet4/35/2 |
| media_leaf | C160064-014B201A | Ethernet55/1 | media_spine | C160064-037B200A | Ethernet5/35/2 |
| media_leaf | C160064-014B201A | Ethernet56/1 | media_spine | C160064-037B200A | Ethernet3/35/1 |
| media_leaf | C160064-014B202A | Ethernet53/1 | media_spine | C160064-037B200A | Ethernet4/35/3 |
| media_leaf | C160064-014B202A | Ethernet54/1 | media_spine | C160064-037B200A | Ethernet5/35/3 |
| media_leaf | C160064-014B202A | Ethernet55/1 | media_spine | C160064-037B200A | Ethernet3/35/2 |
| media_leaf | C160064-014B202A | Ethernet56/1 | media_spine | C160064-037B200A | Ethernet4/35/2 |
| media_leaf | C160064-015B101A | Ethernet55/1 | media_spine | C160064-037B100A | Ethernet3/36/1 |
| media_leaf | C160064-015B101A | Ethernet56/1 | media_spine | C160064-037B100A | Ethernet4/36/1 |
| media_leaf | C160064-015B102A | Ethernet54/1 | media_spine | C160064-037B100A | Ethernet5/36/1 |
| media_leaf | C160064-015B102A | Ethernet55/1 | media_spine | C160064-037B100A | Ethernet3/35/4 |
| media_leaf | C160064-015B102A | Ethernet56/1 | media_spine | C160064-037B100A | Ethernet4/35/4 |
| media_leaf | C160064-015B103A | Ethernet55/1 | media_spine | C160064-037B100A | Ethernet5/35/4 |
| media_leaf | C160064-015B103A | Ethernet56/1 | media_spine | C160064-037B100A | Ethernet3/35/3 |
| media_leaf | C160064-015B201A | Ethernet55/1 | media_spine | C160064-037B200A | Ethernet3/36/1 |
| media_leaf | C160064-015B201A | Ethernet56/1 | media_spine | C160064-037B200A | Ethernet4/36/1 |
| media_leaf | C160064-015B202A | Ethernet54/1 | media_spine | C160064-037B200A | Ethernet5/36/1 |
| media_leaf | C160064-015B202A | Ethernet55/1 | media_spine | C160064-037B200A | Ethernet3/35/4 |
| media_leaf | C160064-015B202A | Ethernet56/1 | media_spine | C160064-037B200A | Ethernet4/35/4 |
| media_leaf | C160064-015B203A | Ethernet55/1 | media_spine | C160064-037B200A | Ethernet5/35/4 |
| media_leaf | C160064-015B203A | Ethernet56/1 | media_spine | C160064-037B200A | Ethernet3/35/3 |
| media_leaf | C160064-016B101A | Ethernet2/1/1 | media_spine | C160064-037B100A | Ethernet6/15/1 |
| media_leaf | C160064-016B101A | Ethernet2/2/1 | media_spine | C160064-037B100A | Ethernet7/15/1 |
| media_leaf | C160064-016B102A | Ethernet2/1/1 | media_spine | C160064-037B100A | Ethernet6/14/1 |
| media_leaf | C160064-016B102A | Ethernet2/2/1 | media_spine | C160064-037B100A | Ethernet7/14/1 |
| media_leaf | C160064-016B201A | Ethernet2/1/1 | media_spine | C160064-037B200A | Ethernet6/15/1 |
| media_leaf | C160064-016B201A | Ethernet2/2/1 | media_spine | C160064-037B200A | Ethernet7/15/1 |
| media_leaf | C160064-016B202A | Ethernet2/1/1 | media_spine | C160064-037B200A | Ethernet6/14/1 |
| media_leaf | C160064-016B202A | Ethernet2/2/1 | media_spine | C160064-037B200A | Ethernet7/14/1 |
| media_leaf | C160064-017B101A | Ethernet54/1 | media_spine | C160064-037B100A | Ethernet4/36/2 |
| media_leaf | C160064-017B101A | Ethernet55/1 | media_spine | C160064-037B100A | Ethernet5/36/2 |
| media_leaf | C160064-017B201A | Ethernet54/1 | media_spine | C160064-037B200A | Ethernet4/36/2 |
| media_leaf | C160064-017B201A | Ethernet55/1 | media_spine | C160064-037B200A | Ethernet5/36/2 |
| media_spine | C160064-037B100A | Ethernet3/31/4 | media_leaf | C160064-037B106A | Ethernet56/1 |
| media_spine | C160064-037B100A | Ethernet3/32/2 | media_leaf | C160064-037B105A | Ethernet55/1 |
| media_spine | C160064-037B100A | Ethernet3/32/3 | media_leaf | C160064-037B106A | Ethernet54/1 |
| media_spine | C160064-037B100A | Ethernet3/36/2 | media_leaf | C160064-046B101A | Ethernet55/1 |
| media_spine | C160064-037B100A | Ethernet3/36/3 | media_leaf | C160064-051B101A | Ethernet54/1 |
| media_spine | C160064-037B100A | Ethernet3/36/4 | media_leaf | C160064-056B101A | Ethernet54/1 |
| media_spine | C160064-037B100A | Ethernet4/32/2 | media_leaf | C160064-037B105A | Ethernet56/1 |
| media_spine | C160064-037B100A | Ethernet4/32/3 | media_leaf | C160064-037B106A | Ethernet55/1 |
| media_spine | C160064-037B100A | Ethernet4/36/3 | media_leaf | C160064-051B101A | Ethernet55/1 |
| media_spine | C160064-037B100A | Ethernet4/36/4 | media_leaf | C160064-056B101A | Ethernet55/1 |
| media_spine | C160064-037B100A | Ethernet5/33/3 | media_leaf | C160064-037B106A | Ethernet53/1 |
| media_spine | C160064-037B100A | Ethernet5/36/3 | media_leaf | C160064-046B101A | Ethernet54/1 |
| media_spine | C160064-037B100A | Ethernet5/36/4 | media_leaf | C160064-056B101A | Ethernet56/1 |
| media_spine | C160064-037B100A | Ethernet6/1/1 | media_leaf | C160064-037B101A | Ethernet2/1/1 |
| media_spine | C160064-037B100A | Ethernet6/2/1 | media_leaf | C160064-037B101A | Ethernet2/3/1 |
| media_spine | C160064-037B100A | Ethernet6/3/1 | media_leaf | C160064-037B101A | Ethernet3/1/1 |
| media_spine | C160064-037B100A | Ethernet6/4/1 | media_leaf | C160064-037B102A | Ethernet2/1/1 |
| media_spine | C160064-037B100A | Ethernet6/5/1 | media_leaf | C160064-037B102A | Ethernet2/3/1 |
| media_spine | C160064-037B100A | Ethernet6/6/1 | media_leaf | C160064-037B102A | Ethernet3/1/1 |
| media_spine | C160064-037B100A | Ethernet6/7/1 | media_leaf | C160064-037B103A | Ethernet2/1/1 |
| media_spine | C160064-037B100A | Ethernet6/8/1 | media_leaf | C160064-037B103A | Ethernet2/3/1 |
| media_spine | C160064-037B100A | Ethernet6/9/1 | media_leaf | C160064-037B104A | Ethernet2/2/1 |
| media_spine | C160064-037B100A | Ethernet6/11/1 | media_leaf | C160064-051B102A | Ethernet2/1/1 |
| media_spine | C160064-037B100A | Ethernet6/12/1 | media_leaf | C160064-050B101A | Ethernet2/1/1 |
| media_spine | C160064-037B100A | Ethernet6/28/1 | media_leaf | C160064-049B101A | Ethernet2/1/1 |
| media_spine | C160064-037B100A | Ethernet7/1/1 | media_leaf | C160064-037B101A | Ethernet2/2/1 |
| media_spine | C160064-037B100A | Ethernet7/2/1 | media_leaf | C160064-037B101A | Ethernet2/4/1 |
| media_spine | C160064-037B100A | Ethernet7/3/1 | media_leaf | C160064-037B101A | Ethernet3/2/1 |
| media_spine | C160064-037B100A | Ethernet7/4/1 | media_leaf | C160064-037B102A | Ethernet2/2/1 |
| media_spine | C160064-037B100A | Ethernet7/5/1 | media_leaf | C160064-037B102A | Ethernet2/4/1 |
| media_spine | C160064-037B100A | Ethernet7/6/1 | media_leaf | C160064-037B102A | Ethernet3/2/1 |
| media_spine | C160064-037B100A | Ethernet7/7/1 | media_leaf | C160064-037B103A | Ethernet2/2/1 |
| media_spine | C160064-037B100A | Ethernet7/8/1 | media_leaf | C160064-037B104A | Ethernet2/1/1 |
| media_spine | C160064-037B100A | Ethernet7/9/1 | media_leaf | C160064-037B104A | Ethernet2/3/1 |
| media_spine | C160064-037B100A | Ethernet7/11/1 | media_leaf | C160064-051B102A | Ethernet2/2/1 |
| media_spine | C160064-037B100A | Ethernet7/12/1 | media_leaf | C160064-050B101A | Ethernet2/2/1 |
| media_spine | C160064-037B100A | Ethernet7/24/1 | media_leaf | C160064-051B102A | Ethernet2/3/1 |
| media_spine | C160064-037B100A | Ethernet7/28/1 | media_leaf | C160064-049B101A | Ethernet2/2/1 |
| media_spine | C160064-037B100A | Ethernet8/10/1 | border_leaf | C160064-037B380A | Ethernet33/1 |
| media_spine | C160064-037B100A | Ethernet8/12/1 | border_leaf | C160064-037B381A | Ethernet33/1 |
| media_spine | C160064-037B100A | Ethernet9/12/1 | ptp_leaf | C160064-037B370A | Ethernet33/1 |
| media_spine | C160064-037B100A | Ethernet9/13/1 | ptp_leaf | C160064-037B371A | Ethernet33/1 |
| media_spine | C160064-037B200A | Ethernet3/31/4 | media_leaf | C160064-037B206A | Ethernet56/1 |
| media_spine | C160064-037B200A | Ethernet3/32/2 | media_leaf | C160064-037B205A | Ethernet55/1 |
| media_spine | C160064-037B200A | Ethernet3/32/3 | media_leaf | C160064-037B206A | Ethernet54/1 |
| media_spine | C160064-037B200A | Ethernet3/36/2 | media_leaf | C160064-046B201A | Ethernet55/1 |
| media_spine | C160064-037B200A | Ethernet3/36/3 | media_leaf | C160064-051B201A | Ethernet54/1 |
| media_spine | C160064-037B200A | Ethernet3/36/4 | media_leaf | C160064-056B201A | Ethernet54/1 |
| media_spine | C160064-037B200A | Ethernet4/32/2 | media_leaf | C160064-037B205A | Ethernet56/1 |
| media_spine | C160064-037B200A | Ethernet4/32/3 | media_leaf | C160064-037B206A | Ethernet55/1 |
| media_spine | C160064-037B200A | Ethernet4/36/3 | media_leaf | C160064-051B201A | Ethernet55/1 |
| media_spine | C160064-037B200A | Ethernet4/36/4 | media_leaf | C160064-056B201A | Ethernet55/1 |
| media_spine | C160064-037B200A | Ethernet5/33/3 | media_leaf | C160064-037B206A | Ethernet53/1 |
| media_spine | C160064-037B200A | Ethernet5/36/3 | media_leaf | C160064-046B201A | Ethernet54/1 |
| media_spine | C160064-037B200A | Ethernet5/36/4 | media_leaf | C160064-056B201A | Ethernet56/1 |
| media_spine | C160064-037B200A | Ethernet6/1/1 | media_leaf | C160064-037B201A | Ethernet2/1/1 |
| media_spine | C160064-037B200A | Ethernet6/2/1 | media_leaf | C160064-037B201A | Ethernet2/3/1 |
| media_spine | C160064-037B200A | Ethernet6/3/1 | media_leaf | C160064-037B201A | Ethernet3/1/1 |
| media_spine | C160064-037B200A | Ethernet6/4/1 | media_leaf | C160064-037B202A | Ethernet2/1/1 |
| media_spine | C160064-037B200A | Ethernet6/5/1 | media_leaf | C160064-037B202A | Ethernet2/3/1 |
| media_spine | C160064-037B200A | Ethernet6/6/1 | media_leaf | C160064-037B202A | Ethernet3/1/1 |
| media_spine | C160064-037B200A | Ethernet6/7/1 | media_leaf | C160064-037B203A | Ethernet2/1/1 |
| media_spine | C160064-037B200A | Ethernet6/8/1 | media_leaf | C160064-037B203A | Ethernet2/3/1 |
| media_spine | C160064-037B200A | Ethernet6/9/1 | media_leaf | C160064-037B204A | Ethernet2/2/1 |
| media_spine | C160064-037B200A | Ethernet6/11/1 | media_leaf | C160064-051B202A | Ethernet2/1/1 |
| media_spine | C160064-037B200A | Ethernet6/12/1 | media_leaf | C160064-050B201A | Ethernet2/1/1 |
| media_spine | C160064-037B200A | Ethernet6/28/1 | media_leaf | C160064-049B201A | Ethernet2/1/1 |
| media_spine | C160064-037B200A | Ethernet7/1/1 | media_leaf | C160064-037B201A | Ethernet2/2/1 |
| media_spine | C160064-037B200A | Ethernet7/2/1 | media_leaf | C160064-037B201A | Ethernet2/4/1 |
| media_spine | C160064-037B200A | Ethernet7/3/1 | media_leaf | C160064-037B201A | Ethernet3/2/1 |
| media_spine | C160064-037B200A | Ethernet7/4/1 | media_leaf | C160064-037B202A | Ethernet2/2/1 |
| media_spine | C160064-037B200A | Ethernet7/5/1 | media_leaf | C160064-037B202A | Ethernet2/4/1 |
| media_spine | C160064-037B200A | Ethernet7/6/1 | media_leaf | C160064-037B202A | Ethernet3/2/1 |
| media_spine | C160064-037B200A | Ethernet7/7/1 | media_leaf | C160064-037B203A | Ethernet2/2/1 |
| media_spine | C160064-037B200A | Ethernet7/8/1 | media_leaf | C160064-037B204A | Ethernet2/1/1 |
| media_spine | C160064-037B200A | Ethernet7/9/1 | media_leaf | C160064-037B204A | Ethernet2/3/1 |
| media_spine | C160064-037B200A | Ethernet7/11/1 | media_leaf | C160064-051B202A | Ethernet2/2/1 |
| media_spine | C160064-037B200A | Ethernet7/12/1 | media_leaf | C160064-050B201A | Ethernet2/2/1 |
| media_spine | C160064-037B200A | Ethernet7/24/1 | media_leaf | C160064-051B202A | Ethernet2/3/1 |
| media_spine | C160064-037B200A | Ethernet7/28/1 | media_leaf | C160064-049B201A | Ethernet2/2/1 |
| media_spine | C160064-037B200A | Ethernet8/11/1 | border_leaf | C160064-037B380A | Ethernet34/1 |
| media_spine | C160064-037B200A | Ethernet8/13/1 | border_leaf | C160064-037B381A | Ethernet34/1 |
| media_spine | C160064-037B200A | Ethernet9/13/1 | ptp_leaf | C160064-037B370A | Ethernet34/1 |
| media_spine | C160064-037B200A | Ethernet9/14/1 | ptp_leaf | C160064-037B371A | Ethernet34/1 |
| ptp_leaf | C160064-037B370A | Ethernet53 | ptp_leaf | C160064-037B371A | Ethernet53 |
| ptp_leaf | C160064-037B370A | Ethernet54 | ptp_leaf | C160064-037B371A | Ethernet54 |
| border_leaf | C160064-037B380A | Ethernet35/1 | border_leaf | C160064-037B381A | Ethernet35/1 |
| border_leaf | C160064-037B380A | Ethernet36/1 | border_leaf | C160064-037B381A | Ethernet36/1 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 100.83.88.0/28 | 16 | 12 | 75.0 % |
| 100.83.88.16/28 | 16 | 12 | 75.0 % |
| 100.83.88.32/28 | 16 | 4 | 25.0 % |
| 100.83.88.48/28 | 16 | 6 | 37.5 % |
| 100.83.88.64/28 | 16 | 8 | 50.0 % |
| 100.83.88.80/28 | 16 | 6 | 37.5 % |
| 100.83.88.96/28 | 16 | 4 | 25.0 % |
| 100.83.88.112/28 | 16 | 10 | 62.5 % |
| 100.83.88.128/28 | 16 | 4 | 25.0 % |
| 100.83.88.144/28 | 16 | 8 | 50.0 % |
| 100.83.88.160/28 | 16 | 4 | 25.0 % |
| 100.83.88.176/28 | 16 | 8 | 50.0 % |
| 100.83.88.192/28 | 16 | 4 | 25.0 % |
| 100.83.88.208/28 | 16 | 8 | 50.0 % |
| 100.83.88.224/28 | 16 | 4 | 25.0 % |
| 100.83.88.240/28 | 16 | 8 | 50.0 % |
| 100.83.89.0/28 | 16 | 4 | 25.0 % |
| 100.83.89.16/28 | 16 | 4 | 25.0 % |
| 100.83.89.32/28 | 16 | 4 | 25.0 % |
| 100.83.89.48/28 | 16 | 8 | 50.0 % |
| 100.83.89.64/28 | 16 | 4 | 25.0 % |
| 100.83.89.80/28 | 16 | 6 | 37.5 % |
| 100.83.89.96/28 | 16 | 4 | 25.0 % |
| 100.83.89.112/28 | 16 | 4 | 25.0 % |
| 100.83.89.128/28 | 16 | 4 | 25.0 % |
| 100.83.89.144/28 | 16 | 4 | 25.0 % |
| 100.83.89.160/28 | 16 | 4 | 25.0 % |
| 100.83.89.176/28 | 16 | 4 | 25.0 % |
| 100.83.89.192/28 | 16 | 4 | 25.0 % |
| 100.83.89.208/28 | 16 | 4 | 25.0 % |
| 100.83.89.224/28 | 16 | 6 | 37.5 % |
| 100.83.89.240/28 | 16 | 6 | 37.5 % |
| 100.83.93.0/24 | 256 | 16 | 6.25 % |
| 100.83.94.0/28 | 16 | 12 | 75.0 % |
| 100.83.94.16/28 | 16 | 12 | 75.0 % |
| 100.83.94.32/28 | 16 | 4 | 25.0 % |
| 100.83.94.48/28 | 16 | 6 | 37.5 % |
| 100.83.94.64/28 | 16 | 8 | 50.0 % |
| 100.83.94.80/28 | 16 | 6 | 37.5 % |
| 100.83.94.96/28 | 16 | 4 | 25.0 % |
| 100.83.94.112/28 | 16 | 10 | 62.5 % |
| 100.83.94.128/28 | 16 | 4 | 25.0 % |
| 100.83.94.144/28 | 16 | 8 | 50.0 % |
| 100.83.94.160/28 | 16 | 4 | 25.0 % |
| 100.83.94.176/28 | 16 | 8 | 50.0 % |
| 100.83.94.192/28 | 16 | 4 | 25.0 % |
| 100.83.94.208/28 | 16 | 8 | 50.0 % |
| 100.83.94.224/28 | 16 | 4 | 25.0 % |
| 100.83.94.240/28 | 16 | 8 | 50.0 % |
| 100.83.95.0/28 | 16 | 4 | 25.0 % |
| 100.83.95.16/28 | 16 | 4 | 25.0 % |
| 100.83.95.32/28 | 16 | 4 | 25.0 % |
| 100.83.95.48/28 | 16 | 8 | 50.0 % |
| 100.83.95.64/28 | 16 | 4 | 25.0 % |
| 100.83.95.80/28 | 16 | 6 | 37.5 % |
| 100.83.95.96/28 | 16 | 4 | 25.0 % |
| 100.83.95.112/28 | 16 | 4 | 25.0 % |
| 100.83.95.128/28 | 16 | 4 | 25.0 % |
| 100.83.95.144/28 | 16 | 4 | 25.0 % |
| 100.83.95.160/28 | 16 | 4 | 25.0 % |
| 100.83.95.176/28 | 16 | 4 | 25.0 % |
| 100.83.95.192/28 | 16 | 4 | 25.0 % |
| 100.83.95.208/28 | 16 | 4 | 25.0 % |
| 100.83.95.224/28 | 16 | 6 | 37.5 % |
| 100.83.95.240/28 | 16 | 6 | 37.5 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| C160064-001B101A | Ethernet2/1/1 | 100.83.94.97/31 | C160064-037B100A | Ethernet6/23/1 | 100.83.94.96/31 |
| C160064-001B101A | Ethernet2/2/1 | 100.83.94.99/31 | C160064-037B100A | Ethernet7/23/1 | 100.83.94.98/31 |
| C160064-001B201A | Ethernet2/1/1 | 100.83.88.97/31 | C160064-037B200A | Ethernet6/23/1 | 100.83.88.96/31 |
| C160064-001B201A | Ethernet2/2/1 | 100.83.88.99/31 | C160064-037B200A | Ethernet7/23/1 | 100.83.88.98/31 |
| C160064-002B101A | Ethernet2/1/1 | 100.83.94.113/31 | C160064-037B100A | Ethernet6/21/1 | 100.83.94.112/31 |
| C160064-002B101A | Ethernet2/2/1 | 100.83.94.115/31 | C160064-037B100A | Ethernet7/21/1 | 100.83.94.114/31 |
| C160064-002B101A | Ethernet2/3/1 | 100.83.94.117/31 | C160064-037B100A | Ethernet6/22/1 | 100.83.94.116/31 |
| C160064-002B101A | Ethernet2/4/1 | 100.83.94.119/31 | C160064-037B100A | Ethernet7/22/1 | 100.83.94.118/31 |
| C160064-002B101A | Ethernet3/1/1 | 100.83.94.121/31 | C160064-037B100A | Ethernet6/24/1 | 100.83.94.120/31 |
| C160064-002B201A | Ethernet2/1/1 | 100.83.88.113/31 | C160064-037B200A | Ethernet6/21/1 | 100.83.88.112/31 |
| C160064-002B201A | Ethernet2/2/1 | 100.83.88.115/31 | C160064-037B200A | Ethernet7/21/1 | 100.83.88.114/31 |
| C160064-002B201A | Ethernet2/3/1 | 100.83.88.117/31 | C160064-037B200A | Ethernet6/22/1 | 100.83.88.116/31 |
| C160064-002B201A | Ethernet2/4/1 | 100.83.88.119/31 | C160064-037B200A | Ethernet7/22/1 | 100.83.88.118/31 |
| C160064-002B201A | Ethernet3/1/1 | 100.83.88.121/31 | C160064-037B200A | Ethernet6/24/1 | 100.83.88.120/31 |
| C160064-003B101A | Ethernet2/1/1 | 100.83.94.129/31 | C160064-037B100A | Ethernet6/20/1 | 100.83.94.128/31 |
| C160064-003B101A | Ethernet2/2/1 | 100.83.94.131/31 | C160064-037B100A | Ethernet7/20/1 | 100.83.94.130/31 |
| C160064-003B201A | Ethernet2/1/1 | 100.83.88.129/31 | C160064-037B200A | Ethernet6/20/1 | 100.83.88.128/31 |
| C160064-003B201A | Ethernet2/2/1 | 100.83.88.131/31 | C160064-037B200A | Ethernet7/20/1 | 100.83.88.130/31 |
| C160064-004B101A | Ethernet53/1 | 100.83.94.145/31 | C160064-037B100A | Ethernet3/33/1 | 100.83.94.144/31 |
| C160064-004B101A | Ethernet54/1 | 100.83.94.147/31 | C160064-037B100A | Ethernet4/32/4 | 100.83.94.146/31 |
| C160064-004B101A | Ethernet55/1 | 100.83.94.149/31 | C160064-037B100A | Ethernet5/33/4 | 100.83.94.148/31 |
| C160064-004B101A | Ethernet56/1 | 100.83.94.151/31 | C160064-037B100A | Ethernet3/32/4 | 100.83.94.150/31 |
| C160064-004B201A | Ethernet53/1 | 100.83.88.145/31 | C160064-037B200A | Ethernet3/33/1 | 100.83.88.144/31 |
| C160064-004B201A | Ethernet54/1 | 100.83.88.147/31 | C160064-037B200A | Ethernet4/32/4 | 100.83.88.146/31 |
| C160064-004B201A | Ethernet55/1 | 100.83.88.149/31 | C160064-037B200A | Ethernet5/33/4 | 100.83.88.148/31 |
| C160064-004B201A | Ethernet56/1 | 100.83.88.151/31 | C160064-037B200A | Ethernet3/32/4 | 100.83.88.150/31 |
| C160064-005B101A | Ethernet2/1/1 | 100.83.94.161/31 | C160064-037B100A | Ethernet6/19/1 | 100.83.94.160/31 |
| C160064-005B101A | Ethernet2/2/1 | 100.83.94.163/31 | C160064-037B100A | Ethernet7/19/1 | 100.83.94.162/31 |
| C160064-005B201A | Ethernet2/1/1 | 100.83.88.161/31 | C160064-037B200A | Ethernet6/19/1 | 100.83.88.160/31 |
| C160064-005B201A | Ethernet2/2/1 | 100.83.88.163/31 | C160064-037B200A | Ethernet7/19/1 | 100.83.88.162/31 |
| C160064-006B101A | Ethernet53/1 | 100.83.94.177/31 | C160064-037B100A | Ethernet5/34/2 | 100.83.94.176/31 |
| C160064-006B101A | Ethernet54/1 | 100.83.94.179/31 | C160064-037B100A | Ethernet3/33/2 | 100.83.94.178/31 |
| C160064-006B101A | Ethernet55/1 | 100.83.94.181/31 | C160064-037B100A | Ethernet4/33/1 | 100.83.94.180/31 |
| C160064-006B101A | Ethernet56/1 | 100.83.94.183/31 | C160064-037B100A | Ethernet5/34/1 | 100.83.94.182/31 |
| C160064-006B201A | Ethernet53/1 | 100.83.88.177/31 | C160064-037B200A | Ethernet5/34/2 | 100.83.88.176/31 |
| C160064-006B201A | Ethernet54/1 | 100.83.88.179/31 | C160064-037B200A | Ethernet3/33/2 | 100.83.88.178/31 |
| C160064-006B201A | Ethernet55/1 | 100.83.88.181/31 | C160064-037B200A | Ethernet4/33/1 | 100.83.88.180/31 |
| C160064-006B201A | Ethernet56/1 | 100.83.88.183/31 | C160064-037B200A | Ethernet5/34/1 | 100.83.88.182/31 |
| C160064-007B101A | Ethernet2/1/1 | 100.83.94.193/31 | C160064-037B100A | Ethernet6/18/1 | 100.83.94.192/31 |
| C160064-007B101A | Ethernet2/2/1 | 100.83.94.195/31 | C160064-037B100A | Ethernet7/18/1 | 100.83.94.194/31 |
| C160064-007B201A | Ethernet2/1/1 | 100.83.88.193/31 | C160064-037B200A | Ethernet6/18/1 | 100.83.88.192/31 |
| C160064-007B201A | Ethernet2/2/1 | 100.83.88.195/31 | C160064-037B200A | Ethernet7/18/1 | 100.83.88.194/31 |
| C160064-008B101A | Ethernet53/1 | 100.83.94.209/31 | C160064-037B100A | Ethernet4/33/3 | 100.83.94.208/31 |
| C160064-008B101A | Ethernet54/1 | 100.83.94.211/31 | C160064-037B100A | Ethernet5/34/3 | 100.83.94.210/31 |
| C160064-008B101A | Ethernet55/1 | 100.83.94.213/31 | C160064-037B100A | Ethernet3/33/3 | 100.83.94.212/31 |
| C160064-008B101A | Ethernet56/1 | 100.83.94.215/31 | C160064-037B100A | Ethernet4/33/2 | 100.83.94.214/31 |
| C160064-008B201A | Ethernet53/1 | 100.83.88.209/31 | C160064-037B200A | Ethernet4/33/3 | 100.83.88.208/31 |
| C160064-008B201A | Ethernet54/1 | 100.83.88.211/31 | C160064-037B200A | Ethernet5/34/3 | 100.83.88.210/31 |
| C160064-008B201A | Ethernet55/1 | 100.83.88.213/31 | C160064-037B200A | Ethernet3/33/3 | 100.83.88.212/31 |
| C160064-008B201A | Ethernet56/1 | 100.83.88.215/31 | C160064-037B200A | Ethernet4/33/2 | 100.83.88.214/31 |
| C160064-009B101A | Ethernet2/1/1 | 100.83.94.225/31 | C160064-037B100A | Ethernet6/17/1 | 100.83.94.224/31 |
| C160064-009B101A | Ethernet2/2/1 | 100.83.94.227/31 | C160064-037B100A | Ethernet7/17/1 | 100.83.94.226/31 |
| C160064-009B201A | Ethernet2/1/1 | 100.83.88.225/31 | C160064-037B200A | Ethernet6/17/1 | 100.83.88.224/31 |
| C160064-009B201A | Ethernet2/2/1 | 100.83.88.227/31 | C160064-037B200A | Ethernet7/17/1 | 100.83.88.226/31 |
| C160064-010B101A | Ethernet53/1 | 100.83.94.241/31 | C160064-037B100A | Ethernet3/34/4 | 100.83.94.240/31 |
| C160064-010B101A | Ethernet54/1 | 100.83.94.243/31 | C160064-037B100A | Ethernet4/33/4 | 100.83.94.242/31 |
| C160064-010B101A | Ethernet55/1 | 100.83.94.245/31 | C160064-037B100A | Ethernet5/34/4 | 100.83.94.244/31 |
| C160064-010B101A | Ethernet56/1 | 100.83.94.247/31 | C160064-037B100A | Ethernet3/34/3 | 100.83.94.246/31 |
| C160064-010B201A | Ethernet53/1 | 100.83.88.241/31 | C160064-037B200A | Ethernet3/34/4 | 100.83.88.240/31 |
| C160064-010B201A | Ethernet54/1 | 100.83.88.243/31 | C160064-037B200A | Ethernet4/33/4 | 100.83.88.242/31 |
| C160064-010B201A | Ethernet55/1 | 100.83.88.245/31 | C160064-037B200A | Ethernet5/34/4 | 100.83.88.244/31 |
| C160064-010B201A | Ethernet56/1 | 100.83.88.247/31 | C160064-037B200A | Ethernet3/34/3 | 100.83.88.246/31 |
| C160064-013B101A | Ethernet55/1 | 100.83.95.1/31 | C160064-037B100A | Ethernet4/35/1 | 100.83.95.0/31 |
| C160064-013B101A | Ethernet56/1 | 100.83.95.3/31 | C160064-037B100A | Ethernet5/35/1 | 100.83.95.2/31 |
| C160064-013B102A | Ethernet2/1/1 | 100.83.95.17/31 | C160064-037B100A | Ethernet6/16/1 | 100.83.95.16/31 |
| C160064-013B102A | Ethernet2/2/1 | 100.83.95.19/31 | C160064-037B100A | Ethernet7/16/1 | 100.83.95.18/31 |
| C160064-013B201A | Ethernet55/1 | 100.83.89.1/31 | C160064-037B200A | Ethernet4/35/1 | 100.83.89.0/31 |
| C160064-013B201A | Ethernet56/1 | 100.83.89.3/31 | C160064-037B200A | Ethernet5/35/1 | 100.83.89.2/31 |
| C160064-013B202A | Ethernet2/1/1 | 100.83.89.17/31 | C160064-037B200A | Ethernet6/16/1 | 100.83.89.16/31 |
| C160064-013B202A | Ethernet2/2/1 | 100.83.89.19/31 | C160064-037B200A | Ethernet7/16/1 | 100.83.89.18/31 |
| C160064-014B101A | Ethernet55/1 | 100.83.95.33/31 | C160064-037B100A | Ethernet5/35/2 | 100.83.95.32/31 |
| C160064-014B101A | Ethernet56/1 | 100.83.95.35/31 | C160064-037B100A | Ethernet3/35/1 | 100.83.95.34/31 |
| C160064-014B102A | Ethernet53/1 | 100.83.95.49/31 | C160064-037B100A | Ethernet4/35/3 | 100.83.95.48/31 |
| C160064-014B102A | Ethernet54/1 | 100.83.95.51/31 | C160064-037B100A | Ethernet5/35/3 | 100.83.95.50/31 |
| C160064-014B102A | Ethernet55/1 | 100.83.95.53/31 | C160064-037B100A | Ethernet3/35/2 | 100.83.95.52/31 |
| C160064-014B102A | Ethernet56/1 | 100.83.95.55/31 | C160064-037B100A | Ethernet4/35/2 | 100.83.95.54/31 |
| C160064-014B201A | Ethernet55/1 | 100.83.89.33/31 | C160064-037B200A | Ethernet5/35/2 | 100.83.89.32/31 |
| C160064-014B201A | Ethernet56/1 | 100.83.89.35/31 | C160064-037B200A | Ethernet3/35/1 | 100.83.89.34/31 |
| C160064-014B202A | Ethernet53/1 | 100.83.89.49/31 | C160064-037B200A | Ethernet4/35/3 | 100.83.89.48/31 |
| C160064-014B202A | Ethernet54/1 | 100.83.89.51/31 | C160064-037B200A | Ethernet5/35/3 | 100.83.89.50/31 |
| C160064-014B202A | Ethernet55/1 | 100.83.89.53/31 | C160064-037B200A | Ethernet3/35/2 | 100.83.89.52/31 |
| C160064-014B202A | Ethernet56/1 | 100.83.89.55/31 | C160064-037B200A | Ethernet4/35/2 | 100.83.89.54/31 |
| C160064-015B101A | Ethernet55/1 | 100.83.95.65/31 | C160064-037B100A | Ethernet3/36/1 | 100.83.95.64/31 |
| C160064-015B101A | Ethernet56/1 | 100.83.95.67/31 | C160064-037B100A | Ethernet4/36/1 | 100.83.95.66/31 |
| C160064-015B102A | Ethernet54/1 | 100.83.95.81/31 | C160064-037B100A | Ethernet5/36/1 | 100.83.95.80/31 |
| C160064-015B102A | Ethernet55/1 | 100.83.95.83/31 | C160064-037B100A | Ethernet3/35/4 | 100.83.95.82/31 |
| C160064-015B102A | Ethernet56/1 | 100.83.95.85/31 | C160064-037B100A | Ethernet4/35/4 | 100.83.95.84/31 |
| C160064-015B103A | Ethernet55/1 | 100.83.95.97/31 | C160064-037B100A | Ethernet5/35/4 | 100.83.95.96/31 |
| C160064-015B103A | Ethernet56/1 | 100.83.95.99/31 | C160064-037B100A | Ethernet3/35/3 | 100.83.95.98/31 |
| C160064-015B201A | Ethernet55/1 | 100.83.89.65/31 | C160064-037B200A | Ethernet3/36/1 | 100.83.89.64/31 |
| C160064-015B201A | Ethernet56/1 | 100.83.89.67/31 | C160064-037B200A | Ethernet4/36/1 | 100.83.89.66/31 |
| C160064-015B202A | Ethernet54/1 | 100.83.89.81/31 | C160064-037B200A | Ethernet5/36/1 | 100.83.89.80/31 |
| C160064-015B202A | Ethernet55/1 | 100.83.89.83/31 | C160064-037B200A | Ethernet3/35/4 | 100.83.89.82/31 |
| C160064-015B202A | Ethernet56/1 | 100.83.89.85/31 | C160064-037B200A | Ethernet4/35/4 | 100.83.89.84/31 |
| C160064-015B203A | Ethernet55/1 | 100.83.89.97/31 | C160064-037B200A | Ethernet5/35/4 | 100.83.89.96/31 |
| C160064-015B203A | Ethernet56/1 | 100.83.89.99/31 | C160064-037B200A | Ethernet3/35/3 | 100.83.89.98/31 |
| C160064-016B101A | Ethernet2/1/1 | 100.83.95.113/31 | C160064-037B100A | Ethernet6/15/1 | 100.83.95.112/31 |
| C160064-016B101A | Ethernet2/2/1 | 100.83.95.115/31 | C160064-037B100A | Ethernet7/15/1 | 100.83.95.114/31 |
| C160064-016B102A | Ethernet2/1/1 | 100.83.95.129/31 | C160064-037B100A | Ethernet6/14/1 | 100.83.95.128/31 |
| C160064-016B102A | Ethernet2/2/1 | 100.83.95.131/31 | C160064-037B100A | Ethernet7/14/1 | 100.83.95.130/31 |
| C160064-016B201A | Ethernet2/1/1 | 100.83.89.113/31 | C160064-037B200A | Ethernet6/15/1 | 100.83.89.112/31 |
| C160064-016B201A | Ethernet2/2/1 | 100.83.89.115/31 | C160064-037B200A | Ethernet7/15/1 | 100.83.89.114/31 |
| C160064-016B202A | Ethernet2/1/1 | 100.83.89.129/31 | C160064-037B200A | Ethernet6/14/1 | 100.83.89.128/31 |
| C160064-016B202A | Ethernet2/2/1 | 100.83.89.131/31 | C160064-037B200A | Ethernet7/14/1 | 100.83.89.130/31 |
| C160064-017B101A | Ethernet54/1 | 100.83.95.145/31 | C160064-037B100A | Ethernet4/36/2 | 100.83.95.144/31 |
| C160064-017B101A | Ethernet55/1 | 100.83.95.147/31 | C160064-037B100A | Ethernet5/36/2 | 100.83.95.146/31 |
| C160064-017B201A | Ethernet54/1 | 100.83.89.145/31 | C160064-037B200A | Ethernet4/36/2 | 100.83.89.144/31 |
| C160064-017B201A | Ethernet55/1 | 100.83.89.147/31 | C160064-037B200A | Ethernet5/36/2 | 100.83.89.146/31 |
| C160064-037B100A | Ethernet3/31/4 | 100.83.94.70/31 | C160064-037B106A | Ethernet56/1 | 100.83.94.71/31 |
| C160064-037B100A | Ethernet3/32/2 | 100.83.94.32/31 | C160064-037B105A | Ethernet55/1 | 100.83.94.33/31 |
| C160064-037B100A | Ethernet3/32/3 | 100.83.94.66/31 | C160064-037B106A | Ethernet54/1 | 100.83.94.67/31 |
| C160064-037B100A | Ethernet3/36/2 | 100.83.95.162/31 | C160064-046B101A | Ethernet55/1 | 100.83.95.163/31 |
| C160064-037B100A | Ethernet3/36/3 | 100.83.95.208/31 | C160064-051B101A | Ethernet54/1 | 100.83.95.209/31 |
| C160064-037B100A | Ethernet3/36/4 | 100.83.95.240/31 | C160064-056B101A | Ethernet54/1 | 100.83.95.241/31 |
| C160064-037B100A | Ethernet4/32/2 | 100.83.94.34/31 | C160064-037B105A | Ethernet56/1 | 100.83.94.35/31 |
| C160064-037B100A | Ethernet4/32/3 | 100.83.94.68/31 | C160064-037B106A | Ethernet55/1 | 100.83.94.69/31 |
| C160064-037B100A | Ethernet4/36/3 | 100.83.95.210/31 | C160064-051B101A | Ethernet55/1 | 100.83.95.211/31 |
| C160064-037B100A | Ethernet4/36/4 | 100.83.95.242/31 | C160064-056B101A | Ethernet55/1 | 100.83.95.243/31 |
| C160064-037B100A | Ethernet5/33/3 | 100.83.94.64/31 | C160064-037B106A | Ethernet53/1 | 100.83.94.65/31 |
| C160064-037B100A | Ethernet5/36/3 | 100.83.95.160/31 | C160064-046B101A | Ethernet54/1 | 100.83.95.161/31 |
| C160064-037B100A | Ethernet5/36/4 | 100.83.95.244/31 | C160064-056B101A | Ethernet56/1 | 100.83.95.245/31 |
| C160064-037B100A | Ethernet6/1/1 | 100.83.94.0/31 | C160064-037B101A | Ethernet2/1/1 | 100.83.94.1/31 |
| C160064-037B100A | Ethernet6/2/1 | 100.83.94.4/31 | C160064-037B101A | Ethernet2/3/1 | 100.83.94.5/31 |
| C160064-037B100A | Ethernet6/3/1 | 100.83.94.8/31 | C160064-037B101A | Ethernet3/1/1 | 100.83.94.9/31 |
| C160064-037B100A | Ethernet6/4/1 | 100.83.94.16/31 | C160064-037B102A | Ethernet2/1/1 | 100.83.94.17/31 |
| C160064-037B100A | Ethernet6/5/1 | 100.83.94.20/31 | C160064-037B102A | Ethernet2/3/1 | 100.83.94.21/31 |
| C160064-037B100A | Ethernet6/6/1 | 100.83.94.24/31 | C160064-037B102A | Ethernet3/1/1 | 100.83.94.25/31 |
| C160064-037B100A | Ethernet6/7/1 | 100.83.94.48/31 | C160064-037B103A | Ethernet2/1/1 | 100.83.94.49/31 |
| C160064-037B100A | Ethernet6/8/1 | 100.83.94.52/31 | C160064-037B103A | Ethernet2/3/1 | 100.83.94.53/31 |
| C160064-037B100A | Ethernet6/9/1 | 100.83.94.82/31 | C160064-037B104A | Ethernet2/2/1 | 100.83.94.83/31 |
| C160064-037B100A | Ethernet6/11/1 | 100.83.95.224/31 | C160064-051B102A | Ethernet2/1/1 | 100.83.95.225/31 |
| C160064-037B100A | Ethernet6/12/1 | 100.83.95.192/31 | C160064-050B101A | Ethernet2/1/1 | 100.83.95.193/31 |
| C160064-037B100A | Ethernet6/28/1 | 100.83.95.176/31 | C160064-049B101A | Ethernet2/1/1 | 100.83.95.177/31 |
| C160064-037B100A | Ethernet7/1/1 | 100.83.94.2/31 | C160064-037B101A | Ethernet2/2/1 | 100.83.94.3/31 |
| C160064-037B100A | Ethernet7/2/1 | 100.83.94.6/31 | C160064-037B101A | Ethernet2/4/1 | 100.83.94.7/31 |
| C160064-037B100A | Ethernet7/3/1 | 100.83.94.10/31 | C160064-037B101A | Ethernet3/2/1 | 100.83.94.11/31 |
| C160064-037B100A | Ethernet7/4/1 | 100.83.94.18/31 | C160064-037B102A | Ethernet2/2/1 | 100.83.94.19/31 |
| C160064-037B100A | Ethernet7/5/1 | 100.83.94.22/31 | C160064-037B102A | Ethernet2/4/1 | 100.83.94.23/31 |
| C160064-037B100A | Ethernet7/6/1 | 100.83.94.26/31 | C160064-037B102A | Ethernet3/2/1 | 100.83.94.27/31 |
| C160064-037B100A | Ethernet7/7/1 | 100.83.94.50/31 | C160064-037B103A | Ethernet2/2/1 | 100.83.94.51/31 |
| C160064-037B100A | Ethernet7/8/1 | 100.83.94.80/31 | C160064-037B104A | Ethernet2/1/1 | 100.83.94.81/31 |
| C160064-037B100A | Ethernet7/9/1 | 100.83.94.84/31 | C160064-037B104A | Ethernet2/3/1 | 100.83.94.85/31 |
| C160064-037B100A | Ethernet7/11/1 | 100.83.95.226/31 | C160064-051B102A | Ethernet2/2/1 | 100.83.95.227/31 |
| C160064-037B100A | Ethernet7/12/1 | 100.83.95.194/31 | C160064-050B101A | Ethernet2/2/1 | 100.83.95.195/31 |
| C160064-037B100A | Ethernet7/24/1 | 100.83.95.228/31 | C160064-051B102A | Ethernet2/3/1 | 100.83.95.229/31 |
| C160064-037B100A | Ethernet7/28/1 | 100.83.95.178/31 | C160064-049B101A | Ethernet2/2/1 | 100.83.95.179/31 |
| C160064-037B100A | Ethernet8/10/1 | 100.83.93.16/31 | C160064-037B380A | Ethernet33/1 | 100.83.93.17/31 |
| C160064-037B100A | Ethernet8/12/1 | 100.83.93.20/31 | C160064-037B381A | Ethernet33/1 | 100.83.93.21/31 |
| C160064-037B100A | Ethernet9/12/1 | 100.83.93.8/31 | C160064-037B370A | Ethernet33/1 | 100.83.93.9/31 |
| C160064-037B100A | Ethernet9/13/1 | 100.83.93.12/31 | C160064-037B371A | Ethernet33/1 | 100.83.93.13/31 |
| C160064-037B200A | Ethernet3/31/4 | 100.83.88.70/31 | C160064-037B206A | Ethernet56/1 | 100.83.88.71/31 |
| C160064-037B200A | Ethernet3/32/2 | 100.83.88.32/31 | C160064-037B205A | Ethernet55/1 | 100.83.88.33/31 |
| C160064-037B200A | Ethernet3/32/3 | 100.83.88.66/31 | C160064-037B206A | Ethernet54/1 | 100.83.88.67/31 |
| C160064-037B200A | Ethernet3/36/2 | 100.83.89.162/31 | C160064-046B201A | Ethernet55/1 | 100.83.89.163/31 |
| C160064-037B200A | Ethernet3/36/3 | 100.83.89.208/31 | C160064-051B201A | Ethernet54/1 | 100.83.89.209/31 |
| C160064-037B200A | Ethernet3/36/4 | 100.83.89.240/31 | C160064-056B201A | Ethernet54/1 | 100.83.89.241/31 |
| C160064-037B200A | Ethernet4/32/2 | 100.83.88.34/31 | C160064-037B205A | Ethernet56/1 | 100.83.88.35/31 |
| C160064-037B200A | Ethernet4/32/3 | 100.83.88.68/31 | C160064-037B206A | Ethernet55/1 | 100.83.88.69/31 |
| C160064-037B200A | Ethernet4/36/3 | 100.83.89.210/31 | C160064-051B201A | Ethernet55/1 | 100.83.89.211/31 |
| C160064-037B200A | Ethernet4/36/4 | 100.83.89.242/31 | C160064-056B201A | Ethernet55/1 | 100.83.89.243/31 |
| C160064-037B200A | Ethernet5/33/3 | 100.83.88.64/31 | C160064-037B206A | Ethernet53/1 | 100.83.88.65/31 |
| C160064-037B200A | Ethernet5/36/3 | 100.83.89.160/31 | C160064-046B201A | Ethernet54/1 | 100.83.89.161/31 |
| C160064-037B200A | Ethernet5/36/4 | 100.83.89.244/31 | C160064-056B201A | Ethernet56/1 | 100.83.89.245/31 |
| C160064-037B200A | Ethernet6/1/1 | 100.83.88.0/31 | C160064-037B201A | Ethernet2/1/1 | 100.83.88.1/31 |
| C160064-037B200A | Ethernet6/2/1 | 100.83.88.4/31 | C160064-037B201A | Ethernet2/3/1 | 100.83.88.5/31 |
| C160064-037B200A | Ethernet6/3/1 | 100.83.88.8/31 | C160064-037B201A | Ethernet3/1/1 | 100.83.88.9/31 |
| C160064-037B200A | Ethernet6/4/1 | 100.83.88.16/31 | C160064-037B202A | Ethernet2/1/1 | 100.83.88.17/31 |
| C160064-037B200A | Ethernet6/5/1 | 100.83.88.20/31 | C160064-037B202A | Ethernet2/3/1 | 100.83.88.21/31 |
| C160064-037B200A | Ethernet6/6/1 | 100.83.88.24/31 | C160064-037B202A | Ethernet3/1/1 | 100.83.88.25/31 |
| C160064-037B200A | Ethernet6/7/1 | 100.83.88.48/31 | C160064-037B203A | Ethernet2/1/1 | 100.83.88.49/31 |
| C160064-037B200A | Ethernet6/8/1 | 100.83.88.52/31 | C160064-037B203A | Ethernet2/3/1 | 100.83.88.53/31 |
| C160064-037B200A | Ethernet6/9/1 | 100.83.88.82/31 | C160064-037B204A | Ethernet2/2/1 | 100.83.88.83/31 |
| C160064-037B200A | Ethernet6/11/1 | 100.83.89.224/31 | C160064-051B202A | Ethernet2/1/1 | 100.83.89.225/31 |
| C160064-037B200A | Ethernet6/12/1 | 100.83.89.192/31 | C160064-050B201A | Ethernet2/1/1 | 100.83.89.193/31 |
| C160064-037B200A | Ethernet6/28/1 | 100.83.89.176/31 | C160064-049B201A | Ethernet2/1/1 | 100.83.89.177/31 |
| C160064-037B200A | Ethernet7/1/1 | 100.83.88.2/31 | C160064-037B201A | Ethernet2/2/1 | 100.83.88.3/31 |
| C160064-037B200A | Ethernet7/2/1 | 100.83.88.6/31 | C160064-037B201A | Ethernet2/4/1 | 100.83.88.7/31 |
| C160064-037B200A | Ethernet7/3/1 | 100.83.88.10/31 | C160064-037B201A | Ethernet3/2/1 | 100.83.88.11/31 |
| C160064-037B200A | Ethernet7/4/1 | 100.83.88.18/31 | C160064-037B202A | Ethernet2/2/1 | 100.83.88.19/31 |
| C160064-037B200A | Ethernet7/5/1 | 100.83.88.22/31 | C160064-037B202A | Ethernet2/4/1 | 100.83.88.23/31 |
| C160064-037B200A | Ethernet7/6/1 | 100.83.88.26/31 | C160064-037B202A | Ethernet3/2/1 | 100.83.88.27/31 |
| C160064-037B200A | Ethernet7/7/1 | 100.83.88.50/31 | C160064-037B203A | Ethernet2/2/1 | 100.83.88.51/31 |
| C160064-037B200A | Ethernet7/8/1 | 100.83.88.80/31 | C160064-037B204A | Ethernet2/1/1 | 100.83.88.81/31 |
| C160064-037B200A | Ethernet7/9/1 | 100.83.88.84/31 | C160064-037B204A | Ethernet2/3/1 | 100.83.88.85/31 |
| C160064-037B200A | Ethernet7/11/1 | 100.83.89.226/31 | C160064-051B202A | Ethernet2/2/1 | 100.83.89.227/31 |
| C160064-037B200A | Ethernet7/12/1 | 100.83.89.194/31 | C160064-050B201A | Ethernet2/2/1 | 100.83.89.195/31 |
| C160064-037B200A | Ethernet7/24/1 | 100.83.89.228/31 | C160064-051B202A | Ethernet2/3/1 | 100.83.89.229/31 |
| C160064-037B200A | Ethernet7/28/1 | 100.83.89.178/31 | C160064-049B201A | Ethernet2/2/1 | 100.83.89.179/31 |
| C160064-037B200A | Ethernet8/11/1 | 100.83.93.18/31 | C160064-037B380A | Ethernet34/1 | 100.83.93.19/31 |
| C160064-037B200A | Ethernet8/13/1 | 100.83.93.22/31 | C160064-037B381A | Ethernet34/1 | 100.83.93.23/31 |
| C160064-037B200A | Ethernet9/13/1 | 100.83.93.10/31 | C160064-037B370A | Ethernet34/1 | 100.83.93.11/31 |
| C160064-037B200A | Ethernet9/14/1 | 100.83.93.14/31 | C160064-037B371A | Ethernet34/1 | 100.83.93.15/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 169.27.195.0/25 | 128 | 70 | 54.69 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| FABRIC | C160064-001B101A | 169.27.195.7/32 |
| FABRIC | C160064-001B201A | 169.27.195.40/32 |
| FABRIC | C160064-002B101A | 169.27.195.8/32 |
| FABRIC | C160064-002B201A | 169.27.195.41/32 |
| FABRIC | C160064-003B101A | 169.27.195.9/32 |
| FABRIC | C160064-003B201A | 169.27.195.42/32 |
| FABRIC | C160064-004B101A | 169.27.195.10/32 |
| FABRIC | C160064-004B201A | 169.27.195.43/32 |
| FABRIC | C160064-005B101A | 169.27.195.11/32 |
| FABRIC | C160064-005B201A | 169.27.195.44/32 |
| FABRIC | C160064-006B101A | 169.27.195.12/32 |
| FABRIC | C160064-006B201A | 169.27.195.45/32 |
| FABRIC | C160064-007B101A | 169.27.195.13/32 |
| FABRIC | C160064-007B201A | 169.27.195.46/32 |
| FABRIC | C160064-008B101A | 169.27.195.14/32 |
| FABRIC | C160064-008B201A | 169.27.195.47/32 |
| FABRIC | C160064-009B101A | 169.27.195.15/32 |
| FABRIC | C160064-009B201A | 169.27.195.48/32 |
| FABRIC | C160064-010B101A | 169.27.195.16/32 |
| FABRIC | C160064-010B201A | 169.27.195.49/32 |
| FABRIC | C160064-013B101A | 169.27.195.17/32 |
| FABRIC | C160064-013B102A | 169.27.195.18/32 |
| FABRIC | C160064-013B201A | 169.27.195.50/32 |
| FABRIC | C160064-013B202A | 169.27.195.51/32 |
| FABRIC | C160064-014B101A | 169.27.195.19/32 |
| FABRIC | C160064-014B102A | 169.27.195.20/32 |
| FABRIC | C160064-014B201A | 169.27.195.52/32 |
| FABRIC | C160064-014B202A | 169.27.195.53/32 |
| FABRIC | C160064-015B101A | 169.27.195.21/32 |
| FABRIC | C160064-015B102A | 169.27.195.22/32 |
| FABRIC | C160064-015B103A | 169.27.195.23/32 |
| FABRIC | C160064-015B201A | 169.27.195.54/32 |
| FABRIC | C160064-015B202A | 169.27.195.55/32 |
| FABRIC | C160064-015B203A | 169.27.195.56/32 |
| FABRIC | C160064-016B101A | 169.27.195.24/32 |
| FABRIC | C160064-016B102A | 169.27.195.25/32 |
| FABRIC | C160064-016B201A | 169.27.195.57/32 |
| FABRIC | C160064-016B202A | 169.27.195.58/32 |
| FABRIC | C160064-017B101A | 169.27.195.26/32 |
| FABRIC | C160064-017B201A | 169.27.195.59/32 |
| FABRIC | C160064-037B100A | 169.27.195.0/32 |
| FABRIC | C160064-037B101A | 169.27.195.1/32 |
| FABRIC | C160064-037B102A | 169.27.195.2/32 |
| FABRIC | C160064-037B103A | 169.27.195.4/32 |
| FABRIC | C160064-037B104A | 169.27.195.6/32 |
| FABRIC | C160064-037B105A | 169.27.195.3/32 |
| FABRIC | C160064-037B106A | 169.27.195.5/32 |
| FABRIC | C160064-037B200A | 169.27.195.33/32 |
| FABRIC | C160064-037B201A | 169.27.195.34/32 |
| FABRIC | C160064-037B202A | 169.27.195.35/32 |
| FABRIC | C160064-037B203A | 169.27.195.37/32 |
| FABRIC | C160064-037B204A | 169.27.195.39/32 |
| FABRIC | C160064-037B205A | 169.27.195.36/32 |
| FABRIC | C160064-037B206A | 169.27.195.38/32 |
| FABRIC | C160064-037B370A | 169.27.195.72/32 |
| FABRIC | C160064-037B371A | 169.27.195.73/32 |
| FABRIC | C160064-037B380A | 169.27.195.70/32 |
| FABRIC | C160064-037B381A | 169.27.195.71/32 |
| FABRIC | C160064-046B101A | 169.27.195.27/32 |
| FABRIC | C160064-046B201A | 169.27.195.60/32 |
| FABRIC | C160064-049B101A | 169.27.195.28/32 |
| FABRIC | C160064-049B201A | 169.27.195.61/32 |
| FABRIC | C160064-050B101A | 169.27.195.29/32 |
| FABRIC | C160064-050B201A | 169.27.195.62/32 |
| FABRIC | C160064-051B101A | 169.27.195.30/32 |
| FABRIC | C160064-051B102A | 169.27.195.31/32 |
| FABRIC | C160064-051B201A | 169.27.195.63/32 |
| FABRIC | C160064-051B202A | 169.27.195.64/32 |
| FABRIC | C160064-056B101A | 169.27.195.32/32 |
| FABRIC | C160064-056B201A | 169.27.195.65/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------ | ------------------- | ------------------ | ------------------ |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
