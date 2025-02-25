# green-spine1

## Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [IP Name Servers](#ip-name-servers)
  - [NTP](#ntp)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
  - [Enable Password](#enable-password)
  - [AAA Authorization](#aaa-authorization)
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
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
- [Filters](#filters)
  - [Prefix-lists](#prefix-lists)
  - [Route-maps](#route-maps)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)

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

#### Local Users Device Configuration

```eos
!
username admin privilege 15 role network-admin secret sha512 <removed>
```

### Enable Password

Enable password has been disabled

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

## MLAG

### MLAG Summary

| Domain-id | Local-interface | Peer-address | Peer-link |
| --------- | --------------- | ------------ | --------- |
| SPINES | Vlan4094 | 192.168.0.141 | Port-Channel8311 |

Dual primary detection is disabled.

### MLAG Device Configuration

```eos
!
mlag configuration
   domain-id SPINES
   local-interface Vlan4094
   peer-address 192.168.0.141
   peer-link Port-Channel8311
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
| 4093 | MLAG_L3_VRF_default | MLAG |
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
   name MLAG_L3_VRF_default
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
| Ethernet3/5/1 | L2_green-leaf1_Ethernet53/1 | *trunk | *113,201-202 | *- | *- | 351 |
| Ethernet3/6/1 | L2_green-leaf2_Ethernet53/1 | *trunk | *113,202-204 | *- | *- | 361 |
| Ethernet3/7/1 | L2_green-leaf3_Ethernet53/1 | *trunk | *113,201,203,205,207,209 | *- | *- | 371 |
| Ethernet3/8/1 | L2_green-leaf4_Ethernet53/1 | *trunk | *113,202,204,206,208 | *- | *- | 381 |
| Ethernet3/9/1 | L2_green-leaf5_Ethernet53/1 | *trunk | *113,202-203 | *- | *- | 391 |
| Ethernet8/31/1 | MLAG_green-spine2_Ethernet8/31/1 | *trunk | *- | *- | *MLAG | 8311 |
| Ethernet8/32/1 | MLAG_green-spine2_Ethernet8/32/1 | *trunk | *- | *- | *MLAG | 8311 |

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
   channel-group 351 mode active
!
interface Ethernet3/6/1
   description L2_green-leaf2_Ethernet53/1
   no shutdown
   channel-group 361 mode active
!
interface Ethernet3/7/1
   description L2_green-leaf3_Ethernet53/1
   no shutdown
   channel-group 371 mode active
!
interface Ethernet3/8/1
   description L2_green-leaf4_Ethernet53/1
   no shutdown
   channel-group 381 mode active
!
interface Ethernet3/9/1
   description L2_green-leaf5_Ethernet53/1
   no shutdown
   channel-group 391 mode active
!
interface Ethernet8/31/1
   description MLAG_green-spine2_Ethernet8/31/1
   no shutdown
   channel-group 8311 mode active
!
interface Ethernet8/32/1
   description MLAG_green-spine2_Ethernet8/32/1
   no shutdown
   channel-group 8311 mode active
```

### Port-Channel Interfaces

#### Port-Channel Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | LACP Fallback Timeout | LACP Fallback Mode | MLAG ID | EVPN ESI |
| --------- | ----------- | ---- | ----- | ----------- | ------------| --------------------- | ------------------ | ------- | -------- |
| Port-Channel351 | L2_green-leaf1_Port-Channel531 | trunk | 113,201-202 | - | - | - | - | 351 | - |
| Port-Channel361 | L2_green-leaf2_Port-Channel531 | trunk | 113,202-204 | - | - | - | - | 361 | - |
| Port-Channel371 | L2_green-leaf3_Port-Channel531 | trunk | 113,201,203,205,207,209 | - | - | - | - | 371 | - |
| Port-Channel381 | L2_green-leaf4_Port-Channel531 | trunk | 113,202,204,206,208 | - | - | - | - | 381 | - |
| Port-Channel391 | L2_green-leaf5_Port-Channel531 | trunk | 113,202-203 | - | - | - | - | 391 | - |
| Port-Channel8311 | MLAG_green-spine2_Port-Channel8311 | trunk | - | - | MLAG | - | - | - | - |

#### Port-Channel Interfaces Device Configuration

```eos
!
interface Port-Channel351
   description L2_green-leaf1_Port-Channel531
   no shutdown
   switchport trunk allowed vlan 113,201-202
   switchport mode trunk
   switchport
   mlag 351
!
interface Port-Channel361
   description L2_green-leaf2_Port-Channel531
   no shutdown
   switchport trunk allowed vlan 113,202-204
   switchport mode trunk
   switchport
   mlag 361
!
interface Port-Channel371
   description L2_green-leaf3_Port-Channel531
   no shutdown
   switchport trunk allowed vlan 113,201,203,205,207,209
   switchport mode trunk
   switchport
   mlag 371
!
interface Port-Channel381
   description L2_green-leaf4_Port-Channel531
   no shutdown
   switchport trunk allowed vlan 113,202,204,206,208
   switchport mode trunk
   switchport
   mlag 381
!
interface Port-Channel391
   description L2_green-leaf5_Port-Channel531
   no shutdown
   switchport trunk allowed vlan 113,202-203
   switchport mode trunk
   switchport
   mlag 391
!
interface Port-Channel8311
   description MLAG_green-spine2_Port-Channel8311
   no shutdown
   switchport mode trunk
   switchport trunk group MLAG
   switchport
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ROUTER_ID | default | 169.27.195.71/32 |

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
   ip address 169.27.195.71/32
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
| Vlan4093 | MLAG_L3_VRF_default | default | 9214 | False |
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
| Vlan4093 |  default  |  10.1.1.140/31  |  -  |  -  |  -  |  -  |
| Vlan4094 |  default  |  192.168.0.140/31  |  -  |  -  |  -  |  -  |

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
   description MLAG_L3_VRF_default
   no shutdown
   mtu 9214
   vrf default
   ip address 10.1.1.140/31
!
interface Vlan4094
   description MLAG
   no shutdown
   mtu 9214
   no autostate
   ip address 192.168.0.140/31
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

### Prefix-lists

#### Prefix-lists Summary

##### PL-MLAG-PEER-VRFS

| Sequence | Action |
| -------- | ------ |
| 10 | permit 10.1.1.140/31 |

#### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-MLAG-PEER-VRFS
   seq 10 permit 10.1.1.140/31
```

### Route-maps

#### Route-maps Summary

##### RM-CONN-2-BGP-VRFS

| Sequence | Type | Match | Set | Sub-Route-Map | Continue |
| -------- | ---- | ----- | --- | ------------- | -------- |
| 10 | deny | ip address prefix-list PL-MLAG-PEER-VRFS | - | - | - |
| 20 | permit | - | - | - | - |

#### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP-VRFS deny 10
   match ip address prefix-list PL-MLAG-PEER-VRFS
!
route-map RM-CONN-2-BGP-VRFS permit 20
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
