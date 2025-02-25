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
| FABRIC | l2leaf | green-leaf1 | 10.100.100.72/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf2 | 10.100.100.73/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf3 | 10.100.100.74/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf4 | 10.100.100.75/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf5 | 10.100.100.76/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf6 | 10.100.100.77/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf7 | 10.100.100.78/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf8 | 10.100.100.79/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf9 | 10.100.100.80/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf10 | 10.100.100.81/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf11 | 10.100.100.82/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf12 | 10.100.100.83/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf13 | 10.100.100.84/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf14 | 10.100.100.85/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf15 | 10.100.100.86/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf16 | 10.100.100.87/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf17 | 10.100.100.88/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf18 | 10.100.100.89/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf19 | 10.100.100.90/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf20 | 10.100.100.91/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf21 | 10.100.100.92/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf22 | 10.100.100.93/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf23 | 10.100.100.94/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf24 | 10.100.100.95/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf25 | 10.100.100.96/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf26 | 10.100.100.97/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf27 | 10.100.100.98/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf28 | 10.100.100.99/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf29 | 10.100.100.100/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf30 | 10.100.100.101/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf31 | 10.100.100.102/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf32 | 10.100.100.103/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf33 | 10.100.100.104/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf34 | 10.100.100.105/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf35 | 10.100.100.106/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf36 | 10.100.100.107/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf37 | 10.100.100.108/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf38 | 10.100.100.109/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf39 | 10.100.100.110/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf40 | 10.100.100.111/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf41 | 10.100.100.112/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf42 | 10.100.100.113/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf43 | 10.100.100.114/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf44 | 10.100.100.115/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf45 | 10.100.100.116/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf46 | 10.100.100.117/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf47 | 10.100.100.118/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf48 | 10.100.100.119/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf49 | 10.100.100.120/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf50 | 10.100.100.121/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf51 | 10.100.100.122/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf52 | 10.100.100.123/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf53 | 10.100.100.124/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf54 | 10.100.100.125/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf55 | 10.100.100.126/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf56 | 10.100.100.127/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf57 | 10.100.100.128/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf58 | 10.100.100.129/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf59 | 10.100.100.130/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf60 | 10.100.100.131/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf61 | 10.100.100.132/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf62 | 10.100.100.133/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf63 | 10.100.100.134/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf64 | 10.100.100.135/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf65 | 10.100.100.136/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf66 | 10.100.100.137/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf67 | 10.100.100.138/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf68 | 10.100.100.139/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf69 | 10.100.100.140/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf70 | 10.100.100.141/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf71 | 10.100.100.142/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf72 | 10.100.100.143/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf73 | 10.100.100.144/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf74 | 10.100.100.145/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf75 | 10.100.100.146/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf76 | 10.100.100.147/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf77 | 10.100.100.148/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf78 | 10.100.100.149/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf79 | 10.100.100.150/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf80 | 10.100.100.151/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf81 | 10.100.100.152/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf82 | 10.100.100.153/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf83 | 10.100.100.154/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf84 | 10.100.100.155/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf85 | 10.100.100.156/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf86 | 10.100.100.157/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf87 | 10.100.100.158/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf88 | 10.100.100.159/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf89 | 10.100.100.160/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf90 | 10.100.100.161/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf91 | 10.100.100.162/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf92 | 10.100.100.163/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf93 | 10.100.100.164/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf94 | 10.100.100.165/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf95 | 10.100.100.166/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf96 | 10.100.100.167/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf97 | 10.100.100.168/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf98 | 10.100.100.169/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf99 | 10.100.100.170/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf100 | 10.100.100.171/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf101 | 10.100.100.172/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf102 | 10.100.100.173/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf103 | 10.100.100.174/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf104 | 10.100.100.175/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf105 | 10.100.100.176/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf106 | 10.100.100.177/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf107 | 10.100.100.178/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf108 | 10.100.100.179/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf109 | 10.100.100.180/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf110 | 10.100.100.181/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf111 | 10.100.100.182/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf112 | 10.100.100.183/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf113 | 10.100.100.184/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf114 | 10.100.100.185/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf115 | 10.100.100.186/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf116 | 10.100.100.187/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf117 | 10.100.100.188/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf118 | 10.100.100.189/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf119 | 10.100.100.190/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf120 | 10.100.100.191/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf121 | 10.100.100.192/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf122 | 10.100.100.193/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf123 | 10.100.100.194/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf124 | 10.100.100.195/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf125 | 10.100.100.196/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf126 | 10.100.100.197/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf127 | 10.100.100.198/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf128 | 10.100.100.199/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf129 | 10.100.100.200/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf130 | 10.100.100.201/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf131 | 10.100.100.202/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf132 | 10.100.100.203/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf133 | 10.100.100.204/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf134 | 10.100.100.205/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf135 | 10.100.100.206/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf136 | 10.100.100.207/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf137 | 10.100.100.208/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf138 | 10.100.100.209/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf139 | 10.100.100.210/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf140 | 10.100.100.211/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf141 | 10.100.100.212/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf142 | 10.100.100.213/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf143 | 10.100.100.214/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf144 | 10.100.100.215/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf145 | 10.100.100.216/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf146 | 10.100.100.217/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf147 | 10.100.100.218/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf148 | 10.100.100.219/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf149 | 10.100.100.220/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf150 | 10.100.100.221/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf151 | 10.100.100.222/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf152 | 10.100.100.223/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf153 | 10.100.100.224/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf154 | 10.100.100.225/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf155 | 10.100.100.226/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf156 | 10.100.100.227/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf157 | 10.100.100.228/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf158 | 10.100.100.229/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf159 | 10.100.100.230/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf160 | 10.100.100.231/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf161 | 10.100.100.232/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf162 | 10.100.100.233/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf163 | 10.100.100.234/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf164 | 10.100.100.235/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf165 | 10.100.100.236/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf166 | 10.100.100.237/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf167 | 10.100.100.238/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf168 | 10.100.100.239/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf169 | 10.100.100.240/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf170 | 10.100.100.241/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf171 | 10.100.100.242/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf172 | 10.100.100.243/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf173 | 10.100.100.244/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf174 | 10.100.100.245/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf175 | 10.100.100.246/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf176 | 10.100.100.247/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf177 | 10.100.100.248/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf178 | 10.100.100.249/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf179 | 10.100.100.250/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf180 | 10.100.100.251/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf181 | 10.100.100.252/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf182 | 10.100.100.253/23 | 720XP | Provisioned | - |
| FABRIC | l2leaf | green-leaf183 | 10.100.100.254/23 | 720XP | Provisioned | - |
| FABRIC | l3spine | green-spine1 | 10.100.100.70/24 | 7308X3 | Provisioned | - |
| FABRIC | l3spine | green-spine2 | 10.100.100.71/24 | 7308X3 | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |
| FABRIC | l2leaf | green-leaf1 | 10.239.1.15/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf2 | 10.239.1.16/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf3 | 10.239.1.17/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf4 | 10.239.1.18/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf5 | 10.239.1.19/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf6 | 10.239.1.20/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf7 | 10.239.1.21/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf8 | 10.239.1.22/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf9 | 10.239.1.23/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf10 | 10.239.1.24/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf11 | 10.239.1.25/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf12 | 10.239.1.26/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf13 | 10.239.1.27/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf14 | 10.239.1.28/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf15 | 10.239.1.29/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf16 | 10.239.1.30/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf17 | 10.239.1.31/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf18 | 10.239.1.32/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf19 | 10.239.1.33/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf20 | 10.239.1.34/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf21 | 10.239.1.35/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf22 | 10.239.1.36/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf23 | 10.239.1.37/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf24 | 10.239.1.38/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf25 | 10.239.1.39/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf26 | 10.239.1.40/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf27 | 10.239.1.41/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf28 | 10.239.1.42/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf29 | 10.239.1.43/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf30 | 10.239.1.44/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf31 | 10.239.1.45/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf32 | 10.239.1.46/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf33 | 10.239.1.47/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf34 | 10.239.1.48/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf35 | 10.239.1.49/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf36 | 10.239.1.50/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf37 | 10.239.1.51/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf38 | 10.239.1.52/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf39 | 10.239.1.53/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf40 | 10.239.1.54/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf41 | 10.239.1.55/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf42 | 10.239.1.56/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf43 | 10.239.1.57/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf44 | 10.239.1.58/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf45 | 10.239.1.59/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf46 | 10.239.1.60/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf47 | 10.239.1.61/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf48 | 10.239.1.62/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf49 | 10.239.1.63/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf50 | 10.239.1.64/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf51 | 10.239.1.65/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf52 | 10.239.1.66/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf53 | 10.239.1.67/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf54 | 10.239.1.68/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf55 | 10.239.1.69/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf56 | 10.239.1.70/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf57 | 10.239.1.71/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf58 | 10.239.1.72/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf59 | 10.239.1.73/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf60 | 10.239.1.74/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf61 | 10.239.1.75/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf62 | 10.239.1.76/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf63 | 10.239.1.77/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf64 | 10.239.1.78/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf65 | 10.239.1.79/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf66 | 10.239.1.80/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf67 | 10.239.1.81/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf68 | 10.239.1.82/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf69 | 10.239.1.83/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf70 | 10.239.1.84/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf71 | 10.239.1.85/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf72 | 10.239.1.86/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf73 | 10.239.1.87/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf74 | 10.239.1.88/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf75 | 10.239.1.89/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf76 | 10.239.1.90/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf77 | 10.239.1.91/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf78 | 10.239.1.92/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf79 | 10.239.1.93/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf80 | 10.239.1.94/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf81 | 10.239.1.95/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf82 | 10.239.1.96/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf83 | 10.239.1.97/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf84 | 10.239.1.98/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf85 | 10.239.1.99/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf86 | 10.239.1.100/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf87 | 10.239.1.101/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf88 | 10.239.1.102/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf89 | 10.239.1.103/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf90 | 10.239.1.104/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf91 | 10.239.1.105/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf92 | 10.239.1.106/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf93 | 10.239.1.107/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf94 | 10.239.1.108/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf95 | 10.239.1.109/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf96 | 10.239.1.110/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf97 | 10.239.1.111/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf98 | 10.239.1.112/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf99 | 10.239.1.113/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf100 | 10.239.1.114/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf101 | 10.239.1.115/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf102 | 10.239.1.116/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf103 | 10.239.1.117/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf104 | 10.239.1.118/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf105 | 10.239.1.119/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf106 | 10.239.1.120/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf107 | 10.239.1.121/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf108 | 10.239.1.122/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf109 | 10.239.1.123/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf110 | 10.239.1.124/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf111 | 10.239.1.125/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf112 | 10.239.1.126/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf113 | 10.239.1.127/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf114 | 10.239.1.128/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf115 | 10.239.1.129/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf116 | 10.239.1.130/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf117 | 10.239.1.131/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf118 | 10.239.1.132/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf119 | 10.239.1.133/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf120 | 10.239.1.134/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf121 | 10.239.1.135/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf122 | 10.239.1.136/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf123 | 10.239.1.137/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf124 | 10.239.1.138/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf125 | 10.239.1.139/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf126 | 10.239.1.140/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf127 | 10.239.1.141/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf128 | 10.239.1.142/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf129 | 10.239.1.143/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf130 | 10.239.1.144/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf131 | 10.239.1.145/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf132 | 10.239.1.146/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf133 | 10.239.1.147/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf134 | 10.239.1.148/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf135 | 10.239.1.149/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf136 | 10.239.1.150/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf137 | 10.239.1.151/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf138 | 10.239.1.152/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf139 | 10.239.1.153/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf140 | 10.239.1.154/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf141 | 10.239.1.155/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf142 | 10.239.1.156/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf143 | 10.239.1.157/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf144 | 10.239.1.158/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf145 | 10.239.1.159/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf146 | 10.239.1.160/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf147 | 10.239.1.161/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf148 | 10.239.1.162/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf149 | 10.239.1.163/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf150 | 10.239.1.164/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf151 | 10.239.1.165/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf152 | 10.239.1.166/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf153 | 10.239.1.167/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf154 | 10.239.1.168/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf155 | 10.239.1.169/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf156 | 10.239.1.170/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf157 | 10.239.1.171/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf158 | 10.239.1.172/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf159 | 10.239.1.173/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf160 | 10.239.1.174/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf161 | 10.239.1.175/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf162 | 10.239.1.176/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf163 | 10.239.1.177/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf164 | 10.239.1.178/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf165 | 10.239.1.179/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf166 | 10.239.1.180/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf167 | 10.239.1.181/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf168 | 10.239.1.182/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf169 | 10.239.1.183/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf170 | 10.239.1.184/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf171 | 10.239.1.185/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf172 | 10.239.1.186/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf173 | 10.239.1.187/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf174 | 10.239.1.188/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf175 | 10.239.1.189/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf176 | 10.239.1.190/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf177 | 10.239.1.191/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf178 | 10.239.1.192/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf179 | 10.239.1.193/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf180 | 10.239.1.194/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf181 | 10.239.1.195/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf182 | 10.239.1.196/24 | Vlan113 |
| FABRIC | l2leaf | green-leaf183 | 10.239.1.197/24 | Vlan113 |

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
| l2leaf | green-leaf6 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/10/1 |
| l2leaf | green-leaf6 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/10/1 |
| l2leaf | green-leaf7 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/11/1 |
| l2leaf | green-leaf7 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/11/1 |
| l2leaf | green-leaf8 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/12/1 |
| l2leaf | green-leaf8 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/12/1 |
| l2leaf | green-leaf9 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/13/1 |
| l2leaf | green-leaf9 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/13/1 |
| l2leaf | green-leaf10 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/14/1 |
| l2leaf | green-leaf10 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/14/1 |
| l2leaf | green-leaf11 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/15/1 |
| l2leaf | green-leaf11 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/15/1 |
| l2leaf | green-leaf12 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/16/1 |
| l2leaf | green-leaf12 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/16/1 |
| l2leaf | green-leaf13 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/17/1 |
| l2leaf | green-leaf13 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/17/1 |
| l2leaf | green-leaf14 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/18/1 |
| l2leaf | green-leaf14 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/18/1 |
| l2leaf | green-leaf15 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/19/1 |
| l2leaf | green-leaf15 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/19/1 |
| l2leaf | green-leaf16 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/20/1 |
| l2leaf | green-leaf16 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/20/1 |
| l2leaf | green-leaf17 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/21/1 |
| l2leaf | green-leaf17 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/21/1 |
| l2leaf | green-leaf18 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/22/1 |
| l2leaf | green-leaf18 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/22/1 |
| l2leaf | green-leaf19 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/23/1 |
| l2leaf | green-leaf19 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/23/1 |
| l2leaf | green-leaf20 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/24/1 |
| l2leaf | green-leaf20 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/24/1 |
| l2leaf | green-leaf21 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/25/1 |
| l2leaf | green-leaf21 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/25/1 |
| l2leaf | green-leaf22 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/26/1 |
| l2leaf | green-leaf22 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/26/1 |
| l2leaf | green-leaf23 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/27/1 |
| l2leaf | green-leaf23 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/27/1 |
| l2leaf | green-leaf24 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/28/1 |
| l2leaf | green-leaf24 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/28/1 |
| l2leaf | green-leaf25 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/29/1 |
| l2leaf | green-leaf25 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/29/1 |
| l2leaf | green-leaf26 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/30/1 |
| l2leaf | green-leaf26 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/30/1 |
| l2leaf | green-leaf27 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/31/1 |
| l2leaf | green-leaf27 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/31/1 |
| l2leaf | green-leaf28 | Ethernet53/1 | l3spine | green-spine1 | Ethernet3/32/1 |
| l2leaf | green-leaf28 | Ethernet54/1 | l3spine | green-spine2 | Ethernet3/32/1 |
| l2leaf | green-leaf29 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/1/1 |
| l2leaf | green-leaf29 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/1/1 |
| l2leaf | green-leaf30 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/2/1 |
| l2leaf | green-leaf30 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/2/1 |
| l2leaf | green-leaf31 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/3/1 |
| l2leaf | green-leaf31 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/3/1 |
| l2leaf | green-leaf32 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/4/1 |
| l2leaf | green-leaf32 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/4/1 |
| l2leaf | green-leaf33 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/5/1 |
| l2leaf | green-leaf33 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/5/1 |
| l2leaf | green-leaf34 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/6/1 |
| l2leaf | green-leaf34 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/6/1 |
| l2leaf | green-leaf35 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/7/1 |
| l2leaf | green-leaf35 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/7/1 |
| l2leaf | green-leaf36 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/8/1 |
| l2leaf | green-leaf36 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/8/1 |
| l2leaf | green-leaf37 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/9/1 |
| l2leaf | green-leaf37 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/9/1 |
| l2leaf | green-leaf38 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/10/1 |
| l2leaf | green-leaf38 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/10/1 |
| l2leaf | green-leaf39 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/11/1 |
| l2leaf | green-leaf39 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/11/1 |
| l2leaf | green-leaf40 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/12/1 |
| l2leaf | green-leaf40 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/12/1 |
| l2leaf | green-leaf41 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/13/1 |
| l2leaf | green-leaf41 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/13/1 |
| l2leaf | green-leaf42 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/14/1 |
| l2leaf | green-leaf42 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/14/1 |
| l2leaf | green-leaf43 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/15/1 |
| l2leaf | green-leaf43 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/15/1 |
| l2leaf | green-leaf44 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/16/1 |
| l2leaf | green-leaf44 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/16/1 |
| l2leaf | green-leaf45 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/17/1 |
| l2leaf | green-leaf45 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/17/1 |
| l2leaf | green-leaf46 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/18/1 |
| l2leaf | green-leaf46 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/18/1 |
| l2leaf | green-leaf47 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/19/1 |
| l2leaf | green-leaf47 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/19/1 |
| l2leaf | green-leaf48 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/20/1 |
| l2leaf | green-leaf48 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/20/1 |
| l2leaf | green-leaf49 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/21/1 |
| l2leaf | green-leaf49 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/21/1 |
| l2leaf | green-leaf50 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/22/1 |
| l2leaf | green-leaf50 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/22/1 |
| l2leaf | green-leaf51 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/23/1 |
| l2leaf | green-leaf51 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/23/1 |
| l2leaf | green-leaf52 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/24/1 |
| l2leaf | green-leaf52 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/24/1 |
| l2leaf | green-leaf53 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/25/1 |
| l2leaf | green-leaf53 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/25/1 |
| l2leaf | green-leaf54 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/26/1 |
| l2leaf | green-leaf54 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/26/1 |
| l2leaf | green-leaf55 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/27/1 |
| l2leaf | green-leaf55 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/27/1 |
| l2leaf | green-leaf56 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/28/1 |
| l2leaf | green-leaf56 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/28/1 |
| l2leaf | green-leaf57 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/29/1 |
| l2leaf | green-leaf57 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/29/1 |
| l2leaf | green-leaf58 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/30/1 |
| l2leaf | green-leaf58 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/30/1 |
| l2leaf | green-leaf59 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/31/1 |
| l2leaf | green-leaf59 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/31/1 |
| l2leaf | green-leaf60 | Ethernet53/1 | l3spine | green-spine1 | Ethernet4/32/1 |
| l2leaf | green-leaf60 | Ethernet54/1 | l3spine | green-spine2 | Ethernet4/32/1 |
| l2leaf | green-leaf61 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/1/1 |
| l2leaf | green-leaf61 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/1/1 |
| l2leaf | green-leaf62 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/2/1 |
| l2leaf | green-leaf62 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/2/1 |
| l2leaf | green-leaf63 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/3/1 |
| l2leaf | green-leaf63 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/3/1 |
| l2leaf | green-leaf64 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/4/1 |
| l2leaf | green-leaf64 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/4/1 |
| l2leaf | green-leaf65 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/5/1 |
| l2leaf | green-leaf65 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/5/1 |
| l2leaf | green-leaf66 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/6/1 |
| l2leaf | green-leaf66 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/6/1 |
| l2leaf | green-leaf67 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/7/1 |
| l2leaf | green-leaf67 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/7/1 |
| l2leaf | green-leaf68 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/8/1 |
| l2leaf | green-leaf68 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/8/1 |
| l2leaf | green-leaf69 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/9/1 |
| l2leaf | green-leaf69 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/9/1 |
| l2leaf | green-leaf70 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/10/1 |
| l2leaf | green-leaf70 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/10/1 |
| l2leaf | green-leaf71 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/11/1 |
| l2leaf | green-leaf71 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/11/1 |
| l2leaf | green-leaf72 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/12/1 |
| l2leaf | green-leaf72 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/12/1 |
| l2leaf | green-leaf73 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/13/1 |
| l2leaf | green-leaf73 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/13/1 |
| l2leaf | green-leaf74 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/14/1 |
| l2leaf | green-leaf74 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/14/1 |
| l2leaf | green-leaf75 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/15/1 |
| l2leaf | green-leaf75 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/15/1 |
| l2leaf | green-leaf76 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/16/1 |
| l2leaf | green-leaf76 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/16/1 |
| l2leaf | green-leaf77 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/17/1 |
| l2leaf | green-leaf77 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/17/1 |
| l2leaf | green-leaf78 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/18/1 |
| l2leaf | green-leaf78 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/18/1 |
| l2leaf | green-leaf79 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/19/1 |
| l2leaf | green-leaf79 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/19/1 |
| l2leaf | green-leaf80 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/20/1 |
| l2leaf | green-leaf80 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/20/1 |
| l2leaf | green-leaf81 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/21/1 |
| l2leaf | green-leaf81 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/21/1 |
| l2leaf | green-leaf82 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/22/1 |
| l2leaf | green-leaf82 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/22/1 |
| l2leaf | green-leaf83 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/23/1 |
| l2leaf | green-leaf83 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/23/1 |
| l2leaf | green-leaf84 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/24/1 |
| l2leaf | green-leaf84 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/24/1 |
| l2leaf | green-leaf85 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/25/1 |
| l2leaf | green-leaf85 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/25/1 |
| l2leaf | green-leaf86 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/26/1 |
| l2leaf | green-leaf86 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/26/1 |
| l2leaf | green-leaf87 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/27/1 |
| l2leaf | green-leaf87 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/27/1 |
| l2leaf | green-leaf88 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/28/1 |
| l2leaf | green-leaf88 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/28/1 |
| l2leaf | green-leaf89 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/29/1 |
| l2leaf | green-leaf89 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/29/1 |
| l2leaf | green-leaf90 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/30/1 |
| l2leaf | green-leaf90 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/30/1 |
| l2leaf | green-leaf91 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/31/1 |
| l2leaf | green-leaf91 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/31/1 |
| l2leaf | green-leaf92 | Ethernet53/1 | l3spine | green-spine1 | Ethernet5/32/1 |
| l2leaf | green-leaf92 | Ethernet54/1 | l3spine | green-spine2 | Ethernet5/32/1 |
| l2leaf | green-leaf93 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/1/1 |
| l2leaf | green-leaf93 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/1/1 |
| l2leaf | green-leaf94 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/2/1 |
| l2leaf | green-leaf94 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/2/1 |
| l2leaf | green-leaf95 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/3/1 |
| l2leaf | green-leaf95 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/3/1 |
| l2leaf | green-leaf96 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/4/1 |
| l2leaf | green-leaf96 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/4/1 |
| l2leaf | green-leaf97 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/5/1 |
| l2leaf | green-leaf97 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/5/1 |
| l2leaf | green-leaf98 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/6/1 |
| l2leaf | green-leaf98 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/6/1 |
| l2leaf | green-leaf99 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/7/1 |
| l2leaf | green-leaf99 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/7/1 |
| l2leaf | green-leaf100 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/8/1 |
| l2leaf | green-leaf100 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/8/1 |
| l2leaf | green-leaf101 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/9/1 |
| l2leaf | green-leaf101 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/9/1 |
| l2leaf | green-leaf102 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/10/1 |
| l2leaf | green-leaf102 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/10/1 |
| l2leaf | green-leaf103 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/11/1 |
| l2leaf | green-leaf103 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/11/1 |
| l2leaf | green-leaf104 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/12/1 |
| l2leaf | green-leaf104 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/12/1 |
| l2leaf | green-leaf105 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/13/1 |
| l2leaf | green-leaf105 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/13/1 |
| l2leaf | green-leaf106 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/14/1 |
| l2leaf | green-leaf106 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/14/1 |
| l2leaf | green-leaf107 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/15/1 |
| l2leaf | green-leaf107 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/15/1 |
| l2leaf | green-leaf108 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/16/1 |
| l2leaf | green-leaf108 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/16/1 |
| l2leaf | green-leaf109 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/17/1 |
| l2leaf | green-leaf109 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/17/1 |
| l2leaf | green-leaf110 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/18/1 |
| l2leaf | green-leaf110 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/18/1 |
| l2leaf | green-leaf111 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/19/1 |
| l2leaf | green-leaf111 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/19/1 |
| l2leaf | green-leaf112 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/20/1 |
| l2leaf | green-leaf112 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/20/1 |
| l2leaf | green-leaf113 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/21/1 |
| l2leaf | green-leaf113 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/21/1 |
| l2leaf | green-leaf114 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/22/1 |
| l2leaf | green-leaf114 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/22/1 |
| l2leaf | green-leaf115 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/23/1 |
| l2leaf | green-leaf115 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/23/1 |
| l2leaf | green-leaf116 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/24/1 |
| l2leaf | green-leaf116 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/24/1 |
| l2leaf | green-leaf117 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/25/1 |
| l2leaf | green-leaf117 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/25/1 |
| l2leaf | green-leaf118 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/26/1 |
| l2leaf | green-leaf118 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/26/1 |
| l2leaf | green-leaf119 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/27/1 |
| l2leaf | green-leaf119 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/27/1 |
| l2leaf | green-leaf120 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/28/1 |
| l2leaf | green-leaf120 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/28/1 |
| l2leaf | green-leaf121 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/29/1 |
| l2leaf | green-leaf121 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/29/1 |
| l2leaf | green-leaf122 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/30/1 |
| l2leaf | green-leaf122 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/30/1 |
| l2leaf | green-leaf123 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/31/1 |
| l2leaf | green-leaf123 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/31/1 |
| l2leaf | green-leaf124 | Ethernet53/1 | l3spine | green-spine1 | Ethernet6/32/1 |
| l2leaf | green-leaf124 | Ethernet54/1 | l3spine | green-spine2 | Ethernet6/32/1 |
| l2leaf | green-leaf125 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/1/1 |
| l2leaf | green-leaf125 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/1/1 |
| l2leaf | green-leaf126 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/2/1 |
| l2leaf | green-leaf126 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/2/1 |
| l2leaf | green-leaf127 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/3/1 |
| l2leaf | green-leaf127 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/3/1 |
| l2leaf | green-leaf128 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/4/1 |
| l2leaf | green-leaf128 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/4/1 |
| l2leaf | green-leaf129 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/5/1 |
| l2leaf | green-leaf129 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/5/1 |
| l2leaf | green-leaf130 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/6/1 |
| l2leaf | green-leaf130 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/6/1 |
| l2leaf | green-leaf131 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/7/1 |
| l2leaf | green-leaf131 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/7/1 |
| l2leaf | green-leaf132 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/8/1 |
| l2leaf | green-leaf132 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/8/1 |
| l2leaf | green-leaf133 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/9/1 |
| l2leaf | green-leaf133 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/9/1 |
| l2leaf | green-leaf134 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/10/1 |
| l2leaf | green-leaf134 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/10/1 |
| l2leaf | green-leaf135 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/11/1 |
| l2leaf | green-leaf135 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/11/1 |
| l2leaf | green-leaf136 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/12/1 |
| l2leaf | green-leaf136 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/12/1 |
| l2leaf | green-leaf137 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/13/1 |
| l2leaf | green-leaf137 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/13/1 |
| l2leaf | green-leaf138 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/14/1 |
| l2leaf | green-leaf138 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/14/1 |
| l2leaf | green-leaf139 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/15/1 |
| l2leaf | green-leaf139 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/15/1 |
| l2leaf | green-leaf140 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/16/1 |
| l2leaf | green-leaf140 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/16/1 |
| l2leaf | green-leaf141 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/17/1 |
| l2leaf | green-leaf141 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/17/1 |
| l2leaf | green-leaf142 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/18/1 |
| l2leaf | green-leaf142 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/18/1 |
| l2leaf | green-leaf143 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/19/1 |
| l2leaf | green-leaf143 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/19/1 |
| l2leaf | green-leaf144 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/20/1 |
| l2leaf | green-leaf144 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/20/1 |
| l2leaf | green-leaf145 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/21/1 |
| l2leaf | green-leaf145 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/21/1 |
| l2leaf | green-leaf146 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/22/1 |
| l2leaf | green-leaf146 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/22/1 |
| l2leaf | green-leaf147 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/23/1 |
| l2leaf | green-leaf147 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/23/1 |
| l2leaf | green-leaf148 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/24/1 |
| l2leaf | green-leaf148 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/24/1 |
| l2leaf | green-leaf149 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/25/1 |
| l2leaf | green-leaf149 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/25/1 |
| l2leaf | green-leaf150 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/26/1 |
| l2leaf | green-leaf150 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/26/1 |
| l2leaf | green-leaf151 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/27/1 |
| l2leaf | green-leaf151 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/27/1 |
| l2leaf | green-leaf152 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/28/1 |
| l2leaf | green-leaf152 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/28/1 |
| l2leaf | green-leaf153 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/29/1 |
| l2leaf | green-leaf153 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/29/1 |
| l2leaf | green-leaf154 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/30/1 |
| l2leaf | green-leaf154 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/30/1 |
| l2leaf | green-leaf155 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/31/1 |
| l2leaf | green-leaf155 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/31/1 |
| l2leaf | green-leaf156 | Ethernet53/1 | l3spine | green-spine1 | Ethernet7/32/1 |
| l2leaf | green-leaf156 | Ethernet54/1 | l3spine | green-spine2 | Ethernet7/32/1 |
| l2leaf | green-leaf157 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/1/1 |
| l2leaf | green-leaf157 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/1/1 |
| l2leaf | green-leaf158 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/2/1 |
| l2leaf | green-leaf158 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/2/1 |
| l2leaf | green-leaf159 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/3/1 |
| l2leaf | green-leaf159 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/3/1 |
| l2leaf | green-leaf160 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/4/1 |
| l2leaf | green-leaf160 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/4/1 |
| l2leaf | green-leaf161 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/5/1 |
| l2leaf | green-leaf161 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/5/1 |
| l2leaf | green-leaf162 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/6/1 |
| l2leaf | green-leaf162 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/6/1 |
| l2leaf | green-leaf163 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/7/1 |
| l2leaf | green-leaf163 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/7/1 |
| l2leaf | green-leaf164 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/8/1 |
| l2leaf | green-leaf164 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/8/1 |
| l2leaf | green-leaf165 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/9/1 |
| l2leaf | green-leaf165 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/9/1 |
| l2leaf | green-leaf166 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/10/1 |
| l2leaf | green-leaf166 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/10/1 |
| l2leaf | green-leaf167 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/11/1 |
| l2leaf | green-leaf167 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/11/1 |
| l2leaf | green-leaf168 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/12/1 |
| l2leaf | green-leaf168 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/12/1 |
| l2leaf | green-leaf169 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/13/1 |
| l2leaf | green-leaf169 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/13/1 |
| l2leaf | green-leaf170 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/14/1 |
| l2leaf | green-leaf170 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/14/1 |
| l2leaf | green-leaf171 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/15/1 |
| l2leaf | green-leaf171 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/15/1 |
| l2leaf | green-leaf172 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/16/1 |
| l2leaf | green-leaf172 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/16/1 |
| l2leaf | green-leaf173 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/17/1 |
| l2leaf | green-leaf173 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/17/1 |
| l2leaf | green-leaf174 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/18/1 |
| l2leaf | green-leaf174 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/18/1 |
| l2leaf | green-leaf175 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/19/1 |
| l2leaf | green-leaf175 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/19/1 |
| l2leaf | green-leaf176 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/20/1 |
| l2leaf | green-leaf176 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/20/1 |
| l2leaf | green-leaf177 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/21/1 |
| l2leaf | green-leaf177 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/21/1 |
| l2leaf | green-leaf178 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/22/1 |
| l2leaf | green-leaf178 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/22/1 |
| l2leaf | green-leaf179 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/23/1 |
| l2leaf | green-leaf179 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/23/1 |
| l2leaf | green-leaf180 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/24/1 |
| l2leaf | green-leaf180 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/24/1 |
| l2leaf | green-leaf181 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/25/1 |
| l2leaf | green-leaf181 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/25/1 |
| l2leaf | green-leaf182 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/26/1 |
| l2leaf | green-leaf182 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/26/1 |
| l2leaf | green-leaf183 | Ethernet53/1 | l3spine | green-spine1 | Ethernet8/27/1 |
| l2leaf | green-leaf183 | Ethernet54/1 | l3spine | green-spine2 | Ethernet8/27/1 |
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
| FABRIC | green-spine1 | 169.27.195.10/32 |
| FABRIC | green-spine2 | 169.27.195.11/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------ | ------------------- | ------------------ | ------------------ |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
