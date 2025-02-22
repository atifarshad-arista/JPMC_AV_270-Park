# blue-spine1

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
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Device Configuration](#internal-vlan-allocation-policy-device-configuration)
- [Interfaces](#interfaces)
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
| Management1 | OOB_MANAGEMENT | oob | MGMT | 10.100.100.4/24 | 10.100.100.1 |

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
   ip address 10.100.100.4/24
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
| 00:1C:73:14:00:01 | - | 20 | 1 | - | 127 | boundary | - |

#### PTP Device Configuration

```eos
!
ptp clock-identity 00:1C:73:14:00:01
ptp domain 127
ptp mode boundary
ptp priority1 20
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

### Ethernet Interfaces

#### Ethernet Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |

*Inherited from Port-Channel Interface

##### IPv4

| Interface | Description | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet4/11/1 | P2P_blue-leaf1_Ethernet49/1 | - | 100.83.88.40/31 | default | 1500 | False | - | - |
| Ethernet4/12/1 | P2P_blue-leaf1_Ethernet50/1 | - | 100.83.88.42/31 | default | 1500 | False | - | - |
| Ethernet4/13/1 | P2P_blue-leaf2_Ethernet49/1 | - | 100.83.88.48/31 | default | 1500 | False | - | - |
| Ethernet4/14/1 | P2P_blue-leaf2_Ethernet50/1 | - | 100.83.88.50/31 | default | 1500 | False | - | - |
| Ethernet4/15/1 | P2P_blue-leaf3_Ethernet49/1 | - | 100.83.88.56/31 | default | 1500 | False | - | - |
| Ethernet4/16/1 | P2P_blue-leaf3_Ethernet50/1 | - | 100.83.88.58/31 | default | 1500 | False | - | - |
| Ethernet4/17/1 | P2P_blue-leaf4_Ethernet49/1 | - | 100.83.88.64/31 | default | 1500 | False | - | - |
| Ethernet4/18/1 | P2P_blue-leaf4_Ethernet50/1 | - | 100.83.88.66/31 | default | 1500 | False | - | - |
| Ethernet4/19/1 | P2P_blue-leaf5_Ethernet49/1 | - | 100.83.88.72/31 | default | 1500 | False | - | - |
| Ethernet4/20/1 | P2P_blue-leaf5_Ethernet50/1 | - | 100.83.88.74/31 | default | 1500 | False | - | - |
| Ethernet4/21/1 | P2P_blue-leaf6_Ethernet49/1 | - | 100.83.88.80/31 | default | 1500 | False | - | - |
| Ethernet4/22/1 | P2P_blue-leaf6_Ethernet50/1 | - | 100.83.88.82/31 | default | 1500 | False | - | - |
| Ethernet4/23/1 | P2P_blue-leaf7_Ethernet49/1 | - | 100.83.88.88/31 | default | 1500 | False | - | - |
| Ethernet4/24/1 | P2P_blue-leaf7_Ethernet50/1 | - | 100.83.88.90/31 | default | 1500 | False | - | - |
| Ethernet4/25/1 | P2P_blue-leaf8_Ethernet49/1 | - | 100.83.88.96/31 | default | 1500 | False | - | - |
| Ethernet4/26/1 | P2P_blue-leaf8_Ethernet50/1 | - | 100.83.88.98/31 | default | 1500 | False | - | - |
| Ethernet4/27/1 | P2P_blue-leaf9_Ethernet49/1 | - | 100.83.88.104/31 | default | 1500 | False | - | - |
| Ethernet4/28/1 | P2P_blue-leaf9_Ethernet50/1 | - | 100.83.88.106/31 | default | 1500 | False | - | - |
| Ethernet4/29/1 | P2P_blue-leaf10_Ethernet49/1 | - | 100.83.88.112/31 | default | 1500 | False | - | - |
| Ethernet4/30/1 | P2P_blue-leaf10_Ethernet50/1 | - | 100.83.88.114/31 | default | 1500 | False | - | - |
| Ethernet4/31/1 | P2P_blue-leaf11_Ethernet49/1 | - | 100.83.88.120/31 | default | 1500 | False | - | - |
| Ethernet4/32/1 | P2P_blue-leaf11_Ethernet50/1 | - | 100.83.88.122/31 | default | 1500 | False | - | - |
| Ethernet4/33/1 | P2P_blue-leaf12_Ethernet49/1 | - | 100.83.88.128/31 | default | 1500 | False | - | - |
| Ethernet4/34/1 | P2P_blue-leaf12_Ethernet50/1 | - | 100.83.88.130/31 | default | 1500 | False | - | - |
| Ethernet4/35/1 | P2P_blue-leaf13_Ethernet49/1 | - | 100.83.88.136/31 | default | 1500 | False | - | - |
| Ethernet4/36/1 | P2P_blue-leaf13_Ethernet50/1 | - | 100.83.88.138/31 | default | 1500 | False | - | - |
| Ethernet5/1/1 | P2P_blue-leaf14_Ethernet49/1 | - | 100.83.88.144/31 | default | 1500 | False | - | - |
| Ethernet5/2/1 | P2P_blue-leaf14_Ethernet50/1 | - | 100.83.88.146/31 | default | 1500 | False | - | - |
| Ethernet5/3/1 | P2P_blue-leaf15_Ethernet49/1 | - | 100.83.88.152/31 | default | 1500 | False | - | - |
| Ethernet5/4/1 | P2P_blue-leaf15_Ethernet50/1 | - | 100.83.88.154/31 | default | 1500 | False | - | - |
| Ethernet5/5/1 | P2P_blue-leaf16_Ethernet49/1 | - | 100.83.88.160/31 | default | 1500 | False | - | - |
| Ethernet5/6/1 | P2P_blue-leaf16_Ethernet50/1 | - | 100.83.88.162/31 | default | 1500 | False | - | - |
| Ethernet5/7/1 | P2P_blue-leaf17_Ethernet49/1 | - | 100.83.88.168/31 | default | 1500 | False | - | - |
| Ethernet5/8/1 | P2P_blue-leaf17_Ethernet50/1 | - | 100.83.88.170/31 | default | 1500 | False | - | - |
| Ethernet5/9/1 | P2P_blue-leaf18_Ethernet49/1 | - | 100.83.88.176/31 | default | 1500 | False | - | - |
| Ethernet5/10/1 | P2P_blue-leaf18_Ethernet50/1 | - | 100.83.88.178/31 | default | 1500 | False | - | - |
| Ethernet5/11/1 | P2P_blue-leaf19_Ethernet49/1 | - | 100.83.88.184/31 | default | 1500 | False | - | - |
| Ethernet5/12/1 | P2P_blue-leaf19_Ethernet50/1 | - | 100.83.88.186/31 | default | 1500 | False | - | - |
| Ethernet5/13/1 | P2P_blue-leaf20_Ethernet49/1 | - | 100.83.88.192/31 | default | 1500 | False | - | - |
| Ethernet5/14/1 | P2P_blue-leaf20_Ethernet50/1 | - | 100.83.88.194/31 | default | 1500 | False | - | - |
| Ethernet5/15/1 | P2P_blue-leaf21_Ethernet49/1 | - | 100.83.88.200/31 | default | 1500 | False | - | - |
| Ethernet5/16/1 | P2P_blue-leaf21_Ethernet50/1 | - | 100.83.88.202/31 | default | 1500 | False | - | - |
| Ethernet5/17/1 | P2P_blue-leaf22_Ethernet49/1 | - | 100.83.88.208/31 | default | 1500 | False | - | - |
| Ethernet5/18/1 | P2P_blue-leaf22_Ethernet50/1 | - | 100.83.88.210/31 | default | 1500 | False | - | - |
| Ethernet5/19/1 | P2P_blue-leaf23_Ethernet49/1 | - | 100.83.88.216/31 | default | 1500 | False | - | - |
| Ethernet5/20/1 | P2P_blue-leaf23_Ethernet50/1 | - | 100.83.88.218/31 | default | 1500 | False | - | - |
| Ethernet5/21/1 | P2P_blue-leaf24_Ethernet49/1 | - | 100.83.88.224/31 | default | 1500 | False | - | - |
| Ethernet5/22/1 | P2P_blue-leaf24_Ethernet50/1 | - | 100.83.88.226/31 | default | 1500 | False | - | - |
| Ethernet5/23/1 | P2P_blue-leaf25_Ethernet49/1 | - | 100.83.88.232/31 | default | 1500 | False | - | - |
| Ethernet5/24/1 | P2P_blue-leaf25_Ethernet50/1 | - | 100.83.88.234/31 | default | 1500 | False | - | - |
| Ethernet5/25/1 | P2P_blue-leaf26_Ethernet49/1 | - | 100.83.88.240/31 | default | 1500 | False | - | - |
| Ethernet5/26/1 | P2P_blue-leaf26_Ethernet50/1 | - | 100.83.88.242/31 | default | 1500 | False | - | - |
| Ethernet5/27/1 | P2P_blue-leaf27_Ethernet49/1 | - | 100.83.88.248/31 | default | 1500 | False | - | - |
| Ethernet5/28/1 | P2P_blue-leaf27_Ethernet50/1 | - | 100.83.88.250/31 | default | 1500 | False | - | - |
| Ethernet5/29/1 | P2P_blue-leaf28_Ethernet49/1 | - | 100.83.89.0/31 | default | 1500 | False | - | - |
| Ethernet5/30/1 | P2P_blue-leaf28_Ethernet50/1 | - | 100.83.89.2/31 | default | 1500 | False | - | - |
| Ethernet5/31/1 | P2P_blue-leaf29_Ethernet49/1 | - | 100.83.89.8/31 | default | 1500 | False | - | - |
| Ethernet5/32/1 | P2P_blue-leaf29_Ethernet50/1 | - | 100.83.89.10/31 | default | 1500 | False | - | - |
| Ethernet5/33/1 | P2P_blue-leaf30_Ethernet49/1 | - | 100.83.89.16/31 | default | 1500 | False | - | - |
| Ethernet5/34/1 | P2P_blue-leaf30_Ethernet50/1 | - | 100.83.89.18/31 | default | 1500 | False | - | - |
| Ethernet5/35/1 | P2P_blue-leaf31_Ethernet49/1 | - | 100.83.89.24/31 | default | 1500 | False | - | - |
| Ethernet5/36/1 | P2P_blue-leaf31_Ethernet50/1 | - | 100.83.89.26/31 | default | 1500 | False | - | - |
| Ethernet6/1/1 | P2P_blue-leaf32_Ethernet49/1 | - | 100.83.89.32/31 | default | 1500 | False | - | - |
| Ethernet6/2/1 | P2P_blue-leaf32_Ethernet50/1 | - | 100.83.89.34/31 | default | 1500 | False | - | - |
| Ethernet33/1 | P2P_border-leaf1_Ethernet34/1 | - | 100.83.88.18/31 | default | 1500 | False | - | - |
| Ethernet34/1 | P2P_border-leaf2_Ethernet34/1 | - | 100.83.88.26/31 | default | 1500 | False | - | - |
| Ethernet49/1 | P2P_media-PTP-1_Ethernet50/1 | - | 100.83.88.2/31 | default | 1500 | False | - | - |
| Ethernet50/1 | P2P_media-PTP-2_Ethernet50/1 | - | 100.83.88.10/31 | default | 1500 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet4/11/1
   description P2P_blue-leaf1_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.40/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/12/1
   description P2P_blue-leaf1_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.42/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/13/1
   description P2P_blue-leaf2_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.48/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/14/1
   description P2P_blue-leaf2_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.50/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/15/1
   description P2P_blue-leaf3_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.56/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/16/1
   description P2P_blue-leaf3_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.58/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/17/1
   description P2P_blue-leaf4_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.64/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/18/1
   description P2P_blue-leaf4_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.66/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/19/1
   description P2P_blue-leaf5_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.72/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/20/1
   description P2P_blue-leaf5_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.74/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/21/1
   description P2P_blue-leaf6_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.80/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/22/1
   description P2P_blue-leaf6_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.82/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/23/1
   description P2P_blue-leaf7_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.88/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/24/1
   description P2P_blue-leaf7_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.90/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/25/1
   description P2P_blue-leaf8_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.96/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/26/1
   description P2P_blue-leaf8_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.98/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/27/1
   description P2P_blue-leaf9_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.104/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/28/1
   description P2P_blue-leaf9_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.106/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/29/1
   description P2P_blue-leaf10_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.112/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/30/1
   description P2P_blue-leaf10_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.114/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/31/1
   description P2P_blue-leaf11_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.120/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/32/1
   description P2P_blue-leaf11_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.122/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/33/1
   description P2P_blue-leaf12_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.128/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/34/1
   description P2P_blue-leaf12_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.130/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/35/1
   description P2P_blue-leaf13_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.136/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet4/36/1
   description P2P_blue-leaf13_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.138/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/1/1
   description P2P_blue-leaf14_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.144/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/2/1
   description P2P_blue-leaf14_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.146/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/3/1
   description P2P_blue-leaf15_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.152/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/4/1
   description P2P_blue-leaf15_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.154/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/5/1
   description P2P_blue-leaf16_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.160/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/6/1
   description P2P_blue-leaf16_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.162/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/7/1
   description P2P_blue-leaf17_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.168/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/8/1
   description P2P_blue-leaf17_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.170/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/9/1
   description P2P_blue-leaf18_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.176/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/10/1
   description P2P_blue-leaf18_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.178/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/11/1
   description P2P_blue-leaf19_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.184/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/12/1
   description P2P_blue-leaf19_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.186/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/13/1
   description P2P_blue-leaf20_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.192/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/14/1
   description P2P_blue-leaf20_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.194/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/15/1
   description P2P_blue-leaf21_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.200/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/16/1
   description P2P_blue-leaf21_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.202/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/17/1
   description P2P_blue-leaf22_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.208/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/18/1
   description P2P_blue-leaf22_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.210/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/19/1
   description P2P_blue-leaf23_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.216/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/20/1
   description P2P_blue-leaf23_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.218/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/21/1
   description P2P_blue-leaf24_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.224/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/22/1
   description P2P_blue-leaf24_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.226/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/23/1
   description P2P_blue-leaf25_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.232/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/24/1
   description P2P_blue-leaf25_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.234/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/25/1
   description P2P_blue-leaf26_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.240/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/26/1
   description P2P_blue-leaf26_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.242/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/27/1
   description P2P_blue-leaf27_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.248/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/28/1
   description P2P_blue-leaf27_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.250/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/29/1
   description P2P_blue-leaf28_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.89.0/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/30/1
   description P2P_blue-leaf28_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.89.2/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/31/1
   description P2P_blue-leaf29_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.89.8/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/32/1
   description P2P_blue-leaf29_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.89.10/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/33/1
   description P2P_blue-leaf30_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.89.16/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/34/1
   description P2P_blue-leaf30_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.89.18/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/35/1
   description P2P_blue-leaf31_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.89.24/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet5/36/1
   description P2P_blue-leaf31_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.89.26/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/1/1
   description P2P_blue-leaf32_Ethernet49/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.89.32/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet6/2/1
   description P2P_blue-leaf32_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.89.34/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet33/1
   description P2P_border-leaf1_Ethernet34/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.18/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet34/1
   description P2P_border-leaf2_Ethernet34/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.26/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet49/1
   description P2P_media-PTP-1_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.2/31
   pim ipv4 sparse-mode
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Ethernet50/1
   description P2P_media-PTP-2_Ethernet50/1
   no shutdown
   mtu 1500
   no switchport
   ip address 100.83.88.10/31
   pim ipv4 sparse-mode
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

### Static Routes

#### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP | Exit interface | Administrative Distance | Tag | Route Name | Metric |
| --- | ------------------ | ----------- | -------------- | ----------------------- | --- | ---------- | ------ |
| MGMT | 0.0.0.0/0 | 10.100.100.1 | - | 1 | - | - | - |

#### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 0.0.0.0/0 10.100.100.1
```

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65010.1 | 169.27.195.1 |

| BGP Tuning |
| ---------- |
| bgp asn notation asdot |
| no bgp default ipv4-unicast |
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
| 100.83.88.3 | 65003.1 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.11 | 65003.1 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.19 | 65003.2 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.27 | 65003.2 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.41 | 65011.1 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.43 | 65011.1 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.49 | 65011.2 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.51 | 65011.2 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.57 | 65011.3 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.59 | 65011.3 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.65 | 65011.4 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.67 | 65011.4 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.73 | 65011.5 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.75 | 65011.5 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.81 | 65011.6 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.83 | 65011.6 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.89 | 65011.7 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.91 | 65011.7 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.97 | 65011.8 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.99 | 65011.8 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.105 | 65011.9 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.107 | 65011.9 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.113 | 65011.10 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.115 | 65011.10 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.121 | 65011.11 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.123 | 65011.11 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.129 | 65011.12 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.131 | 65011.12 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.137 | 65011.13 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.139 | 65011.13 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.145 | 65011.14 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.147 | 65011.14 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.153 | 65011.15 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.155 | 65011.15 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.161 | 65011.16 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.163 | 65011.16 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.169 | 65011.17 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.171 | 65011.17 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.177 | 65011.18 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.179 | 65011.18 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.185 | 65011.19 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.187 | 65011.19 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.193 | 65011.20 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.195 | 65011.20 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.201 | 65011.21 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.203 | 65011.21 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.209 | 65011.22 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.211 | 65011.22 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.217 | 65011.23 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.219 | 65011.23 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.225 | 65011.24 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.227 | 65011.24 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.233 | 65011.25 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.235 | 65011.25 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.241 | 65011.26 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.243 | 65011.26 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.249 | 65011.27 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.251 | 65011.27 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.89.1 | 65011.28 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.89.3 | 65011.28 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.89.9 | 65011.29 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.89.11 | 65011.29 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.89.17 | 65011.30 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.89.19 | 65011.30 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.89.25 | 65011.31 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.89.27 | 65011.31 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.89.33 | 65011.32 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.89.35 | 65011.32 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65010.1
   router-id 169.27.195.1
   update wait-install
   no bgp default ipv4-unicast
   maximum-paths 4 ecmp 4
   bgp asn notation asdot
   no bgp default ipv4-unicast
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
   neighbor 100.83.88.3 remote-as 65003.1
   neighbor 100.83.88.3 description media-PTP-1_Ethernet50/1
   neighbor 100.83.88.11 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.11 remote-as 65003.1
   neighbor 100.83.88.11 description media-PTP-2_Ethernet50/1
   neighbor 100.83.88.19 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.19 remote-as 65003.2
   neighbor 100.83.88.19 description border-leaf1_Ethernet34/1
   neighbor 100.83.88.27 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.27 remote-as 65003.2
   neighbor 100.83.88.27 description border-leaf2_Ethernet34/1
   neighbor 100.83.88.41 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.41 remote-as 65011.1
   neighbor 100.83.88.41 description blue-leaf1_Ethernet49/1
   neighbor 100.83.88.43 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.43 remote-as 65011.1
   neighbor 100.83.88.43 description blue-leaf1_Ethernet50/1
   neighbor 100.83.88.49 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.49 remote-as 65011.2
   neighbor 100.83.88.49 description blue-leaf2_Ethernet49/1
   neighbor 100.83.88.51 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.51 remote-as 65011.2
   neighbor 100.83.88.51 description blue-leaf2_Ethernet50/1
   neighbor 100.83.88.57 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.57 remote-as 65011.3
   neighbor 100.83.88.57 description blue-leaf3_Ethernet49/1
   neighbor 100.83.88.59 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.59 remote-as 65011.3
   neighbor 100.83.88.59 description blue-leaf3_Ethernet50/1
   neighbor 100.83.88.65 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.65 remote-as 65011.4
   neighbor 100.83.88.65 description blue-leaf4_Ethernet49/1
   neighbor 100.83.88.67 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.67 remote-as 65011.4
   neighbor 100.83.88.67 description blue-leaf4_Ethernet50/1
   neighbor 100.83.88.73 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.73 remote-as 65011.5
   neighbor 100.83.88.73 description blue-leaf5_Ethernet49/1
   neighbor 100.83.88.75 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.75 remote-as 65011.5
   neighbor 100.83.88.75 description blue-leaf5_Ethernet50/1
   neighbor 100.83.88.81 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.81 remote-as 65011.6
   neighbor 100.83.88.81 description blue-leaf6_Ethernet49/1
   neighbor 100.83.88.83 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.83 remote-as 65011.6
   neighbor 100.83.88.83 description blue-leaf6_Ethernet50/1
   neighbor 100.83.88.89 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.89 remote-as 65011.7
   neighbor 100.83.88.89 description blue-leaf7_Ethernet49/1
   neighbor 100.83.88.91 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.91 remote-as 65011.7
   neighbor 100.83.88.91 description blue-leaf7_Ethernet50/1
   neighbor 100.83.88.97 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.97 remote-as 65011.8
   neighbor 100.83.88.97 description blue-leaf8_Ethernet49/1
   neighbor 100.83.88.99 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.99 remote-as 65011.8
   neighbor 100.83.88.99 description blue-leaf8_Ethernet50/1
   neighbor 100.83.88.105 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.105 remote-as 65011.9
   neighbor 100.83.88.105 description blue-leaf9_Ethernet49/1
   neighbor 100.83.88.107 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.107 remote-as 65011.9
   neighbor 100.83.88.107 description blue-leaf9_Ethernet50/1
   neighbor 100.83.88.113 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.113 remote-as 65011.10
   neighbor 100.83.88.113 description blue-leaf10_Ethernet49/1
   neighbor 100.83.88.115 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.115 remote-as 65011.10
   neighbor 100.83.88.115 description blue-leaf10_Ethernet50/1
   neighbor 100.83.88.121 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.121 remote-as 65011.11
   neighbor 100.83.88.121 description blue-leaf11_Ethernet49/1
   neighbor 100.83.88.123 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.123 remote-as 65011.11
   neighbor 100.83.88.123 description blue-leaf11_Ethernet50/1
   neighbor 100.83.88.129 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.129 remote-as 65011.12
   neighbor 100.83.88.129 description blue-leaf12_Ethernet49/1
   neighbor 100.83.88.131 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.131 remote-as 65011.12
   neighbor 100.83.88.131 description blue-leaf12_Ethernet50/1
   neighbor 100.83.88.137 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.137 remote-as 65011.13
   neighbor 100.83.88.137 description blue-leaf13_Ethernet49/1
   neighbor 100.83.88.139 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.139 remote-as 65011.13
   neighbor 100.83.88.139 description blue-leaf13_Ethernet50/1
   neighbor 100.83.88.145 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.145 remote-as 65011.14
   neighbor 100.83.88.145 description blue-leaf14_Ethernet49/1
   neighbor 100.83.88.147 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.147 remote-as 65011.14
   neighbor 100.83.88.147 description blue-leaf14_Ethernet50/1
   neighbor 100.83.88.153 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.153 remote-as 65011.15
   neighbor 100.83.88.153 description blue-leaf15_Ethernet49/1
   neighbor 100.83.88.155 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.155 remote-as 65011.15
   neighbor 100.83.88.155 description blue-leaf15_Ethernet50/1
   neighbor 100.83.88.161 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.161 remote-as 65011.16
   neighbor 100.83.88.161 description blue-leaf16_Ethernet49/1
   neighbor 100.83.88.163 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.163 remote-as 65011.16
   neighbor 100.83.88.163 description blue-leaf16_Ethernet50/1
   neighbor 100.83.88.169 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.169 remote-as 65011.17
   neighbor 100.83.88.169 description blue-leaf17_Ethernet49/1
   neighbor 100.83.88.171 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.171 remote-as 65011.17
   neighbor 100.83.88.171 description blue-leaf17_Ethernet50/1
   neighbor 100.83.88.177 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.177 remote-as 65011.18
   neighbor 100.83.88.177 description blue-leaf18_Ethernet49/1
   neighbor 100.83.88.179 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.179 remote-as 65011.18
   neighbor 100.83.88.179 description blue-leaf18_Ethernet50/1
   neighbor 100.83.88.185 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.185 remote-as 65011.19
   neighbor 100.83.88.185 description blue-leaf19_Ethernet49/1
   neighbor 100.83.88.187 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.187 remote-as 65011.19
   neighbor 100.83.88.187 description blue-leaf19_Ethernet50/1
   neighbor 100.83.88.193 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.193 remote-as 65011.20
   neighbor 100.83.88.193 description blue-leaf20_Ethernet49/1
   neighbor 100.83.88.195 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.195 remote-as 65011.20
   neighbor 100.83.88.195 description blue-leaf20_Ethernet50/1
   neighbor 100.83.88.201 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.201 remote-as 65011.21
   neighbor 100.83.88.201 description blue-leaf21_Ethernet49/1
   neighbor 100.83.88.203 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.203 remote-as 65011.21
   neighbor 100.83.88.203 description blue-leaf21_Ethernet50/1
   neighbor 100.83.88.209 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.209 remote-as 65011.22
   neighbor 100.83.88.209 description blue-leaf22_Ethernet49/1
   neighbor 100.83.88.211 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.211 remote-as 65011.22
   neighbor 100.83.88.211 description blue-leaf22_Ethernet50/1
   neighbor 100.83.88.217 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.217 remote-as 65011.23
   neighbor 100.83.88.217 description blue-leaf23_Ethernet49/1
   neighbor 100.83.88.219 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.219 remote-as 65011.23
   neighbor 100.83.88.219 description blue-leaf23_Ethernet50/1
   neighbor 100.83.88.225 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.225 remote-as 65011.24
   neighbor 100.83.88.225 description blue-leaf24_Ethernet49/1
   neighbor 100.83.88.227 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.227 remote-as 65011.24
   neighbor 100.83.88.227 description blue-leaf24_Ethernet50/1
   neighbor 100.83.88.233 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.233 remote-as 65011.25
   neighbor 100.83.88.233 description blue-leaf25_Ethernet49/1
   neighbor 100.83.88.235 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.235 remote-as 65011.25
   neighbor 100.83.88.235 description blue-leaf25_Ethernet50/1
   neighbor 100.83.88.241 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.241 remote-as 65011.26
   neighbor 100.83.88.241 description blue-leaf26_Ethernet49/1
   neighbor 100.83.88.243 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.243 remote-as 65011.26
   neighbor 100.83.88.243 description blue-leaf26_Ethernet50/1
   neighbor 100.83.88.249 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.249 remote-as 65011.27
   neighbor 100.83.88.249 description blue-leaf27_Ethernet49/1
   neighbor 100.83.88.251 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.251 remote-as 65011.27
   neighbor 100.83.88.251 description blue-leaf27_Ethernet50/1
   neighbor 100.83.89.1 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.89.1 remote-as 65011.28
   neighbor 100.83.89.1 description blue-leaf28_Ethernet49/1
   neighbor 100.83.89.3 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.89.3 remote-as 65011.28
   neighbor 100.83.89.3 description blue-leaf28_Ethernet50/1
   neighbor 100.83.89.9 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.89.9 remote-as 65011.29
   neighbor 100.83.89.9 description blue-leaf29_Ethernet49/1
   neighbor 100.83.89.11 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.89.11 remote-as 65011.29
   neighbor 100.83.89.11 description blue-leaf29_Ethernet50/1
   neighbor 100.83.89.17 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.89.17 remote-as 65011.30
   neighbor 100.83.89.17 description blue-leaf30_Ethernet49/1
   neighbor 100.83.89.19 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.89.19 remote-as 65011.30
   neighbor 100.83.89.19 description blue-leaf30_Ethernet50/1
   neighbor 100.83.89.25 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.89.25 remote-as 65011.31
   neighbor 100.83.89.25 description blue-leaf31_Ethernet49/1
   neighbor 100.83.89.27 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.89.27 remote-as 65011.31
   neighbor 100.83.89.27 description blue-leaf31_Ethernet50/1
   neighbor 100.83.89.33 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.89.33 remote-as 65011.32
   neighbor 100.83.89.33 description blue-leaf32_Ethernet49/1
   neighbor 100.83.89.35 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.89.35 remote-as 65011.32
   neighbor 100.83.89.35 description blue-leaf32_Ethernet50/1
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

### PIM Sparse Mode

#### PIM Sparse Mode Enabled Interfaces

| Interface Name | VRF Name | IP Version | Border Router | DR Priority | Local Interface |
| -------------- | -------- | ---------- | ------------- | ----------- | --------------- |
| Ethernet4/11/1 | - | IPv4 | - | - | - |
| Ethernet4/12/1 | - | IPv4 | - | - | - |
| Ethernet4/13/1 | - | IPv4 | - | - | - |
| Ethernet4/14/1 | - | IPv4 | - | - | - |
| Ethernet4/15/1 | - | IPv4 | - | - | - |
| Ethernet4/16/1 | - | IPv4 | - | - | - |
| Ethernet4/17/1 | - | IPv4 | - | - | - |
| Ethernet4/18/1 | - | IPv4 | - | - | - |
| Ethernet4/19/1 | - | IPv4 | - | - | - |
| Ethernet4/20/1 | - | IPv4 | - | - | - |
| Ethernet4/21/1 | - | IPv4 | - | - | - |
| Ethernet4/22/1 | - | IPv4 | - | - | - |
| Ethernet4/23/1 | - | IPv4 | - | - | - |
| Ethernet4/24/1 | - | IPv4 | - | - | - |
| Ethernet4/25/1 | - | IPv4 | - | - | - |
| Ethernet4/26/1 | - | IPv4 | - | - | - |
| Ethernet4/27/1 | - | IPv4 | - | - | - |
| Ethernet4/28/1 | - | IPv4 | - | - | - |
| Ethernet4/29/1 | - | IPv4 | - | - | - |
| Ethernet4/30/1 | - | IPv4 | - | - | - |
| Ethernet4/31/1 | - | IPv4 | - | - | - |
| Ethernet4/32/1 | - | IPv4 | - | - | - |
| Ethernet4/33/1 | - | IPv4 | - | - | - |
| Ethernet4/34/1 | - | IPv4 | - | - | - |
| Ethernet4/35/1 | - | IPv4 | - | - | - |
| Ethernet4/36/1 | - | IPv4 | - | - | - |
| Ethernet5/1/1 | - | IPv4 | - | - | - |
| Ethernet5/2/1 | - | IPv4 | - | - | - |
| Ethernet5/3/1 | - | IPv4 | - | - | - |
| Ethernet5/4/1 | - | IPv4 | - | - | - |
| Ethernet5/5/1 | - | IPv4 | - | - | - |
| Ethernet5/6/1 | - | IPv4 | - | - | - |
| Ethernet5/7/1 | - | IPv4 | - | - | - |
| Ethernet5/8/1 | - | IPv4 | - | - | - |
| Ethernet5/9/1 | - | IPv4 | - | - | - |
| Ethernet5/10/1 | - | IPv4 | - | - | - |
| Ethernet5/11/1 | - | IPv4 | - | - | - |
| Ethernet5/12/1 | - | IPv4 | - | - | - |
| Ethernet5/13/1 | - | IPv4 | - | - | - |
| Ethernet5/14/1 | - | IPv4 | - | - | - |
| Ethernet5/15/1 | - | IPv4 | - | - | - |
| Ethernet5/16/1 | - | IPv4 | - | - | - |
| Ethernet5/17/1 | - | IPv4 | - | - | - |
| Ethernet5/18/1 | - | IPv4 | - | - | - |
| Ethernet5/19/1 | - | IPv4 | - | - | - |
| Ethernet5/20/1 | - | IPv4 | - | - | - |
| Ethernet5/21/1 | - | IPv4 | - | - | - |
| Ethernet5/22/1 | - | IPv4 | - | - | - |
| Ethernet5/23/1 | - | IPv4 | - | - | - |
| Ethernet5/24/1 | - | IPv4 | - | - | - |
| Ethernet5/25/1 | - | IPv4 | - | - | - |
| Ethernet5/26/1 | - | IPv4 | - | - | - |
| Ethernet5/27/1 | - | IPv4 | - | - | - |
| Ethernet5/28/1 | - | IPv4 | - | - | - |
| Ethernet5/29/1 | - | IPv4 | - | - | - |
| Ethernet5/30/1 | - | IPv4 | - | - | - |
| Ethernet5/31/1 | - | IPv4 | - | - | - |
| Ethernet5/32/1 | - | IPv4 | - | - | - |
| Ethernet5/33/1 | - | IPv4 | - | - | - |
| Ethernet5/34/1 | - | IPv4 | - | - | - |
| Ethernet5/35/1 | - | IPv4 | - | - | - |
| Ethernet5/36/1 | - | IPv4 | - | - | - |
| Ethernet6/1/1 | - | IPv4 | - | - | - |
| Ethernet6/2/1 | - | IPv4 | - | - | - |
| Ethernet33/1 | - | IPv4 | - | - | - |
| Ethernet34/1 | - | IPv4 | - | - | - |
| Ethernet49/1 | - | IPv4 | - | - | - |
| Ethernet50/1 | - | IPv4 | - | - | - |

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
