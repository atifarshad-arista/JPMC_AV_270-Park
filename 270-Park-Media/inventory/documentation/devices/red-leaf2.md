# red-leaf2

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
| Management1 | OOB_MANAGEMENT | oob | MGMT | 10.176.143.170/27 | 10.176.143.161 |

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
   ip address 10.176.143.170/27
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
| - | 169.27.195.2 | 30 | 102 | 8 | 100 | boundary | - |

#### PTP Device Configuration

```eos
!
ptp domain 100
ptp mode boundary
ptp priority1 30
ptp priority2 102
ptp source ip 169.27.195.2
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
| 112 | VLAN112 | - |

### VLANs Device Configuration

```eos
!
vlan 112
   name VLAN112
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
| Ethernet1 | - | - | - | - | - | - |
| Ethernet2 | - | - | - | - | - | - |
| Ethernet3 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet4 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet5 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet6 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet7 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet8 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet9 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet10 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet11 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet12 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet13 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet14 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet15 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet16 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet17 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet18 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet19 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet20 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet21 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet22 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet23 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet24 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet25 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet26 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet27 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet28 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet29 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet30 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet31 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet32 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet33 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet34 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet35 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet36 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet37 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet38 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet39 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet40 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet41 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet42 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet43 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet44 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet45 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet46 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet47 | RED_VLAN112 | access | 112 | - | - | - |
| Ethernet48 | RED_VLAN112 | access | 112 | - | - | - |

*Inherited from Port-Channel Interface

##### Multicast Routing

| Interface | IP Version | Static Routes Allowed | Multicast Boundaries |
| --------- | ---------- | --------------------- | -------------------- |
| Ethernet1 | IPv4 | True | - |
| Ethernet2 | IPv4 | True | - |
| Ethernet3 | IPv4 | True | - |
| Ethernet4 | IPv4 | True | - |
| Ethernet5 | IPv4 | True | - |
| Ethernet6 | IPv4 | True | - |
| Ethernet7 | IPv4 | True | - |
| Ethernet8 | IPv4 | True | - |
| Ethernet9 | IPv4 | True | - |
| Ethernet10 | IPv4 | True | - |
| Ethernet11 | IPv4 | True | - |
| Ethernet12 | IPv4 | True | - |
| Ethernet13 | IPv4 | True | - |
| Ethernet14 | IPv4 | True | - |
| Ethernet15 | IPv4 | True | - |
| Ethernet16 | IPv4 | True | - |
| Ethernet17 | IPv4 | True | - |
| Ethernet18 | IPv4 | True | - |
| Ethernet19 | IPv4 | True | - |
| Ethernet20 | IPv4 | True | - |
| Ethernet21 | IPv4 | True | - |
| Ethernet22 | IPv4 | True | - |
| Ethernet23 | IPv4 | True | - |
| Ethernet24 | IPv4 | True | - |
| Ethernet25 | IPv4 | True | - |
| Ethernet26 | IPv4 | True | - |
| Ethernet27 | IPv4 | True | - |
| Ethernet28 | IPv4 | True | - |
| Ethernet29 | IPv4 | True | - |
| Ethernet30 | IPv4 | True | - |
| Ethernet31 | IPv4 | True | - |
| Ethernet32 | IPv4 | True | - |
| Ethernet33 | IPv4 | True | - |
| Ethernet34 | IPv4 | True | - |
| Ethernet35 | IPv4 | True | - |
| Ethernet36 | IPv4 | True | - |
| Ethernet37 | IPv4 | True | - |
| Ethernet38 | IPv4 | True | - |
| Ethernet39 | IPv4 | True | - |
| Ethernet40 | IPv4 | True | - |
| Ethernet41 | IPv4 | True | - |
| Ethernet42 | IPv4 | True | - |
| Ethernet43 | IPv4 | True | - |
| Ethernet44 | IPv4 | True | - |
| Ethernet45 | IPv4 | True | - |
| Ethernet46 | IPv4 | True | - |
| Ethernet47 | IPv4 | True | - |
| Ethernet48 | IPv4 | True | - |

##### IPv4

