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
| FABRIC | l2leaf | green-leaf1 | 10.100.100.72/24 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf2 | 10.100.100.73/24 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf3 | 10.100.100.74/24 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf4 | 10.100.100.75/24 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf5 | 10.100.100.76/24 | 720XP | Provisioned | - |
| FABRIC | l3spine | green-spine1 | 10.100.100.70/24 | 7308X3 | Provisioned | - |
| FABRIC | l3spine | green-spine2 | 10.100.100.71/24 | 7308X3 | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |
| FABRIC | l2leaf | green-leaf1 | 10.239.1.76/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf2 | 10.239.1.77/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf3 | 10.239.1.78/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf4 | 10.239.1.79/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf5 | 10.239.1.80/24 | Vlan113 |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l2leaf | green-leaf1 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/5/1 |
| l2leaf | green-leaf1 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/5/1 |
| l2leaf | green-leaf2 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/6/1 |
| l2leaf | green-leaf2 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/6/1 |
| l2leaf | green-leaf3 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/7/1 |
| l2leaf | green-leaf3 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/7/1 |
| l2leaf | green-leaf4 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/8/1 |
| l2leaf | green-leaf4 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/8/1 |
| l2leaf | green-leaf5 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/9/1 |
| l2leaf | green-leaf5 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/9/1 |
| l3spine | green-spine1 | Ethernet8/31/1 | mlag_peer | green-spine2 | Ethernet8/31/1 |
| l3spine | green-spine1 | Ethernet8/32/1 | mlag_peer | green-spine2 | Ethernet8/32/1 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 169.27.195.0/25 | 128 | 2 | 1.57 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| FABRIC | green-spine1 | 169.27.195.71/32 |
| FABRIC | green-spine2 | 169.27.195.72/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------ | ------------------- | ------------------ | ------------------ |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
