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
| Management0 | OOB_MANAGEMENT | oob | MGMT | 10.176.143.139/27 | 10.176.143.129 |

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
   ip address 10.176.143.139/27
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
| - | 169.27.195.0 | 20 | 101 | 8 | 100 | boundary | - |

#### PTP Device Configuration

```eos
!
ptp domain 100
ptp mode boundary
ptp priority1 20
ptp priority2 101
ptp source ip 169.27.195.0
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
| Ethernet3/31/4 | P2P_red-leaf5_Ethernet56 | - | 100.83.94.64/31 | default | 1500 | False | - | - |
| Ethernet3/32/1 | P2P_media-PTP-1_Ethernet49 | - | 100.83.88.0/31 | default | 1500 | False | - | - |
| Ethernet3/32/2 | P2P_red-leaf3_Ethernet55 | - | 100.83.94.32/31 | default | 1500 | False | - | - |
| Ethernet3/32/3 | P2P_red-leaf5_Ethernet54 | - | 100.83.94.66/31 | default | 1500 | False | - | - |
| Ethernet4/32/1 | P2P_media-PTP-2_Ethernet49 | - | 100.83.88.8/31 | default | 1500 | False | - | - |
| Ethernet4/32/2 | P2P_red-leaf3_Ethernet56 | - | 100.83.94.34/31 | default | 1500 | False | - | - |
| Ethernet4/32/3 | P2P_red-leaf5_Ethernet55 | - | 100.83.94.68/31 | default | 1500 | False | - | - |
| Ethernet5/33/3 | P2P_red-leaf5_Ethernet53 | - | 100.83.94.70/31 | default | 1500 | False | - | - |
| Ethernet6/4/1 | P2P_red-leaf2_Ethernet2/1 | - | 100.83.94.16/31 | default | 1500 | False | - | - |
| Ethernet6/5/1 | P2P_red-leaf2_Ethernet2/3 | - | 100.83.94.18/31 | default | 1500 | False | - | - |
| Ethernet6/6/1 | P2P_red-leaf2_Ethernet3/1 | - | 100.83.94.20/31 | default | 1500 | False | - | - |
| Ethernet6/7/1 | P2P_red-leaf4_Ethernet2/1 | - | 100.83.94.48/31 | default | 1500 | False | - | - |
| Ethernet6/8/1 | P2P_red-leaf4_Ethernet2/3 | - | 100.83.94.50/31 | default | 1500 | False | - | - |
| Ethernet6/9/1 | P2P_red-leaf6_Ethernet2/2 | - | 100.83.94.80/31 | default | 1500 | False | - | - |
| Ethernet6/18/1 | P2P_red-leaf1_Ethernet2/1 | - | 100.83.94.0/31 | default | 1500 | False | - | - |
| Ethernet6/19/1 | P2P_red-leaf1_Ethernet2/2 | - | 100.83.94.2/31 | default | 1500 | False | - | - |
| Ethernet6/20/1 | P2P_red-leaf1_Ethernet2/3 | - | 100.83.94.4/31 | default | 1500 | False | - | - |
| Ethernet6/21/1 | P2P_red-leaf7_Ethernet2/2 | - | 100.83.94.96/31 | default | 1500 | False | - | - |
| Ethernet6/22/1 | P2P_red-leaf8_Ethernet2/2 | - | 100.83.94.112/31 | default | 1500 | False | - | - |
| Ethernet6/23/1 | P2P_red-leaf9_Ethernet2/2 | - | 100.83.94.128/31 | default | 1500 | False | - | - |
| Ethernet6/24/1 | P2P_red-leaf10_Ethernet2/2 | - | 100.83.94.144/31 | default | 1500 | False | - | - |
| Ethernet6/25/1 | P2P_red-leaf11_Ethernet2/2 | - | 100.83.94.160/31 | default | 1500 | False | - | - |
| Ethernet6/26/1 | P2P_red-leaf12_Ethernet2/2 | - | 100.83.94.176/31 | default | 1500 | False | - | - |
| Ethernet6/27/1 | P2P_red-leaf13_Ethernet2/2 | - | 100.83.94.192/31 | default | 1500 | False | - | - |
| Ethernet6/28/1 | P2P_red-leaf14_Ethernet2/2 | - | 100.83.94.208/31 | default | 1500 | False | - | - |
| Ethernet6/29/1 | P2P_red-leaf15_Ethernet2/2 | - | 100.83.94.224/31 | default | 1500 | False | - | - |
| Ethernet6/30/1 | P2P_red-leaf16_Ethernet2/2 | - | 100.83.94.240/31 | default | 1500 | False | - | - |
| Ethernet7/1/1 | P2P_red-leaf1_Ethernet2/4 | - | 100.83.94.6/31 | default | 1500 | False | - | - |
| Ethernet7/2/1 | P2P_red-leaf1_Ethernet3/1 | - | 100.83.94.8/31 | default | 1500 | False | - | - |
| Ethernet7/3/1 | P2P_red-leaf1_Ethernet3/2 | - | 100.83.94.10/31 | default | 1500 | False | - | - |
| Ethernet7/4/1 | P2P_red-leaf2_Ethernet2/2 | - | 100.83.94.22/31 | default | 1500 | False | - | - |
| Ethernet7/5/1 | P2P_red-leaf2_Ethernet2/4 | - | 100.83.94.24/31 | default | 1500 | False | - | - |
| Ethernet7/6/1 | P2P_red-leaf2_Ethernet3/2 | - | 100.83.94.26/31 | default | 1500 | False | - | - |
| Ethernet7/7/1 | P2P_red-leaf4_Ethernet2/2 | - | 100.83.94.52/31 | default | 1500 | False | - | - |
| Ethernet7/8/1 | P2P_red-leaf6_Ethernet2/1 | - | 100.83.94.82/31 | default | 1500 | False | - | - |
| Ethernet7/10/1 | P2P_red-leaf7_Ethernet2/1 | - | 100.83.94.98/31 | default | 1500 | False | - | - |
| Ethernet7/11/1 | P2P_red-leaf8_Ethernet2/1 | - | 100.83.94.114/31 | default | 1500 | False | - | - |
| Ethernet7/12/1 | P2P_red-leaf8_Ethernet2/3 | - | 100.83.94.116/31 | default | 1500 | False | - | - |
| Ethernet7/13/1 | P2P_red-leaf10_Ethernet2/1 | - | 100.83.94.146/31 | default | 1500 | False | - | - |
| Ethernet7/15/1 | P2P_red-leaf11_Ethernet2/1 | - | 100.83.94.162/31 | default | 1500 | False | - | - |
| Ethernet7/17/1 | P2P_red-leaf12_Ethernet2/1 | - | 100.83.94.178/31 | default | 1500 | False | - | - |
| Ethernet7/18/1 | P2P_red-leaf13_Ethernet2/1 | - | 100.83.94.194/31 | default | 1500 | False | - | - |
| Ethernet7/19/1 | P2P_red-leaf14_Ethernet2/1 | - | 100.83.94.210/31 | default | 1500 | False | - | - |
| Ethernet7/21/1 | P2P_red-leaf16_Ethernet2/1 | - | 100.83.94.242/31 | default | 1500 | False | - | - |
| Ethernet7/23/1 | P2P_red-leaf15_Ethernet2/1 | - | 100.83.94.226/31 | default | 1500 | False | - | - |
| Ethernet7/33/1 | P2P_red-leaf9_Ethernet2/1 | - | 100.83.94.130/31 | default | 1500 | False | - | - |
| Ethernet8/29/1 | P2P_red-leaf17_Ethernet2/2 | - | 100.83.95.0/31 | default | 1500 | False | - | - |
| Ethernet8/30/1 | P2P_red-leaf18_Ethernet2/2 | - | 100.83.95.16/31 | default | 1500 | False | - | - |
| Ethernet8/31/1 | P2P_red-leaf19_Ethernet2/2 | - | 100.83.95.32/31 | default | 1500 | False | - | - |
| Ethernet8/32/1 | P2P_red-leaf20_Ethernet2/2 | - | 100.83.95.48/31 | default | 1500 | False | - | - |
| Ethernet8/33/1 | P2P_red-leaf21_Ethernet2/2 | - | 100.83.95.64/31 | default | 1500 | False | - | - |
| Ethernet8/34/1 | P2P_red-leaf22_Ethernet2/2 | - | 100.83.95.80/31 | default | 1500 | False | - | - |
| Ethernet8/35/1 | P2P_red-leaf23_Ethernet2/2 | - | 100.83.95.96/31 | default | 1500 | False | - | - |
| Ethernet8/36/1 | P2P_red-leaf24_Ethernet2/2 | - | 100.83.95.112/31 | default | 1500 | False | - | - |
| Ethernet8/37/1 | P2P_red-leaf25_Ethernet2/2 | - | 100.83.95.128/31 | default | 1500 | False | - | - |
| Ethernet8/38/1 | P2P_red-leaf26_Ethernet2/2 | - | 100.83.95.144/31 | default | 1500 | False | - | - |
| Ethernet8/39/1 | P2P_red-leaf27_Ethernet2/2 | - | 100.83.95.160/31 | default | 1500 | False | - | - |
| Ethernet8/40/1 | P2P_red-leaf28_Ethernet2/2 | - | 100.83.95.176/31 | default | 1500 | False | - | - |
| Ethernet8/41/1 | P2P_red-leaf29_Ethernet2/2 | - | 100.83.95.192/31 | default | 1500 | False | - | - |
| Ethernet8/42/1 | P2P_red-leaf30_Ethernet2/2 | - | 100.83.95.208/31 | default | 1500 | False | - | - |
| Ethernet8/43/1 | P2P_red-leaf31_Ethernet2/2 | - | 100.83.95.224/31 | default | 1500 | False | - | - |
| Ethernet8/44/1 | P2P_red-leaf32_Ethernet2/2 | - | 100.83.95.240/31 | default | 1500 | False | - | - |
| Ethernet9/21/1 | P2P_red-leaf17_Ethernet2/1 | - | 100.83.95.2/31 | default | 1500 | False | - | - |
| Ethernet9/23/1 | P2P_red-leaf18_Ethernet2/1 | - | 100.83.95.18/31 | default | 1500 | False | - | - |
| Ethernet9/25/1 | P2P_red-leaf19_Ethernet2/1 | - | 100.83.95.34/31 | default | 1500 | False | - | - |
| Ethernet9/27/1 | P2P_red-leaf20_Ethernet2/1 | - | 100.83.95.50/31 | default | 1500 | False | - | - |
| Ethernet9/29/1 | P2P_red-leaf21_Ethernet2/1 | - | 100.83.95.66/31 | default | 1500 | False | - | - |
| Ethernet9/31/1 | P2P_red-leaf22_Ethernet2/1 | - | 100.83.95.82/31 | default | 1500 | False | - | - |
| Ethernet9/33/1 | P2P_red-leaf23_Ethernet2/1 | - | 100.83.95.98/31 | default | 1500 | False | - | - |
| Ethernet9/35/1 | P2P_red-leaf24_Ethernet2/1 | - | 100.83.95.114/31 | default | 1500 | False | - | - |
| Ethernet9/37/1 | P2P_red-leaf25_Ethernet2/1 | - | 100.83.95.130/31 | default | 1500 | False | - | - |
| Ethernet9/39/1 | P2P_red-leaf26_Ethernet2/1 | - | 100.83.95.146/31 | default | 1500 | False | - | - |
| Ethernet9/41/1 | P2P_red-leaf27_Ethernet2/1 | - | 100.83.95.162/31 | default | 1500 | False | - | - |
| Ethernet9/43/1 | P2P_red-leaf28_Ethernet2/1 | - | 100.83.95.178/31 | default | 1500 | False | - | - |
| Ethernet9/45/1 | P2P_red-leaf29_Ethernet2/1 | - | 100.83.95.194/31 | default | 1500 | False | - | - |
| Ethernet9/47/1 | P2P_red-leaf30_Ethernet2/1 | - | 100.83.95.210/31 | default | 1500 | False | - | - |
| Ethernet9/49/1 | P2P_red-leaf31_Ethernet2/1 | - | 100.83.95.226/31 | default | 1500 | False | - | - |
| Ethernet9/51/1 | P2P_red-leaf32_Ethernet2/1 | - | 100.83.95.242/31 | default | 1500 | False | - | - |
| Ethernet9/52/1 | P2P_red-leaf8_Ethernet2/4 | - | 100.83.94.118/31 | default | 1500 | False | - | - |
| Ethernet33/1 | P2P_border-leaf1_Ethernet31/1 | - | 100.83.88.16/31 | default | 1500 | False | - | - |
| Ethernet34/1 | P2P_border-leaf2_Ethernet31/1 | - | 100.83.88.24/31 | default | 1500 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet3/31/4
   description P2P_red-leaf5_Ethernet56
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.64/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet3/32/1
   description P2P_media-PTP-1_Ethernet49
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
interface Ethernet3/32/2
   description P2P_red-leaf3_Ethernet55
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.32/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet3/32/3
   description P2P_red-leaf5_Ethernet54
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.66/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/32/1
   description P2P_media-PTP-2_Ethernet49
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
!
interface Ethernet4/32/2
   description P2P_red-leaf3_Ethernet56
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.34/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/32/3
   description P2P_red-leaf5_Ethernet55
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.68/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/33/3
   description P2P_red-leaf5_Ethernet53
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.70/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/4/1
   description P2P_red-leaf2_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.16/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/5/1
   description P2P_red-leaf2_Ethernet2/3
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.18/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/6/1
   description P2P_red-leaf2_Ethernet3/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.20/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/7/1
   description P2P_red-leaf4_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.48/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/8/1
   description P2P_red-leaf4_Ethernet2/3
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.50/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/9/1
   description P2P_red-leaf6_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.80/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/18/1
   description P2P_red-leaf1_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.0/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/19/1
   description P2P_red-leaf1_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.2/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/20/1
   description P2P_red-leaf1_Ethernet2/3
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.4/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/21/1
   description P2P_red-leaf7_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.96/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/22/1
   description P2P_red-leaf8_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.112/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/23/1
   description P2P_red-leaf9_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.128/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/24/1
   description P2P_red-leaf10_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.144/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/25/1
   description P2P_red-leaf11_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.160/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/26/1
   description P2P_red-leaf12_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.176/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/27/1
   description P2P_red-leaf13_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.192/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/28/1
   description P2P_red-leaf14_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.208/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/29/1
   description P2P_red-leaf15_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.224/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/30/1
   description P2P_red-leaf16_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.240/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/1/1
   description P2P_red-leaf1_Ethernet2/4
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.6/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/2/1
   description P2P_red-leaf1_Ethernet3/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.8/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/3/1
   description P2P_red-leaf1_Ethernet3/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.10/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/4/1
   description P2P_red-leaf2_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.22/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/5/1
   description P2P_red-leaf2_Ethernet2/4
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.24/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/6/1
   description P2P_red-leaf2_Ethernet3/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.26/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/7/1
   description P2P_red-leaf4_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.52/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/8/1
   description P2P_red-leaf6_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.82/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/10/1
   description P2P_red-leaf7_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.98/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/11/1
   description P2P_red-leaf8_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.114/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/12/1
   description P2P_red-leaf8_Ethernet2/3
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.116/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/13/1
   description P2P_red-leaf10_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.146/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/15/1
   description P2P_red-leaf11_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.162/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/17/1
   description P2P_red-leaf12_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.178/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/18/1
   description P2P_red-leaf13_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.194/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/19/1
   description P2P_red-leaf14_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.210/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/21/1
   description P2P_red-leaf16_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.242/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/23/1
   description P2P_red-leaf15_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.226/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet7/33/1
   description P2P_red-leaf9_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.130/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/29/1
   description P2P_red-leaf17_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.0/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/30/1
   description P2P_red-leaf18_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.16/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/31/1
   description P2P_red-leaf19_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.32/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/32/1
   description P2P_red-leaf20_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.48/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/33/1
   description P2P_red-leaf21_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.64/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/34/1
   description P2P_red-leaf22_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.80/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/35/1
   description P2P_red-leaf23_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.96/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/36/1
   description P2P_red-leaf24_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.112/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/37/1
   description P2P_red-leaf25_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.128/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/38/1
   description P2P_red-leaf26_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.144/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/39/1
   description P2P_red-leaf27_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.160/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/40/1
   description P2P_red-leaf28_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.176/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/41/1
   description P2P_red-leaf29_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.192/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/42/1
   description P2P_red-leaf30_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.208/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/43/1
   description P2P_red-leaf31_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.224/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet8/44/1
   description P2P_red-leaf32_Ethernet2/2
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.240/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/21/1
   description P2P_red-leaf17_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.2/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/23/1
   description P2P_red-leaf18_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.18/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/25/1
   description P2P_red-leaf19_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.34/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/27/1
   description P2P_red-leaf20_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.50/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/29/1
   description P2P_red-leaf21_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.66/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/31/1
   description P2P_red-leaf22_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.82/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/33/1
   description P2P_red-leaf23_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.98/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/35/1
   description P2P_red-leaf24_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.114/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/37/1
   description P2P_red-leaf25_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.130/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/39/1
   description P2P_red-leaf26_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.146/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/41/1
   description P2P_red-leaf27_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.162/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/43/1
   description P2P_red-leaf28_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.178/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/45/1
   description P2P_red-leaf29_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.194/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/47/1
   description P2P_red-leaf30_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.210/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/49/1
   description P2P_red-leaf31_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.226/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/51/1
   description P2P_red-leaf32_Ethernet2/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.95.242/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet9/52/1
   description P2P_red-leaf8_Ethernet2/4
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.94.118/31
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet33/1
   description P2P_border-leaf1_Ethernet31/1
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
   description P2P_border-leaf2_Ethernet31/1
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
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ROUTER_ID | default | 169.27.195.0/32 |

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
   ip address 169.27.195.0/32
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
| 65210.37100 | 169.27.195.0 |

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
| 100.83.94.1 | 65210.37101 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.3 | 65210.37101 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.5 | 65210.37101 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.7 | 65210.37101 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.9 | 65210.37101 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.11 | 65210.37101 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.17 | 65210.37102 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.19 | 65210.37102 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.21 | 65210.37102 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.23 | 65210.37102 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.25 | 65210.37102 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.27 | 65210.37102 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.33 | 65210.37105 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.35 | 65210.37105 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.49 | 5210.37103 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.51 | 5210.37103 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.53 | 5210.37103 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.65 | 65210.37106 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.67 | 65210.37106 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.69 | 65210.37106 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.71 | 65210.37106 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.81 | 65210.37104 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.83 | 65210.37104 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.97 | 65021.7 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.99 | 65021.7 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.113 | 65021.8 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.115 | 65021.8 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.117 | 65021.8 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.119 | 65021.8 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.129 | 65021.9 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.131 | 65021.9 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.145 | 65021.10 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.147 | 65021.10 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.161 | 65021.11 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.163 | 65021.11 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.177 | 65021.12 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.179 | 65021.12 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.193 | 65021.13 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.195 | 65021.13 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.209 | 65021.14 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.211 | 65021.14 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.225 | 65021.15 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.227 | 65021.15 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.241 | 65021.16 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.94.243 | 65021.16 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.1 | 65021.17 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.3 | 65021.17 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.17 | 65021.18 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.19 | 65021.18 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.33 | 65021.19 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.35 | 65021.19 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.49 | 65021.20 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.51 | 65021.20 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.65 | 65021.21 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.67 | 65021.21 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.81 | 65021.22 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.83 | 65021.22 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.97 | 65021.23 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.99 | 65021.23 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.113 | 65021.24 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.115 | 65021.24 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.129 | 65021.25 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.131 | 65021.25 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.145 | 65021.26 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.147 | 65021.26 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.161 | 65021.27 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.163 | 65021.27 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.177 | 65021.28 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.179 | 65021.28 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.193 | 65021.29 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.195 | 65021.29 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.209 | 65021.30 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.211 | 65021.30 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.225 | 65021.31 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.227 | 65021.31 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.241 | 65021.32 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.95.243 | 65021.32 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65210.37100
   router-id 169.27.195.0
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
   neighbor 100.83.88.1 description media-PTP-1_Ethernet49
   neighbor 100.83.88.9 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.9 remote-as 65213.37370
   neighbor 100.83.88.9 description media-PTP-2_Ethernet49
   neighbor 100.83.88.17 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.17 remote-as 65214
   neighbor 100.83.88.17 description border-leaf1_Ethernet31/1
   neighbor 100.83.88.25 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.25 remote-as 65214
   neighbor 100.83.88.25 description border-leaf2_Ethernet31/1
   neighbor 100.83.94.1 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.1 remote-as 65210.37101
   neighbor 100.83.94.1 description red-leaf1_Ethernet2/1
   neighbor 100.83.94.3 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.3 remote-as 65210.37101
   neighbor 100.83.94.3 description red-leaf1_Ethernet2/2
   neighbor 100.83.94.5 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.5 remote-as 65210.37101
   neighbor 100.83.94.5 description red-leaf1_Ethernet2/3
   neighbor 100.83.94.7 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.7 remote-as 65210.37101
   neighbor 100.83.94.7 description red-leaf1_Ethernet2/4
   neighbor 100.83.94.9 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.9 remote-as 65210.37101
   neighbor 100.83.94.9 description red-leaf1_Ethernet3/1
   neighbor 100.83.94.11 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.11 remote-as 65210.37101
   neighbor 100.83.94.11 description red-leaf1_Ethernet3/2
   neighbor 100.83.94.17 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.17 remote-as 65210.37102
   neighbor 100.83.94.17 description red-leaf2_Ethernet2/1
   neighbor 100.83.94.19 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.19 remote-as 65210.37102
   neighbor 100.83.94.19 description red-leaf2_Ethernet2/3
   neighbor 100.83.94.21 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.21 remote-as 65210.37102
   neighbor 100.83.94.21 description red-leaf2_Ethernet3/1
   neighbor 100.83.94.23 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.23 remote-as 65210.37102
   neighbor 100.83.94.23 description red-leaf2_Ethernet2/2
   neighbor 100.83.94.25 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.25 remote-as 65210.37102
   neighbor 100.83.94.25 description red-leaf2_Ethernet2/4
   neighbor 100.83.94.27 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.27 remote-as 65210.37102
   neighbor 100.83.94.27 description red-leaf2_Ethernet3/2
   neighbor 100.83.94.33 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.33 remote-as 65210.37105
   neighbor 100.83.94.33 description red-leaf3_Ethernet55
   neighbor 100.83.94.35 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.35 remote-as 65210.37105
   neighbor 100.83.94.35 description red-leaf3_Ethernet56
   neighbor 100.83.94.49 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.49 remote-as 5210.37103
   neighbor 100.83.94.49 description red-leaf4_Ethernet2/1
   neighbor 100.83.94.51 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.51 remote-as 5210.37103
   neighbor 100.83.94.51 description red-leaf4_Ethernet2/3
   neighbor 100.83.94.53 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.53 remote-as 5210.37103
   neighbor 100.83.94.53 description red-leaf4_Ethernet2/2
   neighbor 100.83.94.65 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.65 remote-as 65210.37106
   neighbor 100.83.94.65 description red-leaf5_Ethernet56
   neighbor 100.83.94.67 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.67 remote-as 65210.37106
   neighbor 100.83.94.67 description red-leaf5_Ethernet54
   neighbor 100.83.94.69 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.69 remote-as 65210.37106
   neighbor 100.83.94.69 description red-leaf5_Ethernet55
   neighbor 100.83.94.71 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.71 remote-as 65210.37106
   neighbor 100.83.94.71 description red-leaf5_Ethernet53
   neighbor 100.83.94.81 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.81 remote-as 65210.37104
   neighbor 100.83.94.81 description red-leaf6_Ethernet2/2
   neighbor 100.83.94.83 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.83 remote-as 65210.37104
   neighbor 100.83.94.83 description red-leaf6_Ethernet2/1
   neighbor 100.83.94.97 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.97 remote-as 65021.7
   neighbor 100.83.94.97 description red-leaf7_Ethernet2/2
   neighbor 100.83.94.99 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.99 remote-as 65021.7
   neighbor 100.83.94.99 description red-leaf7_Ethernet2/1
   neighbor 100.83.94.113 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.113 remote-as 65021.8
   neighbor 100.83.94.113 description red-leaf8_Ethernet2/2
   neighbor 100.83.94.115 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.115 remote-as 65021.8
   neighbor 100.83.94.115 description red-leaf8_Ethernet2/1
   neighbor 100.83.94.117 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.117 remote-as 65021.8
   neighbor 100.83.94.117 description red-leaf8_Ethernet2/3
   neighbor 100.83.94.119 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.119 remote-as 65021.8
   neighbor 100.83.94.119 description red-leaf8_Ethernet2/4
   neighbor 100.83.94.129 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.129 remote-as 65021.9
   neighbor 100.83.94.129 description red-leaf9_Ethernet2/2
   neighbor 100.83.94.131 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.131 remote-as 65021.9
   neighbor 100.83.94.131 description red-leaf9_Ethernet2/1
   neighbor 100.83.94.145 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.145 remote-as 65021.10
   neighbor 100.83.94.145 description red-leaf10_Ethernet2/2
   neighbor 100.83.94.147 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.147 remote-as 65021.10
   neighbor 100.83.94.147 description red-leaf10_Ethernet2/1
   neighbor 100.83.94.161 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.161 remote-as 65021.11
   neighbor 100.83.94.161 description red-leaf11_Ethernet2/2
   neighbor 100.83.94.163 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.163 remote-as 65021.11
   neighbor 100.83.94.163 description red-leaf11_Ethernet2/1
   neighbor 100.83.94.177 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.177 remote-as 65021.12
   neighbor 100.83.94.177 description red-leaf12_Ethernet2/2
   neighbor 100.83.94.179 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.179 remote-as 65021.12
   neighbor 100.83.94.179 description red-leaf12_Ethernet2/1
   neighbor 100.83.94.193 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.193 remote-as 65021.13
   neighbor 100.83.94.193 description red-leaf13_Ethernet2/2
   neighbor 100.83.94.195 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.195 remote-as 65021.13
   neighbor 100.83.94.195 description red-leaf13_Ethernet2/1
   neighbor 100.83.94.209 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.209 remote-as 65021.14
   neighbor 100.83.94.209 description red-leaf14_Ethernet2/2
   neighbor 100.83.94.211 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.211 remote-as 65021.14
   neighbor 100.83.94.211 description red-leaf14_Ethernet2/1
   neighbor 100.83.94.225 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.225 remote-as 65021.15
   neighbor 100.83.94.225 description red-leaf15_Ethernet2/2
   neighbor 100.83.94.227 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.227 remote-as 65021.15
   neighbor 100.83.94.227 description red-leaf15_Ethernet2/1
   neighbor 100.83.94.241 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.241 remote-as 65021.16
   neighbor 100.83.94.241 description red-leaf16_Ethernet2/2
   neighbor 100.83.94.243 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.94.243 remote-as 65021.16
   neighbor 100.83.94.243 description red-leaf16_Ethernet2/1
   neighbor 100.83.95.1 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.1 remote-as 65021.17
   neighbor 100.83.95.1 description red-leaf17_Ethernet2/2
   neighbor 100.83.95.3 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.3 remote-as 65021.17
   neighbor 100.83.95.3 description red-leaf17_Ethernet2/1
   neighbor 100.83.95.17 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.17 remote-as 65021.18
   neighbor 100.83.95.17 description red-leaf18_Ethernet2/2
   neighbor 100.83.95.19 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.19 remote-as 65021.18
   neighbor 100.83.95.19 description red-leaf18_Ethernet2/1
   neighbor 100.83.95.33 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.33 remote-as 65021.19
   neighbor 100.83.95.33 description red-leaf19_Ethernet2/2
   neighbor 100.83.95.35 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.35 remote-as 65021.19
   neighbor 100.83.95.35 description red-leaf19_Ethernet2/1
   neighbor 100.83.95.49 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.49 remote-as 65021.20
   neighbor 100.83.95.49 description red-leaf20_Ethernet2/2
   neighbor 100.83.95.51 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.51 remote-as 65021.20
   neighbor 100.83.95.51 description red-leaf20_Ethernet2/1
   neighbor 100.83.95.65 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.65 remote-as 65021.21
   neighbor 100.83.95.65 description red-leaf21_Ethernet2/2
   neighbor 100.83.95.67 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.67 remote-as 65021.21
   neighbor 100.83.95.67 description red-leaf21_Ethernet2/1
   neighbor 100.83.95.81 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.81 remote-as 65021.22
   neighbor 100.83.95.81 description red-leaf22_Ethernet2/2
   neighbor 100.83.95.83 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.83 remote-as 65021.22
   neighbor 100.83.95.83 description red-leaf22_Ethernet2/1
   neighbor 100.83.95.97 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.97 remote-as 65021.23
   neighbor 100.83.95.97 description red-leaf23_Ethernet2/2
   neighbor 100.83.95.99 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.99 remote-as 65021.23
   neighbor 100.83.95.99 description red-leaf23_Ethernet2/1
   neighbor 100.83.95.113 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.113 remote-as 65021.24
   neighbor 100.83.95.113 description red-leaf24_Ethernet2/2
   neighbor 100.83.95.115 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.115 remote-as 65021.24
   neighbor 100.83.95.115 description red-leaf24_Ethernet2/1
   neighbor 100.83.95.129 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.129 remote-as 65021.25
   neighbor 100.83.95.129 description red-leaf25_Ethernet2/2
   neighbor 100.83.95.131 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.131 remote-as 65021.25
   neighbor 100.83.95.131 description red-leaf25_Ethernet2/1
   neighbor 100.83.95.145 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.145 remote-as 65021.26
   neighbor 100.83.95.145 description red-leaf26_Ethernet2/2
   neighbor 100.83.95.147 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.147 remote-as 65021.26
   neighbor 100.83.95.147 description red-leaf26_Ethernet2/1
   neighbor 100.83.95.161 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.161 remote-as 65021.27
   neighbor 100.83.95.161 description red-leaf27_Ethernet2/2
   neighbor 100.83.95.163 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.163 remote-as 65021.27
   neighbor 100.83.95.163 description red-leaf27_Ethernet2/1
   neighbor 100.83.95.177 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.177 remote-as 65021.28
   neighbor 100.83.95.177 description red-leaf28_Ethernet2/2
   neighbor 100.83.95.179 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.179 remote-as 65021.28
   neighbor 100.83.95.179 description red-leaf28_Ethernet2/1
   neighbor 100.83.95.193 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.193 remote-as 65021.29
   neighbor 100.83.95.193 description red-leaf29_Ethernet2/2
   neighbor 100.83.95.195 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.195 remote-as 65021.29
   neighbor 100.83.95.195 description red-leaf29_Ethernet2/1
   neighbor 100.83.95.209 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.209 remote-as 65021.30
   neighbor 100.83.95.209 description red-leaf30_Ethernet2/2
   neighbor 100.83.95.211 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.211 remote-as 65021.30
   neighbor 100.83.95.211 description red-leaf30_Ethernet2/1
   neighbor 100.83.95.225 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.225 remote-as 65021.31
   neighbor 100.83.95.225 description red-leaf31_Ethernet2/2
   neighbor 100.83.95.227 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.227 remote-as 65021.31
   neighbor 100.83.95.227 description red-leaf31_Ethernet2/1
   neighbor 100.83.95.241 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.241 remote-as 65021.32
   neighbor 100.83.95.241 description red-leaf32_Ethernet2/2
   neighbor 100.83.95.243 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.95.243 remote-as 65021.32
   neighbor 100.83.95.243 description red-leaf32_Ethernet2/1
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
