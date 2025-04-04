# media-PTP-1

## Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [IP Name Servers](#ip-name-servers)
  - [Clock Settings](#clock-settings)
  - [NTP](#ntp)
  - [PTP](#ptp)
  - [Management SSH](#management-ssh)
  - [IP Client Source Interfaces](#ip-client-source-interfaces)
  - [Management API gNMI](#management-api-gnmi)
  - [Management CVX Summary](#management-cvx-summary)
  - [Management API HTTP](#management-api-http)
  - [Management API Models](#management-api-models)
- [Authentication](#authentication)
  - [Local Users](#local-users)
  - [Roles](#roles)
  - [Enable Password](#enable-password)
  - [AAA Authentication](#aaa-authentication)
  - [AAA Authorization](#aaa-authorization)
- [Monitoring](#monitoring)
  - [TerminAttr Daemon](#terminattr-daemon)
  - [Logging](#logging)
  - [MCS Client Summary](#mcs-client-summary)
  - [SNMP](#snmp)
  - [Hardware](#hardware)
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
  - [Switchport Default](#switchport-default)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Port-Channel Interfaces](#port-channel-interfaces)
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
- [ACL](#acl)
  - [Standard Access-lists](#standard-access-lists)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)
- [System L1](#system-l1)
  - [Unsupported Interface Configurations](#unsupported-interface-configurations)
  - [System L1 Device Configuration](#system-l1-device-configuration)

## Management

### Management Interfaces

#### Management Interfaces Summary

##### IPv4

| Management Interface | Description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management1 | OOB_MANAGEMENT | oob | MGMT | 10.176.143.137/27 | 10.176.143.129 |

##### IPv6

| Management Interface | Description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Management1 | OOB_MANAGEMENT | oob | MGMT | - | - |

#### Management Interfaces Device Configuration

```eos
!
interface Management1
   description OOB_MANAGEMENT
   no shutdown
   vrf MGMT
   ip address 10.176.143.137/27
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

### Clock Settings

#### Clock Timezone Settings

Clock Timezone is set to **America/New_York**.

#### Clock Device Configuration

```eos
!
clock timezone America/New_York
```

### NTP

#### NTP Summary

##### NTP Servers

| Server | VRF | Preferred | Burst | iBurst | Version | Min Poll | Max Poll | Local-interface | Key |
| ------ | --- | --------- | ----- | ------ | ------- | -------- | -------- | --------------- | --- |
| 172.16.131.2 | MGMT | False | False | True | - | - | - | - | - |
| 172.16.131.3 | MGMT | True | False | True | - | - | - | - | - |

#### NTP Device Configuration

```eos
!
ntp server vrf MGMT 172.16.131.2 iburst
ntp server vrf MGMT 172.16.131.3 prefer iburst
```

### PTP
#### PTP Summary

| Clock ID | Source IP | Priority 1 | Priority 2 | TTL | Domain | Mode | Forward Unicast |
| -------- | --------- | ---------- | ---------- | --- | ------ | ---- | --------------- |
| - | 169.27.195.72 | 10 | 101 | 8 | 100 | boundary | - |

#### PTP Device Configuration

```eos
!
ptp domain 100
ptp mode boundary
ptp priority1 10
ptp priority2 101
ptp source ip 169.27.195.72
ptp ttl 8
ptp monitor threshold offset-from-master 500
ptp monitor threshold mean-path-delay 2500
no ptp monitor sequence-id
```

### Management SSH

#### IPv4 ACL

| IPv4 ACL | VRF |
| -------- | --- |
| MGMT-SSH-ACL | MGMT |

#### SSH Timeout and Management

| Idle Timeout | SSH Management |
| ------------ | -------------- |
| default | Enabled |

#### Max number of SSH sessions limit and per-host limit

| Connection Limit | Max from a single Host |
| ---------------- | ---------------------- |
| - | - |

#### Ciphers and Algorithms

| Ciphers | Key-exchange methods | MAC algorithms | Hostkey server algorithms |
|---------|----------------------|----------------|---------------------------|
| default | default | default | default |


#### Management SSH Device Configuration

```eos
!
management ssh
   ip access-group MGMT-SSH-ACL vrf MGMT in
```

### IP Client Source Interfaces

| IP Client | VRF | Source Interface Name |
| --------- | --- | --------------------- |
| HTTP | MGMT | Management 1 |

#### IP Client Source Interfaces Device Configuration

```eos
!
ip http client local-interface Management 1 vrf MGMT
 ```

### Management API gNMI

#### Management API gNMI Summary

| Transport | SSL Profile | VRF | Notification Timestamp | ACL | Port |
| --------- | ----------- | --- | ---------------------- | --- | ---- |
| NRVT | - | MGMT | last-change-time | - | 5909 |

Provider eos-native is configured.

#### Management API gNMI Device Configuration

```eos
!
management api gnmi
   transport grpc NRVT
      port 5909
      vrf MGMT
   provider eos-native
```

### Management CVX Summary

| Shutdown | CVX Servers |
| -------- | ----------- |
| False | 172.16.131.127, 172.16.131.128, 172.16.131.129 |

#### Management CVX Source Interface

| Interface | VRF |
| --------- | --- |
| Loopback0 | - |

#### Management CVX Device Configuration

```eos
!
management cvx
   no shutdown
   server host 172.16.131.127
   server host 172.16.131.128
   server host 172.16.131.129
   source-interface Loopback0
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

### Management API Models

#### Management API Models Summary

| Provider | Path | Disabled |
| -------- | ---- | ------- |
| smash | bridging | False |
| smash | ptp | False |
| smash | routing | False |

#### Management API Models Device Configuration

```eos
!
management api models
   !
   provider smash
      path bridging
      path ptp
      path routing
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

### Roles

#### Roles Summary

##### Role network-user

| Sequence | Action | Mode | Command |
| -------- | ------ | ---- | ------- |
| 10 | deny | exec | enable|configure|bash|python-shell|\| |
| 20 | permit | exec | .* |

#### Roles Device Configuration

```eos
!
role network-user
   10 deny mode exec command enable|configure|bash|python-shell|\|
   20 permit mode exec command .*
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

Authorization for serial console is enabled.

#### AAA Authorization Privilege Levels Summary

| Privilege Level | User Stores |
| --------------- | ----------- |
| all | local |

#### AAA Authorization Device Configuration

```eos
aaa authorization serial-console
aaa authorization exec default local
aaa authorization commands all default local
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

### Logging

#### Logging Servers and Features Summary

| Type | Level |
| -----| ----- |
| Monitor | notifications |

#### Logging Servers and Features Device Configuration

```eos
!
logging monitor notifications
```

### MCS Client Summary

MCS client is enabled

#### MCS Client Device Configuration

```eos
!
mcs client
   no shutdown
```

### SNMP

#### SNMP Configuration Summary

| Contact | Location | SNMP Traps | State |
| ------- | -------- | ---------- | ----- |
| - | - | All | Disabled |

#### SNMP Local Interfaces

| Local Interface | VRF |
| --------------- | --- |
| loopback0 | default |

#### SNMP Hosts Configuration

| Host | VRF | Community | Username | Authentication level | SNMP Version |
| ---- |---- | --------- | -------- | -------------------- | ------------ |
| 202.40.72.61 | - | <removed> | - | - | 2c |
| 202.40.73.61 | - | <removed> | - | - | 2c |

#### SNMP Communities

| Community | Access | Access List IPv4 | Access List IPv6 | View |
| --------- | ------ | ---------------- | ---------------- | ---- |
| <removed> | ro | - | - | - |

#### SNMP Device Configuration

```eos
!
snmp-server local-interface loopback0
snmp-server community <removed> ro
snmp-server host 202.40.72.61 version 2c <removed>
snmp-server host 202.40.73.61 version 2c <removed>
```

### Hardware

#### Hardware Device Configuration

```eos
!
hardware speed-group 4 serdes 10g
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

### Switchport Default

#### Switchport Defaults Summary

- Default Switchport Mode: routed

#### Switchport Default Device Configuration

```eos
!
switchport default mode routed
```

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
| Ethernet49 | P2P_red-spine1_Ethernet3/32/1 | - | 100.83.88.1/31 | default | 1500 | False | - | - |
| Ethernet50 | P2P_blue-spine1_Ethernet3/32/1 | - | 100.83.88.3/31 | default | 1500 | False | - | - |
| Ethernet51 | P2P_green-spine1_Ethernet3/31/1 | - | 100.83.93.25/31 | default | 1500 | False | - | - |
| Ethernet52 | P2P_green-spine2_Ethernet3/31/1 | - | 100.83.93.27/31 | default | 1500 | False | - | - |
| Ethernet53 | P2P_media-PTP-2_Ethernet53 | 1000 | *100.83.93.10/31 | **default | *1500 | *False | **- | **- |
| Ethernet54 | P2P_media-PTP-2_Ethernet54 | 1000 | *100.83.93.10/31 | **default | *1500 | *False | **- | **- |

*Inherited from Port-Channel Interface

#### Ethernet Interfaces Device Configuration

```eos
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
!
interface Ethernet49
   description P2P_red-spine1_Ethernet3/32/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.1/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet50
   description P2P_blue-spine1_Ethernet3/32/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.3/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet51
   description P2P_green-spine1_Ethernet3/31/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.93.25/31
!
interface Ethernet52
   description P2P_green-spine2_Ethernet3/31/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.93.27/31
!
interface Ethernet53
   description P2P_media-PTP-2_Ethernet53
   no shutdown
   channel-group 1000 mode active
!
interface Ethernet54
   description P2P_media-PTP-2_Ethernet54
   no shutdown
   channel-group 1000 mode active
```

### Port-Channel Interfaces

#### Port-Channel Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | LACP Fallback Timeout | LACP Fallback Mode | MLAG ID | EVPN ESI |
| --------- | ----------- | ---- | ----- | ----------- | ------------| --------------------- | ------------------ | ------- | -------- |

##### IPv4

| Interface | Description | MLAG ID | IP Address | VRF | MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | ------- | ---------- | --- | --- | -------- | ------ | ------- |
| Port-Channel1000 | INTER_SWITCH_LINK | - | 100.83.93.10/31 | default | 1500 | False | - | - |

#### Port-Channel Interfaces Device Configuration

```eos
!
interface Port-Channel1000
   description INTER_SWITCH_LINK
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.93.10/31
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ROUTER_ID | default | 169.27.195.72/32 |

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
   ip address 169.27.195.72/32
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
| MGMT | 0.0.0.0/0 | 10.176.143.129 | - | 1 | - | - | - |

#### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 0.0.0.0/0 10.176.143.129
```

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65213.37370 | 169.27.195.72 |

| BGP Tuning |
| ---------- |
| bgp asn notation asdot |
| timers bgp 5 15 |
| distance bgp 20 200 200 |
| graceful-restart restart-time 300 |
| graceful-restart |
| maximum-paths 128 |
| neighbor default send-community |
| update wait-install |
| no bgp default ipv4-unicast |
| maximum-paths 4 ecmp 4 |

#### Router BGP Peer Groups

##### P2P-IPv4-eBGP-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Send community | all |
| Maximum routes | 12000 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 100.83.88.0 | 65210.37100 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.2 | 65211.37200 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.93.11 | 65213.37370 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.93.24 | 65212.37300 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.93.26 | 65212.37300 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65213.37370
   router-id 169.27.195.72
   update wait-install
   no bgp default ipv4-unicast
   maximum-paths 4 ecmp 4
   bgp asn notation asdot
   timers bgp 5 15
   distance bgp 20 200 200
   graceful-restart restart-time 300
   graceful-restart
   maximum-paths 128
   neighbor default send-community
   neighbor P2P-IPv4-eBGP-PEERS peer group
   neighbor P2P-IPv4-eBGP-PEERS password 7 <removed>
   neighbor P2P-IPv4-eBGP-PEERS send-community
   neighbor P2P-IPv4-eBGP-PEERS maximum-routes 12000
   neighbor 100.83.88.0 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.0 remote-as 65210.37100
   neighbor 100.83.88.0 description red-spine1_Ethernet3/32/1
   neighbor 100.83.88.2 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.2 remote-as 65211.37200
   neighbor 100.83.88.2 description blue-spine1_Ethernet3/32/1
   neighbor 100.83.93.11 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.93.11 remote-as 65213.37370
   neighbor 100.83.93.11 description media-PTP-2
   neighbor 100.83.93.24 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.93.24 remote-as 65212.37300
   neighbor 100.83.93.24 local-as 65003.37370 no-prepend replace-as
   neighbor 100.83.93.24 description green-spine1
   neighbor 100.83.93.26 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.93.26 remote-as 65212.37300
   neighbor 100.83.93.26 local-as 65003.37370 no-prepend replace-as
   neighbor 100.83.93.26 description green-spine2
   redistribute connected
   !
   address-family ipv4
      neighbor P2P-IPv4-eBGP-PEERS activate
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

## ACL

### Standard Access-lists

#### Standard Access-lists Summary

##### MGMT-SSH-ACL

| Sequence | Action |
| -------- | ------ |
| 10 | permit host 172.20.111.100 |

#### Standard Access-lists Device Configuration

```eos
!
ip access-list standard MGMT-SSH-ACL
   10 permit host 172.20.111.100
```

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

## System L1

### Unsupported Interface Configurations

| Unsupported Configuration | action |
| ---------------- | -------|
| Speed | error |
| Error correction | error |

### System L1 Device Configuration

```eos
!
system l1
   unsupported speed action error
   unsupported error-correction action error
```
