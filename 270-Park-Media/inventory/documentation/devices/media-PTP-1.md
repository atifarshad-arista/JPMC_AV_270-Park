# media-PTP-1

## Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [IP Name Servers](#ip-name-servers)
  - [NTP](#ntp)
  - [PTP](#ptp)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
  - [Enable Password](#enable-password)
  - [AAA Authentication](#aaa-authentication)
  - [AAA Authorization](#aaa-authorization)
- [Monitoring](#monitoring)
  - [TerminAttr Daemon](#terminattr-daemon)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Device Configuration](#internal-vlan-allocation-policy-device-configuration)
- [VLANs](#vlans)
  - [VLANs Summary](#vlans-summary)
  - [VLANs Device Configuration](#vlans-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
  - [VLAN Interfaces](#vlan-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router BGP](#router-bgp)
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
  - [Router Multicast](#router-multicast)
  - [PIM Sparse Mode](#pim-sparse-mode)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)

## Management

### Management Interfaces

#### Management Interfaces Summary

##### IPv4

| Management Interface | Description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Ethernet0 | OOB_MANAGEMENT | oob | MGMT | 172.16.3.101/24 | 172.16.1.1 |

##### IPv6

| Management Interface | Description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Ethernet0 | OOB_MANAGEMENT | oob | MGMT | - | - |

#### Management Interfaces Device Configuration

```eos
!
interface Ethernet0
   description OOB_MANAGEMENT
   no shutdown
   vrf MGMT
   ip address 172.16.3.101/24
```

### IP Name Servers

#### IP Name Servers Summary

| Name Server | VRF | Priority |
| ----------- | --- | -------- |
| 192.168.1.1 | MGMT | - |

#### IP Name Servers Device Configuration

```eos
ip name-server vrf MGMT 192.168.1.1
```

### NTP

#### NTP Summary

##### NTP Local Interface

| Interface | VRF |
| --------- | --- |
| Management1 | MGMT |

##### NTP Servers

| Server | VRF | Preferred | Burst | iBurst | Version | Min Poll | Max Poll | Local-interface | Key |
| ------ | --- | --------- | ----- | ------ | ------- | -------- | -------- | --------------- | --- |
| 0.pool.ntp.org | MGMT | - | - | - | - | - | - | - | - |

#### NTP Device Configuration

```eos
!
ntp local-interface vrf MGMT Management1
ntp server vrf MGMT 0.pool.ntp.org
```

### PTP
#### PTP Summary

| Clock ID | Source IP | Priority 1 | Priority 2 | TTL | Domain | Mode | Forward Unicast |
| -------- | --------- | ---------- | ---------- | --- | ------ | ---- | --------------- |
| 00:1C:73:0a:00:01 | - | 10 | 1 | - | 127 | boundary | - |

#### PTP Device Configuration

```eos
!
ptp clock-identity 00:1C:73:0a:00:01
ptp domain 127
ptp mode boundary
ptp priority1 10
ptp priority2 1
ptp monitor threshold offset-from-master 250
ptp monitor threshold mean-path-delay 1500
ptp monitor sequence-id
ptp monitor threshold missing-message sync 3 sequence-ids
ptp monitor threshold missing-message follow-up 3 sequence-ids
ptp monitor threshold missing-message delay-resp 3 sequence-ids
ptp monitor threshold missing-message announce 3 sequence-ids
```

### Management API HTTP

#### Management API HTTP Summary

| HTTP | HTTPS | Default Services |
| ---- | ----- | ---------------- |
| False | True | - |

#### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| MGMT | - | - |

#### Management API HTTP Device Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf MGMT
      no shutdown
```

## Authentication

### Local Users

#### Local Users Summary

| User | Privilege | Role | Disabled | Shell |
| ---- | --------- | ---- | -------- | ----- |
| admin | 15 | network-admin | False | - |
| ansible | 15 | network-admin | False | - |

#### Local Users Device Configuration

```eos
!
username admin privilege 15 role network-admin nopassword
username ansible privilege 15 role network-admin secret sha512 <removed>
```

### Enable Password

Enable password has been disabled

### AAA Authentication

#### AAA Authentication Summary

| Type | Sub-type | User Stores |
| ---- | -------- | ---------- |
| Login | default | local |

#### AAA Authentication Device Configuration

```eos
aaa authentication login default local
!
```

### AAA Authorization

#### AAA Authorization Summary

| Type | User Stores |
| ---- | ----------- |
| Exec | local |

Authorization for configuration commands is disabled.

#### AAA Authorization Device Configuration

```eos
aaa authorization exec default local
!
```

## Monitoring

### TerminAttr Daemon

#### TerminAttr Daemon Summary

| CV Compression | CloudVision Servers | VRF | Authentication | Smash Excludes | Ingest Exclude | Bypass AAA |
| -------------- | ------------------- | --- | -------------- | -------------- | -------------- | ---------- |
| gzip | 192.168.1.12:9910 | MGMT | token,/tmp/token | ale,flexCounter,hardware,kni,pulse,strata | /Sysdb/cell/1/agent,/Sysdb/cell/2/agent | True |

#### TerminAttr Daemon Device Configuration

```eos
!
daemon TerminAttr
   exec /usr/bin/TerminAttr -cvaddr=192.168.1.12:9910 -cvauth=token,/tmp/token -cvvrf=MGMT -disableaaa -smashexcludes=ale,flexCounter,hardware,kni,pulse,strata -ingestexclude=/Sysdb/cell/1/agent,/Sysdb/cell/2/agent -taillogs
   no shutdown
```

## Spanning Tree

### Spanning Tree Summary

STP mode: **mstp**

#### MSTP Instance and Priority

| Instance(s) | Priority |
| -------- | -------- |
| 0 | 4096 |

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode mstp
spanning-tree mst 0 priority 4096
```

## Internal VLAN Allocation Policy

### Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

### Internal VLAN Allocation Policy Device Configuration

```eos
!
vlan internal order ascending range 1006 1199
```

## VLANs

### VLANs Summary

| VLAN ID | Name | Trunk Groups |
| ------- | ---- | ------------ |
| 131 | VLAN131 | - |

### VLANs Device Configuration

```eos
!
vlan 131
   name VLAN131
```

## Interfaces

### Ethernet Interfaces

#### Ethernet Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |
| Ethernet5 | PTP Grandmaster 1 | access | 131 | - | - | - |
| Ethernet6 | Routed Endpoints | - | - | - | - | - |
| Ethernet7 | Routed Endpoints | - | - | - | - | - |
| Ethernet8 | Routed Endpoints | - | - | - | - | - |
| Ethernet9 | Routed Endpoints | - | - | - | - | - |
| Ethernet10 | Routed Endpoints | - | - | - | - | - |
| Ethernet11 | Routed Endpoints | - | - | - | - | - |
| Ethernet12 | Routed Endpoints | - | - | - | - | - |
| Ethernet13 | Routed Endpoints | - | - | - | - | - |
| Ethernet14 | Routed Endpoints | - | - | - | - | - |
| Ethernet15 | Routed Endpoints | - | - | - | - | - |
| Ethernet16 | Routed Endpoints | - | - | - | - | - |
| Ethernet17 | Routed Endpoints | - | - | - | - | - |
| Ethernet18 | Routed Endpoints | - | - | - | - | - |
| Ethernet19 | Routed Endpoints | - | - | - | - | - |
| Ethernet20 | Routed Endpoints | - | - | - | - | - |
| Ethernet21 | Routed Endpoints | - | - | - | - | - |
| Ethernet22 | Routed Endpoints | - | - | - | - | - |
| Ethernet23 | Routed Endpoints | - | - | - | - | - |
| Ethernet24 | Routed Endpoints | - | - | - | - | - |
| Ethernet25 | Routed Endpoints | - | - | - | - | - |
| Ethernet26 | Routed Endpoints | - | - | - | - | - |
| Ethernet27 | Routed Endpoints | - | - | - | - | - |
| Ethernet28 | Routed Endpoints | - | - | - | - | - |
| Ethernet29 | Routed Endpoints | - | - | - | - | - |
| Ethernet30 | Routed Endpoints | - | - | - | - | - |
| Ethernet31 | Routed Endpoints | - | - | - | - | - |
| Ethernet32 | Routed Endpoints | - | - | - | - | - |
| Ethernet33 | Routed Endpoints | - | - | - | - | - |
| Ethernet34 | Routed Endpoints | - | - | - | - | - |
| Ethernet35 | Routed Endpoints | - | - | - | - | - |
| Ethernet36 | Routed Endpoints | - | - | - | - | - |
| Ethernet37 | Routed Endpoints | - | - | - | - | - |
| Ethernet38 | Routed Endpoints | - | - | - | - | - |
| Ethernet39 | Routed Endpoints | - | - | - | - | - |
| Ethernet40 | Routed Endpoints | - | - | - | - | - |
| Ethernet41 | Routed Endpoints | - | - | - | - | - |
| Ethernet42 | Routed Endpoints | - | - | - | - | - |
| Ethernet43 | Routed Endpoints | - | - | - | - | - |
| Ethernet44 | Routed Endpoints | - | - | - | - | - |
| Ethernet45 | Routed Endpoints | - | - | - | - | - |
| Ethernet46 | Routed Endpoints | - | - | - | - | - |
| Ethernet47 | Routed Endpoints | - | - | - | - | - |
| Ethernet48 | Routed Endpoints | - | - | - | - | - |

*Inherited from Port-Channel Interface

##### IPv4

| Interface | Description | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet1 | P2P_amber-spine1_Ethernet5 | - | 10.255.253.1/31 | default | 1500 | False | - | - |
| Ethernet2 | P2P_blue-spine1_Ethernet5 | - | 10.255.253.3/31 | default | 1500 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_amber-spine1_Ethernet5
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.253.1/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet2
   description P2P_blue-spine1_Ethernet5
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.253.3/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet3
   description P2P_media-PTP-2_Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4
   description P2P_media-PTP-2_Ethernet4
   no shutdown
   mtu 1500
   no switchport
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5
   description PTP Grandmaster 1
   no shutdown
   speed forced 1000full
   switchport access vlan 131
   switchport mode access
   switchport
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet7
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet8
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet9
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet10
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet11
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet12
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet13
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet14
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet15
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet16
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet17
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet18
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet19
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet20
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet21
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet22
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet23
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet24
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet25
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet26
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet27
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet28
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet29
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet30
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet31
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet32
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet33
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet34
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet35
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet36
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet37
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet38
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet39
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet40
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet41
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet42
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet43
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet44
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet45
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet46
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet47
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
!
interface Ethernet48
   description Routed Endpoints
   shutdown
   speed forced 1000full
   switchport
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ROUTER_ID | default | 10.255.3.1/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | ROUTER_ID | default | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description ROUTER_ID
   no shutdown
   ip address 10.255.3.1/32
```

### VLAN Interfaces

#### VLAN Interfaces Summary

| Interface | Description | VRF |  MTU | Shutdown |
| --------- | ----------- | --- | ---- | -------- |
| Vlan131 | VLAN131 | default | - | False |

##### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ------ | ------- |
| Vlan131 |  default  |  10.10.131.1/24  |  -  |  -  |  -  |  -  |

#### VLAN Interfaces Device Configuration

```eos
!
interface Vlan131
   description VLAN131
   no shutdown
   ip address 10.10.131.1/24
```

## Routing

### Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | True |
| MGMT | False |

#### IP Routing Device Configuration

```eos
!
ip routing
no ip routing vrf MGMT
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| MGMT | false |

### Static Routes

#### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP | Exit interface | Administrative Distance | Tag | Route Name | Metric |
| --- | ------------------ | ----------- | -------------- | ----------------------- | --- | ---------- | ------ |
| MGMT | 0.0.0.0/0 | 172.16.1.1 | - | 1 | - | - | - |

#### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 0.0.0.0/0 172.16.1.1
```

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65401 | 10.255.3.1 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| maximum-paths 4 ecmp 4 |

#### Router BGP Peer Groups

##### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Send community | all |
| Maximum routes | 12000 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 10.255.253.0 | 65100 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.253.2 | 65200 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65401
   router-id 10.255.3.1
   no bgp default ipv4-unicast
   maximum-paths 4 ecmp 4
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS password 7 <removed>
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 10.255.253.0 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.253.0 remote-as 65100
   neighbor 10.255.253.0 description amber-spine1_Ethernet5
   neighbor 10.255.253.2 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.253.2 remote-as 65200
   neighbor 10.255.253.2 description blue-spine1_Ethernet5
   redistribute connected
   !
   address-family ipv4
      neighbor IPv4-UNDERLAY-PEERS activate
```

## Multicast

### IP IGMP Snooping

#### IP IGMP Snooping Summary

| IGMP Snooping | Fast Leave | Interface Restart Query | Proxy | Restart Query Interval | Robustness Variable |
| ------------- | ---------- | ----------------------- | ----- | ---------------------- | ------------------- |
| Enabled | - | - | - | - | - |

#### IP IGMP Snooping Device Configuration

```eos
```

### Router Multicast

#### IP Router Multicast Summary

- Routing for IPv4 multicast is enabled.

#### Router Multicast Device Configuration

```eos
!
router multicast
   ipv4
      routing
```

### PIM Sparse Mode

#### PIM Sparse Mode Enabled Interfaces

| Interface Name | VRF Name | IP Version | Border Router | DR Priority | Local Interface |
| -------------- | -------- | ---------- | ------------- | ----------- | --------------- |
| Ethernet1 | - | IPv4 | - | - | - |
| Ethernet2 | - | IPv4 | - | - | - |

## VRF Instances

### VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| MGMT | disabled |

### VRF Instances Device Configuration

```eos
!
vrf instance MGMT
```
