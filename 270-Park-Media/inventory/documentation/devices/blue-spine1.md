# blue-spine1

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
- [Interfaces](#interfaces)
  - [Switchport Default](#switchport-default)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
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
| Management0 | OOB_MANAGEMENT | oob | MGMT | 10.176.143.168/27 | 10.176.143.161 |

##### IPv6

| Management Interface | Description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Management0 | OOB_MANAGEMENT | oob | MGMT | - | - |

#### Management Interfaces Device Configuration

```eos
!
interface Management0
   description OOB_MANAGEMENT
   no shutdown
   vrf MGMT
   ip address 10.176.143.168/27
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
| - | loopback0 | 20 | 102 | 8 | 100 | boundary | - |

#### PTP Device Configuration

```eos
!
ptp domain 100
ptp mode boundary
ptp priority1 20
ptp priority2 102
ptp source ip loopback0
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

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode mstp
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

*Inherited from Port-Channel Interface

##### IPv4

| Interface | Description | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet3/31/4 | P2P_blue-leaf5_Ethernet56 | - | 100.83.101.64/31 | default | 1500 | False | - | - |
| Ethernet3/32/1 | P2P_media-PTP-1_Ethernet50 | - | 100.83.88.2/31 | default | 1500 | False | - | - |
| Ethernet3/32/2 | P2P_blue-leaf3_Ethernet55 | - | 100.83.100.104/31 | default | 1500 | False | - | - |
| Ethernet3/32/3 | P2P_blue-leaf5_Ethernet54 | - | 100.83.101.66/31 | default | 1500 | False | - | - |
| Ethernet4/32/1 | P2P_media-PTP-2_Ethernet50 | - | 100.83.88.10/31 | default | 1500 | False | - | - |
| Ethernet4/32/2 | P2P_blue-leaf3_Ethernet56 | - | 100.83.100.106/31 | default | 1500 | False | - | - |
| Ethernet4/32/3 | P2P_blue-leaf5_Ethernet55 | - | 100.83.101.68/31 | default | 1500 | False | - | - |
| Ethernet5/33/3 | P2P_blue-leaf5_Ethernet53 | - | 100.83.101.70/31 | default | 1500 | False | - | - |
| Ethernet6/4/1 | P2P_blue-leaf2_Ethernet2/1 | - | 100.83.100.144/31 | default | 1500 | False | - | - |
| Ethernet6/5/1 | P2P_blue-leaf2_Ethernet2/3 | - | 100.83.100.146/31 | default | 1500 | False | - | - |
| Ethernet6/6/1 | P2P_blue-leaf2_Ethernet3/1 | - | 100.83.100.148/31 | default | 1500 | False | - | - |
| Ethernet6/7/1 | P2P_blue-leaf4_Ethernet2/1 | - | 100.83.100.192/31 | default | 1500 | False | - | - |
| Ethernet6/8/1 | P2P_blue-leaf4_Ethernet2/3 | - | 100.83.100.194/31 | default | 1500 | False | - | - |
| Ethernet6/9/1 | P2P_blue-leaf6_Ethernet2/2 | - | 100.83.100.200/31 | default | 1500 | False | - | - |
| Ethernet6/18/1 | P2P_blue-leaf1_Ethernet2/1 | - | 100.83.100.0/31 | default | 1500 | False | - | - |
| Ethernet6/19/1 | P2P_blue-leaf1_Ethernet2/2 | - | 100.83.100.2/31 | default | 1500 | False | - | - |
| Ethernet6/20/1 | P2P_blue-leaf1_Ethernet2/3 | - | 100.83.100.4/31 | default | 1500 | False | - | - |
| Ethernet7/1/1 | P2P_blue-leaf1_Ethernet2/4 | - | 100.83.100.6/31 | default | 1500 | False | - | - |
| Ethernet7/2/1 | P2P_blue-leaf1_Ethernet3/1 | - | 100.83.100.8/31 | default | 1500 | False | - | - |
| Ethernet7/3/1 | P2P_blue-leaf1_Ethernet3/2 | - | 100.83.100.10/31 | default | 1500 | False | - | - |
| Ethernet7/4/1 | P2P_blue-leaf2_Ethernet2/2 | - | 100.83.100.150/31 | default | 1500 | False | - | - |
| Ethernet7/5/1 | P2P_blue-leaf2_Ethernet2/4 | - | 100.83.100.152/31 | default | 1500 | False | - | - |
| Ethernet7/6/1 | P2P_blue-leaf2_Ethernet3/2 | - | 100.83.100.154/31 | default | 1500 | False | - | - |
| Ethernet7/7/1 | P2P_blue-leaf4_Ethernet2/2 | - | 100.83.100.196/31 | default | 1500 | False | - | - |
| Ethernet7/8/1 | P2P_blue-leaf6_Ethernet2/1 | - | 100.83.100.202/31 | default | 1500 | False | - | - |
| Ethernet33/1 | P2P_border-leaf1_Ethernet32/1 | - | 100.83.88.18/31 | default | 1500 | False | - | - |
| Ethernet34/1 | P2P_border-leaf2_Ethernet32/1 | - | 100.83.88.26/31 | default | 1500 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet3/31/4
   description P2P_blue-leaf5_Ethernet56
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.101.64/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet3/32/1
   description P2P_media-PTP-1_Ethernet50
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.2/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet3/32/2
   description P2P_blue-leaf3_Ethernet55
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.104/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet3/32/3
   description P2P_blue-leaf5_Ethernet54
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.101.66/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/32/1
   description P2P_media-PTP-2_Ethernet50
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.10/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/32/2
   description P2P_blue-leaf3_Ethernet56
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.106/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/32/3
   description P2P_blue-leaf5_Ethernet55
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.101.68/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/33/3
   description P2P_blue-leaf5_Ethernet53
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.101.70/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/4/1
   description P2P_blue-leaf2_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.144/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/5/1
   description P2P_blue-leaf2_Ethernet2/3
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.146/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/6/1
   description P2P_blue-leaf2_Ethernet3/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.148/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/7/1
   description P2P_blue-leaf4_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.192/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/8/1
   description P2P_blue-leaf4_Ethernet2/3
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.194/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/9/1
   description P2P_blue-leaf6_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.200/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/18/1
   description P2P_blue-leaf1_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.0/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/19/1
   description P2P_blue-leaf1_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.2/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/20/1
   description P2P_blue-leaf1_Ethernet2/3
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.4/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/1/1
   description P2P_blue-leaf1_Ethernet2/4
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.6/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/2/1
   description P2P_blue-leaf1_Ethernet3/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.8/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/3/1
   description P2P_blue-leaf1_Ethernet3/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.10/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/4/1
   description P2P_blue-leaf2_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.150/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/5/1
   description P2P_blue-leaf2_Ethernet2/4
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.152/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/6/1
   description P2P_blue-leaf2_Ethernet3/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.154/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/7/1
   description P2P_blue-leaf4_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.196/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/8/1
   description P2P_blue-leaf6_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.202/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet33/1
   description P2P_border-leaf1_Ethernet32/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.18/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet34/1
   description P2P_border-leaf2_Ethernet32/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.26/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ROUTER_ID | default | 169.27.195.33/32 |

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
   ip address 169.27.195.33/32
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
| 65211.37200 | 169.27.195.33 |

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
| 100.83.88.3 | 65213.37370 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.11 | 65213.37370 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.19 | 65214 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.27 | 65214 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.1 | 65211.37201 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.3 | 65211.37201 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.5 | 65211.37201 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.7 | 65211.37201 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.9 | 65211.37201 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.11 | 65211.37201 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.105 | 65211.37205 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.107 | 65211.37205 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.145 | 65211.37202 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.147 | 65211.37202 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.149 | 65211.37202 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.151 | 65211.37202 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.153 | 65211.37202 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.155 | 65211.37202 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.193 | 65211.37203 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.195 | 65211.37203 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.197 | 65211.37203 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.201 | 65211.37204 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.203 | 65211.37204 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.101.65 | 65211.37206 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.101.67 | 65211.37206 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.101.69 | 65211.37206 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.101.71 | 65211.37206 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65211.37200
   router-id 169.27.195.33
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
   neighbor 100.83.88.3 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.3 remote-as 65213.37370
   neighbor 100.83.88.3 description media-PTP-1_Ethernet50
   neighbor 100.83.88.11 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.11 remote-as 65213.37370
   neighbor 100.83.88.11 description media-PTP-2_Ethernet50
   neighbor 100.83.88.19 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.19 remote-as 65214
   neighbor 100.83.88.19 description border-leaf1_Ethernet32/1
   neighbor 100.83.88.27 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.27 remote-as 65214
   neighbor 100.83.88.27 description border-leaf2_Ethernet32/1
   neighbor 100.83.100.1 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.1 remote-as 65211.37201
   neighbor 100.83.100.1 description blue-leaf1_Ethernet2/1
   neighbor 100.83.100.3 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.3 remote-as 65211.37201
   neighbor 100.83.100.3 description blue-leaf1_Ethernet2/2
   neighbor 100.83.100.5 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.5 remote-as 65211.37201
   neighbor 100.83.100.5 description blue-leaf1_Ethernet2/3
   neighbor 100.83.100.7 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.7 remote-as 65211.37201
   neighbor 100.83.100.7 description blue-leaf1_Ethernet2/4
   neighbor 100.83.100.9 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.9 remote-as 65211.37201
   neighbor 100.83.100.9 description blue-leaf1_Ethernet3/1
   neighbor 100.83.100.11 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.11 remote-as 65211.37201
   neighbor 100.83.100.11 description blue-leaf1_Ethernet3/2
   neighbor 100.83.100.105 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.105 remote-as 65211.37205
   neighbor 100.83.100.105 description blue-leaf3_Ethernet55
   neighbor 100.83.100.107 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.107 remote-as 65211.37205
   neighbor 100.83.100.107 description blue-leaf3_Ethernet56
   neighbor 100.83.100.145 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.145 remote-as 65211.37202
   neighbor 100.83.100.145 description blue-leaf2_Ethernet2/1
   neighbor 100.83.100.147 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.147 remote-as 65211.37202
   neighbor 100.83.100.147 description blue-leaf2_Ethernet2/3
   neighbor 100.83.100.149 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.149 remote-as 65211.37202
   neighbor 100.83.100.149 description blue-leaf2_Ethernet3/1
   neighbor 100.83.100.151 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.151 remote-as 65211.37202
   neighbor 100.83.100.151 description blue-leaf2_Ethernet2/2
   neighbor 100.83.100.153 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.153 remote-as 65211.37202
   neighbor 100.83.100.153 description blue-leaf2_Ethernet2/4
   neighbor 100.83.100.155 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.155 remote-as 65211.37202
   neighbor 100.83.100.155 description blue-leaf2_Ethernet3/2
   neighbor 100.83.100.193 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.193 remote-as 65211.37203
   neighbor 100.83.100.193 description blue-leaf4_Ethernet2/1
   neighbor 100.83.100.195 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.195 remote-as 65211.37203
   neighbor 100.83.100.195 description blue-leaf4_Ethernet2/3
   neighbor 100.83.100.197 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.197 remote-as 65211.37203
   neighbor 100.83.100.197 description blue-leaf4_Ethernet2/2
   neighbor 100.83.100.201 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.201 remote-as 65211.37204
   neighbor 100.83.100.201 description blue-leaf6_Ethernet2/2
   neighbor 100.83.100.203 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.203 remote-as 65211.37204
   neighbor 100.83.100.203 description blue-leaf6_Ethernet2/1
   neighbor 100.83.101.65 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.101.65 remote-as 65211.37206
   neighbor 100.83.101.65 description blue-leaf5_Ethernet56
   neighbor 100.83.101.67 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.101.67 remote-as 65211.37206
   neighbor 100.83.101.67 description blue-leaf5_Ethernet54
   neighbor 100.83.101.69 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.101.69 remote-as 65211.37206
   neighbor 100.83.101.69 description blue-leaf5_Ethernet55
   neighbor 100.83.101.71 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.101.71 remote-as 65211.37206
   neighbor 100.83.101.71 description blue-leaf5_Ethernet53
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
