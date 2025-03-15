# green-spine1

## Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [IP Name Servers](#ip-name-servers)
  - [Clock Settings](#clock-settings)
  - [NTP](#ntp)
  - [PTP](#ptp)
  - [Management SSH](#management-ssh)
  - [Management API gNMI](#management-api-gnmi)
  - [Management CVX Summary](#management-cvx-summary)
  - [Management API HTTP](#management-api-http)
  - [Management API Models](#management-api-models)
- [Authentication](#authentication)
  - [Local Users](#local-users)
  - [Enable Password](#enable-password)
  - [AAA Authentication](#aaa-authentication)
  - [AAA Authorization](#aaa-authorization)
- [Monitoring](#monitoring)
  - [Logging](#logging)
  - [SNMP](#snmp)
  - [Hardware](#hardware)
- [MLAG](#mlag)
  - [MLAG Summary](#mlag-summary)
  - [MLAG Device Configuration](#mlag-device-configuration)
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
  - [Port-Channel Interfaces](#port-channel-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
  - [VLAN Interfaces](#vlan-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [Virtual Router MAC Address](#virtual-router-mac-address)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router BGP](#router-bgp)
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
- [Filters](#filters)
  - [Route-maps](#route-maps)
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
| Management0 | OOB_MANAGEMENT | oob | MGMT | 10.100.100.70/24 | 172.16.100.1 |

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
   ip address 10.100.100.70/24
```

### IP Name Servers

#### IP Name Servers Summary

| Name Server | VRF | Priority |
| ----------- | --- | -------- |
| 8.8.4.4 | MGMT | - |
| 8.8.8.8 | MGMT | - |

#### IP Name Servers Device Configuration

```eos
ip name-server vrf MGMT 8.8.4.4
ip name-server vrf MGMT 8.8.8.8
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

##### NTP Local Interface

| Interface | VRF |
| --------- | --- |
| Management0 | MGMT |

##### NTP Servers

| Server | VRF | Preferred | Burst | iBurst | Version | Min Poll | Max Poll | Local-interface | Key |
| ------ | --- | --------- | ----- | ------ | ------- | -------- | -------- | --------------- | --- |
| pool.ntp.org | MGMT | - | - | - | - | - | - | - | - |
| time.google.com | MGMT | True | - | - | - | - | - | - | - |

#### NTP Device Configuration

```eos
!
ntp local-interface vrf MGMT Management0
ntp server vrf MGMT pool.ntp.org
ntp server vrf MGMT time.google.com prefer
```

### PTP
#### PTP Summary

| Clock ID | Source IP | Priority 1 | Priority 2 | TTL | Domain | Mode | Forward Unicast |
| -------- | --------- | ---------- | ---------- | --- | ------ | ---- | --------------- |
| - | 172.31.1.12 | 20 | 103 | 8 | 100 | boundary | - |

#### PTP Device Configuration

```eos
!
ptp domain 100
ptp mode boundary
ptp priority1 20
ptp priority2 103
ptp source ip 172.31.1.12
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

#### Local Users Device Configuration

```eos
!
username admin privilege 15 role network-admin secret sha512 <removed>
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

## MLAG

### MLAG Summary

| Domain-id | Local-interface | Peer-address | Peer-link |
| --------- | --------------- | ------------ | --------- |
| CTL_SPINES_MLAG | Vlan4094 | 172.16.0.1 | Port-Channel1000 |

Dual primary detection is disabled.

### MLAG Device Configuration

```eos
!
mlag configuration
   domain-id CTL_SPINES_MLAG
   local-interface Vlan4094
   peer-address 172.16.0.1
   peer-link Port-Channel1000
   reload-delay mlag 300
   reload-delay non-mlag 330
```

## Spanning Tree

### Spanning Tree Summary

STP mode: **mstp**

#### MSTP Instance and Priority

| Instance(s) | Priority |
| -------- | -------- |
| 0 | 4096 |

#### Global Spanning-Tree Settings

- Spanning Tree disabled for VLANs: **4093-4094**

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode mstp
no spanning-tree vlan-id 4093-4094
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
| 113 | INBAND_MGMT | - |
| 201 | VLAN_201 | - |
| 202 | VLAN_202 | - |
| 203 | VLAN_203 | - |
| 204 | VLAN_204 | - |
| 205 | VLAN_205 | - |
| 206 | VLAN_206 | - |
| 207 | VLAN_207 | - |
| 208 | VLAN_208 | - |
| 209 | VLAN_209 | - |
| 210 | VLAN_210 | - |
| 211 | VLAN_211 | - |
| 212 | VLAN_212 | - |
| 213 | VLAN_213 | - |
| 214 | VLAN_214 | - |
| 215 | VLAN_215 | - |
| 216 | VLAN_216 | - |
| 217 | VLAN_217 | - |
| 218 | VLAN_218 | - |
| 219 | VLAN_219 | - |
| 220 | VLAN_220 | - |
| 221 | VLAN_221 | - |
| 222 | VLAN_222 | - |
| 223 | VLAN_223 | - |
| 224 | VLAN_224 | - |
| 225 | VLAN_225 | - |
| 226 | VLAN_226 | - |
| 227 | VLAN_227 | - |
| 228 | VLAN_228 | - |
| 229 | VLAN_229 | - |
| 230 | VLAN_230 | - |
| 231 | VLAN_231 | - |
| 232 | VLAN_232 | - |
| 233 | VLAN_233 | - |
| 234 | VLAN_234 | - |
| 235 | VLAN_235 | - |
| 236 | VLAN_236 | - |
| 237 | VLAN_237 | - |
| 238 | VLAN_238 | - |
| 239 | VLAN_239 | - |
| 240 | VLAN_240 | - |
| 241 | VLAN_241 | - |
| 242 | VLAN_242 | - |
| 243 | VLAN_243 | - |
| 244 | VLAN_244 | - |
| 245 | VLAN_245 | - |
| 246 | VLAN_246 | - |
| 247 | VLAN_247 | - |
| 248 | VLAN_248 | - |
| 249 | VLAN_249 | - |
| 250 | VLAN_250 | - |
| 251 | VLAN_251 | - |
| 252 | VLAN_252 | - |
| 253 | VLAN_253 | - |
| 254 | VLAN_254 | - |
| 255 | VLAN_255 | - |
| 256 | VLAN_256 | - |
| 257 | VLAN_257 | - |
| 258 | VLAN_258 | - |
| 259 | VLAN_259 | - |
| 260 | VLAN_260 | - |
| 261 | VLAN_261 | - |
| 262 | VLAN_262 | - |
| 263 | VLAN_263 | - |
| 264 | VLAN_264 | - |
| 265 | VLAN_265 | - |
| 266 | VLAN_266 | - |
| 267 | VLAN_267 | - |
| 268 | VLAN_268 | - |
| 269 | VLAN_269 | - |
| 270 | VLAN_270 | - |
| 271 | VLAN_271 | - |
| 272 | VLAN_272 | - |
| 273 | VLAN_273 | - |
| 274 | VLAN_274 | - |
| 275 | VLAN_275 | - |
| 276 | VLAN_276 | - |
| 277 | VLAN_277 | - |
| 278 | VLAN_278 | - |
| 279 | VLAN_279 | - |
| 280 | VLAN_280 | - |
| 4093 | MLAG_L3 | MLAG |
| 4094 | MLAG | MLAG |

### VLANs Device Configuration

```eos
!
vlan 113
   name INBAND_MGMT
!
vlan 201
   name VLAN_201
!
vlan 202
   name VLAN_202
!
vlan 203
   name VLAN_203
!
vlan 204
   name VLAN_204
!
vlan 205
   name VLAN_205
!
vlan 206
   name VLAN_206
!
vlan 207
   name VLAN_207
!
vlan 208
   name VLAN_208
!
vlan 209
   name VLAN_209
!
vlan 210
   name VLAN_210
!
vlan 211
   name VLAN_211
!
vlan 212
   name VLAN_212
!
vlan 213
   name VLAN_213
!
vlan 214
   name VLAN_214
!
vlan 215
   name VLAN_215
!
vlan 216
   name VLAN_216
!
vlan 217
   name VLAN_217
!
vlan 218
   name VLAN_218
!
vlan 219
   name VLAN_219
!
vlan 220
   name VLAN_220
!
vlan 221
   name VLAN_221
!
vlan 222
   name VLAN_222
!
vlan 223
   name VLAN_223
!
vlan 224
   name VLAN_224
!
vlan 225
   name VLAN_225
!
vlan 226
   name VLAN_226
!
vlan 227
   name VLAN_227
!
vlan 228
   name VLAN_228
!
vlan 229
   name VLAN_229
!
vlan 230
   name VLAN_230
!
vlan 231
   name VLAN_231
!
vlan 232
   name VLAN_232
!
vlan 233
   name VLAN_233
!
vlan 234
   name VLAN_234
!
vlan 235
   name VLAN_235
!
vlan 236
   name VLAN_236
!
vlan 237
   name VLAN_237
!
vlan 238
   name VLAN_238
!
vlan 239
   name VLAN_239
!
vlan 240
   name VLAN_240
!
vlan 241
   name VLAN_241
!
vlan 242
   name VLAN_242
!
vlan 243
   name VLAN_243
!
vlan 244
   name VLAN_244
!
vlan 245
   name VLAN_245
!
vlan 246
   name VLAN_246
!
vlan 247
   name VLAN_247
!
vlan 248
   name VLAN_248
!
vlan 249
   name VLAN_249
!
vlan 250
   name VLAN_250
!
vlan 251
   name VLAN_251
!
vlan 252
   name VLAN_252
!
vlan 253
   name VLAN_253
!
vlan 254
   name VLAN_254
!
vlan 255
   name VLAN_255
!
vlan 256
   name VLAN_256
!
vlan 257
   name VLAN_257
!
vlan 258
   name VLAN_258
!
vlan 259
   name VLAN_259
!
vlan 260
   name VLAN_260
!
vlan 261
   name VLAN_261
!
vlan 262
   name VLAN_262
!
vlan 263
   name VLAN_263
!
vlan 264
   name VLAN_264
!
vlan 265
   name VLAN_265
!
vlan 266
   name VLAN_266
!
vlan 267
   name VLAN_267
!
vlan 268
   name VLAN_268
!
vlan 269
   name VLAN_269
!
vlan 270
   name VLAN_270
!
vlan 271
   name VLAN_271
!
vlan 272
   name VLAN_272
!
vlan 273
   name VLAN_273
!
vlan 274
   name VLAN_274
!
vlan 275
   name VLAN_275
!
vlan 276
   name VLAN_276
!
vlan 277
   name VLAN_277
!
vlan 278
   name VLAN_278
!
vlan 279
   name VLAN_279
!
vlan 280
   name VLAN_280
!
vlan 4093
   name MLAG_L3
   trunk group MLAG
!
vlan 4094
   name MLAG
   trunk group MLAG
```

## Interfaces

### Ethernet Interfaces

#### Ethernet Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |
| Ethernet3/5/1 | L2_green-leaf1_Ethernet53/1 | *trunk | *113,201-202 | *- | *- | 112 |
| Ethernet3/6/1 | L2_green-leaf2_Ethernet53/1 | *trunk | *113,202-204 | *- | *- | 113 |
| Ethernet3/7/1 | L2_green-leaf3_Ethernet53/1 | *trunk | *113,201,203,205,207,209 | *- | *- | 114 |
| Ethernet3/8/1 | L2_green-leaf4_Ethernet53/1 | *trunk | *113,202,204,206,208 | *- | *- | 115 |
| Ethernet3/9/1 | L2_green-leaf5_Ethernet53/1 | *trunk | *113 | *- | *- | 116 |
| Ethernet3/10/1 | L2_green-leaf6_Ethernet53/1 | *trunk | *113,201,203-205,207-209 | *- | *- | 117 |
| Ethernet3/11/1 | L2_green-leaf7_Ethernet53/1 | *trunk | *113,201-207,209 | *- | *- | 118 |
| Ethernet3/12/1 | L2_green-leaf8_Ethernet53/1 | *trunk | *113,201-204,206-207,209 | *- | *- | 119 |
| Ethernet3/13/1 | L2_green-leaf9_Ethernet53/1 | *trunk | *113,201-204,206-207,209 | *- | *- | 120 |
| Ethernet3/14/1 | L2_green-leaf10_Ethernet53/1 | *trunk | *113,201-204,206-207,209 | *- | *- | 121 |
| Ethernet3/15/1 | L2_green-leaf11_Ethernet53/1 | *trunk | *113,201-204,206-207,209 | *- | *- | 122 |
| Ethernet3/16/1 | L2_green-leaf12_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 123 |
| Ethernet3/17/1 | L2_green-leaf13_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 124 |
| Ethernet3/18/1 | L2_green-leaf14_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 125 |
| Ethernet3/19/1 | L2_green-leaf15_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 126 |
| Ethernet3/20/1 | L2_green-leaf16_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 127 |
| Ethernet3/21/1 | L2_green-leaf17_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 128 |
| Ethernet3/22/1 | L2_green-leaf18_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 129 |
| Ethernet3/23/1 | L2_green-leaf19_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 130 |
| Ethernet3/24/1 | L2_green-leaf20_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 131 |
| Ethernet3/25/1 | L2_green-leaf21_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 132 |
| Ethernet3/26/1 | L2_green-leaf22_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 133 |
| Ethernet3/27/1 | L2_green-leaf23_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 134 |
| Ethernet3/28/1 | L2_green-leaf24_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 135 |
| Ethernet3/29/1 | L2_green-leaf25_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 136 |
| Ethernet3/30/1 | L2_green-leaf26_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 137 |
| Ethernet3/31/1 | L2_green-leaf27_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 138 |
| Ethernet3/32/1 | L2_green-leaf28_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 139 |
| Ethernet4/1/1 | L2_green-leaf29_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 140 |
| Ethernet4/2/1 | L2_green-leaf30_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 141 |
| Ethernet4/3/1 | L2_green-leaf31_Ethernet53/1 | *trunk | *113,201-204,206,209 | *- | *- | 142 |
| Ethernet4/4/1 | L2_green-leaf32_Ethernet53/1 | *trunk | *113,201-204,206,208-209 | *- | *- | 143 |
| Ethernet4/5/1 | L2_green-leaf33_Ethernet53/1 | *trunk | *113,201-204,206,208-209 | *- | *- | 144 |
| Ethernet4/6/1 | L2_green-leaf34_Ethernet53/1 | *trunk | *113,201-204,206,208-209 | *- | *- | 145 |
| Ethernet4/7/1 | L2_green-leaf35_Ethernet53/1 | *trunk | *113,201-204,206,208-209 | *- | *- | 146 |
| Ethernet4/8/1 | L2_green-leaf36_Ethernet53/1 | *trunk | *113,201-204,206,208-209 | *- | *- | 147 |
| Ethernet4/9/1 | L2_green-leaf37_Ethernet53/1 | *trunk | *113,201-204,206,208-209 | *- | *- | 148 |
| Ethernet4/10/1 | L2_green-leaf38_Ethernet53/1 | *trunk | *113,201-204,206,208 | *- | *- | 149 |
| Ethernet4/11/1 | L2_green-leaf39_Ethernet53/1 | *trunk | *113,201-204,208 | *- | *- | 150 |
| Ethernet4/12/1 | L2_green-leaf40_Ethernet53/1 | *trunk | *113,201-204,208 | *- | *- | 151 |
| Ethernet4/13/1 | L2_green-leaf41_Ethernet53/1 | *trunk | *113,201-204,208 | *- | *- | 152 |
| Ethernet4/14/1 | L2_green-leaf42_Ethernet53/1 | *trunk | *113,201-204,208 | *- | *- | 153 |
| Ethernet4/15/1 | L2_green-leaf43_Ethernet53/1 | *trunk | *113,201-204,208 | *- | *- | 154 |
| Ethernet4/16/1 | L2_green-leaf44_Ethernet53/1 | *trunk | *113,201-204,208 | *- | *- | 155 |
| Ethernet4/17/1 | L2_green-leaf45_Ethernet53/1 | *trunk | *113,201-204,208 | *- | *- | 156 |
| Ethernet4/18/1 | L2_green-leaf46_Ethernet53/1 | *trunk | *113,201-204,208 | *- | *- | 157 |
| Ethernet4/19/1 | L2_green-leaf47_Ethernet53/1 | *trunk | *113,201-204,208 | *- | *- | 158 |
| Ethernet4/20/1 | L2_green-leaf48_Ethernet53/1 | *trunk | *113,201-204,207-208 | *- | *- | 159 |
| Ethernet4/21/1 | L2_green-leaf49_Ethernet53/1 | *trunk | *113,201-204,207-208 | *- | *- | 160 |
| Ethernet4/22/1 | L2_green-leaf50_Ethernet53/1 | *trunk | *113,201-204,207-208 | *- | *- | 161 |
| Ethernet4/23/1 | L2_green-leaf51_Ethernet53/1 | *trunk | *113,201-204,207-208 | *- | *- | 162 |
| Ethernet4/24/1 | L2_green-leaf52_Ethernet53/1 | *trunk | *113,201-204,207-208 | *- | *- | 163 |
| Ethernet4/25/1 | L2_green-leaf53_Ethernet53/1 | *trunk | *113,201-204,207-208 | *- | *- | 164 |
| Ethernet4/26/1 | L2_green-leaf54_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 165 |
| Ethernet4/27/1 | L2_green-leaf55_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 166 |
| Ethernet4/28/1 | L2_green-leaf56_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 167 |
| Ethernet4/29/1 | L2_green-leaf57_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 168 |
| Ethernet4/30/1 | L2_green-leaf58_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 169 |
| Ethernet4/31/1 | L2_green-leaf59_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 170 |
| Ethernet4/32/1 | L2_green-leaf60_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 171 |
| Ethernet5/1/1 | L2_green-leaf61_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 172 |
| Ethernet5/2/1 | L2_green-leaf62_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 173 |
| Ethernet5/3/1 | L2_green-leaf63_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 174 |
| Ethernet5/4/1 | L2_green-leaf64_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 175 |
| Ethernet5/5/1 | L2_green-leaf65_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 176 |
| Ethernet5/6/1 | L2_green-leaf66_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 177 |
| Ethernet5/7/1 | L2_green-leaf67_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 178 |
| Ethernet5/8/1 | L2_green-leaf68_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 179 |
| Ethernet5/9/1 | L2_green-leaf69_Ethernet53/1 | *trunk | *113,203-204,207-208 | *- | *- | 180 |
| Ethernet5/10/1 | L2_green-leaf70_Ethernet53/1 | *trunk | *113,203-205,207-208 | *- | *- | 181 |
| Ethernet5/11/1 | L2_green-leaf71_Ethernet53/1 | *trunk | *113,203-205,207-208 | *- | *- | 182 |
| Ethernet5/12/1 | L2_green-leaf72_Ethernet53/1 | *trunk | *113,203-205,207-208 | *- | *- | 183 |
| Ethernet5/13/1 | L2_green-leaf73_Ethernet53/1 | *trunk | *113,203-205,207-208 | *- | *- | 184 |
| Ethernet5/14/1 | L2_green-leaf74_Ethernet53/1 | *trunk | *113,203-205,207-208 | *- | *- | 185 |
| Ethernet5/15/1 | L2_green-leaf75_Ethernet53/1 | *trunk | *113,203-205,207-208 | *- | *- | 186 |
| Ethernet5/16/1 | L2_green-leaf76_Ethernet53/1 | *trunk | *113,203-205,207-209 | *- | *- | 187 |
| Ethernet5/17/1 | L2_green-leaf77_Ethernet53/1 | *trunk | *113,203-205,207-209 | *- | *- | 188 |
| Ethernet5/18/1 | L2_green-leaf78_Ethernet53/1 | *trunk | *113,203-205,207-209 | *- | *- | 189 |
| Ethernet5/19/1 | L2_green-leaf79_Ethernet53/1 | *trunk | *113,203-205,207-209 | *- | *- | 190 |
| Ethernet5/20/1 | L2_green-leaf80_Ethernet53/1 | *trunk | *113,203-204,207-209 | *- | *- | 191 |
| Ethernet5/21/1 | L2_green-leaf81_Ethernet53/1 | *trunk | *113,203-204,207-209 | *- | *- | 192 |
| Ethernet5/22/1 | L2_green-leaf82_Ethernet53/1 | *trunk | *113,203-204,207-209 | *- | *- | 193 |
| Ethernet5/23/1 | L2_green-leaf83_Ethernet53/1 | *trunk | *113,203-204,207-209 | *- | *- | 194 |
| Ethernet5/24/1 | L2_green-leaf84_Ethernet53/1 | *trunk | *113,207-209 | *- | *- | 195 |
| Ethernet5/25/1 | L2_green-leaf85_Ethernet53/1 | *trunk | *113,207,209 | *- | *- | 196 |
| Ethernet5/26/1 | L2_green-leaf86_Ethernet53/1 | *trunk | *113,207,209 | *- | *- | 197 |
| Ethernet5/27/1 | L2_green-leaf87_Ethernet53/1 | *trunk | *113,207,209 | *- | *- | 198 |
| Ethernet5/28/1 | L2_green-leaf88_Ethernet53/1 | *trunk | *113,207,209 | *- | *- | 199 |
| Ethernet5/29/1 | L2_green-leaf89_Ethernet53/1 | *trunk | *113,207,209 | *- | *- | 1100 |
| Ethernet5/30/1 | L2_green-leaf90_Ethernet53/1 | *trunk | *113,207,209 | *- | *- | 1101 |
| Ethernet5/31/1 | L2_green-leaf91_Ethernet53/1 | *trunk | *113,207,209 | *- | *- | 1102 |
| Ethernet5/32/1 | L2_green-leaf92_Ethernet53/1 | *trunk | *113,207,209 | *- | *- | 1103 |
| Ethernet6/1/1 | L2_green-leaf93_Ethernet53/1 | *trunk | *113,207,209 | *- | *- | 1104 |
| Ethernet6/2/1 | L2_green-leaf94_Ethernet53/1 | *trunk | *113,207,209 | *- | *- | 1105 |
| Ethernet6/3/1 | L2_green-leaf95_Ethernet53/1 | *trunk | *113,207,209 | *- | *- | 1106 |
| Ethernet6/4/1 | L2_green-leaf96_Ethernet53/1 | *trunk | *113,205,207,209 | *- | *- | 1107 |
| Ethernet6/5/1 | L2_green-leaf97_Ethernet53/1 | *trunk | *113,205,207,209 | *- | *- | 1108 |
| Ethernet6/6/1 | L2_green-leaf98_Ethernet53/1 | *trunk | *113,205,207,209 | *- | *- | 1109 |
| Ethernet6/7/1 | L2_green-leaf99_Ethernet53/1 | *trunk | *113,205,207,209 | *- | *- | 1110 |
| Ethernet6/8/1 | L2_green-leaf100_Ethernet53/1 | *trunk | *113,205,207,209 | *- | *- | 1111 |
| Ethernet6/9/1 | L2_green-leaf101_Ethernet53/1 | *trunk | *113,205,207,209 | *- | *- | 1112 |
| Ethernet6/10/1 | L2_green-leaf102_Ethernet53/1 | *trunk | *113,205,207,209 | *- | *- | 1113 |
| Ethernet6/11/1 | L2_green-leaf103_Ethernet53/1 | *trunk | *113,205,207,209 | *- | *- | 1114 |
| Ethernet6/12/1 | L2_green-leaf104_Ethernet53/1 | *trunk | *113,205,207,209 | *- | *- | 1115 |
| Ethernet6/13/1 | L2_green-leaf105_Ethernet53/1 | *trunk | *113,205,207,209 | *- | *- | 1116 |
| Ethernet6/14/1 | L2_green-leaf106_Ethernet53/1 | *trunk | *113,205,207,209 | *- | *- | 1117 |
| Ethernet6/15/1 | L2_green-leaf107_Ethernet53/1 | *trunk | *113,205,207 | *- | *- | 1118 |
| Ethernet6/16/1 | L2_green-leaf108_Ethernet53/1 | *trunk | *113,205,207 | *- | *- | 1119 |
| Ethernet6/17/1 | L2_green-leaf109_Ethernet53/1 | *trunk | *113,205,207 | *- | *- | 1120 |
| Ethernet6/18/1 | L2_green-leaf110_Ethernet53/1 | *trunk | *113,205,207 | *- | *- | 1121 |
| Ethernet6/19/1 | L2_green-leaf111_Ethernet53/1 | *trunk | *113,205,207 | *- | *- | 1122 |
| Ethernet6/20/1 | L2_green-leaf112_Ethernet53/1 | *trunk | *113,205,207 | *- | *- | 1123 |
| Ethernet6/21/1 | L2_green-leaf113_Ethernet53/1 | *trunk | *113,203-205,207 | *- | *- | 1124 |
| Ethernet6/22/1 | L2_green-leaf114_Ethernet53/1 | *trunk | *113,203-205,207 | *- | *- | 1125 |
| Ethernet6/23/1 | L2_green-leaf115_Ethernet53/1 | *trunk | *113,203-205,207 | *- | *- | 1126 |
| Ethernet6/24/1 | L2_green-leaf116_Ethernet53/1 | *trunk | *113,201-205,207 | *- | *- | 1127 |
| Ethernet6/25/1 | L2_green-leaf117_Ethernet53/1 | *trunk | *113,201-205,207 | *- | *- | 1128 |
| Ethernet6/26/1 | L2_green-leaf118_Ethernet53/1 | *trunk | *113,201-205,207 | *- | *- | 1129 |
| Ethernet6/27/1 | L2_green-leaf119_Ethernet53/1 | *trunk | *113,201-205,207 | *- | *- | 1130 |
| Ethernet6/28/1 | L2_green-leaf120_Ethernet53/1 | *trunk | *113,201,204-205,207 | *- | *- | 1131 |
| Ethernet6/29/1 | L2_green-leaf121_Ethernet53/1 | *trunk | *113,201,204-205,207 | *- | *- | 1132 |
| Ethernet6/30/1 | L2_green-leaf122_Ethernet53/1 | *trunk | *113,201,204-205,207 | *- | *- | 1133 |
| Ethernet6/31/1 | L2_green-leaf123_Ethernet53/1 | *trunk | *113,201,204-205,207 | *- | *- | 1134 |
| Ethernet6/32/1 | L2_green-leaf124_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1135 |
| Ethernet7/1/1 | L2_green-leaf125_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1136 |
| Ethernet7/2/1 | L2_green-leaf126_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1137 |
| Ethernet7/3/1 | L2_green-leaf127_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1138 |
| Ethernet7/4/1 | L2_green-leaf128_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1139 |
| Ethernet7/5/1 | L2_green-leaf129_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1140 |
| Ethernet7/6/1 | L2_green-leaf130_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1141 |
| Ethernet7/7/1 | L2_green-leaf131_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1142 |
| Ethernet7/8/1 | L2_green-leaf132_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1143 |
| Ethernet7/9/1 | L2_green-leaf133_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1144 |
| Ethernet7/10/1 | L2_green-leaf134_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1145 |
| Ethernet7/11/1 | L2_green-leaf135_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1146 |
| Ethernet7/12/1 | L2_green-leaf136_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1147 |
| Ethernet7/13/1 | L2_green-leaf137_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1148 |
| Ethernet7/14/1 | L2_green-leaf138_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1149 |
| Ethernet7/15/1 | L2_green-leaf139_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1150 |
| Ethernet7/16/1 | L2_green-leaf140_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1151 |
| Ethernet7/17/1 | L2_green-leaf141_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1152 |
| Ethernet7/18/1 | L2_green-leaf142_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1153 |
| Ethernet7/19/1 | L2_green-leaf143_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1154 |
| Ethernet7/20/1 | L2_green-leaf144_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1155 |
| Ethernet7/21/1 | L2_green-leaf145_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1156 |
| Ethernet7/22/1 | L2_green-leaf146_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1157 |
| Ethernet7/23/1 | L2_green-leaf147_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1158 |
| Ethernet7/24/1 | L2_green-leaf148_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1159 |
| Ethernet7/25/1 | L2_green-leaf149_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1160 |
| Ethernet7/26/1 | L2_green-leaf150_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1161 |
| Ethernet7/27/1 | L2_green-leaf151_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1162 |
| Ethernet7/28/1 | L2_green-leaf152_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1163 |
| Ethernet7/29/1 | L2_green-leaf153_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1164 |
| Ethernet7/30/1 | L2_green-leaf154_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1165 |
| Ethernet7/31/1 | L2_green-leaf155_Ethernet53/1 | *trunk | *113,201,204-205,207-208 | *- | *- | 1166 |
| Ethernet7/32/1 | L2_green-leaf156_Ethernet53/1 | *trunk | *113,201,204,207-208 | *- | *- | 1167 |
| Ethernet8/1/1 | L2_green-leaf157_Ethernet53/1 | *trunk | *113,201,204,207-208 | *- | *- | 1168 |
| Ethernet8/2/1 | L2_green-leaf158_Ethernet53/1 | *trunk | *113,201,204,207-208 | *- | *- | 1169 |
| Ethernet8/3/1 | L2_green-leaf159_Ethernet53/1 | *trunk | *113,201,204,207-208 | *- | *- | 1170 |
| Ethernet8/4/1 | L2_green-leaf160_Ethernet53/1 | *trunk | *113,201,204,207-208 | *- | *- | 1171 |
| Ethernet8/5/1 | L2_green-leaf161_Ethernet53/1 | *trunk | *113,201,204,207-208 | *- | *- | 1172 |
| Ethernet8/6/1 | L2_green-leaf162_Ethernet53/1 | *trunk | *113,201,204,207-208 | *- | *- | 1173 |
| Ethernet8/7/1 | L2_green-leaf163_Ethernet53/1 | *trunk | *113,201,204,207-208 | *- | *- | 1174 |
| Ethernet8/8/1 | L2_green-leaf164_Ethernet53/1 | *trunk | *113,201,204,207-208 | *- | *- | 1175 |
| Ethernet8/9/1 | L2_green-leaf165_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1176 |
| Ethernet8/10/1 | L2_green-leaf166_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1177 |
| Ethernet8/11/1 | L2_green-leaf167_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1178 |
| Ethernet8/12/1 | L2_green-leaf168_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1179 |
| Ethernet8/13/1 | L2_green-leaf169_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1180 |
| Ethernet8/14/1 | L2_green-leaf170_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1181 |
| Ethernet8/15/1 | L2_green-leaf171_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1182 |
| Ethernet8/16/1 | L2_green-leaf172_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1183 |
| Ethernet8/17/1 | L2_green-leaf173_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1184 |
| Ethernet8/18/1 | L2_green-leaf174_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1185 |
| Ethernet8/19/1 | L2_green-leaf175_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1186 |
| Ethernet8/20/1 | L2_green-leaf176_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1187 |
| Ethernet8/21/1 | L2_green-leaf177_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1188 |
| Ethernet8/22/1 | L2_green-leaf178_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1189 |
| Ethernet8/23/1 | L2_green-leaf179_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1190 |
| Ethernet8/24/1 | L2_green-leaf180_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1191 |
| Ethernet8/25/1 | L2_green-leaf181_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1192 |
| Ethernet8/26/1 | L2_green-leaf182_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1193 |
| Ethernet8/27/1 | L2_green-leaf183_Ethernet53/1 | *trunk | *113,201,204,206-208 | *- | *- | 1194 |
| Ethernet8/31/1 | MLAG_green-spine2_Ethernet8/31/1 | *trunk | *- | *- | *MLAG | 1000 |
| Ethernet8/32/1 | MLAG_green-spine2_Ethernet8/32/1 | *trunk | *- | *- | *MLAG | 1000 |

*Inherited from Port-Channel Interface

##### IPv4

| Interface | Description | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet3/1/1 | P2P_media-PTP-1_Ethernet1/1 | - | 100.83.88.240/31 | default | 9214 | False | - | - |
| Ethernet3/2/1 | P2P_media-PTP-2_Ethernet1/1 | - | 100.83.88.244/31 | default | 9214 | False | - | - |
| Ethernet3/3/1 | P2P_border-leaf1_Ethernet35/1 | - | 100.83.88.248/31 | default | 9214 | False | - | - |
| Ethernet3/4/1 | P2P_border-leaf2_Ethernet35/1 | - | 100.83.88.252/31 | default | 9214 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet3/1/1
   description P2P_media-PTP-1_Ethernet1/1
   no shutdown
   mtu 9214
   no switchport
   ip address 100.83.88.240/31
!
interface Ethernet3/2/1
   description P2P_media-PTP-2_Ethernet1/1
   no shutdown
   mtu 9214
   no switchport
   ip address 100.83.88.244/31
!
interface Ethernet3/3/1
   description P2P_border-leaf1_Ethernet35/1
   no shutdown
   mtu 9214
   no switchport
   ip address 100.83.88.248/31
!
interface Ethernet3/4/1
   description P2P_border-leaf2_Ethernet35/1
   no shutdown
   mtu 9214
   no switchport
   ip address 100.83.88.252/31
!
interface Ethernet3/5/1
   description L2_green-leaf1_Ethernet53/1
   no shutdown
   channel-group 112 mode active
!
interface Ethernet3/6/1
   description L2_green-leaf2_Ethernet53/1
   no shutdown
   channel-group 113 mode active
!
interface Ethernet3/7/1
   description L2_green-leaf3_Ethernet53/1
   no shutdown
   channel-group 114 mode active
!
interface Ethernet3/8/1
   description L2_green-leaf4_Ethernet53/1
   no shutdown
   channel-group 115 mode active
!
interface Ethernet3/9/1
   description L2_green-leaf5_Ethernet53/1
   no shutdown
   channel-group 116 mode active
!
interface Ethernet3/10/1
   description L2_green-leaf6_Ethernet53/1
   no shutdown
   channel-group 117 mode active
!
interface Ethernet3/11/1
   description L2_green-leaf7_Ethernet53/1
   no shutdown
   channel-group 118 mode active
!
interface Ethernet3/12/1
   description L2_green-leaf8_Ethernet53/1
   no shutdown
   channel-group 119 mode active
!
interface Ethernet3/13/1
   description L2_green-leaf9_Ethernet53/1
   no shutdown
   channel-group 120 mode active
!
interface Ethernet3/14/1
   description L2_green-leaf10_Ethernet53/1
   no shutdown
   channel-group 121 mode active
!
interface Ethernet3/15/1
   description L2_green-leaf11_Ethernet53/1
   no shutdown
   channel-group 122 mode active
!
interface Ethernet3/16/1
   description L2_green-leaf12_Ethernet53/1
   no shutdown
   channel-group 123 mode active
!
interface Ethernet3/17/1
   description L2_green-leaf13_Ethernet53/1
   no shutdown
   channel-group 124 mode active
!
interface Ethernet3/18/1
   description L2_green-leaf14_Ethernet53/1
   no shutdown
   channel-group 125 mode active
!
interface Ethernet3/19/1
   description L2_green-leaf15_Ethernet53/1
   no shutdown
   channel-group 126 mode active
!
interface Ethernet3/20/1
   description L2_green-leaf16_Ethernet53/1
   no shutdown
   channel-group 127 mode active
!
interface Ethernet3/21/1
   description L2_green-leaf17_Ethernet53/1
   no shutdown
   channel-group 128 mode active
!
interface Ethernet3/22/1
   description L2_green-leaf18_Ethernet53/1
   no shutdown
   channel-group 129 mode active
!
interface Ethernet3/23/1
   description L2_green-leaf19_Ethernet53/1
   no shutdown
   channel-group 130 mode active
!
interface Ethernet3/24/1
   description L2_green-leaf20_Ethernet53/1
   no shutdown
   channel-group 131 mode active
!
interface Ethernet3/25/1
   description L2_green-leaf21_Ethernet53/1
   no shutdown
   channel-group 132 mode active
!
interface Ethernet3/26/1
   description L2_green-leaf22_Ethernet53/1
   no shutdown
   channel-group 133 mode active
!
interface Ethernet3/27/1
   description L2_green-leaf23_Ethernet53/1
   no shutdown
   channel-group 134 mode active
!
interface Ethernet3/28/1
   description L2_green-leaf24_Ethernet53/1
   no shutdown
   channel-group 135 mode active
!
interface Ethernet3/29/1
   description L2_green-leaf25_Ethernet53/1
   no shutdown
   channel-group 136 mode active
!
interface Ethernet3/30/1
   description L2_green-leaf26_Ethernet53/1
   no shutdown
   channel-group 137 mode active
!
interface Ethernet3/31/1
   description L2_green-leaf27_Ethernet53/1
   no shutdown
   channel-group 138 mode active
!
interface Ethernet3/32/1
   description L2_green-leaf28_Ethernet53/1
   no shutdown
   channel-group 139 mode active
!
interface Ethernet4/1/1
   description L2_green-leaf29_Ethernet53/1
   no shutdown
   channel-group 140 mode active
!
interface Ethernet4/2/1
   description L2_green-leaf30_Ethernet53/1
   no shutdown
   channel-group 141 mode active
!
interface Ethernet4/3/1
   description L2_green-leaf31_Ethernet53/1
   no shutdown
   channel-group 142 mode active
!
interface Ethernet4/4/1
   description L2_green-leaf32_Ethernet53/1
   no shutdown
   channel-group 143 mode active
!
interface Ethernet4/5/1
   description L2_green-leaf33_Ethernet53/1
   no shutdown
   channel-group 144 mode active
!
interface Ethernet4/6/1
   description L2_green-leaf34_Ethernet53/1
   no shutdown
   channel-group 145 mode active
!
interface Ethernet4/7/1
   description L2_green-leaf35_Ethernet53/1
   no shutdown
   channel-group 146 mode active
!
interface Ethernet4/8/1
   description L2_green-leaf36_Ethernet53/1
   no shutdown
   channel-group 147 mode active
!
interface Ethernet4/9/1
   description L2_green-leaf37_Ethernet53/1
   no shutdown
   channel-group 148 mode active
!
interface Ethernet4/10/1
   description L2_green-leaf38_Ethernet53/1
   no shutdown
   channel-group 149 mode active
!
interface Ethernet4/11/1
   description L2_green-leaf39_Ethernet53/1
   no shutdown
   channel-group 150 mode active
!
interface Ethernet4/12/1
   description L2_green-leaf40_Ethernet53/1
   no shutdown
   channel-group 151 mode active
!
interface Ethernet4/13/1
   description L2_green-leaf41_Ethernet53/1
   no shutdown
   channel-group 152 mode active
!
interface Ethernet4/14/1
   description L2_green-leaf42_Ethernet53/1
   no shutdown
   channel-group 153 mode active
!
interface Ethernet4/15/1
   description L2_green-leaf43_Ethernet53/1
   no shutdown
   channel-group 154 mode active
!
interface Ethernet4/16/1
   description L2_green-leaf44_Ethernet53/1
   no shutdown
   channel-group 155 mode active
!
interface Ethernet4/17/1
   description L2_green-leaf45_Ethernet53/1
   no shutdown
   channel-group 156 mode active
!
interface Ethernet4/18/1
   description L2_green-leaf46_Ethernet53/1
   no shutdown
   channel-group 157 mode active
!
interface Ethernet4/19/1
   description L2_green-leaf47_Ethernet53/1
   no shutdown
   channel-group 158 mode active
!
interface Ethernet4/20/1
   description L2_green-leaf48_Ethernet53/1
   no shutdown
   channel-group 159 mode active
!
interface Ethernet4/21/1
   description L2_green-leaf49_Ethernet53/1
   no shutdown
   channel-group 160 mode active
!
interface Ethernet4/22/1
   description L2_green-leaf50_Ethernet53/1
   no shutdown
   channel-group 161 mode active
!
interface Ethernet4/23/1
   description L2_green-leaf51_Ethernet53/1
   no shutdown
   channel-group 162 mode active
!
interface Ethernet4/24/1
   description L2_green-leaf52_Ethernet53/1
   no shutdown
   channel-group 163 mode active
!
interface Ethernet4/25/1
   description L2_green-leaf53_Ethernet53/1
   no shutdown
   channel-group 164 mode active
!
interface Ethernet4/26/1
   description L2_green-leaf54_Ethernet53/1
   no shutdown
   channel-group 165 mode active
!
interface Ethernet4/27/1
   description L2_green-leaf55_Ethernet53/1
   no shutdown
   channel-group 166 mode active
!
interface Ethernet4/28/1
   description L2_green-leaf56_Ethernet53/1
   no shutdown
   channel-group 167 mode active
!
interface Ethernet4/29/1
   description L2_green-leaf57_Ethernet53/1
   no shutdown
   channel-group 168 mode active
!
interface Ethernet4/30/1
   description L2_green-leaf58_Ethernet53/1
   no shutdown
   channel-group 169 mode active
!
interface Ethernet4/31/1
   description L2_green-leaf59_Ethernet53/1
   no shutdown
   channel-group 170 mode active
!
interface Ethernet4/32/1
   description L2_green-leaf60_Ethernet53/1
   no shutdown
   channel-group 171 mode active
!
interface Ethernet5/1/1
   description L2_green-leaf61_Ethernet53/1
   no shutdown
   channel-group 172 mode active
!
interface Ethernet5/2/1
   description L2_green-leaf62_Ethernet53/1
   no shutdown
   channel-group 173 mode active
!
interface Ethernet5/3/1
   description L2_green-leaf63_Ethernet53/1
   no shutdown
   channel-group 174 mode active
!
interface Ethernet5/4/1
   description L2_green-leaf64_Ethernet53/1
   no shutdown
   channel-group 175 mode active
!
interface Ethernet5/5/1
   description L2_green-leaf65_Ethernet53/1
   no shutdown
   channel-group 176 mode active
!
interface Ethernet5/6/1
   description L2_green-leaf66_Ethernet53/1
   no shutdown
   channel-group 177 mode active
!
interface Ethernet5/7/1
   description L2_green-leaf67_Ethernet53/1
   no shutdown
   channel-group 178 mode active
!
interface Ethernet5/8/1
   description L2_green-leaf68_Ethernet53/1
   no shutdown
   channel-group 179 mode active
!
interface Ethernet5/9/1
   description L2_green-leaf69_Ethernet53/1
   no shutdown
   channel-group 180 mode active
!
interface Ethernet5/10/1
   description L2_green-leaf70_Ethernet53/1
   no shutdown
   channel-group 181 mode active
!
interface Ethernet5/11/1
   description L2_green-leaf71_Ethernet53/1
   no shutdown
   channel-group 182 mode active
!
interface Ethernet5/12/1
   description L2_green-leaf72_Ethernet53/1
   no shutdown
   channel-group 183 mode active
!
interface Ethernet5/13/1
   description L2_green-leaf73_Ethernet53/1
   no shutdown
   channel-group 184 mode active
!
interface Ethernet5/14/1
   description L2_green-leaf74_Ethernet53/1
   no shutdown
   channel-group 185 mode active
!
interface Ethernet5/15/1
   description L2_green-leaf75_Ethernet53/1
   no shutdown
   channel-group 186 mode active
!
interface Ethernet5/16/1
   description L2_green-leaf76_Ethernet53/1
   no shutdown
   channel-group 187 mode active
!
interface Ethernet5/17/1
   description L2_green-leaf77_Ethernet53/1
   no shutdown
   channel-group 188 mode active
!
interface Ethernet5/18/1
   description L2_green-leaf78_Ethernet53/1
   no shutdown
   channel-group 189 mode active
!
interface Ethernet5/19/1
   description L2_green-leaf79_Ethernet53/1
   no shutdown
   channel-group 190 mode active
!
interface Ethernet5/20/1
   description L2_green-leaf80_Ethernet53/1
   no shutdown
   channel-group 191 mode active
!
interface Ethernet5/21/1
   description L2_green-leaf81_Ethernet53/1
   no shutdown
   channel-group 192 mode active
!
interface Ethernet5/22/1
   description L2_green-leaf82_Ethernet53/1
   no shutdown
   channel-group 193 mode active
!
interface Ethernet5/23/1
   description L2_green-leaf83_Ethernet53/1
   no shutdown
   channel-group 194 mode active
!
interface Ethernet5/24/1
   description L2_green-leaf84_Ethernet53/1
   no shutdown
   channel-group 195 mode active
!
interface Ethernet5/25/1
   description L2_green-leaf85_Ethernet53/1
   no shutdown
   channel-group 196 mode active
!
interface Ethernet5/26/1
   description L2_green-leaf86_Ethernet53/1
   no shutdown
   channel-group 197 mode active
!
interface Ethernet5/27/1
   description L2_green-leaf87_Ethernet53/1
   no shutdown
   channel-group 198 mode active
!
interface Ethernet5/28/1
   description L2_green-leaf88_Ethernet53/1
   no shutdown
   channel-group 199 mode active
!
interface Ethernet5/29/1
   description L2_green-leaf89_Ethernet53/1
   no shutdown
   channel-group 1100 mode active
!
interface Ethernet5/30/1
   description L2_green-leaf90_Ethernet53/1
   no shutdown
   channel-group 1101 mode active
!
interface Ethernet5/31/1
   description L2_green-leaf91_Ethernet53/1
   no shutdown
   channel-group 1102 mode active
!
interface Ethernet5/32/1
   description L2_green-leaf92_Ethernet53/1
   no shutdown
   channel-group 1103 mode active
!
interface Ethernet6/1/1
   description L2_green-leaf93_Ethernet53/1
   no shutdown
   channel-group 1104 mode active
!
interface Ethernet6/2/1
   description L2_green-leaf94_Ethernet53/1
   no shutdown
   channel-group 1105 mode active
!
interface Ethernet6/3/1
   description L2_green-leaf95_Ethernet53/1
   no shutdown
   channel-group 1106 mode active
!
interface Ethernet6/4/1
   description L2_green-leaf96_Ethernet53/1
   no shutdown
   channel-group 1107 mode active
!
interface Ethernet6/5/1
   description L2_green-leaf97_Ethernet53/1
   no shutdown
   channel-group 1108 mode active
!
interface Ethernet6/6/1
   description L2_green-leaf98_Ethernet53/1
   no shutdown
   channel-group 1109 mode active
!
interface Ethernet6/7/1
   description L2_green-leaf99_Ethernet53/1
   no shutdown
   channel-group 1110 mode active
!
interface Ethernet6/8/1
   description L2_green-leaf100_Ethernet53/1
   no shutdown
   channel-group 1111 mode active
!
interface Ethernet6/9/1
   description L2_green-leaf101_Ethernet53/1
   no shutdown
   channel-group 1112 mode active
!
interface Ethernet6/10/1
   description L2_green-leaf102_Ethernet53/1
   no shutdown
   channel-group 1113 mode active
!
interface Ethernet6/11/1
   description L2_green-leaf103_Ethernet53/1
   no shutdown
   channel-group 1114 mode active
!
interface Ethernet6/12/1
   description L2_green-leaf104_Ethernet53/1
   no shutdown
   channel-group 1115 mode active
!
interface Ethernet6/13/1
   description L2_green-leaf105_Ethernet53/1
   no shutdown
   channel-group 1116 mode active
!
interface Ethernet6/14/1
   description L2_green-leaf106_Ethernet53/1
   no shutdown
   channel-group 1117 mode active
!
interface Ethernet6/15/1
   description L2_green-leaf107_Ethernet53/1
   no shutdown
   channel-group 1118 mode active
!
interface Ethernet6/16/1
   description L2_green-leaf108_Ethernet53/1
   no shutdown
   channel-group 1119 mode active
!
interface Ethernet6/17/1
   description L2_green-leaf109_Ethernet53/1
   no shutdown
   channel-group 1120 mode active
!
interface Ethernet6/18/1
   description L2_green-leaf110_Ethernet53/1
   no shutdown
   channel-group 1121 mode active
!
interface Ethernet6/19/1
   description L2_green-leaf111_Ethernet53/1
   no shutdown
   channel-group 1122 mode active
!
interface Ethernet6/20/1
   description L2_green-leaf112_Ethernet53/1
   no shutdown
   channel-group 1123 mode active
!
interface Ethernet6/21/1
   description L2_green-leaf113_Ethernet53/1
   no shutdown
   channel-group 1124 mode active
!
interface Ethernet6/22/1
   description L2_green-leaf114_Ethernet53/1
   no shutdown
   channel-group 1125 mode active
!
interface Ethernet6/23/1
   description L2_green-leaf115_Ethernet53/1
   no shutdown
   channel-group 1126 mode active
!
interface Ethernet6/24/1
   description L2_green-leaf116_Ethernet53/1
   no shutdown
   channel-group 1127 mode active
!
interface Ethernet6/25/1
   description L2_green-leaf117_Ethernet53/1
   no shutdown
   channel-group 1128 mode active
!
interface Ethernet6/26/1
   description L2_green-leaf118_Ethernet53/1
   no shutdown
   channel-group 1129 mode active
!
interface Ethernet6/27/1
   description L2_green-leaf119_Ethernet53/1
   no shutdown
   channel-group 1130 mode active
!
interface Ethernet6/28/1
   description L2_green-leaf120_Ethernet53/1
   no shutdown
   channel-group 1131 mode active
!
interface Ethernet6/29/1
   description L2_green-leaf121_Ethernet53/1
   no shutdown
   channel-group 1132 mode active
!
interface Ethernet6/30/1
   description L2_green-leaf122_Ethernet53/1
   no shutdown
   channel-group 1133 mode active
!
interface Ethernet6/31/1
   description L2_green-leaf123_Ethernet53/1
   no shutdown
   channel-group 1134 mode active
!
interface Ethernet6/32/1
   description L2_green-leaf124_Ethernet53/1
   no shutdown
   channel-group 1135 mode active
!
interface Ethernet7/1/1
   description L2_green-leaf125_Ethernet53/1
   no shutdown
   channel-group 1136 mode active
!
interface Ethernet7/2/1
   description L2_green-leaf126_Ethernet53/1
   no shutdown
   channel-group 1137 mode active
!
interface Ethernet7/3/1
   description L2_green-leaf127_Ethernet53/1
   no shutdown
   channel-group 1138 mode active
!
interface Ethernet7/4/1
   description L2_green-leaf128_Ethernet53/1
   no shutdown
   channel-group 1139 mode active
!
interface Ethernet7/5/1
   description L2_green-leaf129_Ethernet53/1
   no shutdown
   channel-group 1140 mode active
!
interface Ethernet7/6/1
   description L2_green-leaf130_Ethernet53/1
   no shutdown
   channel-group 1141 mode active
!
interface Ethernet7/7/1
   description L2_green-leaf131_Ethernet53/1
   no shutdown
   channel-group 1142 mode active
!
interface Ethernet7/8/1
   description L2_green-leaf132_Ethernet53/1
   no shutdown
   channel-group 1143 mode active
!
interface Ethernet7/9/1
   description L2_green-leaf133_Ethernet53/1
   no shutdown
   channel-group 1144 mode active
!
interface Ethernet7/10/1
   description L2_green-leaf134_Ethernet53/1
   no shutdown
   channel-group 1145 mode active
!
interface Ethernet7/11/1
   description L2_green-leaf135_Ethernet53/1
   no shutdown
   channel-group 1146 mode active
!
interface Ethernet7/12/1
   description L2_green-leaf136_Ethernet53/1
   no shutdown
   channel-group 1147 mode active
!
interface Ethernet7/13/1
   description L2_green-leaf137_Ethernet53/1
   no shutdown
   channel-group 1148 mode active
!
interface Ethernet7/14/1
   description L2_green-leaf138_Ethernet53/1
   no shutdown
   channel-group 1149 mode active
!
interface Ethernet7/15/1
   description L2_green-leaf139_Ethernet53/1
   no shutdown
   channel-group 1150 mode active
!
interface Ethernet7/16/1
   description L2_green-leaf140_Ethernet53/1
   no shutdown
   channel-group 1151 mode active
!
interface Ethernet7/17/1
   description L2_green-leaf141_Ethernet53/1
   no shutdown
   channel-group 1152 mode active
!
interface Ethernet7/18/1
   description L2_green-leaf142_Ethernet53/1
   no shutdown
   channel-group 1153 mode active
!
interface Ethernet7/19/1
   description L2_green-leaf143_Ethernet53/1
   no shutdown
   channel-group 1154 mode active
!
interface Ethernet7/20/1
   description L2_green-leaf144_Ethernet53/1
   no shutdown
   channel-group 1155 mode active
!
interface Ethernet7/21/1
   description L2_green-leaf145_Ethernet53/1
   no shutdown
   channel-group 1156 mode active
!
interface Ethernet7/22/1
   description L2_green-leaf146_Ethernet53/1
   no shutdown
   channel-group 1157 mode active
!
interface Ethernet7/23/1
   description L2_green-leaf147_Ethernet53/1
   no shutdown
   channel-group 1158 mode active
!
interface Ethernet7/24/1
   description L2_green-leaf148_Ethernet53/1
   no shutdown
   channel-group 1159 mode active
!
interface Ethernet7/25/1
   description L2_green-leaf149_Ethernet53/1
   no shutdown
   channel-group 1160 mode active
!
interface Ethernet7/26/1
   description L2_green-leaf150_Ethernet53/1
   no shutdown
   channel-group 1161 mode active
!
interface Ethernet7/27/1
   description L2_green-leaf151_Ethernet53/1
   no shutdown
   channel-group 1162 mode active
!
interface Ethernet7/28/1
   description L2_green-leaf152_Ethernet53/1
   no shutdown
   channel-group 1163 mode active
!
interface Ethernet7/29/1
   description L2_green-leaf153_Ethernet53/1
   no shutdown
   channel-group 1164 mode active
!
interface Ethernet7/30/1
   description L2_green-leaf154_Ethernet53/1
   no shutdown
   channel-group 1165 mode active
!
interface Ethernet7/31/1
   description L2_green-leaf155_Ethernet53/1
   no shutdown
   channel-group 1166 mode active
!
interface Ethernet7/32/1
   description L2_green-leaf156_Ethernet53/1
   no shutdown
   channel-group 1167 mode active
!
interface Ethernet8/1/1
   description L2_green-leaf157_Ethernet53/1
   no shutdown
   channel-group 1168 mode active
!
interface Ethernet8/2/1
   description L2_green-leaf158_Ethernet53/1
   no shutdown
   channel-group 1169 mode active
!
interface Ethernet8/3/1
   description L2_green-leaf159_Ethernet53/1
   no shutdown
   channel-group 1170 mode active
!
interface Ethernet8/4/1
   description L2_green-leaf160_Ethernet53/1
   no shutdown
   channel-group 1171 mode active
!
interface Ethernet8/5/1
   description L2_green-leaf161_Ethernet53/1
   no shutdown
   channel-group 1172 mode active
!
interface Ethernet8/6/1
   description L2_green-leaf162_Ethernet53/1
   no shutdown
   channel-group 1173 mode active
!
interface Ethernet8/7/1
   description L2_green-leaf163_Ethernet53/1
   no shutdown
   channel-group 1174 mode active
!
interface Ethernet8/8/1
   description L2_green-leaf164_Ethernet53/1
   no shutdown
   channel-group 1175 mode active
!
interface Ethernet8/9/1
   description L2_green-leaf165_Ethernet53/1
   no shutdown
   channel-group 1176 mode active
!
interface Ethernet8/10/1
   description L2_green-leaf166_Ethernet53/1
   no shutdown
   channel-group 1177 mode active
!
interface Ethernet8/11/1
   description L2_green-leaf167_Ethernet53/1
   no shutdown
   channel-group 1178 mode active
!
interface Ethernet8/12/1
   description L2_green-leaf168_Ethernet53/1
   no shutdown
   channel-group 1179 mode active
!
interface Ethernet8/13/1
   description L2_green-leaf169_Ethernet53/1
   no shutdown
   channel-group 1180 mode active
!
interface Ethernet8/14/1
   description L2_green-leaf170_Ethernet53/1
   no shutdown
   channel-group 1181 mode active
!
interface Ethernet8/15/1
   description L2_green-leaf171_Ethernet53/1
   no shutdown
   channel-group 1182 mode active
!
interface Ethernet8/16/1
   description L2_green-leaf172_Ethernet53/1
   no shutdown
   channel-group 1183 mode active
!
interface Ethernet8/17/1
   description L2_green-leaf173_Ethernet53/1
   no shutdown
   channel-group 1184 mode active
!
interface Ethernet8/18/1
   description L2_green-leaf174_Ethernet53/1
   no shutdown
   channel-group 1185 mode active
!
interface Ethernet8/19/1
   description L2_green-leaf175_Ethernet53/1
   no shutdown
   channel-group 1186 mode active
!
interface Ethernet8/20/1
   description L2_green-leaf176_Ethernet53/1
   no shutdown
   channel-group 1187 mode active
!
interface Ethernet8/21/1
   description L2_green-leaf177_Ethernet53/1
   no shutdown
   channel-group 1188 mode active
!
interface Ethernet8/22/1
   description L2_green-leaf178_Ethernet53/1
   no shutdown
   channel-group 1189 mode active
!
interface Ethernet8/23/1
   description L2_green-leaf179_Ethernet53/1
   no shutdown
   channel-group 1190 mode active
!
interface Ethernet8/24/1
   description L2_green-leaf180_Ethernet53/1
   no shutdown
   channel-group 1191 mode active
!
interface Ethernet8/25/1
   description L2_green-leaf181_Ethernet53/1
   no shutdown
   channel-group 1192 mode active
!
interface Ethernet8/26/1
   description L2_green-leaf182_Ethernet53/1
   no shutdown
   channel-group 1193 mode active
!
interface Ethernet8/27/1
   description L2_green-leaf183_Ethernet53/1
   no shutdown
   channel-group 1194 mode active
!
interface Ethernet8/31/1
   description MLAG_green-spine2_Ethernet8/31/1
   no shutdown
   channel-group 1000 mode active
!
interface Ethernet8/32/1
   description MLAG_green-spine2_Ethernet8/32/1
   no shutdown
   channel-group 1000 mode active
```

### Port-Channel Interfaces

#### Port-Channel Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | LACP Fallback Timeout | LACP Fallback Mode | MLAG ID | EVPN ESI |
| --------- | ----------- | ---- | ----- | ----------- | ------------| --------------------- | ------------------ | ------- | -------- |
| Port-Channel112 | L2_green-leaf1_Port-Channel12 | trunk | 113,201-202 | - | - | - | - | 112 | - |
| Port-Channel113 | L2_green-leaf2_Port-Channel13 | trunk | 113,202-204 | - | - | - | - | 113 | - |
| Port-Channel114 | L2_green-leaf3_Port-Channel14 | trunk | 113,201,203,205,207,209 | - | - | - | - | 114 | - |
| Port-Channel115 | L2_green-leaf4_Port-Channel15 | trunk | 113,202,204,206,208 | - | - | - | - | 115 | - |
| Port-Channel116 | L2_green-leaf5_Port-Channel16 | trunk | 113 | - | - | - | - | 116 | - |
| Port-Channel117 | L2_green-leaf6_Port-Channel17 | trunk | 113,201,203-205,207-209 | - | - | - | - | 117 | - |
| Port-Channel118 | L2_green-leaf7_Port-Channel18 | trunk | 113,201-207,209 | - | - | - | - | 118 | - |
| Port-Channel119 | L2_green-leaf8_Port-Channel19 | trunk | 113,201-204,206-207,209 | - | - | - | - | 119 | - |
| Port-Channel120 | L2_green-leaf9_Port-Channel20 | trunk | 113,201-204,206-207,209 | - | - | - | - | 120 | - |
| Port-Channel121 | L2_green-leaf10_Port-Channel21 | trunk | 113,201-204,206-207,209 | - | - | - | - | 121 | - |
| Port-Channel122 | L2_green-leaf11_Port-Channel22 | trunk | 113,201-204,206-207,209 | - | - | - | - | 122 | - |
| Port-Channel123 | L2_green-leaf12_Port-Channel23 | trunk | 113,201-204,206,209 | - | - | - | - | 123 | - |
| Port-Channel124 | L2_green-leaf13_Port-Channel24 | trunk | 113,201-204,206,209 | - | - | - | - | 124 | - |
| Port-Channel125 | L2_green-leaf14_Port-Channel25 | trunk | 113,201-204,206,209 | - | - | - | - | 125 | - |
| Port-Channel126 | L2_green-leaf15_Port-Channel26 | trunk | 113,201-204,206,209 | - | - | - | - | 126 | - |
| Port-Channel127 | L2_green-leaf16_Port-Channel27 | trunk | 113,201-204,206,209 | - | - | - | - | 127 | - |
| Port-Channel128 | L2_green-leaf17_Port-Channel28 | trunk | 113,201-204,206,209 | - | - | - | - | 128 | - |
| Port-Channel129 | L2_green-leaf18_Port-Channel29 | trunk | 113,201-204,206,209 | - | - | - | - | 129 | - |
| Port-Channel130 | L2_green-leaf19_Port-Channel30 | trunk | 113,201-204,206,209 | - | - | - | - | 130 | - |
| Port-Channel131 | L2_green-leaf20_Port-Channel31 | trunk | 113,201-204,206,209 | - | - | - | - | 131 | - |
| Port-Channel132 | L2_green-leaf21_Port-Channel32 | trunk | 113,201-204,206,209 | - | - | - | - | 132 | - |
| Port-Channel133 | L2_green-leaf22_Port-Channel33 | trunk | 113,201-204,206,209 | - | - | - | - | 133 | - |
| Port-Channel134 | L2_green-leaf23_Port-Channel34 | trunk | 113,201-204,206,209 | - | - | - | - | 134 | - |
| Port-Channel135 | L2_green-leaf24_Port-Channel35 | trunk | 113,201-204,206,209 | - | - | - | - | 135 | - |
| Port-Channel136 | L2_green-leaf25_Port-Channel36 | trunk | 113,201-204,206,209 | - | - | - | - | 136 | - |
| Port-Channel137 | L2_green-leaf26_Port-Channel37 | trunk | 113,201-204,206,209 | - | - | - | - | 137 | - |
| Port-Channel138 | L2_green-leaf27_Port-Channel38 | trunk | 113,201-204,206,209 | - | - | - | - | 138 | - |
| Port-Channel139 | L2_green-leaf28_Port-Channel39 | trunk | 113,201-204,206,209 | - | - | - | - | 139 | - |
| Port-Channel140 | L2_green-leaf29_Port-Channel40 | trunk | 113,201-204,206,209 | - | - | - | - | 140 | - |
| Port-Channel141 | L2_green-leaf30_Port-Channel41 | trunk | 113,201-204,206,209 | - | - | - | - | 141 | - |
| Port-Channel142 | L2_green-leaf31_Port-Channel42 | trunk | 113,201-204,206,209 | - | - | - | - | 142 | - |
| Port-Channel143 | L2_green-leaf32_Port-Channel43 | trunk | 113,201-204,206,208-209 | - | - | - | - | 143 | - |
| Port-Channel144 | L2_green-leaf33_Port-Channel44 | trunk | 113,201-204,206,208-209 | - | - | - | - | 144 | - |
| Port-Channel145 | L2_green-leaf34_Port-Channel45 | trunk | 113,201-204,206,208-209 | - | - | - | - | 145 | - |
| Port-Channel146 | L2_green-leaf35_Port-Channel46 | trunk | 113,201-204,206,208-209 | - | - | - | - | 146 | - |
| Port-Channel147 | L2_green-leaf36_Port-Channel47 | trunk | 113,201-204,206,208-209 | - | - | - | - | 147 | - |
| Port-Channel148 | L2_green-leaf37_Port-Channel48 | trunk | 113,201-204,206,208-209 | - | - | - | - | 148 | - |
| Port-Channel149 | L2_green-leaf38_Port-Channel49 | trunk | 113,201-204,206,208 | - | - | - | - | 149 | - |
| Port-Channel150 | L2_green-leaf39_Port-Channel50 | trunk | 113,201-204,208 | - | - | - | - | 150 | - |
| Port-Channel151 | L2_green-leaf40_Port-Channel51 | trunk | 113,201-204,208 | - | - | - | - | 151 | - |
| Port-Channel152 | L2_green-leaf41_Port-Channel52 | trunk | 113,201-204,208 | - | - | - | - | 152 | - |
| Port-Channel153 | L2_green-leaf42_Port-Channel53 | trunk | 113,201-204,208 | - | - | - | - | 153 | - |
| Port-Channel154 | L2_green-leaf43_Port-Channel54 | trunk | 113,201-204,208 | - | - | - | - | 154 | - |
| Port-Channel155 | L2_green-leaf44_Port-Channel55 | trunk | 113,201-204,208 | - | - | - | - | 155 | - |
| Port-Channel156 | L2_green-leaf45_Port-Channel56 | trunk | 113,201-204,208 | - | - | - | - | 156 | - |
| Port-Channel157 | L2_green-leaf46_Port-Channel57 | trunk | 113,201-204,208 | - | - | - | - | 157 | - |
| Port-Channel158 | L2_green-leaf47_Port-Channel58 | trunk | 113,201-204,208 | - | - | - | - | 158 | - |
| Port-Channel159 | L2_green-leaf48_Port-Channel59 | trunk | 113,201-204,207-208 | - | - | - | - | 159 | - |
| Port-Channel160 | L2_green-leaf49_Port-Channel60 | trunk | 113,201-204,207-208 | - | - | - | - | 160 | - |
| Port-Channel161 | L2_green-leaf50_Port-Channel61 | trunk | 113,201-204,207-208 | - | - | - | - | 161 | - |
| Port-Channel162 | L2_green-leaf51_Port-Channel62 | trunk | 113,201-204,207-208 | - | - | - | - | 162 | - |
| Port-Channel163 | L2_green-leaf52_Port-Channel63 | trunk | 113,201-204,207-208 | - | - | - | - | 163 | - |
| Port-Channel164 | L2_green-leaf53_Port-Channel64 | trunk | 113,201-204,207-208 | - | - | - | - | 164 | - |
| Port-Channel165 | L2_green-leaf54_Port-Channel65 | trunk | 113,203-204,207-208 | - | - | - | - | 165 | - |
| Port-Channel166 | L2_green-leaf55_Port-Channel66 | trunk | 113,203-204,207-208 | - | - | - | - | 166 | - |
| Port-Channel167 | L2_green-leaf56_Port-Channel67 | trunk | 113,203-204,207-208 | - | - | - | - | 167 | - |
| Port-Channel168 | L2_green-leaf57_Port-Channel68 | trunk | 113,203-204,207-208 | - | - | - | - | 168 | - |
| Port-Channel169 | L2_green-leaf58_Port-Channel69 | trunk | 113,203-204,207-208 | - | - | - | - | 169 | - |
| Port-Channel170 | L2_green-leaf59_Port-Channel70 | trunk | 113,203-204,207-208 | - | - | - | - | 170 | - |
| Port-Channel171 | L2_green-leaf60_Port-Channel71 | trunk | 113,203-204,207-208 | - | - | - | - | 171 | - |
| Port-Channel172 | L2_green-leaf61_Port-Channel72 | trunk | 113,203-204,207-208 | - | - | - | - | 172 | - |
| Port-Channel173 | L2_green-leaf62_Port-Channel73 | trunk | 113,203-204,207-208 | - | - | - | - | 173 | - |
| Port-Channel174 | L2_green-leaf63_Port-Channel74 | trunk | 113,203-204,207-208 | - | - | - | - | 174 | - |
| Port-Channel175 | L2_green-leaf64_Port-Channel75 | trunk | 113,203-204,207-208 | - | - | - | - | 175 | - |
| Port-Channel176 | L2_green-leaf65_Port-Channel76 | trunk | 113,203-204,207-208 | - | - | - | - | 176 | - |
| Port-Channel177 | L2_green-leaf66_Port-Channel77 | trunk | 113,203-204,207-208 | - | - | - | - | 177 | - |
| Port-Channel178 | L2_green-leaf67_Port-Channel78 | trunk | 113,203-204,207-208 | - | - | - | - | 178 | - |
| Port-Channel179 | L2_green-leaf68_Port-Channel79 | trunk | 113,203-204,207-208 | - | - | - | - | 179 | - |
| Port-Channel180 | L2_green-leaf69_Port-Channel80 | trunk | 113,203-204,207-208 | - | - | - | - | 180 | - |
| Port-Channel181 | L2_green-leaf70_Port-Channel81 | trunk | 113,203-205,207-208 | - | - | - | - | 181 | - |
| Port-Channel182 | L2_green-leaf71_Port-Channel82 | trunk | 113,203-205,207-208 | - | - | - | - | 182 | - |
| Port-Channel183 | L2_green-leaf72_Port-Channel83 | trunk | 113,203-205,207-208 | - | - | - | - | 183 | - |
| Port-Channel184 | L2_green-leaf73_Port-Channel84 | trunk | 113,203-205,207-208 | - | - | - | - | 184 | - |
| Port-Channel185 | L2_green-leaf74_Port-Channel85 | trunk | 113,203-205,207-208 | - | - | - | - | 185 | - |
| Port-Channel186 | L2_green-leaf75_Port-Channel86 | trunk | 113,203-205,207-208 | - | - | - | - | 186 | - |
| Port-Channel187 | L2_green-leaf76_Port-Channel87 | trunk | 113,203-205,207-209 | - | - | - | - | 187 | - |
| Port-Channel188 | L2_green-leaf77_Port-Channel88 | trunk | 113,203-205,207-209 | - | - | - | - | 188 | - |
| Port-Channel189 | L2_green-leaf78_Port-Channel89 | trunk | 113,203-205,207-209 | - | - | - | - | 189 | - |
| Port-Channel190 | L2_green-leaf79_Port-Channel90 | trunk | 113,203-205,207-209 | - | - | - | - | 190 | - |
| Port-Channel191 | L2_green-leaf80_Port-Channel91 | trunk | 113,203-204,207-209 | - | - | - | - | 191 | - |
| Port-Channel192 | L2_green-leaf81_Port-Channel92 | trunk | 113,203-204,207-209 | - | - | - | - | 192 | - |
| Port-Channel193 | L2_green-leaf82_Port-Channel93 | trunk | 113,203-204,207-209 | - | - | - | - | 193 | - |
| Port-Channel194 | L2_green-leaf83_Port-Channel94 | trunk | 113,203-204,207-209 | - | - | - | - | 194 | - |
| Port-Channel195 | L2_green-leaf84_Port-Channel95 | trunk | 113,207-209 | - | - | - | - | 195 | - |
| Port-Channel196 | L2_green-leaf85_Port-Channel96 | trunk | 113,207,209 | - | - | - | - | 196 | - |
| Port-Channel197 | L2_green-leaf86_Port-Channel97 | trunk | 113,207,209 | - | - | - | - | 197 | - |
| Port-Channel198 | L2_green-leaf87_Port-Channel98 | trunk | 113,207,209 | - | - | - | - | 198 | - |
| Port-Channel199 | L2_green-leaf88_Port-Channel99 | trunk | 113,207,209 | - | - | - | - | 199 | - |
| Port-Channel1000 | MLAG_green-spine2_Port-Channel1000 | trunk | - | - | MLAG | - | - | - | - |
| Port-Channel1100 | L2_green-leaf89_Port-Channel100 | trunk | 113,207,209 | - | - | - | - | 1100 | - |
| Port-Channel1101 | L2_green-leaf90_Port-Channel101 | trunk | 113,207,209 | - | - | - | - | 1101 | - |
| Port-Channel1102 | L2_green-leaf91_Port-Channel102 | trunk | 113,207,209 | - | - | - | - | 1102 | - |
| Port-Channel1103 | L2_green-leaf92_Port-Channel103 | trunk | 113,207,209 | - | - | - | - | 1103 | - |
| Port-Channel1104 | L2_green-leaf93_Port-Channel104 | trunk | 113,207,209 | - | - | - | - | 1104 | - |
| Port-Channel1105 | L2_green-leaf94_Port-Channel105 | trunk | 113,207,209 | - | - | - | - | 1105 | - |
| Port-Channel1106 | L2_green-leaf95_Port-Channel106 | trunk | 113,207,209 | - | - | - | - | 1106 | - |
| Port-Channel1107 | L2_green-leaf96_Port-Channel107 | trunk | 113,205,207,209 | - | - | - | - | 1107 | - |
| Port-Channel1108 | L2_green-leaf97_Port-Channel108 | trunk | 113,205,207,209 | - | - | - | - | 1108 | - |
| Port-Channel1109 | L2_green-leaf98_Port-Channel109 | trunk | 113,205,207,209 | - | - | - | - | 1109 | - |
| Port-Channel1110 | L2_green-leaf99_Port-Channel110 | trunk | 113,205,207,209 | - | - | - | - | 1110 | - |
| Port-Channel1111 | L2_green-leaf100_Port-Channel111 | trunk | 113,205,207,209 | - | - | - | - | 1111 | - |
| Port-Channel1112 | L2_green-leaf101_Port-Channel112 | trunk | 113,205,207,209 | - | - | - | - | 1112 | - |
| Port-Channel1113 | L2_green-leaf102_Port-Channel113 | trunk | 113,205,207,209 | - | - | - | - | 1113 | - |
| Port-Channel1114 | L2_green-leaf103_Port-Channel114 | trunk | 113,205,207,209 | - | - | - | - | 1114 | - |
| Port-Channel1115 | L2_green-leaf104_Port-Channel115 | trunk | 113,205,207,209 | - | - | - | - | 1115 | - |
| Port-Channel1116 | L2_green-leaf105_Port-Channel116 | trunk | 113,205,207,209 | - | - | - | - | 1116 | - |
| Port-Channel1117 | L2_green-leaf106_Port-Channel117 | trunk | 113,205,207,209 | - | - | - | - | 1117 | - |
| Port-Channel1118 | L2_green-leaf107_Port-Channel118 | trunk | 113,205,207 | - | - | - | - | 1118 | - |
| Port-Channel1119 | L2_green-leaf108_Port-Channel119 | trunk | 113,205,207 | - | - | - | - | 1119 | - |
| Port-Channel1120 | L2_green-leaf109_Port-Channel120 | trunk | 113,205,207 | - | - | - | - | 1120 | - |
| Port-Channel1121 | L2_green-leaf110_Port-Channel121 | trunk | 113,205,207 | - | - | - | - | 1121 | - |
| Port-Channel1122 | L2_green-leaf111_Port-Channel122 | trunk | 113,205,207 | - | - | - | - | 1122 | - |
| Port-Channel1123 | L2_green-leaf112_Port-Channel123 | trunk | 113,205,207 | - | - | - | - | 1123 | - |
| Port-Channel1124 | L2_green-leaf113_Port-Channel124 | trunk | 113,203-205,207 | - | - | - | - | 1124 | - |
| Port-Channel1125 | L2_green-leaf114_Port-Channel125 | trunk | 113,203-205,207 | - | - | - | - | 1125 | - |
| Port-Channel1126 | L2_green-leaf115_Port-Channel126 | trunk | 113,203-205,207 | - | - | - | - | 1126 | - |
| Port-Channel1127 | L2_green-leaf116_Port-Channel127 | trunk | 113,201-205,207 | - | - | - | - | 1127 | - |
| Port-Channel1128 | L2_green-leaf117_Port-Channel128 | trunk | 113,201-205,207 | - | - | - | - | 1128 | - |
| Port-Channel1129 | L2_green-leaf118_Port-Channel129 | trunk | 113,201-205,207 | - | - | - | - | 1129 | - |
| Port-Channel1130 | L2_green-leaf119_Port-Channel130 | trunk | 113,201-205,207 | - | - | - | - | 1130 | - |
| Port-Channel1131 | L2_green-leaf120_Port-Channel131 | trunk | 113,201,204-205,207 | - | - | - | - | 1131 | - |
| Port-Channel1132 | L2_green-leaf121_Port-Channel132 | trunk | 113,201,204-205,207 | - | - | - | - | 1132 | - |
| Port-Channel1133 | L2_green-leaf122_Port-Channel133 | trunk | 113,201,204-205,207 | - | - | - | - | 1133 | - |
| Port-Channel1134 | L2_green-leaf123_Port-Channel134 | trunk | 113,201,204-205,207 | - | - | - | - | 1134 | - |
| Port-Channel1135 | L2_green-leaf124_Port-Channel135 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1135 | - |
| Port-Channel1136 | L2_green-leaf125_Port-Channel136 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1136 | - |
| Port-Channel1137 | L2_green-leaf126_Port-Channel137 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1137 | - |
| Port-Channel1138 | L2_green-leaf127_Port-Channel138 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1138 | - |
| Port-Channel1139 | L2_green-leaf128_Port-Channel139 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1139 | - |
| Port-Channel1140 | L2_green-leaf129_Port-Channel140 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1140 | - |
| Port-Channel1141 | L2_green-leaf130_Port-Channel141 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1141 | - |
| Port-Channel1142 | L2_green-leaf131_Port-Channel142 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1142 | - |
| Port-Channel1143 | L2_green-leaf132_Port-Channel143 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1143 | - |
| Port-Channel1144 | L2_green-leaf133_Port-Channel144 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1144 | - |
| Port-Channel1145 | L2_green-leaf134_Port-Channel145 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1145 | - |
| Port-Channel1146 | L2_green-leaf135_Port-Channel146 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1146 | - |
| Port-Channel1147 | L2_green-leaf136_Port-Channel147 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1147 | - |
| Port-Channel1148 | L2_green-leaf137_Port-Channel148 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1148 | - |
| Port-Channel1149 | L2_green-leaf138_Port-Channel149 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1149 | - |
| Port-Channel1150 | L2_green-leaf139_Port-Channel150 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1150 | - |
| Port-Channel1151 | L2_green-leaf140_Port-Channel151 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1151 | - |
| Port-Channel1152 | L2_green-leaf141_Port-Channel152 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1152 | - |
| Port-Channel1153 | L2_green-leaf142_Port-Channel153 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1153 | - |
| Port-Channel1154 | L2_green-leaf143_Port-Channel154 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1154 | - |
| Port-Channel1155 | L2_green-leaf144_Port-Channel155 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1155 | - |
| Port-Channel1156 | L2_green-leaf145_Port-Channel156 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1156 | - |
| Port-Channel1157 | L2_green-leaf146_Port-Channel157 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1157 | - |
| Port-Channel1158 | L2_green-leaf147_Port-Channel158 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1158 | - |
| Port-Channel1159 | L2_green-leaf148_Port-Channel159 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1159 | - |
| Port-Channel1160 | L2_green-leaf149_Port-Channel160 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1160 | - |
| Port-Channel1161 | L2_green-leaf150_Port-Channel161 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1161 | - |
| Port-Channel1162 | L2_green-leaf151_Port-Channel162 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1162 | - |
| Port-Channel1163 | L2_green-leaf152_Port-Channel163 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1163 | - |
| Port-Channel1164 | L2_green-leaf153_Port-Channel164 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1164 | - |
| Port-Channel1165 | L2_green-leaf154_Port-Channel165 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1165 | - |
| Port-Channel1166 | L2_green-leaf155_Port-Channel166 | trunk | 113,201,204-205,207-208 | - | - | - | - | 1166 | - |
| Port-Channel1167 | L2_green-leaf156_Port-Channel167 | trunk | 113,201,204,207-208 | - | - | - | - | 1167 | - |
| Port-Channel1168 | L2_green-leaf157_Port-Channel168 | trunk | 113,201,204,207-208 | - | - | - | - | 1168 | - |
| Port-Channel1169 | L2_green-leaf158_Port-Channel169 | trunk | 113,201,204,207-208 | - | - | - | - | 1169 | - |
| Port-Channel1170 | L2_green-leaf159_Port-Channel170 | trunk | 113,201,204,207-208 | - | - | - | - | 1170 | - |
| Port-Channel1171 | L2_green-leaf160_Port-Channel171 | trunk | 113,201,204,207-208 | - | - | - | - | 1171 | - |
| Port-Channel1172 | L2_green-leaf161_Port-Channel172 | trunk | 113,201,204,207-208 | - | - | - | - | 1172 | - |
| Port-Channel1173 | L2_green-leaf162_Port-Channel173 | trunk | 113,201,204,207-208 | - | - | - | - | 1173 | - |
| Port-Channel1174 | L2_green-leaf163_Port-Channel174 | trunk | 113,201,204,207-208 | - | - | - | - | 1174 | - |
| Port-Channel1175 | L2_green-leaf164_Port-Channel175 | trunk | 113,201,204,207-208 | - | - | - | - | 1175 | - |
| Port-Channel1176 | L2_green-leaf165_Port-Channel176 | trunk | 113,201,204,206-208 | - | - | - | - | 1176 | - |
| Port-Channel1177 | L2_green-leaf166_Port-Channel177 | trunk | 113,201,204,206-208 | - | - | - | - | 1177 | - |
| Port-Channel1178 | L2_green-leaf167_Port-Channel178 | trunk | 113,201,204,206-208 | - | - | - | - | 1178 | - |
| Port-Channel1179 | L2_green-leaf168_Port-Channel179 | trunk | 113,201,204,206-208 | - | - | - | - | 1179 | - |
| Port-Channel1180 | L2_green-leaf169_Port-Channel180 | trunk | 113,201,204,206-208 | - | - | - | - | 1180 | - |
| Port-Channel1181 | L2_green-leaf170_Port-Channel181 | trunk | 113,201,204,206-208 | - | - | - | - | 1181 | - |
| Port-Channel1182 | L2_green-leaf171_Port-Channel182 | trunk | 113,201,204,206-208 | - | - | - | - | 1182 | - |
| Port-Channel1183 | L2_green-leaf172_Port-Channel183 | trunk | 113,201,204,206-208 | - | - | - | - | 1183 | - |
| Port-Channel1184 | L2_green-leaf173_Port-Channel184 | trunk | 113,201,204,206-208 | - | - | - | - | 1184 | - |
| Port-Channel1185 | L2_green-leaf174_Port-Channel185 | trunk | 113,201,204,206-208 | - | - | - | - | 1185 | - |
| Port-Channel1186 | L2_green-leaf175_Port-Channel186 | trunk | 113,201,204,206-208 | - | - | - | - | 1186 | - |
| Port-Channel1187 | L2_green-leaf176_Port-Channel187 | trunk | 113,201,204,206-208 | - | - | - | - | 1187 | - |
| Port-Channel1188 | L2_green-leaf177_Port-Channel188 | trunk | 113,201,204,206-208 | - | - | - | - | 1188 | - |
| Port-Channel1189 | L2_green-leaf178_Port-Channel189 | trunk | 113,201,204,206-208 | - | - | - | - | 1189 | - |
| Port-Channel1190 | L2_green-leaf179_Port-Channel190 | trunk | 113,201,204,206-208 | - | - | - | - | 1190 | - |
| Port-Channel1191 | L2_green-leaf180_Port-Channel191 | trunk | 113,201,204,206-208 | - | - | - | - | 1191 | - |
| Port-Channel1192 | L2_green-leaf181_Port-Channel192 | trunk | 113,201,204,206-208 | - | - | - | - | 1192 | - |
| Port-Channel1193 | L2_green-leaf182_Port-Channel193 | trunk | 113,201,204,206-208 | - | - | - | - | 1193 | - |
| Port-Channel1194 | L2_green-leaf183_Port-Channel194 | trunk | 113,201,204,206-208 | - | - | - | - | 1194 | - |

#### Port-Channel Interfaces Device Configuration

```eos
!
interface Port-Channel112
   description L2_green-leaf1_Port-Channel12
   no shutdown
   switchport trunk allowed vlan 113,201-202
   switchport mode trunk
   switchport
   mlag 112
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel113
   description L2_green-leaf2_Port-Channel13
   no shutdown
   switchport trunk allowed vlan 113,202-204
   switchport mode trunk
   switchport
   mlag 113
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel114
   description L2_green-leaf3_Port-Channel14
   no shutdown
   switchport trunk allowed vlan 113,201,203,205,207,209
   switchport mode trunk
   switchport
   mlag 114
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel115
   description L2_green-leaf4_Port-Channel15
   no shutdown
   switchport trunk allowed vlan 113,202,204,206,208
   switchport mode trunk
   switchport
   mlag 115
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel116
   description L2_green-leaf5_Port-Channel16
   no shutdown
   switchport trunk allowed vlan 113
   switchport mode trunk
   switchport
   mlag 116
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel117
   description L2_green-leaf6_Port-Channel17
   no shutdown
   switchport trunk allowed vlan 113,201,203-205,207-209
   switchport mode trunk
   switchport
   mlag 117
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel118
   description L2_green-leaf7_Port-Channel18
   no shutdown
   switchport trunk allowed vlan 113,201-207,209
   switchport mode trunk
   switchport
   mlag 118
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel119
   description L2_green-leaf8_Port-Channel19
   no shutdown
   switchport trunk allowed vlan 113,201-204,206-207,209
   switchport mode trunk
   switchport
   mlag 119
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel120
   description L2_green-leaf9_Port-Channel20
   no shutdown
   switchport trunk allowed vlan 113,201-204,206-207,209
   switchport mode trunk
   switchport
   mlag 120
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel121
   description L2_green-leaf10_Port-Channel21
   no shutdown
   switchport trunk allowed vlan 113,201-204,206-207,209
   switchport mode trunk
   switchport
   mlag 121
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel122
   description L2_green-leaf11_Port-Channel22
   no shutdown
   switchport trunk allowed vlan 113,201-204,206-207,209
   switchport mode trunk
   switchport
   mlag 122
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel123
   description L2_green-leaf12_Port-Channel23
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 123
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel124
   description L2_green-leaf13_Port-Channel24
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 124
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel125
   description L2_green-leaf14_Port-Channel25
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 125
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel126
   description L2_green-leaf15_Port-Channel26
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 126
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel127
   description L2_green-leaf16_Port-Channel27
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 127
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel128
   description L2_green-leaf17_Port-Channel28
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 128
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel129
   description L2_green-leaf18_Port-Channel29
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 129
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel130
   description L2_green-leaf19_Port-Channel30
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 130
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel131
   description L2_green-leaf20_Port-Channel31
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 131
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel132
   description L2_green-leaf21_Port-Channel32
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 132
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel133
   description L2_green-leaf22_Port-Channel33
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 133
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel134
   description L2_green-leaf23_Port-Channel34
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 134
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel135
   description L2_green-leaf24_Port-Channel35
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 135
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel136
   description L2_green-leaf25_Port-Channel36
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 136
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel137
   description L2_green-leaf26_Port-Channel37
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 137
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel138
   description L2_green-leaf27_Port-Channel38
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 138
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel139
   description L2_green-leaf28_Port-Channel39
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 139
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel140
   description L2_green-leaf29_Port-Channel40
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 140
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel141
   description L2_green-leaf30_Port-Channel41
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 141
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel142
   description L2_green-leaf31_Port-Channel42
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,209
   switchport mode trunk
   switchport
   mlag 142
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel143
   description L2_green-leaf32_Port-Channel43
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,208-209
   switchport mode trunk
   switchport
   mlag 143
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel144
   description L2_green-leaf33_Port-Channel44
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,208-209
   switchport mode trunk
   switchport
   mlag 144
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel145
   description L2_green-leaf34_Port-Channel45
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,208-209
   switchport mode trunk
   switchport
   mlag 145
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel146
   description L2_green-leaf35_Port-Channel46
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,208-209
   switchport mode trunk
   switchport
   mlag 146
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel147
   description L2_green-leaf36_Port-Channel47
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,208-209
   switchport mode trunk
   switchport
   mlag 147
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel148
   description L2_green-leaf37_Port-Channel48
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,208-209
   switchport mode trunk
   switchport
   mlag 148
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel149
   description L2_green-leaf38_Port-Channel49
   no shutdown
   switchport trunk allowed vlan 113,201-204,206,208
   switchport mode trunk
   switchport
   mlag 149
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel150
   description L2_green-leaf39_Port-Channel50
   no shutdown
   switchport trunk allowed vlan 113,201-204,208
   switchport mode trunk
   switchport
   mlag 150
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel151
   description L2_green-leaf40_Port-Channel51
   no shutdown
   switchport trunk allowed vlan 113,201-204,208
   switchport mode trunk
   switchport
   mlag 151
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel152
   description L2_green-leaf41_Port-Channel52
   no shutdown
   switchport trunk allowed vlan 113,201-204,208
   switchport mode trunk
   switchport
   mlag 152
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel153
   description L2_green-leaf42_Port-Channel53
   no shutdown
   switchport trunk allowed vlan 113,201-204,208
   switchport mode trunk
   switchport
   mlag 153
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel154
   description L2_green-leaf43_Port-Channel54
   no shutdown
   switchport trunk allowed vlan 113,201-204,208
   switchport mode trunk
   switchport
   mlag 154
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel155
   description L2_green-leaf44_Port-Channel55
   no shutdown
   switchport trunk allowed vlan 113,201-204,208
   switchport mode trunk
   switchport
   mlag 155
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel156
   description L2_green-leaf45_Port-Channel56
   no shutdown
   switchport trunk allowed vlan 113,201-204,208
   switchport mode trunk
   switchport
   mlag 156
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel157
   description L2_green-leaf46_Port-Channel57
   no shutdown
   switchport trunk allowed vlan 113,201-204,208
   switchport mode trunk
   switchport
   mlag 157
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel158
   description L2_green-leaf47_Port-Channel58
   no shutdown
   switchport trunk allowed vlan 113,201-204,208
   switchport mode trunk
   switchport
   mlag 158
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel159
   description L2_green-leaf48_Port-Channel59
   no shutdown
   switchport trunk allowed vlan 113,201-204,207-208
   switchport mode trunk
   switchport
   mlag 159
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel160
   description L2_green-leaf49_Port-Channel60
   no shutdown
   switchport trunk allowed vlan 113,201-204,207-208
   switchport mode trunk
   switchport
   mlag 160
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel161
   description L2_green-leaf50_Port-Channel61
   no shutdown
   switchport trunk allowed vlan 113,201-204,207-208
   switchport mode trunk
   switchport
   mlag 161
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel162
   description L2_green-leaf51_Port-Channel62
   no shutdown
   switchport trunk allowed vlan 113,201-204,207-208
   switchport mode trunk
   switchport
   mlag 162
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel163
   description L2_green-leaf52_Port-Channel63
   no shutdown
   switchport trunk allowed vlan 113,201-204,207-208
   switchport mode trunk
   switchport
   mlag 163
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel164
   description L2_green-leaf53_Port-Channel64
   no shutdown
   switchport trunk allowed vlan 113,201-204,207-208
   switchport mode trunk
   switchport
   mlag 164
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel165
   description L2_green-leaf54_Port-Channel65
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 165
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel166
   description L2_green-leaf55_Port-Channel66
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 166
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel167
   description L2_green-leaf56_Port-Channel67
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 167
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel168
   description L2_green-leaf57_Port-Channel68
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 168
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel169
   description L2_green-leaf58_Port-Channel69
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 169
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel170
   description L2_green-leaf59_Port-Channel70
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 170
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel171
   description L2_green-leaf60_Port-Channel71
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 171
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel172
   description L2_green-leaf61_Port-Channel72
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 172
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel173
   description L2_green-leaf62_Port-Channel73
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 173
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel174
   description L2_green-leaf63_Port-Channel74
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 174
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel175
   description L2_green-leaf64_Port-Channel75
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 175
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel176
   description L2_green-leaf65_Port-Channel76
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 176
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel177
   description L2_green-leaf66_Port-Channel77
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 177
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel178
   description L2_green-leaf67_Port-Channel78
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 178
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel179
   description L2_green-leaf68_Port-Channel79
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 179
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel180
   description L2_green-leaf69_Port-Channel80
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-208
   switchport mode trunk
   switchport
   mlag 180
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel181
   description L2_green-leaf70_Port-Channel81
   no shutdown
   switchport trunk allowed vlan 113,203-205,207-208
   switchport mode trunk
   switchport
   mlag 181
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel182
   description L2_green-leaf71_Port-Channel82
   no shutdown
   switchport trunk allowed vlan 113,203-205,207-208
   switchport mode trunk
   switchport
   mlag 182
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel183
   description L2_green-leaf72_Port-Channel83
   no shutdown
   switchport trunk allowed vlan 113,203-205,207-208
   switchport mode trunk
   switchport
   mlag 183
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel184
   description L2_green-leaf73_Port-Channel84
   no shutdown
   switchport trunk allowed vlan 113,203-205,207-208
   switchport mode trunk
   switchport
   mlag 184
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel185
   description L2_green-leaf74_Port-Channel85
   no shutdown
   switchport trunk allowed vlan 113,203-205,207-208
   switchport mode trunk
   switchport
   mlag 185
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel186
   description L2_green-leaf75_Port-Channel86
   no shutdown
   switchport trunk allowed vlan 113,203-205,207-208
   switchport mode trunk
   switchport
   mlag 186
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel187
   description L2_green-leaf76_Port-Channel87
   no shutdown
   switchport trunk allowed vlan 113,203-205,207-209
   switchport mode trunk
   switchport
   mlag 187
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel188
   description L2_green-leaf77_Port-Channel88
   no shutdown
   switchport trunk allowed vlan 113,203-205,207-209
   switchport mode trunk
   switchport
   mlag 188
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel189
   description L2_green-leaf78_Port-Channel89
   no shutdown
   switchport trunk allowed vlan 113,203-205,207-209
   switchport mode trunk
   switchport
   mlag 189
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel190
   description L2_green-leaf79_Port-Channel90
   no shutdown
   switchport trunk allowed vlan 113,203-205,207-209
   switchport mode trunk
   switchport
   mlag 190
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel191
   description L2_green-leaf80_Port-Channel91
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-209
   switchport mode trunk
   switchport
   mlag 191
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel192
   description L2_green-leaf81_Port-Channel92
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-209
   switchport mode trunk
   switchport
   mlag 192
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel193
   description L2_green-leaf82_Port-Channel93
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-209
   switchport mode trunk
   switchport
   mlag 193
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel194
   description L2_green-leaf83_Port-Channel94
   no shutdown
   switchport trunk allowed vlan 113,203-204,207-209
   switchport mode trunk
   switchport
   mlag 194
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel195
   description L2_green-leaf84_Port-Channel95
   no shutdown
   switchport trunk allowed vlan 113,207-209
   switchport mode trunk
   switchport
   mlag 195
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel196
   description L2_green-leaf85_Port-Channel96
   no shutdown
   switchport trunk allowed vlan 113,207,209
   switchport mode trunk
   switchport
   mlag 196
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel197
   description L2_green-leaf86_Port-Channel97
   no shutdown
   switchport trunk allowed vlan 113,207,209
   switchport mode trunk
   switchport
   mlag 197
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel198
   description L2_green-leaf87_Port-Channel98
   no shutdown
   switchport trunk allowed vlan 113,207,209
   switchport mode trunk
   switchport
   mlag 198
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel199
   description L2_green-leaf88_Port-Channel99
   no shutdown
   switchport trunk allowed vlan 113,207,209
   switchport mode trunk
   switchport
   mlag 199
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1000
   description MLAG_green-spine2_Port-Channel1000
   no shutdown
   switchport mode trunk
   switchport trunk group MLAG
   switchport
!
interface Port-Channel1100
   description L2_green-leaf89_Port-Channel100
   no shutdown
   switchport trunk allowed vlan 113,207,209
   switchport mode trunk
   switchport
   mlag 1100
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1101
   description L2_green-leaf90_Port-Channel101
   no shutdown
   switchport trunk allowed vlan 113,207,209
   switchport mode trunk
   switchport
   mlag 1101
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1102
   description L2_green-leaf91_Port-Channel102
   no shutdown
   switchport trunk allowed vlan 113,207,209
   switchport mode trunk
   switchport
   mlag 1102
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1103
   description L2_green-leaf92_Port-Channel103
   no shutdown
   switchport trunk allowed vlan 113,207,209
   switchport mode trunk
   switchport
   mlag 1103
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1104
   description L2_green-leaf93_Port-Channel104
   no shutdown
   switchport trunk allowed vlan 113,207,209
   switchport mode trunk
   switchport
   mlag 1104
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1105
   description L2_green-leaf94_Port-Channel105
   no shutdown
   switchport trunk allowed vlan 113,207,209
   switchport mode trunk
   switchport
   mlag 1105
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1106
   description L2_green-leaf95_Port-Channel106
   no shutdown
   switchport trunk allowed vlan 113,207,209
   switchport mode trunk
   switchport
   mlag 1106
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1107
   description L2_green-leaf96_Port-Channel107
   no shutdown
   switchport trunk allowed vlan 113,205,207,209
   switchport mode trunk
   switchport
   mlag 1107
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1108
   description L2_green-leaf97_Port-Channel108
   no shutdown
   switchport trunk allowed vlan 113,205,207,209
   switchport mode trunk
   switchport
   mlag 1108
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1109
   description L2_green-leaf98_Port-Channel109
   no shutdown
   switchport trunk allowed vlan 113,205,207,209
   switchport mode trunk
   switchport
   mlag 1109
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1110
   description L2_green-leaf99_Port-Channel110
   no shutdown
   switchport trunk allowed vlan 113,205,207,209
   switchport mode trunk
   switchport
   mlag 1110
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1111
   description L2_green-leaf100_Port-Channel111
   no shutdown
   switchport trunk allowed vlan 113,205,207,209
   switchport mode trunk
   switchport
   mlag 1111
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1112
   description L2_green-leaf101_Port-Channel112
   no shutdown
   switchport trunk allowed vlan 113,205,207,209
   switchport mode trunk
   switchport
   mlag 1112
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1113
   description L2_green-leaf102_Port-Channel113
   no shutdown
   switchport trunk allowed vlan 113,205,207,209
   switchport mode trunk
   switchport
   mlag 1113
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1114
   description L2_green-leaf103_Port-Channel114
   no shutdown
   switchport trunk allowed vlan 113,205,207,209
   switchport mode trunk
   switchport
   mlag 1114
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1115
   description L2_green-leaf104_Port-Channel115
   no shutdown
   switchport trunk allowed vlan 113,205,207,209
   switchport mode trunk
   switchport
   mlag 1115
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1116
   description L2_green-leaf105_Port-Channel116
   no shutdown
   switchport trunk allowed vlan 113,205,207,209
   switchport mode trunk
   switchport
   mlag 1116
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1117
   description L2_green-leaf106_Port-Channel117
   no shutdown
   switchport trunk allowed vlan 113,205,207,209
   switchport mode trunk
   switchport
   mlag 1117
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1118
   description L2_green-leaf107_Port-Channel118
   no shutdown
   switchport trunk allowed vlan 113,205,207
   switchport mode trunk
   switchport
   mlag 1118
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1119
   description L2_green-leaf108_Port-Channel119
   no shutdown
   switchport trunk allowed vlan 113,205,207
   switchport mode trunk
   switchport
   mlag 1119
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1120
   description L2_green-leaf109_Port-Channel120
   no shutdown
   switchport trunk allowed vlan 113,205,207
   switchport mode trunk
   switchport
   mlag 1120
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1121
   description L2_green-leaf110_Port-Channel121
   no shutdown
   switchport trunk allowed vlan 113,205,207
   switchport mode trunk
   switchport
   mlag 1121
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1122
   description L2_green-leaf111_Port-Channel122
   no shutdown
   switchport trunk allowed vlan 113,205,207
   switchport mode trunk
   switchport
   mlag 1122
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1123
   description L2_green-leaf112_Port-Channel123
   no shutdown
   switchport trunk allowed vlan 113,205,207
   switchport mode trunk
   switchport
   mlag 1123
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1124
   description L2_green-leaf113_Port-Channel124
   no shutdown
   switchport trunk allowed vlan 113,203-205,207
   switchport mode trunk
   switchport
   mlag 1124
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1125
   description L2_green-leaf114_Port-Channel125
   no shutdown
   switchport trunk allowed vlan 113,203-205,207
   switchport mode trunk
   switchport
   mlag 1125
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1126
   description L2_green-leaf115_Port-Channel126
   no shutdown
   switchport trunk allowed vlan 113,203-205,207
   switchport mode trunk
   switchport
   mlag 1126
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1127
   description L2_green-leaf116_Port-Channel127
   no shutdown
   switchport trunk allowed vlan 113,201-205,207
   switchport mode trunk
   switchport
   mlag 1127
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1128
   description L2_green-leaf117_Port-Channel128
   no shutdown
   switchport trunk allowed vlan 113,201-205,207
   switchport mode trunk
   switchport
   mlag 1128
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1129
   description L2_green-leaf118_Port-Channel129
   no shutdown
   switchport trunk allowed vlan 113,201-205,207
   switchport mode trunk
   switchport
   mlag 1129
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1130
   description L2_green-leaf119_Port-Channel130
   no shutdown
   switchport trunk allowed vlan 113,201-205,207
   switchport mode trunk
   switchport
   mlag 1130
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1131
   description L2_green-leaf120_Port-Channel131
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207
   switchport mode trunk
   switchport
   mlag 1131
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1132
   description L2_green-leaf121_Port-Channel132
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207
   switchport mode trunk
   switchport
   mlag 1132
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1133
   description L2_green-leaf122_Port-Channel133
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207
   switchport mode trunk
   switchport
   mlag 1133
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1134
   description L2_green-leaf123_Port-Channel134
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207
   switchport mode trunk
   switchport
   mlag 1134
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1135
   description L2_green-leaf124_Port-Channel135
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1135
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1136
   description L2_green-leaf125_Port-Channel136
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1136
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1137
   description L2_green-leaf126_Port-Channel137
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1137
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1138
   description L2_green-leaf127_Port-Channel138
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1138
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1139
   description L2_green-leaf128_Port-Channel139
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1139
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1140
   description L2_green-leaf129_Port-Channel140
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1140
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1141
   description L2_green-leaf130_Port-Channel141
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1141
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1142
   description L2_green-leaf131_Port-Channel142
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1142
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1143
   description L2_green-leaf132_Port-Channel143
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1143
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1144
   description L2_green-leaf133_Port-Channel144
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1144
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1145
   description L2_green-leaf134_Port-Channel145
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1145
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1146
   description L2_green-leaf135_Port-Channel146
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1146
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1147
   description L2_green-leaf136_Port-Channel147
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1147
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1148
   description L2_green-leaf137_Port-Channel148
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1148
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1149
   description L2_green-leaf138_Port-Channel149
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1149
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1150
   description L2_green-leaf139_Port-Channel150
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1150
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1151
   description L2_green-leaf140_Port-Channel151
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1151
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1152
   description L2_green-leaf141_Port-Channel152
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1152
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1153
   description L2_green-leaf142_Port-Channel153
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1153
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1154
   description L2_green-leaf143_Port-Channel154
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1154
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1155
   description L2_green-leaf144_Port-Channel155
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1155
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1156
   description L2_green-leaf145_Port-Channel156
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1156
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1157
   description L2_green-leaf146_Port-Channel157
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1157
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1158
   description L2_green-leaf147_Port-Channel158
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1158
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1159
   description L2_green-leaf148_Port-Channel159
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1159
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1160
   description L2_green-leaf149_Port-Channel160
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1160
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1161
   description L2_green-leaf150_Port-Channel161
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1161
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1162
   description L2_green-leaf151_Port-Channel162
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1162
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1163
   description L2_green-leaf152_Port-Channel163
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1163
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1164
   description L2_green-leaf153_Port-Channel164
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1164
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1165
   description L2_green-leaf154_Port-Channel165
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1165
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1166
   description L2_green-leaf155_Port-Channel166
   no shutdown
   switchport trunk allowed vlan 113,201,204-205,207-208
   switchport mode trunk
   switchport
   mlag 1166
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1167
   description L2_green-leaf156_Port-Channel167
   no shutdown
   switchport trunk allowed vlan 113,201,204,207-208
   switchport mode trunk
   switchport
   mlag 1167
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1168
   description L2_green-leaf157_Port-Channel168
   no shutdown
   switchport trunk allowed vlan 113,201,204,207-208
   switchport mode trunk
   switchport
   mlag 1168
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1169
   description L2_green-leaf158_Port-Channel169
   no shutdown
   switchport trunk allowed vlan 113,201,204,207-208
   switchport mode trunk
   switchport
   mlag 1169
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1170
   description L2_green-leaf159_Port-Channel170
   no shutdown
   switchport trunk allowed vlan 113,201,204,207-208
   switchport mode trunk
   switchport
   mlag 1170
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1171
   description L2_green-leaf160_Port-Channel171
   no shutdown
   switchport trunk allowed vlan 113,201,204,207-208
   switchport mode trunk
   switchport
   mlag 1171
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1172
   description L2_green-leaf161_Port-Channel172
   no shutdown
   switchport trunk allowed vlan 113,201,204,207-208
   switchport mode trunk
   switchport
   mlag 1172
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1173
   description L2_green-leaf162_Port-Channel173
   no shutdown
   switchport trunk allowed vlan 113,201,204,207-208
   switchport mode trunk
   switchport
   mlag 1173
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1174
   description L2_green-leaf163_Port-Channel174
   no shutdown
   switchport trunk allowed vlan 113,201,204,207-208
   switchport mode trunk
   switchport
   mlag 1174
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1175
   description L2_green-leaf164_Port-Channel175
   no shutdown
   switchport trunk allowed vlan 113,201,204,207-208
   switchport mode trunk
   switchport
   mlag 1175
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1176
   description L2_green-leaf165_Port-Channel176
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1176
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1177
   description L2_green-leaf166_Port-Channel177
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1177
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1178
   description L2_green-leaf167_Port-Channel178
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1178
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1179
   description L2_green-leaf168_Port-Channel179
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1179
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1180
   description L2_green-leaf169_Port-Channel180
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1180
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1181
   description L2_green-leaf170_Port-Channel181
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1181
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1182
   description L2_green-leaf171_Port-Channel182
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1182
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1183
   description L2_green-leaf172_Port-Channel183
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1183
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1184
   description L2_green-leaf173_Port-Channel184
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1184
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1185
   description L2_green-leaf174_Port-Channel185
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1185
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1186
   description L2_green-leaf175_Port-Channel186
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1186
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1187
   description L2_green-leaf176_Port-Channel187
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1187
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1188
   description L2_green-leaf177_Port-Channel188
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1188
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1189
   description L2_green-leaf178_Port-Channel189
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1189
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1190
   description L2_green-leaf179_Port-Channel190
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1190
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1191
   description L2_green-leaf180_Port-Channel191
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1191
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1192
   description L2_green-leaf181_Port-Channel192
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1192
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1193
   description L2_green-leaf182_Port-Channel193
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1193
   ptp enable
   ptp announce interval 0
   ptp announce timeout 3
   ptp delay-req interval -3
   ptp sync-message interval -3
   ptp transport ipv4
!
interface Port-Channel1194
   description L2_green-leaf183_Port-Channel194
   no shutdown
   switchport trunk allowed vlan 113,201,204,206-208
   switchport mode trunk
   switchport
   mlag 1194
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

### VLAN Interfaces

#### VLAN Interfaces Summary

| Interface | Description | VRF |  MTU | Shutdown |
| --------- | ----------- | --- | ---- | -------- |
| Vlan113 | Inband Management | default | 1500 | False |
| Vlan201 | VLAN_201 | default | - | False |
| Vlan202 | VLAN_202 | default | - | False |
| Vlan203 | VLAN_203 | default | - | False |
| Vlan204 | VLAN_204 | default | - | False |
| Vlan205 | VLAN_205 | default | - | False |
| Vlan206 | VLAN_206 | default | - | False |
| Vlan207 | VLAN_207 | default | - | False |
| Vlan208 | VLAN_208 | default | - | False |
| Vlan209 | VLAN_209 | default | - | False |
| Vlan210 | VLAN_210 | default | - | False |
| Vlan211 | VLAN_211 | default | - | False |
| Vlan212 | VLAN_212 | default | - | False |
| Vlan213 | VLAN_213 | default | - | False |
| Vlan214 | VLAN_214 | default | - | False |
| Vlan215 | VLAN_215 | default | - | False |
| Vlan216 | VLAN_216 | default | - | False |
| Vlan217 | VLAN_217 | default | - | False |
| Vlan218 | VLAN_218 | default | - | False |
| Vlan219 | VLAN_219 | default | - | False |
| Vlan220 | VLAN_220 | default | - | False |
| Vlan221 | VLAN_221 | default | - | False |
| Vlan222 | VLAN_222 | default | - | False |
| Vlan223 | VLAN_223 | default | - | False |
| Vlan224 | VLAN_224 | default | - | False |
| Vlan225 | VLAN_225 | default | - | False |
| Vlan226 | VLAN_226 | default | - | False |
| Vlan227 | VLAN_227 | default | - | False |
| Vlan228 | VLAN_228 | default | - | False |
| Vlan229 | VLAN_229 | default | - | False |
| Vlan230 | VLAN_230 | default | - | False |
| Vlan231 | VLAN_231 | default | - | False |
| Vlan232 | VLAN_232 | default | - | False |
| Vlan233 | VLAN_233 | default | - | False |
| Vlan234 | VLAN_234 | default | - | False |
| Vlan235 | VLAN_235 | default | - | False |
| Vlan236 | VLAN_236 | default | - | False |
| Vlan237 | VLAN_237 | default | - | False |
| Vlan238 | VLAN_238 | default | - | False |
| Vlan239 | VLAN_239 | default | - | False |
| Vlan240 | VLAN_240 | default | - | False |
| Vlan241 | VLAN_241 | default | - | False |
| Vlan242 | VLAN_242 | default | - | False |
| Vlan243 | VLAN_243 | default | - | False |
| Vlan244 | VLAN_244 | default | - | False |
| Vlan245 | VLAN_245 | default | - | False |
| Vlan246 | VLAN_246 | default | - | False |
| Vlan247 | VLAN_247 | default | - | False |
| Vlan248 | VLAN_248 | default | - | False |
| Vlan249 | VLAN_249 | default | - | False |
| Vlan250 | VLAN_250 | default | - | False |
| Vlan251 | VLAN_251 | default | - | False |
| Vlan252 | VLAN_252 | default | - | False |
| Vlan253 | VLAN_253 | default | - | False |
| Vlan254 | VLAN_254 | default | - | False |
| Vlan255 | VLAN_255 | default | - | False |
| Vlan256 | VLAN_256 | default | - | False |
| Vlan257 | VLAN_257 | default | - | False |
| Vlan258 | VLAN_258 | default | - | False |
| Vlan259 | VLAN_259 | default | - | False |
| Vlan260 | VLAN_260 | default | - | False |
| Vlan261 | VLAN_261 | default | - | False |
| Vlan262 | VLAN_262 | default | - | False |
| Vlan263 | VLAN_263 | default | - | False |
| Vlan264 | VLAN_264 | default | - | False |
| Vlan265 | VLAN_265 | default | - | False |
| Vlan266 | VLAN_266 | default | - | False |
| Vlan267 | VLAN_267 | default | - | False |
| Vlan268 | VLAN_268 | default | - | False |
| Vlan269 | VLAN_269 | default | - | False |
| Vlan270 | VLAN_270 | default | - | False |
| Vlan271 | VLAN_271 | default | - | False |
| Vlan272 | VLAN_272 | default | - | False |
| Vlan273 | VLAN_273 | default | - | False |
| Vlan274 | VLAN_274 | default | - | False |
| Vlan275 | VLAN_275 | default | - | False |
| Vlan276 | VLAN_276 | default | - | False |
| Vlan277 | VLAN_277 | default | - | False |
| Vlan278 | VLAN_278 | default | - | False |
| Vlan279 | VLAN_279 | default | - | False |
| Vlan280 | VLAN_280 | default | - | False |
| Vlan4093 | MLAG_L3 | default | 9214 | False |
| Vlan4094 | MLAG | default | 9214 | False |

##### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ------ | ------- |
| Vlan113 |  default  |  10.239.1.2/24  |  -  |  10.239.113.1/24, 10.239.1.1  |  -  |  -  |
| Vlan201 |  default  |  10.239.1.2/24  |  -  |  10.239.1.1/24  |  -  |  -  |
| Vlan202 |  default  |  10.239.2.2/24  |  -  |  10.239.2.1/24  |  -  |  -  |
| Vlan203 |  default  |  10.239.3.2/24  |  -  |  10.239.3.1/24  |  -  |  -  |
| Vlan204 |  default  |  10.239.4.2/24  |  -  |  10.239.4.1/24  |  -  |  -  |
| Vlan205 |  default  |  10.239.5.2/24  |  -  |  10.239.5.1/24  |  -  |  -  |
| Vlan206 |  default  |  10.239.6.2/24  |  -  |  10.239.6.1/24  |  -  |  -  |
| Vlan207 |  default  |  10.239.7.2/24  |  -  |  10.239.7.1/24  |  -  |  -  |
| Vlan208 |  default  |  10.239.8.2/24  |  -  |  10.239.8.1/24  |  -  |  -  |
| Vlan209 |  default  |  10.239.9.2/24  |  -  |  10.239.9.1/24  |  -  |  -  |
| Vlan210 |  default  |  10.239.10.2/24  |  -  |  10.239.10.1/24  |  -  |  -  |
| Vlan211 |  default  |  10.239.11.2/24  |  -  |  10.239.11.1/24  |  -  |  -  |
| Vlan212 |  default  |  10.239.12.2/24  |  -  |  10.239.12.1/24  |  -  |  -  |
| Vlan213 |  default  |  10.239.13.2/24  |  -  |  10.239.13.1/24  |  -  |  -  |
| Vlan214 |  default  |  10.239.14.2/24  |  -  |  10.239.14.1/24  |  -  |  -  |
| Vlan215 |  default  |  10.239.15.2/24  |  -  |  10.239.15.1/24  |  -  |  -  |
| Vlan216 |  default  |  10.239.16.2/24  |  -  |  10.239.16.1/24  |  -  |  -  |
| Vlan217 |  default  |  10.239.17.2/24  |  -  |  10.239.17.1/24  |  -  |  -  |
| Vlan218 |  default  |  10.239.18.2/24  |  -  |  10.239.18.1/24  |  -  |  -  |
| Vlan219 |  default  |  10.239.19.2/24  |  -  |  10.239.19.1/24  |  -  |  -  |
| Vlan220 |  default  |  10.239.20.2/24  |  -  |  10.239.20.1/24  |  -  |  -  |
| Vlan221 |  default  |  10.239.21.2/24  |  -  |  10.239.21.1/24  |  -  |  -  |
| Vlan222 |  default  |  10.239.22.2/24  |  -  |  10.239.22.1/24  |  -  |  -  |
| Vlan223 |  default  |  10.239.23.2/24  |  -  |  10.239.23.1/24  |  -  |  -  |
| Vlan224 |  default  |  10.239.24.2/24  |  -  |  10.239.24.1/24  |  -  |  -  |
| Vlan225 |  default  |  10.239.25.2/24  |  -  |  10.239.25.1/24  |  -  |  -  |
| Vlan226 |  default  |  10.239.26.2/24  |  -  |  10.239.26.1/24  |  -  |  -  |
| Vlan227 |  default  |  10.239.27.2/24  |  -  |  10.239.27.1/24  |  -  |  -  |
| Vlan228 |  default  |  10.239.28.2/24  |  -  |  10.239.28.1/24  |  -  |  -  |
| Vlan229 |  default  |  10.239.29.2/24  |  -  |  10.239.29.1/24  |  -  |  -  |
| Vlan230 |  default  |  10.239.30.2/24  |  -  |  10.239.30.1/24  |  -  |  -  |
| Vlan231 |  default  |  10.239.31.2/24  |  -  |  10.239.31.1/24  |  -  |  -  |
| Vlan232 |  default  |  10.239.32.2/24  |  -  |  10.239.32.1/24  |  -  |  -  |
| Vlan233 |  default  |  10.239.33.2/24  |  -  |  10.239.33.1/24  |  -  |  -  |
| Vlan234 |  default  |  10.239.34.2/24  |  -  |  10.239.34.1/24  |  -  |  -  |
| Vlan235 |  default  |  10.239.35.2/24  |  -  |  10.239.35.1/24  |  -  |  -  |
| Vlan236 |  default  |  10.239.36.2/24  |  -  |  10.239.36.1/24  |  -  |  -  |
| Vlan237 |  default  |  10.239.37.2/24  |  -  |  10.239.37.1/24  |  -  |  -  |
| Vlan238 |  default  |  10.239.38.2/24  |  -  |  10.239.38.1/24  |  -  |  -  |
| Vlan239 |  default  |  10.239.39.2/24  |  -  |  10.239.39.1/24  |  -  |  -  |
| Vlan240 |  default  |  10.239.40.2/24  |  -  |  10.239.40.1/24  |  -  |  -  |
| Vlan241 |  default  |  10.239.41.2/24  |  -  |  10.239.41.1/24  |  -  |  -  |
| Vlan242 |  default  |  10.239.42.2/24  |  -  |  10.239.42.1/24  |  -  |  -  |
| Vlan243 |  default  |  10.239.43.2/24  |  -  |  10.239.43.1/24  |  -  |  -  |
| Vlan244 |  default  |  10.239.44.2/24  |  -  |  10.239.44.1/24  |  -  |  -  |
| Vlan245 |  default  |  10.239.45.2/24  |  -  |  10.239.45.1/24  |  -  |  -  |
| Vlan246 |  default  |  10.239.46.2/24  |  -  |  10.239.46.1/24  |  -  |  -  |
| Vlan247 |  default  |  10.239.47.2/24  |  -  |  10.239.47.1/24  |  -  |  -  |
| Vlan248 |  default  |  10.239.48.2/24  |  -  |  10.239.48.1/24  |  -  |  -  |
| Vlan249 |  default  |  10.239.49.2/24  |  -  |  10.239.49.1/24  |  -  |  -  |
| Vlan250 |  default  |  10.239.50.2/24  |  -  |  10.239.50.1/24  |  -  |  -  |
| Vlan251 |  default  |  10.239.51.2/24  |  -  |  10.239.51.1/24  |  -  |  -  |
| Vlan252 |  default  |  10.239.52.2/24  |  -  |  10.239.52.1/24  |  -  |  -  |
| Vlan253 |  default  |  10.239.53.2/24  |  -  |  10.239.53.1/24  |  -  |  -  |
| Vlan254 |  default  |  10.239.54.2/24  |  -  |  10.239.54.1/24  |  -  |  -  |
| Vlan255 |  default  |  10.239.55.2/24  |  -  |  10.239.55.1/24  |  -  |  -  |
| Vlan256 |  default  |  10.239.56.2/24  |  -  |  10.239.56.1/24  |  -  |  -  |
| Vlan257 |  default  |  10.239.57.2/24  |  -  |  10.239.57.1/24  |  -  |  -  |
| Vlan258 |  default  |  10.239.58.2/24  |  -  |  10.239.58.1/24  |  -  |  -  |
| Vlan259 |  default  |  10.239.59.2/24  |  -  |  10.239.59.1/24  |  -  |  -  |
| Vlan260 |  default  |  10.239.60.2/24  |  -  |  10.239.60.1/24  |  -  |  -  |
| Vlan261 |  default  |  10.239.61.2/24  |  -  |  10.239.61.1/24  |  -  |  -  |
| Vlan262 |  default  |  10.239.62.2/24  |  -  |  10.239.62.1/24  |  -  |  -  |
| Vlan263 |  default  |  10.239.63.2/24  |  -  |  10.239.63.1/24  |  -  |  -  |
| Vlan264 |  default  |  10.239.64.2/24  |  -  |  10.239.64.1/24  |  -  |  -  |
| Vlan265 |  default  |  10.239.65.2/24  |  -  |  10.239.65.1/24  |  -  |  -  |
| Vlan266 |  default  |  10.239.66.2/24  |  -  |  10.239.66.1/24  |  -  |  -  |
| Vlan267 |  default  |  10.239.67.2/24  |  -  |  10.239.67.1/24  |  -  |  -  |
| Vlan268 |  default  |  10.239.68.2/24  |  -  |  10.239.68.1/24  |  -  |  -  |
| Vlan269 |  default  |  10.239.69.2/24  |  -  |  10.239.69.1/24  |  -  |  -  |
| Vlan270 |  default  |  10.239.70.2/24  |  -  |  10.239.70.1/24  |  -  |  -  |
| Vlan271 |  default  |  10.239.71.2/24  |  -  |  10.239.71.1/24  |  -  |  -  |
| Vlan272 |  default  |  10.239.72.2/24  |  -  |  10.239.72.1/24  |  -  |  -  |
| Vlan273 |  default  |  10.239.73.2/24  |  -  |  10.239.73.1/24  |  -  |  -  |
| Vlan274 |  default  |  10.239.74.2/24  |  -  |  10.239.74.1/24  |  -  |  -  |
| Vlan275 |  default  |  10.239.75.2/24  |  -  |  10.239.75.1/24  |  -  |  -  |
| Vlan276 |  default  |  10.239.76.2/24  |  -  |  10.239.76.1/24  |  -  |  -  |
| Vlan277 |  default  |  10.239.77.2/24  |  -  |  10.239.77.1/24  |  -  |  -  |
| Vlan278 |  default  |  10.239.78.2/24  |  -  |  10.239.78.1/24  |  -  |  -  |
| Vlan279 |  default  |  10.239.79.2/24  |  -  |  10.239.79.1/24  |  -  |  -  |
| Vlan280 |  default  |  10.239.80.2/24  |  -  |  10.239.80.1/24  |  -  |  -  |
| Vlan4093 |  default  |  100.83.88.0/31  |  -  |  -  |  -  |  -  |
| Vlan4094 |  default  |  172.16.0.0/31  |  -  |  -  |  -  |  -  |

#### VLAN Interfaces Device Configuration

```eos
!
interface Vlan113
   description Inband Management
   no shutdown
   mtu 1500
   ip address 10.239.1.2/24
   ip attached-host route export 19
   ip virtual-router address 10.239.1.1
   ip virtual-router address 10.239.113.1/24
!
interface Vlan201
   description VLAN_201
   no shutdown
   ip address 10.239.1.2/24
   ip virtual-router address 10.239.1.1/24
!
interface Vlan202
   description VLAN_202
   no shutdown
   ip address 10.239.2.2/24
   ip virtual-router address 10.239.2.1/24
!
interface Vlan203
   description VLAN_203
   no shutdown
   ip address 10.239.3.2/24
   ip virtual-router address 10.239.3.1/24
!
interface Vlan204
   description VLAN_204
   no shutdown
   ip address 10.239.4.2/24
   ip virtual-router address 10.239.4.1/24
!
interface Vlan205
   description VLAN_205
   no shutdown
   ip address 10.239.5.2/24
   ip virtual-router address 10.239.5.1/24
!
interface Vlan206
   description VLAN_206
   no shutdown
   ip address 10.239.6.2/24
   ip virtual-router address 10.239.6.1/24
!
interface Vlan207
   description VLAN_207
   no shutdown
   ip address 10.239.7.2/24
   ip virtual-router address 10.239.7.1/24
!
interface Vlan208
   description VLAN_208
   no shutdown
   ip address 10.239.8.2/24
   ip virtual-router address 10.239.8.1/24
!
interface Vlan209
   description VLAN_209
   no shutdown
   ip address 10.239.9.2/24
   ip virtual-router address 10.239.9.1/24
!
interface Vlan210
   description VLAN_210
   no shutdown
   ip address 10.239.10.2/24
   ip virtual-router address 10.239.10.1/24
!
interface Vlan211
   description VLAN_211
   no shutdown
   ip address 10.239.11.2/24
   ip virtual-router address 10.239.11.1/24
!
interface Vlan212
   description VLAN_212
   no shutdown
   ip address 10.239.12.2/24
   ip virtual-router address 10.239.12.1/24
!
interface Vlan213
   description VLAN_213
   no shutdown
   ip address 10.239.13.2/24
   ip virtual-router address 10.239.13.1/24
!
interface Vlan214
   description VLAN_214
   no shutdown
   ip address 10.239.14.2/24
   ip virtual-router address 10.239.14.1/24
!
interface Vlan215
   description VLAN_215
   no shutdown
   ip address 10.239.15.2/24
   ip virtual-router address 10.239.15.1/24
!
interface Vlan216
   description VLAN_216
   no shutdown
   ip address 10.239.16.2/24
   ip virtual-router address 10.239.16.1/24
!
interface Vlan217
   description VLAN_217
   no shutdown
   ip address 10.239.17.2/24
   ip virtual-router address 10.239.17.1/24
!
interface Vlan218
   description VLAN_218
   no shutdown
   ip address 10.239.18.2/24
   ip virtual-router address 10.239.18.1/24
!
interface Vlan219
   description VLAN_219
   no shutdown
   ip address 10.239.19.2/24
   ip virtual-router address 10.239.19.1/24
!
interface Vlan220
   description VLAN_220
   no shutdown
   ip address 10.239.20.2/24
   ip virtual-router address 10.239.20.1/24
!
interface Vlan221
   description VLAN_221
   no shutdown
   ip address 10.239.21.2/24
   ip virtual-router address 10.239.21.1/24
!
interface Vlan222
   description VLAN_222
   no shutdown
   ip address 10.239.22.2/24
   ip virtual-router address 10.239.22.1/24
!
interface Vlan223
   description VLAN_223
   no shutdown
   ip address 10.239.23.2/24
   ip virtual-router address 10.239.23.1/24
!
interface Vlan224
   description VLAN_224
   no shutdown
   ip address 10.239.24.2/24
   ip virtual-router address 10.239.24.1/24
!
interface Vlan225
   description VLAN_225
   no shutdown
   ip address 10.239.25.2/24
   ip virtual-router address 10.239.25.1/24
!
interface Vlan226
   description VLAN_226
   no shutdown
   ip address 10.239.26.2/24
   ip virtual-router address 10.239.26.1/24
!
interface Vlan227
   description VLAN_227
   no shutdown
   ip address 10.239.27.2/24
   ip virtual-router address 10.239.27.1/24
!
interface Vlan228
   description VLAN_228
   no shutdown
   ip address 10.239.28.2/24
   ip virtual-router address 10.239.28.1/24
!
interface Vlan229
   description VLAN_229
   no shutdown
   ip address 10.239.29.2/24
   ip virtual-router address 10.239.29.1/24
!
interface Vlan230
   description VLAN_230
   no shutdown
   ip address 10.239.30.2/24
   ip virtual-router address 10.239.30.1/24
!
interface Vlan231
   description VLAN_231
   no shutdown
   ip address 10.239.31.2/24
   ip virtual-router address 10.239.31.1/24
!
interface Vlan232
   description VLAN_232
   no shutdown
   ip address 10.239.32.2/24
   ip virtual-router address 10.239.32.1/24
!
interface Vlan233
   description VLAN_233
   no shutdown
   ip address 10.239.33.2/24
   ip virtual-router address 10.239.33.1/24
!
interface Vlan234
   description VLAN_234
   no shutdown
   ip address 10.239.34.2/24
   ip virtual-router address 10.239.34.1/24
!
interface Vlan235
   description VLAN_235
   no shutdown
   ip address 10.239.35.2/24
   ip virtual-router address 10.239.35.1/24
!
interface Vlan236
   description VLAN_236
   no shutdown
   ip address 10.239.36.2/24
   ip virtual-router address 10.239.36.1/24
!
interface Vlan237
   description VLAN_237
   no shutdown
   ip address 10.239.37.2/24
   ip virtual-router address 10.239.37.1/24
!
interface Vlan238
   description VLAN_238
   no shutdown
   ip address 10.239.38.2/24
   ip virtual-router address 10.239.38.1/24
!
interface Vlan239
   description VLAN_239
   no shutdown
   ip address 10.239.39.2/24
   ip virtual-router address 10.239.39.1/24
!
interface Vlan240
   description VLAN_240
   no shutdown
   ip address 10.239.40.2/24
   ip virtual-router address 10.239.40.1/24
!
interface Vlan241
   description VLAN_241
   no shutdown
   ip address 10.239.41.2/24
   ip virtual-router address 10.239.41.1/24
!
interface Vlan242
   description VLAN_242
   no shutdown
   ip address 10.239.42.2/24
   ip virtual-router address 10.239.42.1/24
!
interface Vlan243
   description VLAN_243
   no shutdown
   ip address 10.239.43.2/24
   ip virtual-router address 10.239.43.1/24
!
interface Vlan244
   description VLAN_244
   no shutdown
   ip address 10.239.44.2/24
   ip virtual-router address 10.239.44.1/24
!
interface Vlan245
   description VLAN_245
   no shutdown
   ip address 10.239.45.2/24
   ip virtual-router address 10.239.45.1/24
!
interface Vlan246
   description VLAN_246
   no shutdown
   ip address 10.239.46.2/24
   ip virtual-router address 10.239.46.1/24
!
interface Vlan247
   description VLAN_247
   no shutdown
   ip address 10.239.47.2/24
   ip virtual-router address 10.239.47.1/24
!
interface Vlan248
   description VLAN_248
   no shutdown
   ip address 10.239.48.2/24
   ip virtual-router address 10.239.48.1/24
!
interface Vlan249
   description VLAN_249
   no shutdown
   ip address 10.239.49.2/24
   ip virtual-router address 10.239.49.1/24
!
interface Vlan250
   description VLAN_250
   no shutdown
   ip address 10.239.50.2/24
   ip virtual-router address 10.239.50.1/24
!
interface Vlan251
   description VLAN_251
   no shutdown
   ip address 10.239.51.2/24
   ip virtual-router address 10.239.51.1/24
!
interface Vlan252
   description VLAN_252
   no shutdown
   ip address 10.239.52.2/24
   ip virtual-router address 10.239.52.1/24
!
interface Vlan253
   description VLAN_253
   no shutdown
   ip address 10.239.53.2/24
   ip virtual-router address 10.239.53.1/24
!
interface Vlan254
   description VLAN_254
   no shutdown
   ip address 10.239.54.2/24
   ip virtual-router address 10.239.54.1/24
!
interface Vlan255
   description VLAN_255
   no shutdown
   ip address 10.239.55.2/24
   ip virtual-router address 10.239.55.1/24
!
interface Vlan256
   description VLAN_256
   no shutdown
   ip address 10.239.56.2/24
   ip virtual-router address 10.239.56.1/24
!
interface Vlan257
   description VLAN_257
   no shutdown
   ip address 10.239.57.2/24
   ip virtual-router address 10.239.57.1/24
!
interface Vlan258
   description VLAN_258
   no shutdown
   ip address 10.239.58.2/24
   ip virtual-router address 10.239.58.1/24
!
interface Vlan259
   description VLAN_259
   no shutdown
   ip address 10.239.59.2/24
   ip virtual-router address 10.239.59.1/24
!
interface Vlan260
   description VLAN_260
   no shutdown
   ip address 10.239.60.2/24
   ip virtual-router address 10.239.60.1/24
!
interface Vlan261
   description VLAN_261
   no shutdown
   ip address 10.239.61.2/24
   ip virtual-router address 10.239.61.1/24
!
interface Vlan262
   description VLAN_262
   no shutdown
   ip address 10.239.62.2/24
   ip virtual-router address 10.239.62.1/24
!
interface Vlan263
   description VLAN_263
   no shutdown
   ip address 10.239.63.2/24
   ip virtual-router address 10.239.63.1/24
!
interface Vlan264
   description VLAN_264
   no shutdown
   ip address 10.239.64.2/24
   ip virtual-router address 10.239.64.1/24
!
interface Vlan265
   description VLAN_265
   no shutdown
   ip address 10.239.65.2/24
   ip virtual-router address 10.239.65.1/24
!
interface Vlan266
   description VLAN_266
   no shutdown
   ip address 10.239.66.2/24
   ip virtual-router address 10.239.66.1/24
!
interface Vlan267
   description VLAN_267
   no shutdown
   ip address 10.239.67.2/24
   ip virtual-router address 10.239.67.1/24
!
interface Vlan268
   description VLAN_268
   no shutdown
   ip address 10.239.68.2/24
   ip virtual-router address 10.239.68.1/24
!
interface Vlan269
   description VLAN_269
   no shutdown
   ip address 10.239.69.2/24
   ip virtual-router address 10.239.69.1/24
!
interface Vlan270
   description VLAN_270
   no shutdown
   ip address 10.239.70.2/24
   ip virtual-router address 10.239.70.1/24
!
interface Vlan271
   description VLAN_271
   no shutdown
   ip address 10.239.71.2/24
   ip virtual-router address 10.239.71.1/24
!
interface Vlan272
   description VLAN_272
   no shutdown
   ip address 10.239.72.2/24
   ip virtual-router address 10.239.72.1/24
!
interface Vlan273
   description VLAN_273
   no shutdown
   ip address 10.239.73.2/24
   ip virtual-router address 10.239.73.1/24
!
interface Vlan274
   description VLAN_274
   no shutdown
   ip address 10.239.74.2/24
   ip virtual-router address 10.239.74.1/24
!
interface Vlan275
   description VLAN_275
   no shutdown
   ip address 10.239.75.2/24
   ip virtual-router address 10.239.75.1/24
!
interface Vlan276
   description VLAN_276
   no shutdown
   ip address 10.239.76.2/24
   ip virtual-router address 10.239.76.1/24
!
interface Vlan277
   description VLAN_277
   no shutdown
   ip address 10.239.77.2/24
   ip virtual-router address 10.239.77.1/24
!
interface Vlan278
   description VLAN_278
   no shutdown
   ip address 10.239.78.2/24
   ip virtual-router address 10.239.78.1/24
!
interface Vlan279
   description VLAN_279
   no shutdown
   ip address 10.239.79.2/24
   ip virtual-router address 10.239.79.1/24
!
interface Vlan280
   description VLAN_280
   no shutdown
   ip address 10.239.80.2/24
   ip virtual-router address 10.239.80.1/24
!
interface Vlan4093
   description MLAG_L3
   no shutdown
   mtu 9214
   ip address 100.83.88.0/31
!
interface Vlan4094
   description MLAG
   no shutdown
   mtu 9214
   no autostate
   ip address 172.16.0.0/31
```

## Routing

### Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

### Virtual Router MAC Address

#### Virtual Router MAC Address Summary

Virtual Router MAC Address: 00:1c:73:00:dc:01

#### Virtual Router MAC Address Device Configuration

```eos
!
ip virtual-router mac-address 00:1c:73:00:dc:01
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
| MGMT | 0.0.0.0/0 | 172.16.100.1 | - | 1 | - | - | - |
| default | 10.239.113.0/24 | - | Vlan113 | 1 | - | VARP | - |
| default | 10.239.1.0/24 | - | Vlan201 | 1 | - | VARP | - |
| default | 10.239.2.0/24 | - | Vlan202 | 1 | - | VARP | - |
| default | 10.239.3.0/24 | - | Vlan203 | 1 | - | VARP | - |
| default | 10.239.4.0/24 | - | Vlan204 | 1 | - | VARP | - |
| default | 10.239.5.0/24 | - | Vlan205 | 1 | - | VARP | - |
| default | 10.239.6.0/24 | - | Vlan206 | 1 | - | VARP | - |
| default | 10.239.7.0/24 | - | Vlan207 | 1 | - | VARP | - |
| default | 10.239.8.0/24 | - | Vlan208 | 1 | - | VARP | - |
| default | 10.239.9.0/24 | - | Vlan209 | 1 | - | VARP | - |
| default | 10.239.10.0/24 | - | Vlan210 | 1 | - | VARP | - |
| default | 10.239.11.0/24 | - | Vlan211 | 1 | - | VARP | - |
| default | 10.239.12.0/24 | - | Vlan212 | 1 | - | VARP | - |
| default | 10.239.13.0/24 | - | Vlan213 | 1 | - | VARP | - |
| default | 10.239.14.0/24 | - | Vlan214 | 1 | - | VARP | - |
| default | 10.239.15.0/24 | - | Vlan215 | 1 | - | VARP | - |
| default | 10.239.16.0/24 | - | Vlan216 | 1 | - | VARP | - |
| default | 10.239.17.0/24 | - | Vlan217 | 1 | - | VARP | - |
| default | 10.239.18.0/24 | - | Vlan218 | 1 | - | VARP | - |
| default | 10.239.19.0/24 | - | Vlan219 | 1 | - | VARP | - |
| default | 10.239.20.0/24 | - | Vlan220 | 1 | - | VARP | - |
| default | 10.239.21.0/24 | - | Vlan221 | 1 | - | VARP | - |
| default | 10.239.22.0/24 | - | Vlan222 | 1 | - | VARP | - |
| default | 10.239.23.0/24 | - | Vlan223 | 1 | - | VARP | - |
| default | 10.239.24.0/24 | - | Vlan224 | 1 | - | VARP | - |
| default | 10.239.25.0/24 | - | Vlan225 | 1 | - | VARP | - |
| default | 10.239.26.0/24 | - | Vlan226 | 1 | - | VARP | - |
| default | 10.239.27.0/24 | - | Vlan227 | 1 | - | VARP | - |
| default | 10.239.28.0/24 | - | Vlan228 | 1 | - | VARP | - |
| default | 10.239.29.0/24 | - | Vlan229 | 1 | - | VARP | - |
| default | 10.239.30.0/24 | - | Vlan230 | 1 | - | VARP | - |
| default | 10.239.31.0/24 | - | Vlan231 | 1 | - | VARP | - |
| default | 10.239.32.0/24 | - | Vlan232 | 1 | - | VARP | - |
| default | 10.239.33.0/24 | - | Vlan233 | 1 | - | VARP | - |
| default | 10.239.34.0/24 | - | Vlan234 | 1 | - | VARP | - |
| default | 10.239.35.0/24 | - | Vlan235 | 1 | - | VARP | - |
| default | 10.239.36.0/24 | - | Vlan236 | 1 | - | VARP | - |
| default | 10.239.37.0/24 | - | Vlan237 | 1 | - | VARP | - |
| default | 10.239.38.0/24 | - | Vlan238 | 1 | - | VARP | - |
| default | 10.239.39.0/24 | - | Vlan239 | 1 | - | VARP | - |
| default | 10.239.40.0/24 | - | Vlan240 | 1 | - | VARP | - |
| default | 10.239.41.0/24 | - | Vlan241 | 1 | - | VARP | - |
| default | 10.239.42.0/24 | - | Vlan242 | 1 | - | VARP | - |
| default | 10.239.43.0/24 | - | Vlan243 | 1 | - | VARP | - |
| default | 10.239.44.0/24 | - | Vlan244 | 1 | - | VARP | - |
| default | 10.239.45.0/24 | - | Vlan245 | 1 | - | VARP | - |
| default | 10.239.46.0/24 | - | Vlan246 | 1 | - | VARP | - |
| default | 10.239.47.0/24 | - | Vlan247 | 1 | - | VARP | - |
| default | 10.239.48.0/24 | - | Vlan248 | 1 | - | VARP | - |
| default | 10.239.49.0/24 | - | Vlan249 | 1 | - | VARP | - |
| default | 10.239.50.0/24 | - | Vlan250 | 1 | - | VARP | - |
| default | 10.239.51.0/24 | - | Vlan251 | 1 | - | VARP | - |
| default | 10.239.52.0/24 | - | Vlan252 | 1 | - | VARP | - |
| default | 10.239.53.0/24 | - | Vlan253 | 1 | - | VARP | - |
| default | 10.239.54.0/24 | - | Vlan254 | 1 | - | VARP | - |
| default | 10.239.55.0/24 | - | Vlan255 | 1 | - | VARP | - |
| default | 10.239.56.0/24 | - | Vlan256 | 1 | - | VARP | - |
| default | 10.239.57.0/24 | - | Vlan257 | 1 | - | VARP | - |
| default | 10.239.58.0/24 | - | Vlan258 | 1 | - | VARP | - |
| default | 10.239.59.0/24 | - | Vlan259 | 1 | - | VARP | - |
| default | 10.239.60.0/24 | - | Vlan260 | 1 | - | VARP | - |
| default | 10.239.61.0/24 | - | Vlan261 | 1 | - | VARP | - |
| default | 10.239.62.0/24 | - | Vlan262 | 1 | - | VARP | - |
| default | 10.239.63.0/24 | - | Vlan263 | 1 | - | VARP | - |
| default | 10.239.64.0/24 | - | Vlan264 | 1 | - | VARP | - |
| default | 10.239.65.0/24 | - | Vlan265 | 1 | - | VARP | - |
| default | 10.239.66.0/24 | - | Vlan266 | 1 | - | VARP | - |
| default | 10.239.67.0/24 | - | Vlan267 | 1 | - | VARP | - |
| default | 10.239.68.0/24 | - | Vlan268 | 1 | - | VARP | - |
| default | 10.239.69.0/24 | - | Vlan269 | 1 | - | VARP | - |
| default | 10.239.70.0/24 | - | Vlan270 | 1 | - | VARP | - |
| default | 10.239.71.0/24 | - | Vlan271 | 1 | - | VARP | - |
| default | 10.239.72.0/24 | - | Vlan272 | 1 | - | VARP | - |
| default | 10.239.73.0/24 | - | Vlan273 | 1 | - | VARP | - |
| default | 10.239.74.0/24 | - | Vlan274 | 1 | - | VARP | - |
| default | 10.239.75.0/24 | - | Vlan275 | 1 | - | VARP | - |
| default | 10.239.76.0/24 | - | Vlan276 | 1 | - | VARP | - |
| default | 10.239.77.0/24 | - | Vlan277 | 1 | - | VARP | - |
| default | 10.239.78.0/24 | - | Vlan278 | 1 | - | VARP | - |
| default | 10.239.79.0/24 | - | Vlan279 | 1 | - | VARP | - |
| default | 10.239.80.0/24 | - | Vlan280 | 1 | - | VARP | - |

#### Static Routes Device Configuration

```eos
!
ip route 10.239.1.0/24 Vlan201 name VARP
ip route 10.239.2.0/24 Vlan202 name VARP
ip route 10.239.3.0/24 Vlan203 name VARP
ip route 10.239.4.0/24 Vlan204 name VARP
ip route 10.239.5.0/24 Vlan205 name VARP
ip route 10.239.6.0/24 Vlan206 name VARP
ip route 10.239.7.0/24 Vlan207 name VARP
ip route 10.239.8.0/24 Vlan208 name VARP
ip route 10.239.9.0/24 Vlan209 name VARP
ip route 10.239.10.0/24 Vlan210 name VARP
ip route 10.239.11.0/24 Vlan211 name VARP
ip route 10.239.12.0/24 Vlan212 name VARP
ip route 10.239.13.0/24 Vlan213 name VARP
ip route 10.239.14.0/24 Vlan214 name VARP
ip route 10.239.15.0/24 Vlan215 name VARP
ip route 10.239.16.0/24 Vlan216 name VARP
ip route 10.239.17.0/24 Vlan217 name VARP
ip route 10.239.18.0/24 Vlan218 name VARP
ip route 10.239.19.0/24 Vlan219 name VARP
ip route 10.239.20.0/24 Vlan220 name VARP
ip route 10.239.21.0/24 Vlan221 name VARP
ip route 10.239.22.0/24 Vlan222 name VARP
ip route 10.239.23.0/24 Vlan223 name VARP
ip route 10.239.24.0/24 Vlan224 name VARP
ip route 10.239.25.0/24 Vlan225 name VARP
ip route 10.239.26.0/24 Vlan226 name VARP
ip route 10.239.27.0/24 Vlan227 name VARP
ip route 10.239.28.0/24 Vlan228 name VARP
ip route 10.239.29.0/24 Vlan229 name VARP
ip route 10.239.30.0/24 Vlan230 name VARP
ip route 10.239.31.0/24 Vlan231 name VARP
ip route 10.239.32.0/24 Vlan232 name VARP
ip route 10.239.33.0/24 Vlan233 name VARP
ip route 10.239.34.0/24 Vlan234 name VARP
ip route 10.239.35.0/24 Vlan235 name VARP
ip route 10.239.36.0/24 Vlan236 name VARP
ip route 10.239.37.0/24 Vlan237 name VARP
ip route 10.239.38.0/24 Vlan238 name VARP
ip route 10.239.39.0/24 Vlan239 name VARP
ip route 10.239.40.0/24 Vlan240 name VARP
ip route 10.239.41.0/24 Vlan241 name VARP
ip route 10.239.42.0/24 Vlan242 name VARP
ip route 10.239.43.0/24 Vlan243 name VARP
ip route 10.239.44.0/24 Vlan244 name VARP
ip route 10.239.45.0/24 Vlan245 name VARP
ip route 10.239.46.0/24 Vlan246 name VARP
ip route 10.239.47.0/24 Vlan247 name VARP
ip route 10.239.48.0/24 Vlan248 name VARP
ip route 10.239.49.0/24 Vlan249 name VARP
ip route 10.239.50.0/24 Vlan250 name VARP
ip route 10.239.51.0/24 Vlan251 name VARP
ip route 10.239.52.0/24 Vlan252 name VARP
ip route 10.239.53.0/24 Vlan253 name VARP
ip route 10.239.54.0/24 Vlan254 name VARP
ip route 10.239.55.0/24 Vlan255 name VARP
ip route 10.239.56.0/24 Vlan256 name VARP
ip route 10.239.57.0/24 Vlan257 name VARP
ip route 10.239.58.0/24 Vlan258 name VARP
ip route 10.239.59.0/24 Vlan259 name VARP
ip route 10.239.60.0/24 Vlan260 name VARP
ip route 10.239.61.0/24 Vlan261 name VARP
ip route 10.239.62.0/24 Vlan262 name VARP
ip route 10.239.63.0/24 Vlan263 name VARP
ip route 10.239.64.0/24 Vlan264 name VARP
ip route 10.239.65.0/24 Vlan265 name VARP
ip route 10.239.66.0/24 Vlan266 name VARP
ip route 10.239.67.0/24 Vlan267 name VARP
ip route 10.239.68.0/24 Vlan268 name VARP
ip route 10.239.69.0/24 Vlan269 name VARP
ip route 10.239.70.0/24 Vlan270 name VARP
ip route 10.239.71.0/24 Vlan271 name VARP
ip route 10.239.72.0/24 Vlan272 name VARP
ip route 10.239.73.0/24 Vlan273 name VARP
ip route 10.239.74.0/24 Vlan274 name VARP
ip route 10.239.75.0/24 Vlan275 name VARP
ip route 10.239.76.0/24 Vlan276 name VARP
ip route 10.239.77.0/24 Vlan277 name VARP
ip route 10.239.78.0/24 Vlan278 name VARP
ip route 10.239.79.0/24 Vlan279 name VARP
ip route 10.239.80.0/24 Vlan280 name VARP
ip route 10.239.113.0/24 Vlan113 name VARP
ip route vrf MGMT 0.0.0.0/0 172.16.100.1
```

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65003.3 | 169.27.195.1 |

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

##### MLAG-iBGP-PEER

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Remote AS | 65003.3 |
| Next-hop self | True |
| Send community | all |
| Maximum routes | 12000 |

##### P2P-IPv4-eBGP-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Send community | all |
| Maximum routes | 12000 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 100.83.88.1 | Inherited from peer group MLAG-iBGP-PEER | default | - | Inherited from peer group MLAG-iBGP-PEER | Inherited from peer group MLAG-iBGP-PEER | - | - | - | - | - | - |
| 100.83.88.241 | 65003.1 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.245 | 65003.1 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.249 | 65003.2 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |
| 100.83.88.253 | 65003.2 | default | - | Inherited from peer group P2P-IPv4-eBGP-PEERS | Inherited from peer group P2P-IPv4-eBGP-PEERS | - | - | - | - | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65003.3
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
   neighbor MLAG-iBGP-PEER peer group
   neighbor MLAG-iBGP-PEER remote-as 65003.3
   neighbor MLAG-iBGP-PEER next-hop-self
   neighbor MLAG-iBGP-PEER description green-spine2
   neighbor MLAG-iBGP-PEER route-map RM-MLAG-PEER-IN in
   neighbor MLAG-iBGP-PEER password 7 <removed>
   neighbor MLAG-iBGP-PEER send-community
   neighbor MLAG-iBGP-PEER maximum-routes 12000
   neighbor P2P-IPv4-eBGP-PEERS peer group
   neighbor P2P-IPv4-eBGP-PEERS password 7 <removed>
   neighbor P2P-IPv4-eBGP-PEERS send-community
   neighbor P2P-IPv4-eBGP-PEERS maximum-routes 12000
   neighbor 100.83.88.1 peer group MLAG-iBGP-PEER
   neighbor 100.83.88.1 description Testing
   neighbor 100.83.88.241 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.241 remote-as 65003.1
   neighbor 100.83.88.241 description media-PTP-1
   neighbor 100.83.88.245 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.245 remote-as 65003.1
   neighbor 100.83.88.245 description media-PTP-2
   neighbor 100.83.88.249 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.249 remote-as 65003.2
   neighbor 100.83.88.249 description border-leaf1
   neighbor 100.83.88.253 peer group P2P-IPv4-eBGP-PEERS
   neighbor 100.83.88.253 remote-as 65003.2
   neighbor 100.83.88.253 description border-leaf2
   redistribute connected
   redistribute attached-host
   !
   address-family ipv4
      neighbor MLAG-iBGP-PEER activate
      neighbor P2P-IPv4-eBGP-PEERS activate
```

## Multicast

### IP IGMP Snooping

#### IP IGMP Snooping Summary

| IGMP Snooping | Fast Leave | Interface Restart Query | Proxy | Restart Query Interval | Robustness Variable |
| ------------- | ---------- | ----------------------- | ----- | ---------------------- | ------------------- |
| Enabled | - | - | - | - | - |

##### IP IGMP Snooping Vlan Summary

| Vlan | IGMP Snooping | Fast Leave | Max Groups | Proxy |
| ---- | ------------- | ---------- | ---------- | ----- |
| 113 | True | - | - | - |
| 201 | True | - | - | - |
| 202 | True | - | - | - |
| 203 | True | - | - | - |
| 204 | True | - | - | - |
| 205 | True | - | - | - |
| 206 | True | - | - | - |
| 207 | True | - | - | - |
| 208 | True | - | - | - |
| 209 | True | - | - | - |
| 210 | True | - | - | - |
| 211 | True | - | - | - |
| 212 | True | - | - | - |
| 213 | True | - | - | - |
| 214 | True | - | - | - |
| 215 | True | - | - | - |
| 216 | True | - | - | - |
| 217 | True | - | - | - |
| 218 | True | - | - | - |
| 219 | True | - | - | - |
| 220 | True | - | - | - |
| 221 | True | - | - | - |
| 222 | True | - | - | - |
| 223 | True | - | - | - |
| 224 | True | - | - | - |
| 225 | True | - | - | - |
| 226 | True | - | - | - |
| 227 | True | - | - | - |
| 228 | True | - | - | - |
| 229 | True | - | - | - |
| 230 | True | - | - | - |
| 231 | True | - | - | - |
| 232 | True | - | - | - |
| 233 | True | - | - | - |
| 234 | True | - | - | - |
| 235 | True | - | - | - |
| 236 | True | - | - | - |
| 237 | True | - | - | - |
| 238 | True | - | - | - |
| 239 | True | - | - | - |
| 240 | True | - | - | - |
| 241 | True | - | - | - |
| 242 | True | - | - | - |
| 243 | True | - | - | - |
| 244 | True | - | - | - |
| 245 | True | - | - | - |
| 246 | True | - | - | - |
| 247 | True | - | - | - |
| 248 | True | - | - | - |
| 249 | True | - | - | - |
| 250 | True | - | - | - |
| 251 | True | - | - | - |
| 252 | True | - | - | - |
| 253 | True | - | - | - |
| 254 | True | - | - | - |
| 255 | True | - | - | - |
| 256 | True | - | - | - |
| 257 | True | - | - | - |
| 258 | True | - | - | - |
| 259 | True | - | - | - |
| 260 | True | - | - | - |
| 261 | True | - | - | - |
| 262 | True | - | - | - |
| 263 | True | - | - | - |
| 264 | True | - | - | - |
| 265 | True | - | - | - |
| 266 | True | - | - | - |
| 267 | True | - | - | - |
| 268 | True | - | - | - |
| 269 | True | - | - | - |
| 270 | True | - | - | - |
| 271 | True | - | - | - |
| 272 | True | - | - | - |
| 273 | True | - | - | - |
| 274 | True | - | - | - |
| 275 | True | - | - | - |
| 276 | True | - | - | - |
| 277 | True | - | - | - |
| 278 | True | - | - | - |
| 279 | True | - | - | - |
| 280 | True | - | - | - |

| Vlan | Querier Enabled | IP Address | Query Interval | Max Response Time | Last Member Query Interval | Last Member Query Count | Startup Query Interval | Startup Query Count | Version |
| ---- | --------------- | ---------- | -------------- | ----------------- | -------------------------- | ----------------------- | ---------------------- | ------------------- | ------- |
| 113 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 201 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 202 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 203 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 204 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 205 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 206 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 207 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 208 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 209 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 210 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 211 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 212 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 213 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 214 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 215 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 216 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 217 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 218 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 219 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 220 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 221 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 222 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 223 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 224 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 225 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 226 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 227 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 228 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 229 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 230 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 231 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 232 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 233 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 234 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 235 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 236 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 237 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 238 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 239 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 240 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 241 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 242 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 243 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 244 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 245 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 246 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 247 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 248 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 249 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 250 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 251 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 252 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 253 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 254 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 255 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 256 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 257 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 258 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 259 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 260 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 261 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 262 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 263 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 264 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 265 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 266 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 267 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 268 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 269 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 270 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 271 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 272 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 273 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 274 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 275 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 276 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 277 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 278 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 279 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |
| 280 | True | 172.16.16.16 | - | - | - | - | - | - | 3 |

#### IP IGMP Snooping Device Configuration

```eos
!
ip igmp snooping vlan 113
ip igmp snooping vlan 113 querier
ip igmp snooping vlan 113 querier address 172.16.16.16
ip igmp snooping vlan 113 querier version 3
ip igmp snooping vlan 201
ip igmp snooping vlan 201 querier
ip igmp snooping vlan 201 querier address 172.16.16.16
ip igmp snooping vlan 201 querier version 3
ip igmp snooping vlan 202
ip igmp snooping vlan 202 querier
ip igmp snooping vlan 202 querier address 172.16.16.16
ip igmp snooping vlan 202 querier version 3
ip igmp snooping vlan 203
ip igmp snooping vlan 203 querier
ip igmp snooping vlan 203 querier address 172.16.16.16
ip igmp snooping vlan 203 querier version 3
ip igmp snooping vlan 204
ip igmp snooping vlan 204 querier
ip igmp snooping vlan 204 querier address 172.16.16.16
ip igmp snooping vlan 204 querier version 3
ip igmp snooping vlan 205
ip igmp snooping vlan 205 querier
ip igmp snooping vlan 205 querier address 172.16.16.16
ip igmp snooping vlan 205 querier version 3
ip igmp snooping vlan 206
ip igmp snooping vlan 206 querier
ip igmp snooping vlan 206 querier address 172.16.16.16
ip igmp snooping vlan 206 querier version 3
ip igmp snooping vlan 207
ip igmp snooping vlan 207 querier
ip igmp snooping vlan 207 querier address 172.16.16.16
ip igmp snooping vlan 207 querier version 3
ip igmp snooping vlan 208
ip igmp snooping vlan 208 querier
ip igmp snooping vlan 208 querier address 172.16.16.16
ip igmp snooping vlan 208 querier version 3
ip igmp snooping vlan 209
ip igmp snooping vlan 209 querier
ip igmp snooping vlan 209 querier address 172.16.16.16
ip igmp snooping vlan 209 querier version 3
ip igmp snooping vlan 210
ip igmp snooping vlan 210 querier
ip igmp snooping vlan 210 querier address 172.16.16.16
ip igmp snooping vlan 210 querier version 3
ip igmp snooping vlan 211
ip igmp snooping vlan 211 querier
ip igmp snooping vlan 211 querier address 172.16.16.16
ip igmp snooping vlan 211 querier version 3
ip igmp snooping vlan 212
ip igmp snooping vlan 212 querier
ip igmp snooping vlan 212 querier address 172.16.16.16
ip igmp snooping vlan 212 querier version 3
ip igmp snooping vlan 213
ip igmp snooping vlan 213 querier
ip igmp snooping vlan 213 querier address 172.16.16.16
ip igmp snooping vlan 213 querier version 3
ip igmp snooping vlan 214
ip igmp snooping vlan 214 querier
ip igmp snooping vlan 214 querier address 172.16.16.16
ip igmp snooping vlan 214 querier version 3
ip igmp snooping vlan 215
ip igmp snooping vlan 215 querier
ip igmp snooping vlan 215 querier address 172.16.16.16
ip igmp snooping vlan 215 querier version 3
ip igmp snooping vlan 216
ip igmp snooping vlan 216 querier
ip igmp snooping vlan 216 querier address 172.16.16.16
ip igmp snooping vlan 216 querier version 3
ip igmp snooping vlan 217
ip igmp snooping vlan 217 querier
ip igmp snooping vlan 217 querier address 172.16.16.16
ip igmp snooping vlan 217 querier version 3
ip igmp snooping vlan 218
ip igmp snooping vlan 218 querier
ip igmp snooping vlan 218 querier address 172.16.16.16
ip igmp snooping vlan 218 querier version 3
ip igmp snooping vlan 219
ip igmp snooping vlan 219 querier
ip igmp snooping vlan 219 querier address 172.16.16.16
ip igmp snooping vlan 219 querier version 3
ip igmp snooping vlan 220
ip igmp snooping vlan 220 querier
ip igmp snooping vlan 220 querier address 172.16.16.16
ip igmp snooping vlan 220 querier version 3
ip igmp snooping vlan 221
ip igmp snooping vlan 221 querier
ip igmp snooping vlan 221 querier address 172.16.16.16
ip igmp snooping vlan 221 querier version 3
ip igmp snooping vlan 222
ip igmp snooping vlan 222 querier
ip igmp snooping vlan 222 querier address 172.16.16.16
ip igmp snooping vlan 222 querier version 3
ip igmp snooping vlan 223
ip igmp snooping vlan 223 querier
ip igmp snooping vlan 223 querier address 172.16.16.16
ip igmp snooping vlan 223 querier version 3
ip igmp snooping vlan 224
ip igmp snooping vlan 224 querier
ip igmp snooping vlan 224 querier address 172.16.16.16
ip igmp snooping vlan 224 querier version 3
ip igmp snooping vlan 225
ip igmp snooping vlan 225 querier
ip igmp snooping vlan 225 querier address 172.16.16.16
ip igmp snooping vlan 225 querier version 3
ip igmp snooping vlan 226
ip igmp snooping vlan 226 querier
ip igmp snooping vlan 226 querier address 172.16.16.16
ip igmp snooping vlan 226 querier version 3
ip igmp snooping vlan 227
ip igmp snooping vlan 227 querier
ip igmp snooping vlan 227 querier address 172.16.16.16
ip igmp snooping vlan 227 querier version 3
ip igmp snooping vlan 228
ip igmp snooping vlan 228 querier
ip igmp snooping vlan 228 querier address 172.16.16.16
ip igmp snooping vlan 228 querier version 3
ip igmp snooping vlan 229
ip igmp snooping vlan 229 querier
ip igmp snooping vlan 229 querier address 172.16.16.16
ip igmp snooping vlan 229 querier version 3
ip igmp snooping vlan 230
ip igmp snooping vlan 230 querier
ip igmp snooping vlan 230 querier address 172.16.16.16
ip igmp snooping vlan 230 querier version 3
ip igmp snooping vlan 231
ip igmp snooping vlan 231 querier
ip igmp snooping vlan 231 querier address 172.16.16.16
ip igmp snooping vlan 231 querier version 3
ip igmp snooping vlan 232
ip igmp snooping vlan 232 querier
ip igmp snooping vlan 232 querier address 172.16.16.16
ip igmp snooping vlan 232 querier version 3
ip igmp snooping vlan 233
ip igmp snooping vlan 233 querier
ip igmp snooping vlan 233 querier address 172.16.16.16
ip igmp snooping vlan 233 querier version 3
ip igmp snooping vlan 234
ip igmp snooping vlan 234 querier
ip igmp snooping vlan 234 querier address 172.16.16.16
ip igmp snooping vlan 234 querier version 3
ip igmp snooping vlan 235
ip igmp snooping vlan 235 querier
ip igmp snooping vlan 235 querier address 172.16.16.16
ip igmp snooping vlan 235 querier version 3
ip igmp snooping vlan 236
ip igmp snooping vlan 236 querier
ip igmp snooping vlan 236 querier address 172.16.16.16
ip igmp snooping vlan 236 querier version 3
ip igmp snooping vlan 237
ip igmp snooping vlan 237 querier
ip igmp snooping vlan 237 querier address 172.16.16.16
ip igmp snooping vlan 237 querier version 3
ip igmp snooping vlan 238
ip igmp snooping vlan 238 querier
ip igmp snooping vlan 238 querier address 172.16.16.16
ip igmp snooping vlan 238 querier version 3
ip igmp snooping vlan 239
ip igmp snooping vlan 239 querier
ip igmp snooping vlan 239 querier address 172.16.16.16
ip igmp snooping vlan 239 querier version 3
ip igmp snooping vlan 240
ip igmp snooping vlan 240 querier
ip igmp snooping vlan 240 querier address 172.16.16.16
ip igmp snooping vlan 240 querier version 3
ip igmp snooping vlan 241
ip igmp snooping vlan 241 querier
ip igmp snooping vlan 241 querier address 172.16.16.16
ip igmp snooping vlan 241 querier version 3
ip igmp snooping vlan 242
ip igmp snooping vlan 242 querier
ip igmp snooping vlan 242 querier address 172.16.16.16
ip igmp snooping vlan 242 querier version 3
ip igmp snooping vlan 243
ip igmp snooping vlan 243 querier
ip igmp snooping vlan 243 querier address 172.16.16.16
ip igmp snooping vlan 243 querier version 3
ip igmp snooping vlan 244
ip igmp snooping vlan 244 querier
ip igmp snooping vlan 244 querier address 172.16.16.16
ip igmp snooping vlan 244 querier version 3
ip igmp snooping vlan 245
ip igmp snooping vlan 245 querier
ip igmp snooping vlan 245 querier address 172.16.16.16
ip igmp snooping vlan 245 querier version 3
ip igmp snooping vlan 246
ip igmp snooping vlan 246 querier
ip igmp snooping vlan 246 querier address 172.16.16.16
ip igmp snooping vlan 246 querier version 3
ip igmp snooping vlan 247
ip igmp snooping vlan 247 querier
ip igmp snooping vlan 247 querier address 172.16.16.16
ip igmp snooping vlan 247 querier version 3
ip igmp snooping vlan 248
ip igmp snooping vlan 248 querier
ip igmp snooping vlan 248 querier address 172.16.16.16
ip igmp snooping vlan 248 querier version 3
ip igmp snooping vlan 249
ip igmp snooping vlan 249 querier
ip igmp snooping vlan 249 querier address 172.16.16.16
ip igmp snooping vlan 249 querier version 3
ip igmp snooping vlan 250
ip igmp snooping vlan 250 querier
ip igmp snooping vlan 250 querier address 172.16.16.16
ip igmp snooping vlan 250 querier version 3
ip igmp snooping vlan 251
ip igmp snooping vlan 251 querier
ip igmp snooping vlan 251 querier address 172.16.16.16
ip igmp snooping vlan 251 querier version 3
ip igmp snooping vlan 252
ip igmp snooping vlan 252 querier
ip igmp snooping vlan 252 querier address 172.16.16.16
ip igmp snooping vlan 252 querier version 3
ip igmp snooping vlan 253
ip igmp snooping vlan 253 querier
ip igmp snooping vlan 253 querier address 172.16.16.16
ip igmp snooping vlan 253 querier version 3
ip igmp snooping vlan 254
ip igmp snooping vlan 254 querier
ip igmp snooping vlan 254 querier address 172.16.16.16
ip igmp snooping vlan 254 querier version 3
ip igmp snooping vlan 255
ip igmp snooping vlan 255 querier
ip igmp snooping vlan 255 querier address 172.16.16.16
ip igmp snooping vlan 255 querier version 3
ip igmp snooping vlan 256
ip igmp snooping vlan 256 querier
ip igmp snooping vlan 256 querier address 172.16.16.16
ip igmp snooping vlan 256 querier version 3
ip igmp snooping vlan 257
ip igmp snooping vlan 257 querier
ip igmp snooping vlan 257 querier address 172.16.16.16
ip igmp snooping vlan 257 querier version 3
ip igmp snooping vlan 258
ip igmp snooping vlan 258 querier
ip igmp snooping vlan 258 querier address 172.16.16.16
ip igmp snooping vlan 258 querier version 3
ip igmp snooping vlan 259
ip igmp snooping vlan 259 querier
ip igmp snooping vlan 259 querier address 172.16.16.16
ip igmp snooping vlan 259 querier version 3
ip igmp snooping vlan 260
ip igmp snooping vlan 260 querier
ip igmp snooping vlan 260 querier address 172.16.16.16
ip igmp snooping vlan 260 querier version 3
ip igmp snooping vlan 261
ip igmp snooping vlan 261 querier
ip igmp snooping vlan 261 querier address 172.16.16.16
ip igmp snooping vlan 261 querier version 3
ip igmp snooping vlan 262
ip igmp snooping vlan 262 querier
ip igmp snooping vlan 262 querier address 172.16.16.16
ip igmp snooping vlan 262 querier version 3
ip igmp snooping vlan 263
ip igmp snooping vlan 263 querier
ip igmp snooping vlan 263 querier address 172.16.16.16
ip igmp snooping vlan 263 querier version 3
ip igmp snooping vlan 264
ip igmp snooping vlan 264 querier
ip igmp snooping vlan 264 querier address 172.16.16.16
ip igmp snooping vlan 264 querier version 3
ip igmp snooping vlan 265
ip igmp snooping vlan 265 querier
ip igmp snooping vlan 265 querier address 172.16.16.16
ip igmp snooping vlan 265 querier version 3
ip igmp snooping vlan 266
ip igmp snooping vlan 266 querier
ip igmp snooping vlan 266 querier address 172.16.16.16
ip igmp snooping vlan 266 querier version 3
ip igmp snooping vlan 267
ip igmp snooping vlan 267 querier
ip igmp snooping vlan 267 querier address 172.16.16.16
ip igmp snooping vlan 267 querier version 3
ip igmp snooping vlan 268
ip igmp snooping vlan 268 querier
ip igmp snooping vlan 268 querier address 172.16.16.16
ip igmp snooping vlan 268 querier version 3
ip igmp snooping vlan 269
ip igmp snooping vlan 269 querier
ip igmp snooping vlan 269 querier address 172.16.16.16
ip igmp snooping vlan 269 querier version 3
ip igmp snooping vlan 270
ip igmp snooping vlan 270 querier
ip igmp snooping vlan 270 querier address 172.16.16.16
ip igmp snooping vlan 270 querier version 3
ip igmp snooping vlan 271
ip igmp snooping vlan 271 querier
ip igmp snooping vlan 271 querier address 172.16.16.16
ip igmp snooping vlan 271 querier version 3
ip igmp snooping vlan 272
ip igmp snooping vlan 272 querier
ip igmp snooping vlan 272 querier address 172.16.16.16
ip igmp snooping vlan 272 querier version 3
ip igmp snooping vlan 273
ip igmp snooping vlan 273 querier
ip igmp snooping vlan 273 querier address 172.16.16.16
ip igmp snooping vlan 273 querier version 3
ip igmp snooping vlan 274
ip igmp snooping vlan 274 querier
ip igmp snooping vlan 274 querier address 172.16.16.16
ip igmp snooping vlan 274 querier version 3
ip igmp snooping vlan 275
ip igmp snooping vlan 275 querier
ip igmp snooping vlan 275 querier address 172.16.16.16
ip igmp snooping vlan 275 querier version 3
ip igmp snooping vlan 276
ip igmp snooping vlan 276 querier
ip igmp snooping vlan 276 querier address 172.16.16.16
ip igmp snooping vlan 276 querier version 3
ip igmp snooping vlan 277
ip igmp snooping vlan 277 querier
ip igmp snooping vlan 277 querier address 172.16.16.16
ip igmp snooping vlan 277 querier version 3
ip igmp snooping vlan 278
ip igmp snooping vlan 278 querier
ip igmp snooping vlan 278 querier address 172.16.16.16
ip igmp snooping vlan 278 querier version 3
ip igmp snooping vlan 279
ip igmp snooping vlan 279 querier
ip igmp snooping vlan 279 querier address 172.16.16.16
ip igmp snooping vlan 279 querier version 3
ip igmp snooping vlan 280
ip igmp snooping vlan 280 querier
ip igmp snooping vlan 280 querier address 172.16.16.16
ip igmp snooping vlan 280 querier version 3
```

## Filters

### Route-maps

#### Route-maps Summary

##### RM-MLAG-PEER-IN

| Sequence | Type | Match | Set | Sub-Route-Map | Continue |
| -------- | ---- | ----- | --- | ------------- | -------- |
| 10 | permit | - | origin incomplete | - | - |

#### Route-maps Device Configuration

```eos
!
route-map RM-MLAG-PEER-IN permit 10
   description Make routes learned over MLAG Peer-link less preferred on spines to ensure optimal routing
   set origin incomplete
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
