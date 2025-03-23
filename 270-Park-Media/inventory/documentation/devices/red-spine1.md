# red-spine1

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
| Management1 | OOB_MANAGEMENT | oob | MGMT | 10.100.100.37/24 | - |

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
   ip address 10.100.100.37/24
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
| - | 172.31.1.11 | 20 | 101 | 8 | 100 | boundary | - |

#### PTP Device Configuration

```eos
!
ptp domain 100
ptp mode boundary
ptp priority1 20
ptp priority2 101
ptp source ip 172.31.1.11
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
| Ethernet4/11/1 | P2P_red-leaf1_Ethernet49/1 | - | 100.83.100.40/31 | default | 1500 | False | - | - |
| Ethernet4/12/1 | P2P_red-leaf1_Ethernet50/1 | - | 100.83.100.42/31 | default | 1500 | False | - | - |
| Ethernet4/13/1 | P2P_red-leaf2_Ethernet49/1 | - | 100.83.100.48/31 | default | 1500 | False | - | - |
| Ethernet4/14/1 | P2P_red-leaf2_Ethernet50/1 | - | 100.83.100.50/31 | default | 1500 | False | - | - |
| Ethernet4/15/1 | P2P_red-leaf3_Ethernet49/1 | - | 100.83.100.56/31 | default | 1500 | False | - | - |
| Ethernet4/16/1 | P2P_red-leaf3_Ethernet50/1 | - | 100.83.100.58/31 | default | 1500 | False | - | - |
| Ethernet4/17/1 | P2P_red-leaf4_Ethernet49/1 | - | 100.83.100.64/31 | default | 1500 | False | - | - |
| Ethernet4/18/1 | P2P_red-leaf4_Ethernet50/1 | - | 100.83.100.66/31 | default | 1500 | False | - | - |
| Ethernet4/19/1 | P2P_red-leaf5_Ethernet49/1 | - | 100.83.100.72/31 | default | 1500 | False | - | - |
| Ethernet4/20/1 | P2P_red-leaf5_Ethernet50/1 | - | 100.83.100.74/31 | default | 1500 | False | - | - |
| Ethernet4/21/1 | P2P_red-leaf6_Ethernet49/1 | - | 100.83.100.80/31 | default | 1500 | False | - | - |
| Ethernet4/22/1 | P2P_red-leaf6_Ethernet50/1 | - | 100.83.100.82/31 | default | 1500 | False | - | - |
| Ethernet4/23/1 | P2P_red-leaf7_Ethernet49/1 | - | 100.83.100.88/31 | default | 1500 | False | - | - |
| Ethernet4/24/1 | P2P_red-leaf7_Ethernet50/1 | - | 100.83.100.90/31 | default | 1500 | False | - | - |
| Ethernet4/25/1 | P2P_red-leaf8_Ethernet49/1 | - | 100.83.100.96/31 | default | 1500 | False | - | - |
| Ethernet4/26/1 | P2P_red-leaf8_Ethernet50/1 | - | 100.83.100.98/31 | default | 1500 | False | - | - |
| Ethernet4/27/1 | P2P_red-leaf9_Ethernet49/1 | - | 100.83.100.104/31 | default | 1500 | False | - | - |
| Ethernet4/28/1 | P2P_red-leaf9_Ethernet50/1 | - | 100.83.100.106/31 | default | 1500 | False | - | - |
| Ethernet4/29/1 | P2P_red-leaf10_Ethernet49/1 | - | 100.83.100.112/31 | default | 1500 | False | - | - |
| Ethernet4/30/1 | P2P_red-leaf10_Ethernet50/1 | - | 100.83.100.114/31 | default | 1500 | False | - | - |
| Ethernet4/31/1 | P2P_red-leaf11_Ethernet49/1 | - | 100.83.100.120/31 | default | 1500 | False | - | - |
| Ethernet4/32/1 | P2P_red-leaf11_Ethernet50/1 | - | 100.83.100.122/31 | default | 1500 | False | - | - |
| Ethernet4/33/1 | P2P_red-leaf12_Ethernet49/1 | - | 100.83.100.128/31 | default | 1500 | False | - | - |
| Ethernet4/34/1 | P2P_red-leaf12_Ethernet50/1 | - | 100.83.100.130/31 | default | 1500 | False | - | - |
| Ethernet4/35/1 | P2P_red-leaf13_Ethernet49/1 | - | 100.83.100.136/31 | default | 1500 | False | - | - |
| Ethernet4/36/1 | P2P_red-leaf13_Ethernet50/1 | - | 100.83.100.138/31 | default | 1500 | False | - | - |
| Ethernet5/1/1 | P2P_red-leaf14_Ethernet49/1 | - | 100.83.100.144/31 | default | 1500 | False | - | - |
| Ethernet5/2/1 | P2P_red-leaf14_Ethernet50/1 | - | 100.83.100.146/31 | default | 1500 | False | - | - |
| Ethernet5/3/1 | P2P_red-leaf15_Ethernet49/1 | - | 100.83.100.152/31 | default | 1500 | False | - | - |
| Ethernet5/4/1 | P2P_red-leaf15_Ethernet50/1 | - | 100.83.100.154/31 | default | 1500 | False | - | - |
| Ethernet5/5/1 | P2P_red-leaf16_Ethernet49/1 | - | 100.83.100.160/31 | default | 1500 | False | - | - |
| Ethernet5/6/1 | P2P_red-leaf16_Ethernet50/1 | - | 100.83.100.162/31 | default | 1500 | False | - | - |
| Ethernet5/7/1 | P2P_red-leaf17_Ethernet49/1 | - | 100.83.100.168/31 | default | 1500 | False | - | - |
| Ethernet5/8/1 | P2P_red-leaf17_Ethernet50/1 | - | 100.83.100.170/31 | default | 1500 | False | - | - |
| Ethernet5/9/1 | P2P_red-leaf18_Ethernet49/1 | - | 100.83.100.176/31 | default | 1500 | False | - | - |
| Ethernet5/10/1 | P2P_red-leaf18_Ethernet50/1 | - | 100.83.100.178/31 | default | 1500 | False | - | - |
| Ethernet5/11/1 | P2P_red-leaf19_Ethernet49/1 | - | 100.83.100.184/31 | default | 1500 | False | - | - |
| Ethernet5/12/1 | P2P_red-leaf19_Ethernet50/1 | - | 100.83.100.186/31 | default | 1500 | False | - | - |
| Ethernet5/13/1 | P2P_red-leaf20_Ethernet49/1 | - | 100.83.100.192/31 | default | 1500 | False | - | - |
| Ethernet5/14/1 | P2P_red-leaf20_Ethernet50/1 | - | 100.83.100.194/31 | default | 1500 | False | - | - |
| Ethernet5/15/1 | P2P_red-leaf21_Ethernet49/1 | - | 100.83.100.200/31 | default | 1500 | False | - | - |
| Ethernet5/16/1 | P2P_red-leaf21_Ethernet50/1 | - | 100.83.100.202/31 | default | 1500 | False | - | - |
| Ethernet5/17/1 | P2P_red-leaf22_Ethernet49/1 | - | 100.83.100.208/31 | default | 1500 | False | - | - |
| Ethernet5/18/1 | P2P_red-leaf22_Ethernet50/1 | - | 100.83.100.210/31 | default | 1500 | False | - | - |
| Ethernet5/19/1 | P2P_red-leaf23_Ethernet49/1 | - | 100.83.100.216/31 | default | 1500 | False | - | - |
| Ethernet5/20/1 | P2P_red-leaf23_Ethernet50/1 | - | 100.83.100.218/31 | default | 1500 | False | - | - |
| Ethernet5/21/1 | P2P_red-leaf24_Ethernet49/1 | - | 100.83.100.224/31 | default | 1500 | False | - | - |
| Ethernet5/22/1 | P2P_red-leaf24_Ethernet50/1 | - | 100.83.100.226/31 | default | 1500 | False | - | - |
| Ethernet5/23/1 | P2P_red-leaf25_Ethernet49/1 | - | 100.83.100.232/31 | default | 1500 | False | - | - |
| Ethernet5/24/1 | P2P_red-leaf25_Ethernet50/1 | - | 100.83.100.234/31 | default | 1500 | False | - | - |
| Ethernet5/25/1 | P2P_red-leaf26_Ethernet49/1 | - | 100.83.100.240/31 | default | 1500 | False | - | - |
| Ethernet5/26/1 | P2P_red-leaf26_Ethernet50/1 | - | 100.83.100.242/31 | default | 1500 | False | - | - |
| Ethernet5/27/1 | P2P_red-leaf27_Ethernet49/1 | - | 100.83.100.248/31 | default | 1500 | False | - | - |
| Ethernet5/28/1 | P2P_red-leaf27_Ethernet50/1 | - | 100.83.100.250/31 | default | 1500 | False | - | - |
| Ethernet5/29/1 | P2P_red-leaf28_Ethernet49/1 | - | 100.83.101.0/31 | default | 1500 | False | - | - |
| Ethernet5/30/1 | P2P_red-leaf28_Ethernet50/1 | - | 100.83.101.2/31 | default | 1500 | False | - | - |
| Ethernet5/31/1 | P2P_red-leaf29_Ethernet49/1 | - | 100.83.101.8/31 | default | 1500 | False | - | - |
| Ethernet5/32/1 | P2P_red-leaf29_Ethernet50/1 | - | 100.83.101.10/31 | default | 1500 | False | - | - |
| Ethernet5/33/1 | P2P_red-leaf30_Ethernet49/1 | - | 100.83.101.16/31 | default | 1500 | False | - | - |
| Ethernet5/34/1 | P2P_red-leaf30_Ethernet50/1 | - | 100.83.101.18/31 | default | 1500 | False | - | - |
| Ethernet5/35/1 | P2P_red-leaf31_Ethernet49/1 | - | 100.83.101.24/31 | default | 1500 | False | - | - |
| Ethernet5/36/1 | P2P_red-leaf31_Ethernet50/1 | - | 100.83.101.26/31 | default | 1500 | False | - | - |
| Ethernet6/1/1 | P2P_red-leaf32_Ethernet49/1 | - | 100.83.101.32/31 | default | 1500 | False | - | - |
| Ethernet6/2/1 | P2P_red-leaf32_Ethernet50/1 | - | 100.83.101.34/31 | default | 1500 | False | - | - |
| Ethernet33/1 | P2P_border-leaf1_Ethernet33/1 | - | 100.83.88.16/31 | default | 1500 | False | - | - |
| Ethernet34/1 | P2P_border-leaf2_Ethernet33/1 | - | 100.83.88.24/31 | default | 1500 | False | - | - |
| Ethernet49/1 | P2P_media-PTP-1_Ethernet49/1 | - | 100.83.88.0/31 | default | 1500 | False | - | - |
| Ethernet50/1 | P2P_media-PTP-2_Ethernet49/1 | - | 100.83.88.8/31 | default | 1500 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet4/11/1
   description P2P_red-leaf1_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.40/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/12/1
   description P2P_red-leaf1_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.42/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/13/1
   description P2P_red-leaf2_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.48/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/14/1
   description P2P_red-leaf2_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.50/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/15/1
   description P2P_red-leaf3_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.56/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/16/1
   description P2P_red-leaf3_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.58/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/17/1
   description P2P_red-leaf4_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.64/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/18/1
   description P2P_red-leaf4_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.66/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/19/1
   description P2P_red-leaf5_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.72/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/20/1
   description P2P_red-leaf5_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.74/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/21/1
   description P2P_red-leaf6_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.80/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/22/1
   description P2P_red-leaf6_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.82/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/23/1
   description P2P_red-leaf7_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.88/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/24/1
   description P2P_red-leaf7_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.90/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/25/1
   description P2P_red-leaf8_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.96/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/26/1
   description P2P_red-leaf8_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.98/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/27/1
   description P2P_red-leaf9_Ethernet49/1
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
interface Ethernet4/28/1
   description P2P_red-leaf9_Ethernet50/1
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
interface Ethernet4/29/1
   description P2P_red-leaf10_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.112/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/30/1
   description P2P_red-leaf10_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.114/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/31/1
   description P2P_red-leaf11_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.120/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/32/1
   description P2P_red-leaf11_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.122/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/33/1
   description P2P_red-leaf12_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.128/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/34/1
   description P2P_red-leaf12_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.130/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/35/1
   description P2P_red-leaf13_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.136/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/36/1
   description P2P_red-leaf13_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.138/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/1/1
   description P2P_red-leaf14_Ethernet49/1
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
interface Ethernet5/2/1
   description P2P_red-leaf14_Ethernet50/1
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
interface Ethernet5/3/1
   description P2P_red-leaf15_Ethernet49/1
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
interface Ethernet5/4/1
   description P2P_red-leaf15_Ethernet50/1
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
interface Ethernet5/5/1
   description P2P_red-leaf16_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.160/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/6/1
   description P2P_red-leaf16_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.162/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/7/1
   description P2P_red-leaf17_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.168/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/8/1
   description P2P_red-leaf17_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.170/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/9/1
   description P2P_red-leaf18_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.176/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/10/1
   description P2P_red-leaf18_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.178/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/11/1
   description P2P_red-leaf19_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.184/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/12/1
   description P2P_red-leaf19_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.186/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/13/1
   description P2P_red-leaf20_Ethernet49/1
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
interface Ethernet5/14/1
   description P2P_red-leaf20_Ethernet50/1
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
interface Ethernet5/15/1
   description P2P_red-leaf21_Ethernet49/1
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
interface Ethernet5/16/1
   description P2P_red-leaf21_Ethernet50/1
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
interface Ethernet5/17/1
   description P2P_red-leaf22_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.208/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/18/1
   description P2P_red-leaf22_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.210/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/19/1
   description P2P_red-leaf23_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.216/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/20/1
   description P2P_red-leaf23_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.218/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/21/1
   description P2P_red-leaf24_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.224/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/22/1
   description P2P_red-leaf24_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.226/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/23/1
   description P2P_red-leaf25_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.232/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/24/1
   description P2P_red-leaf25_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.234/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/25/1
   description P2P_red-leaf26_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.240/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/26/1
   description P2P_red-leaf26_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.242/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/27/1
   description P2P_red-leaf27_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.248/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/28/1
   description P2P_red-leaf27_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.100.250/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/29/1
   description P2P_red-leaf28_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.101.0/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/30/1
   description P2P_red-leaf28_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.101.2/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/31/1
   description P2P_red-leaf29_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.101.8/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/32/1
   description P2P_red-leaf29_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.101.10/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/33/1
   description P2P_red-leaf30_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.101.16/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/34/1
   description P2P_red-leaf30_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.101.18/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/35/1
   description P2P_red-leaf31_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.101.24/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/36/1
   description P2P_red-leaf31_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.101.26/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/1/1
   description P2P_red-leaf32_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.101.32/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/2/1
   description P2P_red-leaf32_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.101.34/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet33/1
   description P2P_border-leaf1_Ethernet33/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.16/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet34/1
   description P2P_border-leaf2_Ethernet33/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.24/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet49/1
   description P2P_media-PTP-1_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.0/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet50/1
   description P2P_media-PTP-2_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.8/31
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
| Loopback0 | ROUTER_ID | default | 169.27.195.1/32 |

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
   ip address 169.27.195.1/32
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

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65020.1 | 169.27.195.1 |

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
| 100.83.88.1 | 65213.37370 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.9 | 65213.37370 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.17 | 65214 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.25 | 65214 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.41 | 65021.1 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.43 | 65021.1 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.49 | 65021.2 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.51 | 65021.2 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.57 | 65021.3 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.59 | 65021.3 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.65 | 65021.4 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.67 | 65021.4 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.73 | 65021.5 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.75 | 65021.5 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.81 | 65021.6 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.83 | 65021.6 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.89 | 65021.7 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.91 | 65021.7 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.97 | 65021.8 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.99 | 65021.8 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.105 | 65021.9 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.107 | 65021.9 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.113 | 65021.10 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.115 | 65021.10 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.121 | 65021.11 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.123 | 65021.11 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.129 | 65021.12 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.131 | 65021.12 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.137 | 65021.13 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.139 | 65021.13 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.145 | 65021.14 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.147 | 65021.14 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.153 | 65021.15 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.155 | 65021.15 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.161 | 65021.16 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.163 | 65021.16 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.169 | 65021.17 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.171 | 65021.17 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.177 | 65021.18 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.179 | 65021.18 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.185 | 65021.19 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.187 | 65021.19 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.193 | 65021.20 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.195 | 65021.20 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.201 | 65021.21 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.203 | 65021.21 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.209 | 65021.22 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.211 | 65021.22 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.217 | 65021.23 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.219 | 65021.23 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.225 | 65021.24 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.227 | 65021.24 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.233 | 65021.25 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.235 | 65021.25 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.241 | 65021.26 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.243 | 65021.26 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.249 | 65021.27 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.100.251 | 65021.27 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.101.1 | 65021.28 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.101.3 | 65021.28 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.101.9 | 65021.29 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.101.11 | 65021.29 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.101.17 | 65021.30 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.101.19 | 65021.30 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.101.25 | 65021.31 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.101.27 | 65021.31 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.101.33 | 65021.32 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.101.35 | 65021.32 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65020.1
   router-id 169.27.195.1
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
   neighbor 100.83.88.1 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.1 remote-as 65213.37370
   neighbor 100.83.88.1 description media-PTP-1_Ethernet49/1
   neighbor 100.83.88.9 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.9 remote-as 65213.37370
   neighbor 100.83.88.9 description media-PTP-2_Ethernet49/1
   neighbor 100.83.88.17 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.17 remote-as 65214
   neighbor 100.83.88.17 description border-leaf1_Ethernet33/1
   neighbor 100.83.88.25 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.25 remote-as 65214
   neighbor 100.83.88.25 description border-leaf2_Ethernet33/1
   neighbor 100.83.100.41 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.41 remote-as 65021.1
   neighbor 100.83.100.41 description red-leaf1_Ethernet49/1
   neighbor 100.83.100.43 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.43 remote-as 65021.1
   neighbor 100.83.100.43 description red-leaf1_Ethernet50/1
   neighbor 100.83.100.49 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.49 remote-as 65021.2
   neighbor 100.83.100.49 description red-leaf2_Ethernet49/1
   neighbor 100.83.100.51 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.51 remote-as 65021.2
   neighbor 100.83.100.51 description red-leaf2_Ethernet50/1
   neighbor 100.83.100.57 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.57 remote-as 65021.3
   neighbor 100.83.100.57 description red-leaf3_Ethernet49/1
   neighbor 100.83.100.59 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.59 remote-as 65021.3
   neighbor 100.83.100.59 description red-leaf3_Ethernet50/1
   neighbor 100.83.100.65 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.65 remote-as 65021.4
   neighbor 100.83.100.65 description red-leaf4_Ethernet49/1
   neighbor 100.83.100.67 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.67 remote-as 65021.4
   neighbor 100.83.100.67 description red-leaf4_Ethernet50/1
   neighbor 100.83.100.73 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.73 remote-as 65021.5
   neighbor 100.83.100.73 description red-leaf5_Ethernet49/1
   neighbor 100.83.100.75 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.75 remote-as 65021.5
   neighbor 100.83.100.75 description red-leaf5_Ethernet50/1
   neighbor 100.83.100.81 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.81 remote-as 65021.6
   neighbor 100.83.100.81 description red-leaf6_Ethernet49/1
   neighbor 100.83.100.83 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.83 remote-as 65021.6
   neighbor 100.83.100.83 description red-leaf6_Ethernet50/1
   neighbor 100.83.100.89 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.89 remote-as 65021.7
   neighbor 100.83.100.89 description red-leaf7_Ethernet49/1
   neighbor 100.83.100.91 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.91 remote-as 65021.7
   neighbor 100.83.100.91 description red-leaf7_Ethernet50/1
   neighbor 100.83.100.97 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.97 remote-as 65021.8
   neighbor 100.83.100.97 description red-leaf8_Ethernet49/1
   neighbor 100.83.100.99 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.99 remote-as 65021.8
   neighbor 100.83.100.99 description red-leaf8_Ethernet50/1
   neighbor 100.83.100.105 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.105 remote-as 65021.9
   neighbor 100.83.100.105 description red-leaf9_Ethernet49/1
   neighbor 100.83.100.107 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.107 remote-as 65021.9
   neighbor 100.83.100.107 description red-leaf9_Ethernet50/1
   neighbor 100.83.100.113 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.113 remote-as 65021.10
   neighbor 100.83.100.113 description red-leaf10_Ethernet49/1
   neighbor 100.83.100.115 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.115 remote-as 65021.10
   neighbor 100.83.100.115 description red-leaf10_Ethernet50/1
   neighbor 100.83.100.121 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.121 remote-as 65021.11
   neighbor 100.83.100.121 description red-leaf11_Ethernet49/1
   neighbor 100.83.100.123 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.123 remote-as 65021.11
   neighbor 100.83.100.123 description red-leaf11_Ethernet50/1
   neighbor 100.83.100.129 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.129 remote-as 65021.12
   neighbor 100.83.100.129 description red-leaf12_Ethernet49/1
   neighbor 100.83.100.131 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.131 remote-as 65021.12
   neighbor 100.83.100.131 description red-leaf12_Ethernet50/1
   neighbor 100.83.100.137 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.137 remote-as 65021.13
   neighbor 100.83.100.137 description red-leaf13_Ethernet49/1
   neighbor 100.83.100.139 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.139 remote-as 65021.13
   neighbor 100.83.100.139 description red-leaf13_Ethernet50/1
   neighbor 100.83.100.145 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.145 remote-as 65021.14
   neighbor 100.83.100.145 description red-leaf14_Ethernet49/1
   neighbor 100.83.100.147 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.147 remote-as 65021.14
   neighbor 100.83.100.147 description red-leaf14_Ethernet50/1
   neighbor 100.83.100.153 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.153 remote-as 65021.15
   neighbor 100.83.100.153 description red-leaf15_Ethernet49/1
   neighbor 100.83.100.155 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.155 remote-as 65021.15
   neighbor 100.83.100.155 description red-leaf15_Ethernet50/1
   neighbor 100.83.100.161 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.161 remote-as 65021.16
   neighbor 100.83.100.161 description red-leaf16_Ethernet49/1
   neighbor 100.83.100.163 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.163 remote-as 65021.16
   neighbor 100.83.100.163 description red-leaf16_Ethernet50/1
   neighbor 100.83.100.169 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.169 remote-as 65021.17
   neighbor 100.83.100.169 description red-leaf17_Ethernet49/1
   neighbor 100.83.100.171 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.171 remote-as 65021.17
   neighbor 100.83.100.171 description red-leaf17_Ethernet50/1
   neighbor 100.83.100.177 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.177 remote-as 65021.18
   neighbor 100.83.100.177 description red-leaf18_Ethernet49/1
   neighbor 100.83.100.179 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.179 remote-as 65021.18
   neighbor 100.83.100.179 description red-leaf18_Ethernet50/1
   neighbor 100.83.100.185 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.185 remote-as 65021.19
   neighbor 100.83.100.185 description red-leaf19_Ethernet49/1
   neighbor 100.83.100.187 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.187 remote-as 65021.19
   neighbor 100.83.100.187 description red-leaf19_Ethernet50/1
   neighbor 100.83.100.193 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.193 remote-as 65021.20
   neighbor 100.83.100.193 description red-leaf20_Ethernet49/1
   neighbor 100.83.100.195 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.195 remote-as 65021.20
   neighbor 100.83.100.195 description red-leaf20_Ethernet50/1
   neighbor 100.83.100.201 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.201 remote-as 65021.21
   neighbor 100.83.100.201 description red-leaf21_Ethernet49/1
   neighbor 100.83.100.203 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.203 remote-as 65021.21
   neighbor 100.83.100.203 description red-leaf21_Ethernet50/1
   neighbor 100.83.100.209 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.209 remote-as 65021.22
   neighbor 100.83.100.209 description red-leaf22_Ethernet49/1
   neighbor 100.83.100.211 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.211 remote-as 65021.22
   neighbor 100.83.100.211 description red-leaf22_Ethernet50/1
   neighbor 100.83.100.217 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.217 remote-as 65021.23
   neighbor 100.83.100.217 description red-leaf23_Ethernet49/1
   neighbor 100.83.100.219 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.219 remote-as 65021.23
   neighbor 100.83.100.219 description red-leaf23_Ethernet50/1
   neighbor 100.83.100.225 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.225 remote-as 65021.24
   neighbor 100.83.100.225 description red-leaf24_Ethernet49/1
   neighbor 100.83.100.227 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.227 remote-as 65021.24
   neighbor 100.83.100.227 description red-leaf24_Ethernet50/1
   neighbor 100.83.100.233 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.233 remote-as 65021.25
   neighbor 100.83.100.233 description red-leaf25_Ethernet49/1
   neighbor 100.83.100.235 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.235 remote-as 65021.25
   neighbor 100.83.100.235 description red-leaf25_Ethernet50/1
   neighbor 100.83.100.241 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.241 remote-as 65021.26
   neighbor 100.83.100.241 description red-leaf26_Ethernet49/1
   neighbor 100.83.100.243 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.243 remote-as 65021.26
   neighbor 100.83.100.243 description red-leaf26_Ethernet50/1
   neighbor 100.83.100.249 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.249 remote-as 65021.27
   neighbor 100.83.100.249 description red-leaf27_Ethernet49/1
   neighbor 100.83.100.251 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.100.251 remote-as 65021.27
   neighbor 100.83.100.251 description red-leaf27_Ethernet50/1
   neighbor 100.83.101.1 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.101.1 remote-as 65021.28
   neighbor 100.83.101.1 description red-leaf28_Ethernet49/1
   neighbor 100.83.101.3 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.101.3 remote-as 65021.28
   neighbor 100.83.101.3 description red-leaf28_Ethernet50/1
   neighbor 100.83.101.9 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.101.9 remote-as 65021.29
   neighbor 100.83.101.9 description red-leaf29_Ethernet49/1
   neighbor 100.83.101.11 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.101.11 remote-as 65021.29
   neighbor 100.83.101.11 description red-leaf29_Ethernet50/1
   neighbor 100.83.101.17 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.101.17 remote-as 65021.30
   neighbor 100.83.101.17 description red-leaf30_Ethernet49/1
   neighbor 100.83.101.19 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.101.19 remote-as 65021.30
   neighbor 100.83.101.19 description red-leaf30_Ethernet50/1
   neighbor 100.83.101.25 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.101.25 remote-as 65021.31
   neighbor 100.83.101.25 description red-leaf31_Ethernet49/1
   neighbor 100.83.101.27 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.101.27 remote-as 65021.31
   neighbor 100.83.101.27 description red-leaf31_Ethernet50/1
   neighbor 100.83.101.33 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.101.33 remote-as 65021.32
   neighbor 100.83.101.33 description red-leaf32_Ethernet49/1
   neighbor 100.83.101.35 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.101.35 remote-as 65021.32
   neighbor 100.83.101.35 description red-leaf32_Ethernet50/1
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
