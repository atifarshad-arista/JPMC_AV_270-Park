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
| FABRIC | media_leaf | blue-leaf1 | 10.176.143.143/27 | 720XP | Provisioned | JPA2423A0HG |
| FABRIC | media_leaf | blue-leaf2 | 10.176.143.172/27 | 720XP | Provisioned | JPA2401A3W3 |
| FABRIC | media_leaf | blue-leaf3 | 10.166.80.7/27 | 720XP | Provisioned | JPA2416P3K9 |
| FABRIC | media_leaf | blue-leaf4 | 10.166.80.12/27 | 720XP | Provisioned | JPA2402A092 |
| FABRIC | media_leaf | blue-leaf5 | 10.166.80.41/27 | 720XP | Provisioned | JPA2416P3GF |
| FABRIC | media_leaf | blue-leaf6 | 10.166.80.46/27 | 720XP | Provisioned | JPA2401A3W5 |
| FABRIC | media_spine | blue-spine1 | 10.176.143.168/27 | 7808R3 | Provisioned | TBDxxxxxxxx |
| FABRIC | border_leaf | border-leaf1 | 10.176.143.138/27 | 7280CR3 | Provisioned | - |
| FABRIC | border_leaf | border-leaf2 | 10.176.143.167/27 | 7280CR3 | Provisioned | - |
| FABRIC | ptp_leaf | media-PTP-1 | 10.176.143.137/27 | 7280SR3 | Provisioned | - |
| FABRIC | ptp_leaf | media-PTP-2 | 10.176.143.167/27 | 7280SR3 | Provisioned | - |
| FABRIC | media_leaf | red-leaf1 | 10.176.143.141/27 | 720XP | Provisioned | JPA2423A0HM |
| FABRIC | media_leaf | red-leaf2 | 10.176.143.170/27 | 720XP | Provisioned | JPA2403A1WC |
| FABRIC | media_leaf | red-leaf3 | 10.166.80.6/27 | 720XP | Provisioned | JPA2416P3JC |
| FABRIC | media_leaf | red-leaf4 | 10.166.80.10/27 | 720XP | Provisioned | JPA2401A3GM |
| FABRIC | media_leaf | red-leaf5 | 10.166.80.40/27 | 720XP | Provisioned | JPA2416P1VH |
| FABRIC | media_leaf | red-leaf6 | 10.166.80.44/27 | 720XP | Provisioned | JPA2401A3W6 |
| FABRIC | media_leaf | red-leaf7 | 10.100.100.44/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf8 | 10.100.100.45/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf9 | 10.100.100.46/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf10 | 10.100.100.47/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf11 | 10.100.100.48/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf12 | 10.100.100.49/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf13 | 10.100.100.50/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf14 | 10.100.100.51/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf15 | 10.100.100.52/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf16 | 10.100.100.53/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf17 | 10.100.100.54/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf18 | 10.100.100.55/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf19 | 10.100.100.56/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf20 | 10.100.100.57/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf21 | 10.100.100.58/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf22 | 10.100.100.59/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf23 | 10.100.100.60/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf24 | 10.100.100.61/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf25 | 10.100.100.62/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf26 | 10.100.100.63/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf27 | 10.100.100.64/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf28 | 10.100.100.65/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf29 | 10.100.100.66/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf30 | 10.100.100.67/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf31 | 10.100.100.68/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | red-leaf32 | 10.100.100.69/24 | 720XP | Provisioned | - |
| FABRIC | media_spine | red-spine1 | 10.176.143.139/27 | 7808R3 | Provisioned | HNN23076021 |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| media_leaf | blue-leaf1 | Ethernet2/1 | media_spine | blue-spine1 | Ethernet6/18/1 |
| media_leaf | blue-leaf1 | Ethernet2/2 | media_spine | blue-spine1 | Ethernet6/19/1 |
| media_leaf | blue-leaf1 | Ethernet2/3 | media_spine | blue-spine1 | Ethernet6/20/1 |
| media_leaf | blue-leaf1 | Ethernet2/4 | media_spine | blue-spine1 | Ethernet7/1/1 |
| media_leaf | blue-leaf1 | Ethernet3/1 | media_spine | blue-spine1 | Ethernet7/2/1 |
| media_leaf | blue-leaf1 | Ethernet3/2 | media_spine | blue-spine1 | Ethernet7/3/1 |
| media_leaf | blue-leaf2 | Ethernet2/1 | media_spine | blue-spine1 | Ethernet6/4/1 |
| media_leaf | blue-leaf2 | Ethernet2/2 | media_spine | blue-spine1 | Ethernet7/4/1 |
| media_leaf | blue-leaf2 | Ethernet2/3 | media_spine | blue-spine1 | Ethernet6/5/1 |
| media_leaf | blue-leaf2 | Ethernet2/4 | media_spine | blue-spine1 | Ethernet7/5/1 |
| media_leaf | blue-leaf2 | Ethernet3/1 | media_spine | blue-spine1 | Ethernet6/6/1 |
| media_leaf | blue-leaf2 | Ethernet3/2 | media_spine | blue-spine1 | Ethernet7/6/1 |
| media_leaf | blue-leaf3 | Ethernet55 | media_spine | blue-spine1 | Ethernet3/32/2 |
| media_leaf | blue-leaf3 | Ethernet56 | media_spine | blue-spine1 | Ethernet4/32/2 |
| media_leaf | blue-leaf4 | Ethernet2/1 | media_spine | blue-spine1 | Ethernet6/7/1 |
| media_leaf | blue-leaf4 | Ethernet2/2 | media_spine | blue-spine1 | Ethernet7/7/1 |
| media_leaf | blue-leaf4 | Ethernet2/3 | media_spine | blue-spine1 | Ethernet6/8/1 |
| media_leaf | blue-leaf5 | Ethernet53 | media_spine | blue-spine1 | Ethernet5/33/3 |
| media_leaf | blue-leaf5 | Ethernet54 | media_spine | blue-spine1 | Ethernet3/32/3 |
| media_leaf | blue-leaf5 | Ethernet55 | media_spine | blue-spine1 | Ethernet4/32/3 |
| media_leaf | blue-leaf5 | Ethernet56 | media_spine | blue-spine1 | Ethernet3/31/4 |
| media_leaf | blue-leaf6 | Ethernet2/1 | media_spine | blue-spine1 | Ethernet7/8/1 |
| media_leaf | blue-leaf6 | Ethernet2/2 | media_spine | blue-spine1 | Ethernet6/9/1 |
| media_spine | blue-spine1 | Ethernet3/32/1 | ptp_leaf | media-PTP-1 | Ethernet50 |
| media_spine | blue-spine1 | Ethernet4/32/1 | ptp_leaf | media-PTP-2 | Ethernet50 |
| media_spine | blue-spine1 | Ethernet33/1 | border_leaf | border-leaf1 | Ethernet32/1 |
| media_spine | blue-spine1 | Ethernet34/1 | border_leaf | border-leaf2 | Ethernet32/1 |
| border_leaf | border-leaf1 | Ethernet31/1 | media_spine | red-spine1 | Ethernet33/1 |
| border_leaf | border-leaf1 | Ethernet35/1 | border_leaf | border-leaf2 | Ethernet35/1 |
| border_leaf | border-leaf1 | Ethernet36/1 | border_leaf | border-leaf2 | Ethernet36/1 |
| border_leaf | border-leaf2 | Ethernet31/1 | media_spine | red-spine1 | Ethernet34/1 |
| ptp_leaf | media-PTP-1 | Ethernet49 | media_spine | red-spine1 | Ethernet3/32/1 |
| ptp_leaf | media-PTP-1 | Ethernet53 | ptp_leaf | media-PTP-2 | Ethernet53 |
| ptp_leaf | media-PTP-1 | Ethernet54 | ptp_leaf | media-PTP-2 | Ethernet54 |
| ptp_leaf | media-PTP-2 | Ethernet49 | media_spine | red-spine1 | Ethernet4/32/1 |
| media_leaf | red-leaf1 | Ethernet2/1 | media_spine | red-spine1 | Ethernet6/18/1 |
| media_leaf | red-leaf1 | Ethernet2/2 | media_spine | red-spine1 | Ethernet6/19/1 |
| media_leaf | red-leaf1 | Ethernet2/3 | media_spine | red-spine1 | Ethernet6/20/1 |
| media_leaf | red-leaf1 | Ethernet2/4 | media_spine | red-spine1 | Ethernet7/1/1 |
| media_leaf | red-leaf1 | Ethernet3/1 | media_spine | red-spine1 | Ethernet7/2/1 |
| media_leaf | red-leaf1 | Ethernet3/2 | media_spine | red-spine1 | Ethernet7/3/1 |
| media_leaf | red-leaf2 | Ethernet2/1 | media_spine | red-spine1 | Ethernet6/4/1 |
| media_leaf | red-leaf2 | Ethernet2/2 | media_spine | red-spine1 | Ethernet7/4/1 |
| media_leaf | red-leaf2 | Ethernet2/3 | media_spine | red-spine1 | Ethernet6/5/1 |
| media_leaf | red-leaf2 | Ethernet2/4 | media_spine | red-spine1 | Ethernet7/5/1 |
| media_leaf | red-leaf2 | Ethernet3/1 | media_spine | red-spine1 | Ethernet6/6/1 |
| media_leaf | red-leaf2 | Ethernet3/2 | media_spine | red-spine1 | Ethernet7/6/1 |
| media_leaf | red-leaf3 | Ethernet55 | media_spine | red-spine1 | Ethernet3/32/2 |
| media_leaf | red-leaf3 | Ethernet56 | media_spine | red-spine1 | Ethernet4/32/2 |
| media_leaf | red-leaf4 | Ethernet2/1 | media_spine | red-spine1 | Ethernet6/7/1 |
| media_leaf | red-leaf4 | Ethernet2/2 | media_spine | red-spine1 | Ethernet7/7/1 |
| media_leaf | red-leaf4 | Ethernet2/3 | media_spine | red-spine1 | Ethernet6/8/1 |
| media_leaf | red-leaf5 | Ethernet53 | media_spine | red-spine1 | Ethernet5/33/3 |
| media_leaf | red-leaf5 | Ethernet54 | media_spine | red-spine1 | Ethernet3/32/3 |
| media_leaf | red-leaf5 | Ethernet55 | media_spine | red-spine1 | Ethernet4/32/3 |
| media_leaf | red-leaf5 | Ethernet56 | media_spine | red-spine1 | Ethernet3/31/4 |
| media_leaf | red-leaf6 | Ethernet2/1 | media_spine | red-spine1 | Ethernet7/8/1 |
| media_leaf | red-leaf6 | Ethernet2/2 | media_spine | red-spine1 | Ethernet6/9/1 |
| media_leaf | red-leaf7 | Ethernet2/1 | media_spine | red-spine1 | Ethernet7/10/1 |
| media_leaf | red-leaf7 | Ethernet2/2 | media_spine | red-spine1 | Ethernet6/21/1 |
| media_leaf | red-leaf8 | Ethernet2/1 | media_spine | red-spine1 | Ethernet7/11/1 |
| media_leaf | red-leaf8 | Ethernet2/2 | media_spine | red-spine1 | Ethernet6/22/1 |
| media_leaf | red-leaf9 | Ethernet2/1 | media_spine | red-spine1 | Ethernet7/12/1 |
| media_leaf | red-leaf9 | Ethernet2/2 | media_spine | red-spine1 | Ethernet6/23/1 |
| media_leaf | red-leaf10 | Ethernet2/1 | media_spine | red-spine1 | Ethernet7/13/1 |
| media_leaf | red-leaf10 | Ethernet2/2 | media_spine | red-spine1 | Ethernet6/24/1 |
| media_leaf | red-leaf11 | Ethernet2/1 | media_spine | red-spine1 | Ethernet7/15/1 |
| media_leaf | red-leaf11 | Ethernet2/2 | media_spine | red-spine1 | Ethernet6/25/1 |
| media_leaf | red-leaf12 | Ethernet2/1 | media_spine | red-spine1 | Ethernet7/17/1 |
| media_leaf | red-leaf12 | Ethernet2/2 | media_spine | red-spine1 | Ethernet6/26/1 |
| media_leaf | red-leaf13 | Ethernet2/1 | media_spine | red-spine1 | Ethernet7/18/1 |
| media_leaf | red-leaf13 | Ethernet2/2 | media_spine | red-spine1 | Ethernet6/27/1 |
| media_leaf | red-leaf14 | Ethernet2/1 | media_spine | red-spine1 | Ethernet7/19/1 |
| media_leaf | red-leaf14 | Ethernet2/2 | media_spine | red-spine1 | Ethernet6/28/1 |
| media_leaf | red-leaf15 | Ethernet2/1 | media_spine | red-spine1 | Ethernet7/21/1 |
| media_leaf | red-leaf15 | Ethernet2/1 | media_spine | red-spine1 | Ethernet7/23/1 |
| media_leaf | red-leaf15 | Ethernet2/2 | media_spine | red-spine1 | Ethernet6/29/1 |
| media_leaf | red-leaf16 | Ethernet2/1 | media_spine | red-spine1 | Ethernet7/21/1 |
| media_leaf | red-leaf16 | Ethernet2/2 | media_spine | red-spine1 | Ethernet6/30/1 |
| media_leaf | red-leaf17 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/21/1 |
| media_leaf | red-leaf17 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/29/1 |
| media_leaf | red-leaf18 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/23/1 |
| media_leaf | red-leaf18 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/30/1 |
| media_leaf | red-leaf19 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/25/1 |
| media_leaf | red-leaf19 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/31/1 |
| media_leaf | red-leaf20 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/27/1 |
| media_leaf | red-leaf20 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/32/1 |
| media_leaf | red-leaf21 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/29/1 |
| media_leaf | red-leaf21 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/33/1 |
| media_leaf | red-leaf22 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/31/1 |
| media_leaf | red-leaf22 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/34/1 |
| media_leaf | red-leaf23 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/33/1 |
| media_leaf | red-leaf23 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/35/1 |
| media_leaf | red-leaf24 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/35/1 |
| media_leaf | red-leaf24 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/36/1 |
| media_leaf | red-leaf25 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/37/1 |
| media_leaf | red-leaf25 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/37/1 |
| media_leaf | red-leaf26 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/39/1 |
| media_leaf | red-leaf26 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/38/1 |
| media_leaf | red-leaf27 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/41/1 |
| media_leaf | red-leaf27 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/39/1 |
| media_leaf | red-leaf28 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/43/1 |
| media_leaf | red-leaf28 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/40/1 |
| media_leaf | red-leaf29 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/45/1 |
| media_leaf | red-leaf29 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/41/1 |
| media_leaf | red-leaf30 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/47/1 |
| media_leaf | red-leaf30 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/42/1 |
| media_leaf | red-leaf31 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/49/1 |
| media_leaf | red-leaf31 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/43/1 |
| media_leaf | red-leaf32 | Ethernet2/1 | media_spine | red-spine1 | Ethernet9/51/1 |
| media_leaf | red-leaf32 | Ethernet2/2 | media_spine | red-spine1 | Ethernet8/44/1 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 100.83.88.0/23 | 512 | 10 | 1.96 % |
| 100.83.100.0/23 | 512 | 46 | 8.99 % |
| 100.83.200.0/22 | 1024 | 78 | 7.62 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| blue-leaf1 | Ethernet2/1 | 100.83.100.1/31 | blue-spine1 | Ethernet6/18/1 | 100.83.100.0/31 |
| blue-leaf1 | Ethernet2/2 | 100.83.100.3/31 | blue-spine1 | Ethernet6/19/1 | 100.83.100.2/31 |
| blue-leaf1 | Ethernet2/3 | 100.83.100.5/31 | blue-spine1 | Ethernet6/20/1 | 100.83.100.4/31 |
| blue-leaf1 | Ethernet2/4 | 100.83.100.7/31 | blue-spine1 | Ethernet7/1/1 | 100.83.100.6/31 |
| blue-leaf1 | Ethernet3/1 | 100.83.100.9/31 | blue-spine1 | Ethernet7/2/1 | 100.83.100.8/31 |
| blue-leaf1 | Ethernet3/2 | 100.83.100.11/31 | blue-spine1 | Ethernet7/3/1 | 100.83.100.10/31 |
| blue-leaf2 | Ethernet2/1 | 100.83.100.145/31 | blue-spine1 | Ethernet6/4/1 | 100.83.100.144/31 |
| blue-leaf2 | Ethernet2/2 | 100.83.100.151/31 | blue-spine1 | Ethernet7/4/1 | 100.83.100.150/31 |
| blue-leaf2 | Ethernet2/3 | 100.83.100.147/31 | blue-spine1 | Ethernet6/5/1 | 100.83.100.146/31 |
| blue-leaf2 | Ethernet2/4 | 100.83.100.153/31 | blue-spine1 | Ethernet7/5/1 | 100.83.100.152/31 |
| blue-leaf2 | Ethernet3/1 | 100.83.100.149/31 | blue-spine1 | Ethernet6/6/1 | 100.83.100.148/31 |
| blue-leaf2 | Ethernet3/2 | 100.83.100.155/31 | blue-spine1 | Ethernet7/6/1 | 100.83.100.154/31 |
| blue-leaf3 | Ethernet55 | 100.83.100.105/31 | blue-spine1 | Ethernet3/32/2 | 100.83.100.104/31 |
| blue-leaf3 | Ethernet56 | 100.83.100.107/31 | blue-spine1 | Ethernet4/32/2 | 100.83.100.106/31 |
| blue-leaf4 | Ethernet2/1 | 100.83.100.193/31 | blue-spine1 | Ethernet6/7/1 | 100.83.100.192/31 |
| blue-leaf4 | Ethernet2/2 | 100.83.100.197/31 | blue-spine1 | Ethernet7/7/1 | 100.83.100.196/31 |
| blue-leaf4 | Ethernet2/3 | 100.83.100.195/31 | blue-spine1 | Ethernet6/8/1 | 100.83.100.194/31 |
| blue-leaf5 | Ethernet53 | 100.83.101.71/31 | blue-spine1 | Ethernet5/33/3 | 100.83.101.70/31 |
| blue-leaf5 | Ethernet54 | 100.83.101.67/31 | blue-spine1 | Ethernet3/32/3 | 100.83.101.66/31 |
| blue-leaf5 | Ethernet55 | 100.83.101.69/31 | blue-spine1 | Ethernet4/32/3 | 100.83.101.68/31 |
| blue-leaf5 | Ethernet56 | 100.83.101.65/31 | blue-spine1 | Ethernet3/31/4 | 100.83.101.64/31 |
| blue-leaf6 | Ethernet2/1 | 100.83.100.203/31 | blue-spine1 | Ethernet7/8/1 | 100.83.100.202/31 |
| blue-leaf6 | Ethernet2/2 | 100.83.100.201/31 | blue-spine1 | Ethernet6/9/1 | 100.83.100.200/31 |
| blue-spine1 | Ethernet3/32/1 | 100.83.88.2/31 | media-PTP-1 | Ethernet50 | 100.83.88.3/31 |
| blue-spine1 | Ethernet4/32/1 | 100.83.88.10/31 | media-PTP-2 | Ethernet50 | 100.83.88.11/31 |
| blue-spine1 | Ethernet33/1 | 100.83.88.18/31 | border-leaf1 | Ethernet32/1 | 100.83.93.19/31 |
| blue-spine1 | Ethernet34/1 | 100.83.88.26/31 | border-leaf2 | Ethernet32/1 | 100.83.93.23/31 |
| border-leaf1 | Ethernet31/1 | 100.83.93.17/31 | red-spine1 | Ethernet33/1 | 100.83.88.16/31 |
| border-leaf2 | Ethernet31/1 | 100.83.93.21/31 | red-spine1 | Ethernet34/1 | 100.83.88.24/31 |
| media-PTP-1 | Ethernet49 | 100.83.88.1/31 | red-spine1 | Ethernet3/32/1 | 100.83.200.0/31 |
| media-PTP-2 | Ethernet49 | 100.83.88.9/31 | red-spine1 | Ethernet4/32/1 | 100.83.200.4/31 |
| red-leaf1 | Ethernet2/1 | 100.83.200.1/31 | red-spine1 | Ethernet6/18/1 | 100.83.94.0/31 |
| red-leaf1 | Ethernet2/2 | 100.83.200.3/31 | red-spine1 | Ethernet6/19/1 | 100.83.94.2/31 |
| red-leaf1 | Ethernet2/3 | 100.83.200.5/31 | red-spine1 | Ethernet6/20/1 | 100.83.94.4/31 |
| red-leaf1 | Ethernet2/4 | 100.83.200.7/31 | red-spine1 | Ethernet7/1/1 | 100.83.94.6/31 |
| red-leaf1 | Ethernet3/1 | 100.83.200.9/31 | red-spine1 | Ethernet7/2/1 | 100.83.94.8/31 |
| red-leaf1 | Ethernet3/2 | 100.83.200.11/31 | red-spine1 | Ethernet7/3/1 | 100.83.94.10/31 |
| red-leaf2 | Ethernet2/1 | 100.83.200.73/31 | red-spine1 | Ethernet6/4/1 | 100.83.94.72/31 |
| red-leaf2 | Ethernet2/2 | 100.83.200.79/31 | red-spine1 | Ethernet7/4/1 | 100.83.94.78/31 |
| red-leaf2 | Ethernet2/3 | 100.83.200.75/31 | red-spine1 | Ethernet6/5/1 | 100.83.94.74/31 |
| red-leaf2 | Ethernet2/4 | 100.83.200.81/31 | red-spine1 | Ethernet7/5/1 | 100.83.94.80/31 |
| red-leaf2 | Ethernet3/1 | 100.83.200.77/31 | red-spine1 | Ethernet6/6/1 | 100.83.94.76/31 |
| red-leaf2 | Ethernet3/2 | 100.83.200.83/31 | red-spine1 | Ethernet7/6/1 | 100.83.94.82/31 |
| red-leaf3 | Ethernet55 | 100.83.200.49/31 | red-spine1 | Ethernet3/32/2 | 100.83.94.48/31 |
| red-leaf3 | Ethernet56 | 100.83.200.51/31 | red-spine1 | Ethernet4/32/2 | 100.83.94.50/31 |
| red-leaf4 | Ethernet2/1 | 100.83.200.109/31 | red-spine1 | Ethernet6/7/1 | 100.83.94.108/31 |
| red-leaf4 | Ethernet2/2 | 100.83.200.113/31 | red-spine1 | Ethernet7/7/1 | 100.83.94.112/31 |
| red-leaf4 | Ethernet2/3 | 100.83.200.111/31 | red-spine1 | Ethernet6/8/1 | 100.83.94.110/31 |
| red-leaf5 | Ethernet53 | 100.83.200.199/31 | red-spine1 | Ethernet5/33/3 | 100.83.94.198/31 |
| red-leaf5 | Ethernet54 | 100.83.200.195/31 | red-spine1 | Ethernet3/32/3 | 100.83.94.194/31 |
| red-leaf5 | Ethernet55 | 100.83.200.197/31 | red-spine1 | Ethernet4/32/3 | 100.83.94.196/31 |
| red-leaf5 | Ethernet56 | 100.83.200.193/31 | red-spine1 | Ethernet3/31/4 | 100.83.94.192/31 |
| red-leaf6 | Ethernet2/1 | 100.83.200.123/31 | red-spine1 | Ethernet7/8/1 | 100.83.94.122/31 |
| red-leaf6 | Ethernet2/2 | 100.83.200.121/31 | red-spine1 | Ethernet6/9/1 | 100.83.94.120/31 |
| red-leaf7 | Ethernet2/1 | 100.83.200.147/31 | red-spine1 | Ethernet7/10/1 | 100.83.95.10/31 |
| red-leaf7 | Ethernet2/2 | 100.83.200.145/31 | red-spine1 | Ethernet6/21/1 | 100.83.95.8/31 |
| red-leaf8 | Ethernet2/1 | 100.83.200.171/31 | red-spine1 | Ethernet7/11/1 | 100.83.95.34/31 |
| red-leaf8 | Ethernet2/2 | 100.83.200.169/31 | red-spine1 | Ethernet6/22/1 | 100.83.95.32/31 |
| red-leaf9 | Ethernet2/1 | 100.83.200.195/31 | red-spine1 | Ethernet7/12/1 | 100.83.95.58/31 |
| red-leaf9 | Ethernet2/2 | 100.83.200.193/31 | red-spine1 | Ethernet6/23/1 | 100.83.95.56/31 |
| red-leaf10 | Ethernet2/1 | 100.83.200.219/31 | red-spine1 | Ethernet7/13/1 | 100.83.95.82/31 |
| red-leaf10 | Ethernet2/2 | 100.83.200.217/31 | red-spine1 | Ethernet6/24/1 | 100.83.95.80/31 |
| red-leaf11 | Ethernet2/1 | 100.83.200.243/31 | red-spine1 | Ethernet7/15/1 | 100.83.95.106/31 |
| red-leaf11 | Ethernet2/2 | 100.83.200.241/31 | red-spine1 | Ethernet6/25/1 | 100.83.95.104/31 |
| red-leaf12 | Ethernet2/1 | 100.83.201.11/31 | red-spine1 | Ethernet7/17/1 | 100.83.95.130/31 |
| red-leaf12 | Ethernet2/2 | 100.83.201.9/31 | red-spine1 | Ethernet6/26/1 | 100.83.95.128/31 |
| red-leaf13 | Ethernet2/1 | 100.83.201.35/31 | red-spine1 | Ethernet7/18/1 | 100.83.95.154/31 |
| red-leaf13 | Ethernet2/2 | 100.83.201.33/31 | red-spine1 | Ethernet6/27/1 | 100.83.95.152/31 |
| red-leaf14 | Ethernet2/1 | 100.83.201.59/31 | red-spine1 | Ethernet7/19/1 | 100.83.95.178/31 |
| red-leaf14 | Ethernet2/2 | 100.83.201.57/31 | red-spine1 | Ethernet6/28/1 | 100.83.95.176/31 |
| red-leaf15 | Ethernet2/1 | 100.83.201.83/31 | red-spine1 | Ethernet7/21/1 | 100.83.95.202/31 |
| red-leaf15 | Ethernet2/1 | 100.83.201.83/31 | red-spine1 | Ethernet7/23/1 | None |
| red-leaf15 | Ethernet2/2 | 100.83.201.81/31 | red-spine1 | Ethernet6/29/1 | 100.83.95.200/31 |
| red-leaf16 | Ethernet2/1 | 100.83.201.107/31 | red-spine1 | Ethernet7/21/1 | 100.83.95.202/31 |
| red-leaf16 | Ethernet2/2 | 100.83.201.105/31 | red-spine1 | Ethernet6/30/1 | None |
| red-leaf17 | Ethernet2/1 | 100.83.201.131/31 | red-spine1 | Ethernet9/21/1 | None |
| red-leaf17 | Ethernet2/2 | 100.83.201.129/31 | red-spine1 | Ethernet8/29/1 | None |
| red-leaf18 | Ethernet2/1 | 100.83.201.155/31 | red-spine1 | Ethernet9/23/1 | None |
| red-leaf18 | Ethernet2/2 | 100.83.201.153/31 | red-spine1 | Ethernet8/30/1 | None |
| red-leaf19 | Ethernet2/1 | 100.83.201.179/31 | red-spine1 | Ethernet9/25/1 | None |
| red-leaf19 | Ethernet2/2 | 100.83.201.177/31 | red-spine1 | Ethernet8/31/1 | None |
| red-leaf20 | Ethernet2/1 | 100.83.201.203/31 | red-spine1 | Ethernet9/27/1 | None |
| red-leaf20 | Ethernet2/2 | 100.83.201.201/31 | red-spine1 | Ethernet8/32/1 | None |
| red-leaf21 | Ethernet2/1 | 100.83.201.227/31 | red-spine1 | Ethernet9/29/1 | None |
| red-leaf21 | Ethernet2/2 | 100.83.201.225/31 | red-spine1 | Ethernet8/33/1 | None |
| red-leaf22 | Ethernet2/1 | 100.83.201.251/31 | red-spine1 | Ethernet9/31/1 | None |
| red-leaf22 | Ethernet2/2 | 100.83.201.249/31 | red-spine1 | Ethernet8/34/1 | None |
| red-leaf23 | Ethernet2/1 | 100.83.202.19/31 | red-spine1 | Ethernet9/33/1 | None |
| red-leaf23 | Ethernet2/2 | 100.83.202.17/31 | red-spine1 | Ethernet8/35/1 | None |
| red-leaf24 | Ethernet2/1 | 100.83.202.43/31 | red-spine1 | Ethernet9/35/1 | None |
| red-leaf24 | Ethernet2/2 | 100.83.202.41/31 | red-spine1 | Ethernet8/36/1 | None |
| red-leaf25 | Ethernet2/1 | 100.83.202.67/31 | red-spine1 | Ethernet9/37/1 | None |
| red-leaf25 | Ethernet2/2 | 100.83.202.65/31 | red-spine1 | Ethernet8/37/1 | None |
| red-leaf26 | Ethernet2/1 | 100.83.202.91/31 | red-spine1 | Ethernet9/39/1 | None |
| red-leaf26 | Ethernet2/2 | 100.83.202.89/31 | red-spine1 | Ethernet8/38/1 | None |
| red-leaf27 | Ethernet2/1 | 100.83.202.115/31 | red-spine1 | Ethernet9/41/1 | None |
| red-leaf27 | Ethernet2/2 | 100.83.202.113/31 | red-spine1 | Ethernet8/39/1 | None |
| red-leaf28 | Ethernet2/1 | 100.83.202.139/31 | red-spine1 | Ethernet9/43/1 | None |
| red-leaf28 | Ethernet2/2 | 100.83.202.137/31 | red-spine1 | Ethernet8/40/1 | None |
| red-leaf29 | Ethernet2/1 | 100.83.202.163/31 | red-spine1 | Ethernet9/45/1 | None |
| red-leaf29 | Ethernet2/2 | 100.83.202.161/31 | red-spine1 | Ethernet8/41/1 | None |
| red-leaf30 | Ethernet2/1 | 100.83.202.187/31 | red-spine1 | Ethernet9/47/1 | None |
| red-leaf30 | Ethernet2/2 | 100.83.202.185/31 | red-spine1 | Ethernet8/42/1 | None |
| red-leaf31 | Ethernet2/1 | 100.83.202.211/31 | red-spine1 | Ethernet9/49/1 | None |
| red-leaf31 | Ethernet2/2 | 100.83.202.209/31 | red-spine1 | Ethernet8/43/1 | None |
| red-leaf32 | Ethernet2/1 | 100.83.202.235/31 | red-spine1 | Ethernet9/51/1 | None |
| red-leaf32 | Ethernet2/2 | 100.83.202.233/31 | red-spine1 | Ethernet8/44/1 | None |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 169.27.195.0/25 | 128 | 44 | 34.38 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| FABRIC | blue-leaf1 | 169.27.195.34/32 |
| FABRIC | blue-leaf2 | 169.27.195.35/32 |
| FABRIC | blue-leaf3 | 169.27.195.36/32 |
| FABRIC | blue-leaf4 | 169.27.195.37/32 |
| FABRIC | blue-leaf5 | 169.27.195.38/32 |
| FABRIC | blue-leaf6 | 169.27.195.39/32 |
| FABRIC | blue-spine1 | 169.27.195.33/32 |
| FABRIC | border-leaf1 | 169.27.195.70/32 |
| FABRIC | border-leaf2 | 169.27.195.71/32 |
| FABRIC | media-PTP-1 | 169.27.195.72/32 |
| FABRIC | media-PTP-2 | 169.27.195.73/32 |
| FABRIC | red-leaf1 | 169.27.195.1/32 |
| FABRIC | red-leaf2 | 169.27.195.2/32 |
| FABRIC | red-leaf3 | 169.27.195.3/32 |
| FABRIC | red-leaf4 | 169.27.195.4/32 |
| FABRIC | red-leaf5 | 169.27.195.5/32 |
| FABRIC | red-leaf6 | 169.27.195.6/32 |
| FABRIC | red-leaf7 | 169.27.195.8/32 |
| FABRIC | red-leaf8 | 169.27.195.9/32 |
| FABRIC | red-leaf9 | 169.27.195.10/32 |
| FABRIC | red-leaf10 | 169.27.195.11/32 |
| FABRIC | red-leaf11 | 169.27.195.12/32 |
| FABRIC | red-leaf12 | 169.27.195.13/32 |
| FABRIC | red-leaf13 | 169.27.195.14/32 |
| FABRIC | red-leaf14 | 169.27.195.15/32 |
| FABRIC | red-leaf15 | 169.27.195.16/32 |
| FABRIC | red-leaf16 | 169.27.195.17/32 |
| FABRIC | red-leaf17 | 169.27.195.18/32 |
| FABRIC | red-leaf18 | 169.27.195.19/32 |
| FABRIC | red-leaf19 | 169.27.195.20/32 |
| FABRIC | red-leaf20 | 169.27.195.21/32 |
| FABRIC | red-leaf21 | 169.27.195.22/32 |
| FABRIC | red-leaf22 | 169.27.195.23/32 |
| FABRIC | red-leaf23 | 169.27.195.24/32 |
| FABRIC | red-leaf24 | 169.27.195.25/32 |
| FABRIC | red-leaf25 | 169.27.195.26/32 |
| FABRIC | red-leaf26 | 169.27.195.27/32 |
| FABRIC | red-leaf27 | 169.27.195.28/32 |
| FABRIC | red-leaf28 | 169.27.195.29/32 |
| FABRIC | red-leaf29 | 169.27.195.30/32 |
| FABRIC | red-leaf30 | 169.27.195.31/32 |
| FABRIC | red-leaf31 | 169.27.195.32/32 |
| FABRIC | red-leaf32 | 169.27.195.33/32 |
| FABRIC | red-spine1 | 169.27.195.0/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------ | ------------------- | ------------------ | ------------------ |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
