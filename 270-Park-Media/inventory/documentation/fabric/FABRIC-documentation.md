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
| FABRIC | media_leaf | blue-leaf1 | 10.100.100.5/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf2 | 10.100.100.6/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf3 | 10.100.100.7/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf4 | 10.100.100.8/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf5 | 10.100.100.9/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf6 | 10.100.100.10/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf7 | 10.100.100.11/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf8 | 10.100.100.12/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf9 | 10.100.100.13/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf10 | 10.100.100.14/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf11 | 10.100.100.15/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf12 | 10.100.100.16/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf13 | 10.100.100.17/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf14 | 10.100.100.18/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf15 | 10.100.100.19/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf16 | 10.100.100.20/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf17 | 10.100.100.21/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf18 | 10.100.100.22/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf19 | 10.100.100.23/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf20 | 10.100.100.24/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf21 | 10.100.100.25/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf22 | 10.100.100.26/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf23 | 10.100.100.27/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf24 | 10.100.100.28/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf25 | 10.100.100.29/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf26 | 10.100.100.30/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf27 | 10.100.100.31/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf28 | 10.100.100.32/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf29 | 10.100.100.33/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf30 | 10.100.100.34/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf31 | 10.100.100.35/24 | 720XP | Provisioned | - |
| FABRIC | media_leaf | blue-leaf32 | 10.100.100.36/24 | 720XP | Provisioned | - |
| FABRIC | media_spine | blue-spine1 | 10.100.100.4/24 | 7808R3 | Provisioned | - |
| FABRIC | border_leaf | border-leaf1 | 10.100.101.4/24 | 7280CR3 | Provisioned | - |
| FABRIC | border_leaf | border-leaf2 | 10.100.101.5/24 | 7280CR3 | Provisioned | - |
| FABRIC | ptp_leaf | media-PTP-1 | 10.100.101.2/24 | 7280SR3 | Provisioned | - |
| FABRIC | ptp_leaf | media-PTP-2 | 10.100.100.3/24 | 7280SR3 | Provisioned | - |
| FABRIC | media_leaf | red-leaf1 | 10.100.100.38/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf2 | 10.100.100.39/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf3 | 10.100.100.40/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf4 | 10.100.100.41/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf5 | 10.100.100.42/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf6 | 10.100.100.43/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf7 | 10.100.100.44/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf8 | 10.100.100.45/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf9 | 10.100.100.46/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf10 | 10.100.100.47/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf11 | 10.100.100.48/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf12 | 10.100.100.49/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf13 | 10.100.100.50/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf14 | 10.100.100.51/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf15 | 10.100.100.52/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf16 | 10.100.100.53/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf17 | 10.100.100.54/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf18 | 10.100.100.55/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf19 | 10.100.100.56/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf20 | 10.100.100.57/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf21 | 10.100.100.58/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf22 | 10.100.100.59/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf23 | 10.100.100.60/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf24 | 10.100.100.61/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf25 | 10.100.100.62/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf26 | 10.100.100.63/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf27 | 10.100.100.64/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf28 | 10.100.100.65/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf29 | 10.100.100.66/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf30 | 10.100.100.67/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf31 | 10.100.100.68/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_leaf | red-leaf32 | 10.100.100.69/24 | vEOS-lab | Provisioned | - |
| FABRIC | media_spine | red-spine1 | 10.100.100.37/24 | 7808R3 | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| media_leaf | blue-leaf1 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet4/11/1 |
| media_leaf | blue-leaf1 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet4/12/1 |
| media_leaf | blue-leaf2 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet4/13/1 |
| media_leaf | blue-leaf2 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet4/14/1 |
| media_leaf | blue-leaf3 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet4/15/1 |
| media_leaf | blue-leaf3 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet4/16/1 |
| media_leaf | blue-leaf4 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet4/17/1 |
| media_leaf | blue-leaf4 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet4/18/1 |
| media_leaf | blue-leaf5 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet4/19/1 |
| media_leaf | blue-leaf5 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet4/20/1 |
| media_leaf | blue-leaf6 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet4/21/1 |
| media_leaf | blue-leaf6 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet4/22/1 |
| media_leaf | blue-leaf7 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet4/23/1 |
| media_leaf | blue-leaf7 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet4/24/1 |
| media_leaf | blue-leaf8 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet4/25/1 |
| media_leaf | blue-leaf8 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet4/26/1 |
| media_leaf | blue-leaf9 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet4/27/1 |
| media_leaf | blue-leaf9 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet4/28/1 |
| media_leaf | blue-leaf10 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet4/29/1 |
| media_leaf | blue-leaf10 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet4/30/1 |
| media_leaf | blue-leaf11 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet4/31/1 |
| media_leaf | blue-leaf11 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet4/32/1 |
| media_leaf | blue-leaf12 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet4/33/1 |
| media_leaf | blue-leaf12 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet4/34/1 |
| media_leaf | blue-leaf13 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet4/35/1 |
| media_leaf | blue-leaf13 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet4/36/1 |
| media_leaf | blue-leaf14 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/1/1 |
| media_leaf | blue-leaf14 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/2/1 |
| media_leaf | blue-leaf15 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/3/1 |
| media_leaf | blue-leaf15 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/4/1 |
| media_leaf | blue-leaf16 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/5/1 |
| media_leaf | blue-leaf16 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/6/1 |
| media_leaf | blue-leaf17 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/7/1 |
| media_leaf | blue-leaf17 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/8/1 |
| media_leaf | blue-leaf18 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/9/1 |
| media_leaf | blue-leaf18 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/10/1 |
| media_leaf | blue-leaf19 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/11/1 |
| media_leaf | blue-leaf19 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/12/1 |
| media_leaf | blue-leaf20 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/13/1 |
| media_leaf | blue-leaf20 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/14/1 |
| media_leaf | blue-leaf21 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/15/1 |
| media_leaf | blue-leaf21 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/16/1 |
| media_leaf | blue-leaf22 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/17/1 |
| media_leaf | blue-leaf22 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/18/1 |
| media_leaf | blue-leaf23 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/19/1 |
| media_leaf | blue-leaf23 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/20/1 |
| media_leaf | blue-leaf24 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/21/1 |
| media_leaf | blue-leaf24 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/22/1 |
| media_leaf | blue-leaf25 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/23/1 |
| media_leaf | blue-leaf25 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/24/1 |
| media_leaf | blue-leaf26 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/25/1 |
| media_leaf | blue-leaf26 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/26/1 |
| media_leaf | blue-leaf27 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/27/1 |
| media_leaf | blue-leaf27 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/28/1 |
| media_leaf | blue-leaf28 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/29/1 |
| media_leaf | blue-leaf28 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/30/1 |
| media_leaf | blue-leaf29 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/31/1 |
| media_leaf | blue-leaf29 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/32/1 |
| media_leaf | blue-leaf30 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/33/1 |
| media_leaf | blue-leaf30 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/34/1 |
| media_leaf | blue-leaf31 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet5/35/1 |
| media_leaf | blue-leaf31 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet5/36/1 |
| media_leaf | blue-leaf32 | Ethernet49/1 | media_spine | blue-spine1 | Ethernet6/1/1 |
| media_leaf | blue-leaf32 | Ethernet50/1 | media_spine | blue-spine1 | Ethernet6/2/1 |
| media_spine | blue-spine1 | Ethernet33/1 | border_leaf | border-leaf1 | Ethernet34/1 |
| media_spine | blue-spine1 | Ethernet34/1 | border_leaf | border-leaf2 | Ethernet34/1 |
| media_spine | blue-spine1 | Ethernet49/1 | ptp_leaf | media-PTP-1 | Ethernet50/1 |
| media_spine | blue-spine1 | Ethernet50/1 | ptp_leaf | media-PTP-2 | Ethernet50/1 |
| border_leaf | border-leaf1 | Ethernet3/3/1 | border_leaf | border-leaf2 | Ethernet3/3/1 |
| border_leaf | border-leaf1 | Ethernet3/4/1 | border_leaf | border-leaf2 | Ethernet3/4/1 |
| border_leaf | border-leaf1 | Ethernet33/1 | media_spine | red-spine1 | Ethernet33/1 |
| border_leaf | border-leaf2 | Ethernet33/1 | media_spine | red-spine1 | Ethernet34/1 |
| ptp_leaf | media-PTP-1 | Ethernet3/1/1 | ptp_leaf | media-PTP-2 | Ethernet3/1/1 |
| ptp_leaf | media-PTP-1 | Ethernet3/2/1 | ptp_leaf | media-PTP-2 | Ethernet3/2/1 |
| ptp_leaf | media-PTP-1 | Ethernet49/1 | media_spine | red-spine1 | Ethernet49/1 |
| ptp_leaf | media-PTP-2 | Ethernet49/1 | media_spine | red-spine1 | Ethernet50/1 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 100.83.88.0/23 | 512 | 144 | 28.13 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| blue-leaf1 | Ethernet49/1 | 100.83.88.41/31 | blue-spine1 | Ethernet4/11/1 | 100.83.88.40/31 |
| blue-leaf1 | Ethernet50/1 | 100.83.88.43/31 | blue-spine1 | Ethernet4/12/1 | 100.83.88.42/31 |
| blue-leaf2 | Ethernet49/1 | 100.83.88.49/31 | blue-spine1 | Ethernet4/13/1 | 100.83.88.48/31 |
| blue-leaf2 | Ethernet50/1 | 100.83.88.51/31 | blue-spine1 | Ethernet4/14/1 | 100.83.88.50/31 |
| blue-leaf3 | Ethernet49/1 | 100.83.88.57/31 | blue-spine1 | Ethernet4/15/1 | 100.83.88.56/31 |
| blue-leaf3 | Ethernet50/1 | 100.83.88.59/31 | blue-spine1 | Ethernet4/16/1 | 100.83.88.58/31 |
| blue-leaf4 | Ethernet49/1 | 100.83.88.65/31 | blue-spine1 | Ethernet4/17/1 | 100.83.88.64/31 |
| blue-leaf4 | Ethernet50/1 | 100.83.88.67/31 | blue-spine1 | Ethernet4/18/1 | 100.83.88.66/31 |
| blue-leaf5 | Ethernet49/1 | 100.83.88.73/31 | blue-spine1 | Ethernet4/19/1 | 100.83.88.72/31 |
| blue-leaf5 | Ethernet50/1 | 100.83.88.75/31 | blue-spine1 | Ethernet4/20/1 | 100.83.88.74/31 |
| blue-leaf6 | Ethernet49/1 | 100.83.88.81/31 | blue-spine1 | Ethernet4/21/1 | 100.83.88.80/31 |
| blue-leaf6 | Ethernet50/1 | 100.83.88.83/31 | blue-spine1 | Ethernet4/22/1 | 100.83.88.82/31 |
| blue-leaf7 | Ethernet49/1 | 100.83.88.89/31 | blue-spine1 | Ethernet4/23/1 | 100.83.88.88/31 |
| blue-leaf7 | Ethernet50/1 | 100.83.88.91/31 | blue-spine1 | Ethernet4/24/1 | 100.83.88.90/31 |
| blue-leaf8 | Ethernet49/1 | 100.83.88.97/31 | blue-spine1 | Ethernet4/25/1 | 100.83.88.96/31 |
| blue-leaf8 | Ethernet50/1 | 100.83.88.99/31 | blue-spine1 | Ethernet4/26/1 | 100.83.88.98/31 |
| blue-leaf9 | Ethernet49/1 | 100.83.88.105/31 | blue-spine1 | Ethernet4/27/1 | 100.83.88.104/31 |
| blue-leaf9 | Ethernet50/1 | 100.83.88.107/31 | blue-spine1 | Ethernet4/28/1 | 100.83.88.106/31 |
| blue-leaf10 | Ethernet49/1 | 100.83.88.113/31 | blue-spine1 | Ethernet4/29/1 | 100.83.88.112/31 |
| blue-leaf10 | Ethernet50/1 | 100.83.88.115/31 | blue-spine1 | Ethernet4/30/1 | 100.83.88.114/31 |
| blue-leaf11 | Ethernet49/1 | 100.83.88.121/31 | blue-spine1 | Ethernet4/31/1 | 100.83.88.120/31 |
| blue-leaf11 | Ethernet50/1 | 100.83.88.123/31 | blue-spine1 | Ethernet4/32/1 | 100.83.88.122/31 |
| blue-leaf12 | Ethernet49/1 | 100.83.88.129/31 | blue-spine1 | Ethernet4/33/1 | 100.83.88.128/31 |
| blue-leaf12 | Ethernet50/1 | 100.83.88.131/31 | blue-spine1 | Ethernet4/34/1 | 100.83.88.130/31 |
| blue-leaf13 | Ethernet49/1 | 100.83.88.137/31 | blue-spine1 | Ethernet4/35/1 | 100.83.88.136/31 |
| blue-leaf13 | Ethernet50/1 | 100.83.88.139/31 | blue-spine1 | Ethernet4/36/1 | 100.83.88.138/31 |
| blue-leaf14 | Ethernet49/1 | 100.83.88.145/31 | blue-spine1 | Ethernet5/1/1 | 100.83.88.144/31 |
| blue-leaf14 | Ethernet50/1 | 100.83.88.147/31 | blue-spine1 | Ethernet5/2/1 | 100.83.88.146/31 |
| blue-leaf15 | Ethernet49/1 | 100.83.88.153/31 | blue-spine1 | Ethernet5/3/1 | 100.83.88.152/31 |
| blue-leaf15 | Ethernet50/1 | 100.83.88.155/31 | blue-spine1 | Ethernet5/4/1 | 100.83.88.154/31 |
| blue-leaf16 | Ethernet49/1 | 100.83.88.161/31 | blue-spine1 | Ethernet5/5/1 | 100.83.88.160/31 |
| blue-leaf16 | Ethernet50/1 | 100.83.88.163/31 | blue-spine1 | Ethernet5/6/1 | 100.83.88.162/31 |
| blue-leaf17 | Ethernet49/1 | 100.83.88.169/31 | blue-spine1 | Ethernet5/7/1 | 100.83.88.168/31 |
| blue-leaf17 | Ethernet50/1 | 100.83.88.171/31 | blue-spine1 | Ethernet5/8/1 | 100.83.88.170/31 |
| blue-leaf18 | Ethernet49/1 | 100.83.88.177/31 | blue-spine1 | Ethernet5/9/1 | 100.83.88.176/31 |
| blue-leaf18 | Ethernet50/1 | 100.83.88.179/31 | blue-spine1 | Ethernet5/10/1 | 100.83.88.178/31 |
| blue-leaf19 | Ethernet49/1 | 100.83.88.185/31 | blue-spine1 | Ethernet5/11/1 | 100.83.88.184/31 |
| blue-leaf19 | Ethernet50/1 | 100.83.88.187/31 | blue-spine1 | Ethernet5/12/1 | 100.83.88.186/31 |
| blue-leaf20 | Ethernet49/1 | 100.83.88.193/31 | blue-spine1 | Ethernet5/13/1 | 100.83.88.192/31 |
| blue-leaf20 | Ethernet50/1 | 100.83.88.195/31 | blue-spine1 | Ethernet5/14/1 | 100.83.88.194/31 |
| blue-leaf21 | Ethernet49/1 | 100.83.88.201/31 | blue-spine1 | Ethernet5/15/1 | 100.83.88.200/31 |
| blue-leaf21 | Ethernet50/1 | 100.83.88.203/31 | blue-spine1 | Ethernet5/16/1 | 100.83.88.202/31 |
| blue-leaf22 | Ethernet49/1 | 100.83.88.209/31 | blue-spine1 | Ethernet5/17/1 | 100.83.88.208/31 |
| blue-leaf22 | Ethernet50/1 | 100.83.88.211/31 | blue-spine1 | Ethernet5/18/1 | 100.83.88.210/31 |
| blue-leaf23 | Ethernet49/1 | 100.83.88.217/31 | blue-spine1 | Ethernet5/19/1 | 100.83.88.216/31 |
| blue-leaf23 | Ethernet50/1 | 100.83.88.219/31 | blue-spine1 | Ethernet5/20/1 | 100.83.88.218/31 |
| blue-leaf24 | Ethernet49/1 | 100.83.88.225/31 | blue-spine1 | Ethernet5/21/1 | 100.83.88.224/31 |
| blue-leaf24 | Ethernet50/1 | 100.83.88.227/31 | blue-spine1 | Ethernet5/22/1 | 100.83.88.226/31 |
| blue-leaf25 | Ethernet49/1 | 100.83.88.233/31 | blue-spine1 | Ethernet5/23/1 | 100.83.88.232/31 |
| blue-leaf25 | Ethernet50/1 | 100.83.88.235/31 | blue-spine1 | Ethernet5/24/1 | 100.83.88.234/31 |
| blue-leaf26 | Ethernet49/1 | 100.83.88.241/31 | blue-spine1 | Ethernet5/25/1 | 100.83.88.240/31 |
| blue-leaf26 | Ethernet50/1 | 100.83.88.243/31 | blue-spine1 | Ethernet5/26/1 | 100.83.88.242/31 |
| blue-leaf27 | Ethernet49/1 | 100.83.88.249/31 | blue-spine1 | Ethernet5/27/1 | 100.83.88.248/31 |
| blue-leaf27 | Ethernet50/1 | 100.83.88.251/31 | blue-spine1 | Ethernet5/28/1 | 100.83.88.250/31 |
| blue-leaf28 | Ethernet49/1 | 100.83.89.1/31 | blue-spine1 | Ethernet5/29/1 | 100.83.89.0/31 |
| blue-leaf28 | Ethernet50/1 | 100.83.89.3/31 | blue-spine1 | Ethernet5/30/1 | 100.83.89.2/31 |
| blue-leaf29 | Ethernet49/1 | 100.83.89.9/31 | blue-spine1 | Ethernet5/31/1 | 100.83.89.8/31 |
| blue-leaf29 | Ethernet50/1 | 100.83.89.11/31 | blue-spine1 | Ethernet5/32/1 | 100.83.89.10/31 |
| blue-leaf30 | Ethernet49/1 | 100.83.89.17/31 | blue-spine1 | Ethernet5/33/1 | 100.83.89.16/31 |
| blue-leaf30 | Ethernet50/1 | 100.83.89.19/31 | blue-spine1 | Ethernet5/34/1 | 100.83.89.18/31 |
| blue-leaf31 | Ethernet49/1 | 100.83.89.25/31 | blue-spine1 | Ethernet5/35/1 | 100.83.89.24/31 |
| blue-leaf31 | Ethernet50/1 | 100.83.89.27/31 | blue-spine1 | Ethernet5/36/1 | 100.83.89.26/31 |
| blue-leaf32 | Ethernet49/1 | 100.83.89.33/31 | blue-spine1 | Ethernet6/1/1 | 100.83.89.32/31 |
| blue-leaf32 | Ethernet50/1 | 100.83.89.35/31 | blue-spine1 | Ethernet6/2/1 | 100.83.89.34/31 |
| blue-spine1 | Ethernet33/1 | 100.83.88.18/31 | border-leaf1 | Ethernet34/1 | 100.83.88.19/31 |
| blue-spine1 | Ethernet34/1 | 100.83.88.26/31 | border-leaf2 | Ethernet34/1 | 100.83.88.27/31 |
| blue-spine1 | Ethernet49/1 | 100.83.88.2/31 | media-PTP-1 | Ethernet50/1 | 100.83.88.3/31 |
| blue-spine1 | Ethernet50/1 | 100.83.88.10/31 | media-PTP-2 | Ethernet50/1 | 100.83.88.11/31 |
| border-leaf1 | Ethernet33/1 | 100.83.88.17/31 | red-spine1 | Ethernet33/1 | 100.83.88.16/31 |
| border-leaf2 | Ethernet33/1 | 100.83.88.25/31 | red-spine1 | Ethernet34/1 | 100.83.88.24/31 |
| media-PTP-1 | Ethernet49/1 | 100.83.88.1/31 | red-spine1 | Ethernet49/1 | 100.83.88.0/31 |
| media-PTP-2 | Ethernet49/1 | 100.83.88.9/31 | red-spine1 | Ethernet50/1 | 100.83.88.8/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 169.27.195.0/25 | 128 | 70 | 54.69 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| FABRIC | blue-leaf1 | 169.27.195.7/32 |
| FABRIC | blue-leaf2 | 169.27.195.8/32 |
| FABRIC | blue-leaf3 | 169.27.195.9/32 |
| FABRIC | blue-leaf4 | 169.27.195.10/32 |
| FABRIC | blue-leaf5 | 169.27.195.11/32 |
| FABRIC | blue-leaf6 | 169.27.195.12/32 |
| FABRIC | blue-leaf7 | 169.27.195.13/32 |
| FABRIC | blue-leaf8 | 169.27.195.14/32 |
| FABRIC | blue-leaf9 | 169.27.195.15/32 |
| FABRIC | blue-leaf10 | 169.27.195.16/32 |
| FABRIC | blue-leaf11 | 169.27.195.17/32 |
| FABRIC | blue-leaf12 | 169.27.195.18/32 |
| FABRIC | blue-leaf13 | 169.27.195.19/32 |
| FABRIC | blue-leaf14 | 169.27.195.20/32 |
| FABRIC | blue-leaf15 | 169.27.195.21/32 |
| FABRIC | blue-leaf16 | 169.27.195.22/32 |
| FABRIC | blue-leaf17 | 169.27.195.23/32 |
| FABRIC | blue-leaf18 | 169.27.195.24/32 |
| FABRIC | blue-leaf19 | 169.27.195.25/32 |
| FABRIC | blue-leaf20 | 169.27.195.26/32 |
| FABRIC | blue-leaf21 | 169.27.195.27/32 |
| FABRIC | blue-leaf22 | 169.27.195.28/32 |
| FABRIC | blue-leaf23 | 169.27.195.29/32 |
| FABRIC | blue-leaf24 | 169.27.195.30/32 |
| FABRIC | blue-leaf25 | 169.27.195.31/32 |
| FABRIC | blue-leaf26 | 169.27.195.32/32 |
| FABRIC | blue-leaf27 | 169.27.195.33/32 |
| FABRIC | blue-leaf28 | 169.27.195.34/32 |
| FABRIC | blue-leaf29 | 169.27.195.35/32 |
| FABRIC | blue-leaf30 | 169.27.195.36/32 |
| FABRIC | blue-leaf31 | 169.27.195.37/32 |
| FABRIC | blue-leaf32 | 169.27.195.38/32 |
| FABRIC | blue-spine1 | 169.27.195.1/32 |
| FABRIC | border-leaf1 | 169.27.195.3/32 |
| FABRIC | border-leaf2 | 169.27.195.4/32 |
| FABRIC | media-PTP-1 | 169.27.195.1/32 |
| FABRIC | media-PTP-2 | 169.27.195.2/32 |
| FABRIC | red-leaf1 | 169.27.195.40/32 |
| FABRIC | red-leaf2 | 169.27.195.41/32 |
| FABRIC | red-leaf3 | 169.27.195.42/32 |
| FABRIC | red-leaf4 | 169.27.195.43/32 |
| FABRIC | red-leaf5 | 169.27.195.44/32 |
| FABRIC | red-leaf6 | 169.27.195.45/32 |
| FABRIC | red-leaf7 | 169.27.195.46/32 |
| FABRIC | red-leaf8 | 169.27.195.47/32 |
| FABRIC | red-leaf9 | 169.27.195.48/32 |
| FABRIC | red-leaf10 | 169.27.195.49/32 |
| FABRIC | red-leaf11 | 169.27.195.50/32 |
| FABRIC | red-leaf12 | 169.27.195.51/32 |
| FABRIC | red-leaf13 | 169.27.195.52/32 |
| FABRIC | red-leaf14 | 169.27.195.53/32 |
| FABRIC | red-leaf15 | 169.27.195.54/32 |
| FABRIC | red-leaf16 | 169.27.195.55/32 |
| FABRIC | red-leaf17 | 169.27.195.56/32 |
| FABRIC | red-leaf18 | 169.27.195.57/32 |
| FABRIC | red-leaf19 | 169.27.195.58/32 |
| FABRIC | red-leaf20 | 169.27.195.59/32 |
| FABRIC | red-leaf21 | 169.27.195.60/32 |
| FABRIC | red-leaf22 | 169.27.195.61/32 |
| FABRIC | red-leaf23 | 169.27.195.62/32 |
| FABRIC | red-leaf24 | 169.27.195.63/32 |
| FABRIC | red-leaf25 | 169.27.195.64/32 |
| FABRIC | red-leaf26 | 169.27.195.65/32 |
| FABRIC | red-leaf27 | 169.27.195.66/32 |
| FABRIC | red-leaf28 | 169.27.195.67/32 |
| FABRIC | red-leaf29 | 169.27.195.68/32 |
| FABRIC | red-leaf30 | 169.27.195.69/32 |
| FABRIC | red-leaf31 | 169.27.195.70/32 |
| FABRIC | red-leaf32 | 169.27.195.71/32 |
| FABRIC | red-spine1 | 169.27.195.1/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------ | ------------------- | ------------------ | ------------------ |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