| Interface | Description | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet2/1 | P2P_red-spine1_Ethernet6/4/1 | - | 100.83.94.17/31 | default | 1500 | False | - | - |
| Ethernet2/2 | P2P_red-spine1_Ethernet7/4/1 | - | 100.83.94.23/31 | default | 1500 | False | - | - |
| Ethernet2/3 | P2P_red-spine1_Ethernet6/5/1 | - | 100.83.94.19/31 | default | 1500 | False | - | - |
| Ethernet2/4 | P2P_red-spine1_Ethernet7/5/1 | - | 100.83.94.25/31 | default | 1500 | False | - | - |
| Ethernet3/1 | P2P_red-spine1_Ethernet6/6/1 | - | 100.83.94.21/31 | default | 1500 | False | - | - |
| Ethernet3/2 | P2P_red-spine1_Ethernet7/6/1 | - | 100.83.94.27/31 | default | 1500 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   no shutdown
   switchport
   multicast ipv4 static
!
interface Ethernet2
   no shutdown
   switchport
   multicast ipv4 static
!
interface Ethernet2/1
   description P2P_red-spine1_Ethernet6/4/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.17/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet2/2
   description P2P_red-spine1_Ethernet7/4/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.23/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet2/3
   description P2P_red-spine1_Ethernet6/5/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.19/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet2/4
   description P2P_red-spine1_Ethernet7/5/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.25/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet3
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet3/1
   description P2P_red-spine1_Ethernet6/6/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.21/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet3/2
   description P2P_red-spine1_Ethernet7/6/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.27/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet5
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet6
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet7
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet8
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet9
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet10
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet11
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet12
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet13
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet14
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet15
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet16
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet17
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet18
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet19
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet20
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet21
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet22
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet23
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet24
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet25
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet26
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet27
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet28
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet29
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet30
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet31
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet32
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet33
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet34
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet35
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet36
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet37
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet38
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet39
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet40
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet41
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet42
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet43
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet44
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet45
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet46
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet47
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
!
interface Ethernet48
   description RED_VLAN112
   shutdown
   switchport access vlan 112
   switchport mode access
   switchport
   multicast ipv4 static
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp role master
   ptp sync-message interval -3
   ptp transport ipv4
   spanning-tree portfast
   spanning-tree bpdufilter enable
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ROUTER_ID | default | 169.27.195.2/32 |

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
   ip address 169.27.195.2/32
```

### VLAN Interfaces

#### VLAN Interfaces Summary

| Interface | Description | VRF |  MTU | Shutdown |
| --------- | ----------- | --- | ---- | -------- |
| Vlan112 | VLAN112 | default | - | False |

##### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ------ | ------- |
| Vlan112 |  default  |  10.10.112.1/24  |  -  |  -  |  -  |  -  |

#### VLAN Interfaces Device Configuration

```eos
!
interface Vlan112
   description VLAN112
   no shutdown
   ip address 10.10.112.1/24
   ip helper-address 10.252.4.253
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
| MGMT | 0.0.0.0/0 | 10.176.143.161 | - | 1 | - | - | - |

#### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 0.0.0.0/0 10.176.143.161
```

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65210.37102 | 169.27.195.2 |

| BGP Tuning |
| ---------- |
| bgp asn notation asdot |
| timers bgp 5 15 |
| distance bgp 20 200 200 |
| graceful-restart restart-time 300 |
| graceful-restart |
| maximum-paths 128 |
| neighbor default send-community |
| redistribute attached-host |
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
| 100.83.94.16 | 65210.37100 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.18 | 65210.37100 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.20 | 65210.37100 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.22 | 65210.37100 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.24 | 65210.37100 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.26 | 65210.37100 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65210.37102
   router-id 169.27.195.2
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
   redistribute attached-host
   neighbor P2P-IPv4-eBGP-PEERS peer group
   neighbor P2P-IPv4-eBGP-PEERS password 7 <removed>
   neighbor P2P-IPv4-eBGP-PEERS send-community
   neighbor P2P-IPv4-eBGP-PEERS maximum-routes 12000
   neighbor 100.83.94.16 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.16 remote-as 65210.37100
   neighbor 100.83.94.16 description red-spine1_Ethernet6/4/1
   neighbor 100.83.94.18 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.18 remote-as 65210.37100
   neighbor 100.83.94.18 description red-spine1_Ethernet6/5/1
   neighbor 100.83.94.20 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.20 remote-as 65210.37100
   neighbor 100.83.94.20 description red-spine1_Ethernet6/6/1
   neighbor 100.83.94.22 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.22 remote-as 65210.37100
   neighbor 100.83.94.22 description red-spine1_Ethernet7/4/1
   neighbor 100.83.94.24 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.24 remote-as 65210.37100
   neighbor 100.83.94.24 description red-spine1_Ethernet7/5/1
   neighbor 100.83.94.26 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.26 remote-as 65210.37100
   neighbor 100.83.94.26 description red-spine1_Ethernet7/6/1
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
