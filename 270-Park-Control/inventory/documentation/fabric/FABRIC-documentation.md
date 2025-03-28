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
| FABRIC | l2leaf | C160064-001B301A | 10.176.142.82/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-002B301A | 10.176.136.115/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-002B302A | 10.176.136.131/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-002B303A | 10.176.136.116/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-002B304A | 10.176.136.117/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-002B305A | 10.176.142.98/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-002B306A | 10.176.142.99/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-002B307A | 10.176.142.100/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-002B308A | 10.176.142.101/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-003B301A | 10.176.136.152/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-003B302A | 10.176.136.153/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-004B301A | 10.176.136.183/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-004B302A | 10.176.136.184/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-005B301A | 10.176.136.216/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-005B302A | 10.176.136.217/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-006B301A | 10.176.136.248/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-006B302A | 10.176.136.249/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-007B301A | 10.176.137.24/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-007B302A | 10.176.137.25/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-008B301A | 10.176.137.56/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-008B302A | 10.176.137.57/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-009B301A | 10.176.137.88/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-009B302A | 10.176.137.89/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-010B301A | 10.176.137.120/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-010B302A | 10.176.137.121/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-013B301A | 10.176.142.114/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-013B302A | 10.176.142.115/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-013B303A | 10.176.142.130/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-013B304A | 10.176.142.131/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-013B305A | 10.176.142.132/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-014B301A | 10.176.138.3/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-014B302A | 10.176.142.146/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-014B303A | 10.176.142.147/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-014B304A | 10.176.142.162/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-014B305A | 10.176.142.163/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-015B301A | 10.176.138.36/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-015B302A | 10.176.138.37/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-015B303A | 10.176.142.178/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-015B304A | 10.176.142.179/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-015B305A | 10.176.142.180/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-015B306A | 10.176.142.181/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-015B307A | 10.176.142.182/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-015B308A | 10.176.142.183/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-015B309A | 10.176.142.184/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-015B310A | 10.176.142.185/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-015B311A | 10.176.142.186/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-015B313A | 10.176.142.194/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-015B314A | 10.176.142.195/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-016B301A | 10.176.138.68/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-016B302A | 10.176.138.69/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-016B303A | 10.176.142.210/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-016B304A | 10.176.142.211/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-016B305A | 10.176.142.212/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-016B306A | 10.176.142.213/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-016B307A | 10.176.142.214/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-016B308A | 10.176.142.226/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-016B309A | 10.176.142.227/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-016B310A | 10.176.142.228/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-016B311A | 10.176.142.229/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-016B312A | 10.176.142.230/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-017B301A | 10.176.138.84/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-017B302A | 10.176.142.242/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-017B303A | 10.176.142.243/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-017B304A | 10.176.142.244/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-017B305A | 10.176.142.245/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-017B306A | 10.176.142.246/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-017B307A | 10.176.142.247/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-020B301A | 10.176.138.179/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-021B301A | 10.176.138.211/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-022B301A | 10.176.138.243/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-023B301A | 10.176.139.19/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-024B301A | 10.176.139.51/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-025B301A | 10.176.139.83/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-026B301A | 10.176.139.115/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-027B301A | 10.176.139.147/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-028B301A | 10.176.139.179/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-030B301A | 10.176.139.243/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-031B301A | 10.176.140.19/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-032B301A | 10.176.140.51/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-033B301A | 10.176.140.83/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-034B301A | 10.176.140.115/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-035B301A | 10.176.140.147/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-036B301A | 10.176.140.179/28 | 720XP | Provisioned | NA |
| FABRIC | l3spine | C160064-037B300A | 10.176.143.136/27 | 7308X3 | Provisioned | HBG24140357 |
| FABRIC | l3spine | C160064-037B301A | 10.176.143.165/27 | 7308X3 | Provisioned | HBG24120B3C |
| FABRIC | l2leaf | C160064-037B302A | 10.176.143.130/27 | 720XP | Provisioned | HBG2414034A |
| FABRIC | l2leaf | C160064-037B303A | 10.176.143.131/27 | 720XP | Provisioned | HBG2414032M |
| FABRIC | l2leaf | C160064-037B304A | 10.176.143.133/27 | 720XP | Provisioned | HBG24120AZM |
| FABRIC | l2leaf | C160064-037B305A | 10.176.143.140/27 | 720XP | Provisioned | HBG241100BS |
| FABRIC | l2leaf | C160064-037B306A | 10.176.143.142/27 | 720XP | Provisioned | HBG241100AA |
| FABRIC | l2leaf | C160064-037B307A | 10.176.143.145/27 | 720XP | Provisioned | HBG241100BV |
| FABRIC | l2leaf | C160064-037B308A | 10.176.143.146/27 | 720XP | Provisioned | HBG241605HG |
| FABRIC | l2leaf | C160064-037B309A | 10.176.143.132/27 | 720XP | Provisioned | HBG24120B12 |
| FABRIC | l2leaf | C160064-037B310A | 10.176.143.162/27 | 720XP | Provisioned | HBG24140358 |
| FABRIC | l2leaf | C160064-037B311A | 10.176.143.163/27 | 720XP | Provisioned | HBG2414033L |
| FABRIC | l2leaf | C160064-037B312A | 10.176.143.164/27 | 720XP | Provisioned | HBG241605K0 |
| FABRIC | l2leaf | C160064-037B313A | 10.176.143.169/27 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-037B314A | 10.176.143.171/27 | 720XP | Provisioned | HBG24140320 |
| FABRIC | l2leaf | C160064-037B315A | 10.176.143.174/27 | 720XP | Provisioned | HBG24120B03 |
| FABRIC | l2leaf | C160064-037B316A | 10.176.143.175/27 | 720XP | Provisioned | HBG24120AZL |
| FABRIC | l2leaf | C160064-037B317A | 10.176.143.194/27 | 720XP | Provisioned | HBG24120B3T |
| FABRIC | l2leaf | C160064-037B318A | 10.176.143.195/27 | 720XP | Provisioned | HBG24120B34 |
| FABRIC | l2leaf | C160064-037B319A | 10.176.143.196/27 | 720XP | Provisioned | HBG24120B09 |
| FABRIC | l2leaf | C160064-037B320A | 10.176.143.197/27 | 720XP | Provisioned | HBG24120B25 |
| FABRIC | l2leaf | C160064-037B321A | 10.176.143.198/27 | 720XP | Provisioned | HBG2414032C |
| FABRIC | l2leaf | C160064-037B323A | 10.176.143.199/27 | 720XP | Provisioned | HBG241605HU |
| FABRIC | l2leaf | C160064-037B324A | 10.176.143.200/27 | 720XP | Provisioned | HBG241605GY |
| FABRIC | l2leaf | C160064-037B325A | 10.176.143.201/27 | 720XP | Provisioned | HBG241605K1 |
| FABRIC | l2leaf | C160064-037B326A | 10.176.143.226/27 | 720XP | Provisioned | HBG241605HL |
| FABRIC | l2leaf | C160064-037B327A | 10.176.143.227/27 | 720XP | Provisioned | HBG2414032N |
| FABRIC | l2leaf | C160064-037B328A | 10.176.143.228/27 | 720XP | Provisioned | HBG2414032G |
| FABRIC | l2leaf | C160064-037B329A | 10.176.143.229/27 | 720XP | Provisioned | HBG2414034E |
| FABRIC | l2leaf | C160064-037B330A | 10.176.143.230/27 | 720XP | Provisioned | HBG241605GT |
| FABRIC | l2leaf | C160064-037B331A | 10.176.143.231/27 | 720XP | Provisioned | HBG241605H0 |
| FABRIC | l2leaf | C160064-037B332A | 10.176.143.232/27 | 720XP | Provisioned | HBG241605HA |
| FABRIC | l2leaf | C160064-037B333A | 10.176.143.233/27 | 720XP | Provisioned | HBG241605HK |
| FABRIC | l2leaf | C160064-037B334A | 10.176.143.234/27 | 720XP | Provisioned | HBG2414033N |
| FABRIC | l2leaf | C160064-037B335A | 10.176.143.235/27 | 720XP | Provisioned | HBG241605GS |
| FABRIC | l2leaf | C160064-037B336A | 10.166.80.2/27 | 720XP | Provisioned | HBG241605GM |
| FABRIC | l2leaf | C160064-037B337A | 10.166.80.3/27 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-037B338A | 10.166.80.4/27 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-037B339A | 10.166.80.5/27 | 720XP | Provisioned | HBG24110009F |
| FABRIC | l2leaf | C160064-037B340A | 10.166.80.8/27 | 720XP | Provisioned | HBG2414034L |
| FABRIC | l2leaf | C160064-037B341A | 10.166.80.9/27 | 720XP | Provisioned | HBG241100AL |
| FABRIC | l2leaf | C160064-037B342A | 10.166.80.11/27 | 720XP | Provisioned | HBG241100BU |
| FABRIC | l2leaf | C160064-037B343A | 10.166.80.13/27 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-037B344A | 10.166.80.14/27 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-037B345A | 10.166.80.15/27 | 720XP | Provisioned | HBG241605HZ |
| FABRIC | l2leaf | C160064-037B346A | 10.166.80.16/27 | 720XP | Provisioned | HBG241605GU |
| FABRIC | l2leaf | C160064-037B347A | 10.166.80.17/27 | 720XP | Provisioned | HBG2411009C |
| FABRIC | l2leaf | C160064-037B348A | 10.166.80.18/27 | 720XP | Provisioned | HBG241100AB |
| FABRIC | l2leaf | C160064-037B349A | 10.166.80.34/27 | 720XP | Provisioned | HBG241605GN |
| FABRIC | l2leaf | C160064-037B350A | 10.166.80.35/27 | 720XP | Provisioned | HBG241605GV |
| FABRIC | l2leaf | C160064-037B351A | 10.166.80.36/27 | 720XP | Provisioned | HBG24120B0J |
| FABRIC | l2leaf | C160064-037B352A | 10.166.80.37/27 | 720XP | Provisioned | HBG24110097 |
| FABRIC | l2leaf | C160064-037B353A | 10.166.80.38/27 | 720XP | Provisioned | HBG241100AN |
| FABRIC | l2leaf | C160064-037B354A | 10.166.80.39/27 | 720XP | Provisioned | HBG241605HM |
| FABRIC | l2leaf | C160064-037B355A | 10.166.80.43/27 | 720XP | Provisioned | HBG241100C0 |
| FABRIC | l2leaf | C160064-037B356A | 10.166.80.45/27 | 720XP | Provisioned | HBG24110094 |
| FABRIC | l2leaf | C160064-037B357A | 10.166.80.47/27 | 720XP | Provisioned | HBG241100B6 |
| FABRIC | l2leaf | C160064-037B358A | 10.166.80.48/27 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-037B359A | 10.166.80.49/27 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-037B360A | 10.166.80.50/27 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-037B361A | 10.166.80.51/27 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-037B362A | 10.166.80.42/27 | 720XP | Provisioned | HBG241605JJ |
| FABRIC | l2leaf | C160064-037B369A | 10.176.140.229/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-040B301A | 10.176.141.20/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-041B301A | 10.176.141.36/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-042B301A | 10.176.141.52/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-043B301A | 10.176.141.68/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-044B301A | 10.176.141.84/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-045B301A | 10.176.141.100/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-045B302A | 10.176.141.101/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-045B303A | 10.176.141.102/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-046B301A | 10.176.141.116/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-046B302A | 10.176.141.117/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-046B303A | 10.176.141.118/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-047B301A | 10.176.141.132/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-048B301A | 10.176.143.2/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-048B302A | 10.176.143.3/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-048B303A | 10.176.143.18/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-048B304A | 10.176.143.19/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-049B301A | 10.176.141.165/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-049B302A | 10.176.141.166/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-049B303A | 10.176.143.34/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-049B304A | 10.176.143.35/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-049B305A | 10.176.143.50/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-049B306A | 10.176.143.51/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-050B301A | 10.176.143.66/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-050B302A | 10.176.143.67/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-050B303A | 10.176.143.68/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-050B304A | 10.176.143.82/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-050B305A | 10.176.143.83/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-050B306A | 10.176.143.84/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-050B307A | 10.176.143.85/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-051B301A | 10.176.143.98/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-051B302A | 10.176.143.99/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-051B304A | 10.176.143.114/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-051B305A | 10.176.143.115/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-051B306A | 10.176.143.116/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-051B307A | 10.176.143.117/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-056B301A | 10.176.142.19/28 | 720XP | Provisioned | NA |
| FABRIC | l2leaf | C160064-056B302A | 10.176.142.20/28 | 720XP | Provisioned | NA |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |
| FABRIC | l2leaf | C160064-001B301A | 10.93.240.71/24 | Vlan200 |
| FABRIC | l2leaf | C160064-002B301A | 10.93.240.72/24 | Vlan200 |
| FABRIC | l2leaf | C160064-002B302A | 10.93.240.73/24 | Vlan200 |
| FABRIC | l2leaf | C160064-002B303A | 10.93.240.74/24 | Vlan200 |
| FABRIC | l2leaf | C160064-002B304A | 10.93.240.75/24 | Vlan200 |
| FABRIC | l2leaf | C160064-002B305A | 10.93.240.76/24 | Vlan200 |
| FABRIC | l2leaf | C160064-002B306A | 10.93.240.77/24 | Vlan200 |
| FABRIC | l2leaf | C160064-002B307A | 10.93.240.78/24 | Vlan200 |
| FABRIC | l2leaf | C160064-002B308A | 10.93.240.79/24 | Vlan200 |
| FABRIC | l2leaf | C160064-003B301A | 10.93.240.80/24 | Vlan200 |
| FABRIC | l2leaf | C160064-003B302A | 10.93.240.81/24 | Vlan200 |
| FABRIC | l2leaf | C160064-004B301A | 10.93.240.82/24 | Vlan200 |
| FABRIC | l2leaf | C160064-004B302A | 10.93.240.83/24 | Vlan200 |
| FABRIC | l2leaf | C160064-005B301A | 10.93.240.84/24 | Vlan200 |
| FABRIC | l2leaf | C160064-005B302A | 10.93.240.85/24 | Vlan200 |
| FABRIC | l2leaf | C160064-006B301A | 10.93.240.86/24 | Vlan200 |
| FABRIC | l2leaf | C160064-006B302A | 10.93.240.87/24 | Vlan200 |
| FABRIC | l2leaf | C160064-007B301A | 10.93.240.88/24 | Vlan200 |
| FABRIC | l2leaf | C160064-007B302A | 10.93.240.89/24 | Vlan200 |
| FABRIC | l2leaf | C160064-008B301A | 10.93.240.90/24 | Vlan200 |
| FABRIC | l2leaf | C160064-008B302A | 10.93.240.91/24 | Vlan200 |
| FABRIC | l2leaf | C160064-009B301A | 10.93.240.92/24 | Vlan200 |
| FABRIC | l2leaf | C160064-009B302A | 10.93.240.93/24 | Vlan200 |
| FABRIC | l2leaf | C160064-010B301A | 10.93.240.94/24 | Vlan200 |
| FABRIC | l2leaf | C160064-010B302A | 10.93.240.95/24 | Vlan200 |
| FABRIC | l2leaf | C160064-013B301A | 10.93.240.96/24 | Vlan200 |
| FABRIC | l2leaf | C160064-013B302A | 10.93.240.97/24 | Vlan200 |
| FABRIC | l2leaf | C160064-013B303A | 10.93.240.98/24 | Vlan200 |
| FABRIC | l2leaf | C160064-013B304A | 10.93.240.99/24 | Vlan200 |
| FABRIC | l2leaf | C160064-013B305A | 10.93.240.100/24 | Vlan200 |
| FABRIC | l2leaf | C160064-014B301A | 10.93.240.101/24 | Vlan200 |
| FABRIC | l2leaf | C160064-014B302A | 10.93.240.102/24 | Vlan200 |
| FABRIC | l2leaf | C160064-014B303A | 10.93.240.103/24 | Vlan200 |
| FABRIC | l2leaf | C160064-014B304A | 10.93.240.104/24 | Vlan200 |
| FABRIC | l2leaf | C160064-014B305A | 10.93.240.105/24 | Vlan200 |
| FABRIC | l2leaf | C160064-015B301A | 10.93.240.106/24 | Vlan200 |
| FABRIC | l2leaf | C160064-015B302A | 10.93.240.107/24 | Vlan200 |
| FABRIC | l2leaf | C160064-015B303A | 10.93.240.108/24 | Vlan200 |
| FABRIC | l2leaf | C160064-015B304A | 10.93.240.109/24 | Vlan200 |
| FABRIC | l2leaf | C160064-015B305A | 10.93.240.110/24 | Vlan200 |
| FABRIC | l2leaf | C160064-015B306A | 10.93.240.111/24 | Vlan200 |
| FABRIC | l2leaf | C160064-015B307A | 10.93.240.112/24 | Vlan200 |
| FABRIC | l2leaf | C160064-015B308A | 10.93.240.113/24 | Vlan200 |
| FABRIC | l2leaf | C160064-015B309A | 10.93.240.114/24 | Vlan200 |
| FABRIC | l2leaf | C160064-015B310A | 10.93.240.115/24 | Vlan200 |
| FABRIC | l2leaf | C160064-015B311A | 10.93.240.116/24 | Vlan200 |
| FABRIC | l2leaf | C160064-015B313A | 10.93.240.117/24 | Vlan200 |
| FABRIC | l2leaf | C160064-015B314A | 10.93.240.118/24 | Vlan200 |
| FABRIC | l2leaf | C160064-016B301A | 10.93.240.119/24 | Vlan200 |
| FABRIC | l2leaf | C160064-016B302A | 10.93.240.120/24 | Vlan200 |
| FABRIC | l2leaf | C160064-016B303A | 10.93.240.121/24 | Vlan200 |
| FABRIC | l2leaf | C160064-016B304A | 10.93.240.122/24 | Vlan200 |
| FABRIC | l2leaf | C160064-016B305A | 10.93.240.123/24 | Vlan200 |
| FABRIC | l2leaf | C160064-016B306A | 10.93.240.124/24 | Vlan200 |
| FABRIC | l2leaf | C160064-016B307A | 10.93.240.125/24 | Vlan200 |
| FABRIC | l2leaf | C160064-016B308A | 10.93.240.126/24 | Vlan200 |
| FABRIC | l2leaf | C160064-016B309A | 10.93.240.127/24 | Vlan200 |
| FABRIC | l2leaf | C160064-016B310A | 10.93.240.128/24 | Vlan200 |
| FABRIC | l2leaf | C160064-016B311A | 10.93.240.129/24 | Vlan200 |
| FABRIC | l2leaf | C160064-016B312A | 10.93.240.130/24 | Vlan200 |
| FABRIC | l2leaf | C160064-017B301A | 10.93.240.131/24 | Vlan200 |
| FABRIC | l2leaf | C160064-017B302A | 10.93.240.132/24 | Vlan200 |
| FABRIC | l2leaf | C160064-017B303A | 10.93.240.133/24 | Vlan200 |
| FABRIC | l2leaf | C160064-017B304A | 10.93.240.134/24 | Vlan200 |
| FABRIC | l2leaf | C160064-017B305A | 10.93.240.135/24 | Vlan200 |
| FABRIC | l2leaf | C160064-017B306A | 10.93.240.136/24 | Vlan200 |
| FABRIC | l2leaf | C160064-017B307A | 10.93.240.137/24 | Vlan200 |
| FABRIC | l2leaf | C160064-020B301A | 10.93.240.138/24 | Vlan200 |
| FABRIC | l2leaf | C160064-021B301A | 10.93.240.139/24 | Vlan200 |
| FABRIC | l2leaf | C160064-022B301A | 10.93.240.140/24 | Vlan200 |
| FABRIC | l2leaf | C160064-023B301A | 10.93.240.141/24 | Vlan200 |
| FABRIC | l2leaf | C160064-024B301A | 10.93.240.142/24 | Vlan200 |
| FABRIC | l2leaf | C160064-025B301A | 10.93.240.143/24 | Vlan200 |
| FABRIC | l2leaf | C160064-026B301A | 10.93.240.144/24 | Vlan200 |
| FABRIC | l2leaf | C160064-027B301A | 10.93.240.145/24 | Vlan200 |
| FABRIC | l2leaf | C160064-028B301A | 10.93.240.146/24 | Vlan200 |
| FABRIC | l2leaf | C160064-030B301A | 10.93.240.147/24 | Vlan200 |
| FABRIC | l2leaf | C160064-031B301A | 10.93.240.148/24 | Vlan200 |
| FABRIC | l2leaf | C160064-032B301A | 10.93.240.149/24 | Vlan200 |
| FABRIC | l2leaf | C160064-033B301A | 10.93.240.150/24 | Vlan200 |
| FABRIC | l2leaf | C160064-034B301A | 10.93.240.151/24 | Vlan200 |
| FABRIC | l2leaf | C160064-035B301A | 10.93.240.152/24 | Vlan200 |
| FABRIC | l2leaf | C160064-036B301A | 10.93.240.153/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B302A | 10.93.240.11/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B303A | 10.93.240.12/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B304A | 10.93.240.14/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B305A | 10.93.240.15/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B306A | 10.93.240.16/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B307A | 10.93.240.17/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B308A | 10.93.240.18/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B309A | 10.93.240.13/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B310A | 10.93.240.19/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B311A | 10.93.240.20/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B312A | 10.93.240.21/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B313A | 10.93.240.22/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B314A | 10.93.240.23/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B315A | 10.93.240.24/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B316A | 10.93.240.25/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B317A | 10.93.240.26/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B318A | 10.93.240.27/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B319A | 10.93.240.28/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B320A | 10.93.240.29/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B321A | 10.93.240.30/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B323A | 10.93.240.31/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B324A | 10.93.240.32/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B325A | 10.93.240.33/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B326A | 10.93.240.34/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B327A | 10.93.240.35/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B328A | 10.93.240.36/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B329A | 10.93.240.37/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B330A | 10.93.240.38/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B331A | 10.93.240.39/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B332A | 10.93.240.40/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B333A | 10.93.240.41/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B334A | 10.93.240.42/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B335A | 10.93.240.43/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B336A | 10.93.240.44/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B337A | 10.93.240.45/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B338A | 10.93.240.46/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B339A | 10.93.240.47/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B340A | 10.93.240.48/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B341A | 10.93.240.49/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B342A | 10.93.240.50/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B343A | 10.93.240.51/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B344A | 10.93.240.52/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B345A | 10.93.240.53/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B346A | 10.93.240.54/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B347A | 10.93.240.55/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B348A | 10.93.240.56/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B349A | 10.93.240.57/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B350A | 10.93.240.58/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B351A | 10.93.240.59/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B352A | 10.93.240.60/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B353A | 10.93.240.61/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B354A | 10.93.240.62/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B355A | 10.93.240.64/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B356A | 10.93.240.65/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B357A | 10.93.240.66/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B358A | 10.93.240.67/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B359A | 10.93.240.68/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B360A | 10.93.240.69/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B361A | 10.93.240.70/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B362A | 10.93.240.63/24 | Vlan200 |
| FABRIC | l2leaf | C160064-037B369A | 10.93.240.154/24 | Vlan200 |
| FABRIC | l2leaf | C160064-040B301A | 10.93.240.155/24 | Vlan200 |
| FABRIC | l2leaf | C160064-041B301A | 10.93.240.156/24 | Vlan200 |
| FABRIC | l2leaf | C160064-042B301A | 10.93.240.157/24 | Vlan200 |
| FABRIC | l2leaf | C160064-043B301A | 10.93.240.158/24 | Vlan200 |
| FABRIC | l2leaf | C160064-044B301A | 10.93.240.159/24 | Vlan200 |
| FABRIC | l2leaf | C160064-045B301A | 10.93.240.160/24 | Vlan200 |
| FABRIC | l2leaf | C160064-045B302A | 10.93.240.161/24 | Vlan200 |
| FABRIC | l2leaf | C160064-045B303A | 10.93.240.162/24 | Vlan200 |
| FABRIC | l2leaf | C160064-046B301A | 10.93.240.163/24 | Vlan200 |
| FABRIC | l2leaf | C160064-046B302A | 10.93.240.164/24 | Vlan200 |
| FABRIC | l2leaf | C160064-046B303A | 10.93.240.165/24 | Vlan200 |
| FABRIC | l2leaf | C160064-047B301A | 10.93.240.166/24 | Vlan200 |
| FABRIC | l2leaf | C160064-048B301A | 10.93.240.167/24 | Vlan200 |
| FABRIC | l2leaf | C160064-048B302A | 10.93.240.168/24 | Vlan200 |
| FABRIC | l2leaf | C160064-048B303A | 10.93.240.169/24 | Vlan200 |
| FABRIC | l2leaf | C160064-048B304A | 10.93.240.170/24 | Vlan200 |
| FABRIC | l2leaf | C160064-049B301A | 10.93.240.171/24 | Vlan200 |
| FABRIC | l2leaf | C160064-049B302A | 10.93.240.172/24 | Vlan200 |
| FABRIC | l2leaf | C160064-049B303A | 10.93.240.173/24 | Vlan200 |
| FABRIC | l2leaf | C160064-049B304A | 10.93.240.174/24 | Vlan200 |
| FABRIC | l2leaf | C160064-049B305A | 10.93.240.175/24 | Vlan200 |
| FABRIC | l2leaf | C160064-049B306A | 10.93.240.176/24 | Vlan200 |
| FABRIC | l2leaf | C160064-050B301A | 10.93.240.177/24 | Vlan200 |
| FABRIC | l2leaf | C160064-050B302A | 10.93.240.178/24 | Vlan200 |
| FABRIC | l2leaf | C160064-050B303A | 10.93.240.179/24 | Vlan200 |
| FABRIC | l2leaf | C160064-050B304A | 10.93.240.180/24 | Vlan200 |
| FABRIC | l2leaf | C160064-050B305A | 10.93.240.181/24 | Vlan200 |
| FABRIC | l2leaf | C160064-050B306A | 10.93.240.182/24 | Vlan200 |
| FABRIC | l2leaf | C160064-050B307A | 10.93.240.183/24 | Vlan200 |
| FABRIC | l2leaf | C160064-051B301A | 10.93.240.184/24 | Vlan200 |
| FABRIC | l2leaf | C160064-051B302A | 10.93.240.185/24 | Vlan200 |
| FABRIC | l2leaf | C160064-051B304A | 10.93.240.186/24 | Vlan200 |
| FABRIC | l2leaf | C160064-051B305A | 10.93.240.187/24 | Vlan200 |
| FABRIC | l2leaf | C160064-051B306A | 10.93.240.188/24 | Vlan200 |
| FABRIC | l2leaf | C160064-051B307A | 10.93.240.189/24 | Vlan200 |
| FABRIC | l2leaf | C160064-056B301A | 10.93.240.190/24 | Vlan200 |
| FABRIC | l2leaf | C160064-056B302A | 10.93.240.191/24 | Vlan200 |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l2leaf | C160064-001B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet7/8/1 |
| l2leaf | C160064-001B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet7/8/1 |
| l2leaf | C160064-002B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet8/8/1 |
| l2leaf | C160064-002B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet8/8/1 |
| l2leaf | C160064-002B302A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet9/8/1 |
| l2leaf | C160064-002B302A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet9/8/1 |
| l2leaf | C160064-002B303A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet10/8/1 |
| l2leaf | C160064-002B303A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet10/8/1 |
| l2leaf | C160064-002B304A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet3/9/1 |
| l2leaf | C160064-002B304A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet3/9/1 |
| l2leaf | C160064-002B305A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet4/9/1 |
| l2leaf | C160064-002B305A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet4/9/1 |
| l2leaf | C160064-002B306A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet5/9/1 |
| l2leaf | C160064-002B306A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet5/9/1 |
| l2leaf | C160064-002B307A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet6/9/1 |
| l2leaf | C160064-002B307A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet6/9/1 |
| l2leaf | C160064-002B308A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet7/9/1 |
| l2leaf | C160064-002B308A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet7/9/1 |
| l2leaf | C160064-003B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet8/9/1 |
| l2leaf | C160064-003B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet8/9/1 |
| l2leaf | C160064-003B302A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet9/9/1 |
| l2leaf | C160064-003B302A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet9/9/1 |
| l2leaf | C160064-004B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet10/9/1 |
| l2leaf | C160064-004B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet10/9/1 |
| l2leaf | C160064-004B302A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet3/10/1 |
| l2leaf | C160064-004B302A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet3/10/1 |
| l2leaf | C160064-005B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet4/10/1 |
| l2leaf | C160064-005B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet4/10/1 |
| l2leaf | C160064-005B302A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet5/10/1 |
| l2leaf | C160064-005B302A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet5/10/1 |
| l2leaf | C160064-006B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet6/10/1 |
| l2leaf | C160064-006B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet6/10/1 |
| l2leaf | C160064-006B302A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet7/10/1 |
| l2leaf | C160064-006B302A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet7/10/1 |
| l2leaf | C160064-007B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet8/10/1 |
| l2leaf | C160064-007B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet8/10/1 |
| l2leaf | C160064-007B302A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet9/10/1 |
| l2leaf | C160064-007B302A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet9/10/1 |
| l2leaf | C160064-008B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet10/10/1 |
| l2leaf | C160064-008B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet10/10/1 |
| l2leaf | C160064-008B302A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet3/11/1 |
| l2leaf | C160064-008B302A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet3/11/1 |
| l2leaf | C160064-009B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet4/11/1 |
| l2leaf | C160064-009B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet4/11/1 |
| l2leaf | C160064-009B302A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet5/11/1 |
| l2leaf | C160064-009B302A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet5/11/1 |
| l2leaf | C160064-010B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet6/11/1 |
| l2leaf | C160064-010B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet6/11/1 |
| l2leaf | C160064-010B302A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet7/11/1 |
| l2leaf | C160064-010B302A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet7/11/1 |
| l2leaf | C160064-013B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet8/11/1 |
| l2leaf | C160064-013B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet8/11/1 |
| l2leaf | C160064-013B302A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet9/11/1 |
| l2leaf | C160064-013B302A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet9/11/1 |
| l2leaf | C160064-013B303A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet10/11/1 |
| l2leaf | C160064-013B303A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet10/11/1 |
| l2leaf | C160064-013B304A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet3/12/1 |
| l2leaf | C160064-013B304A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet3/12/1 |
| l2leaf | C160064-013B305A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet4/12/1 |
| l2leaf | C160064-013B305A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet4/12/1 |
| l2leaf | C160064-014B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet5/12/1 |
| l2leaf | C160064-014B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet5/12/1 |
| l2leaf | C160064-014B302A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet6/12/1 |
| l2leaf | C160064-014B302A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet6/12/1 |
| l2leaf | C160064-014B303A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet7/12/1 |
| l2leaf | C160064-014B303A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet7/12/1 |
| l2leaf | C160064-014B304A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet8/12/1 |
| l2leaf | C160064-014B304A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet8/12/1 |
| l2leaf | C160064-014B305A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet9/12/1 |
| l2leaf | C160064-014B305A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet9/12/1 |
| l2leaf | C160064-015B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet10/12/1 |
| l2leaf | C160064-015B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet10/12/1 |
| l2leaf | C160064-015B302A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet3/13/1 |
| l2leaf | C160064-015B302A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet3/13/1 |
| l2leaf | C160064-015B303A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet4/13/1 |
| l2leaf | C160064-015B303A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet4/13/1 |
| l2leaf | C160064-015B304A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet5/13/1 |
| l2leaf | C160064-015B304A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet5/13/1 |
| l2leaf | C160064-015B305A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet6/13/1 |
| l2leaf | C160064-015B305A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet6/13/1 |
| l2leaf | C160064-015B306A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet7/13/1 |
| l2leaf | C160064-015B306A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet7/13/1 |
| l2leaf | C160064-015B307A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet8/13/1 |
| l2leaf | C160064-015B307A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet8/13/1 |
| l2leaf | C160064-015B308A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet9/13/1 |
| l2leaf | C160064-015B308A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet9/13/1 |
| l2leaf | C160064-015B309A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet10/13/1 |
| l2leaf | C160064-015B309A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet10/13/1 |
| l2leaf | C160064-015B310A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet3/14/1 |
| l2leaf | C160064-015B310A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet3/14/1 |
| l2leaf | C160064-015B311A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet4/14/1 |
| l2leaf | C160064-015B311A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet4/14/1 |
| l2leaf | C160064-015B313A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet5/14/1 |
| l2leaf | C160064-015B313A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet5/14/1 |
| l2leaf | C160064-015B314A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet6/14/1 |
| l2leaf | C160064-015B314A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet6/14/1 |
| l2leaf | C160064-016B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet7/14/1 |
| l2leaf | C160064-016B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet7/14/1 |
| l2leaf | C160064-016B302A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet8/14/1 |
| l2leaf | C160064-016B302A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet8/14/1 |
| l2leaf | C160064-016B303A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet9/14/1 |
| l2leaf | C160064-016B303A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet9/14/1 |
| l2leaf | C160064-016B304A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet10/14/1 |
| l2leaf | C160064-016B304A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet10/14/1 |
| l2leaf | C160064-016B305A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet3/15/1 |
| l2leaf | C160064-016B305A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet3/15/1 |
| l2leaf | C160064-016B306A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet4/15/1 |
| l2leaf | C160064-016B306A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet4/15/1 |
| l2leaf | C160064-016B307A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet5/15/1 |
| l2leaf | C160064-016B307A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet5/15/1 |
| l2leaf | C160064-016B308A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet6/15/1 |
| l2leaf | C160064-016B308A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet6/15/1 |
| l2leaf | C160064-016B309A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet7/15/1 |
| l2leaf | C160064-016B309A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet7/15/1 |
| l2leaf | C160064-016B310A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet8/15/1 |
| l2leaf | C160064-016B310A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet8/15/1 |
| l2leaf | C160064-016B311A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet9/15/1 |
| l2leaf | C160064-016B311A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet9/15/1 |
| l2leaf | C160064-016B312A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet10/15/1 |
| l2leaf | C160064-016B312A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet10/15/1 |
| l2leaf | C160064-017B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet3/16/1 |
| l2leaf | C160064-017B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet3/16/1 |
| l2leaf | C160064-017B302A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet4/16/1 |
| l2leaf | C160064-017B302A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet4/16/1 |
| l2leaf | C160064-017B303A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet5/16/1 |
| l2leaf | C160064-017B303A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet5/16/1 |
| l2leaf | C160064-017B304A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet6/16/1 |
| l2leaf | C160064-017B304A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet6/16/1 |
| l2leaf | C160064-017B305A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet7/16/1 |
| l2leaf | C160064-017B305A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet7/16/1 |
| l2leaf | C160064-017B306A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet8/16/1 |
| l2leaf | C160064-017B306A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet8/16/1 |
| l2leaf | C160064-017B307A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet9/16/1 |
| l2leaf | C160064-017B307A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet9/16/1 |
| l2leaf | C160064-020B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet10/16/1 |
| l2leaf | C160064-020B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet10/16/1 |
| l2leaf | C160064-021B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet3/17/1 |
| l2leaf | C160064-021B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet3/17/1 |
| l2leaf | C160064-022B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet4/17/1 |
| l2leaf | C160064-022B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet4/17/1 |
| l2leaf | C160064-023B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet5/17/1 |
| l2leaf | C160064-023B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet5/17/1 |
| l2leaf | C160064-024B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet6/17/1 |
| l2leaf | C160064-024B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet6/17/1 |
| l2leaf | C160064-025B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet7/17/1 |
| l2leaf | C160064-025B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet7/17/1 |
| l2leaf | C160064-026B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet8/17/1 |
| l2leaf | C160064-026B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet8/17/1 |
| l2leaf | C160064-027B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet9/17/1 |
| l2leaf | C160064-027B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet9/17/1 |
| l2leaf | C160064-028B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet10/17/1 |
| l2leaf | C160064-028B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet10/17/1 |
| l2leaf | C160064-030B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet3/18/1 |
| l2leaf | C160064-030B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet3/18/1 |
| l2leaf | C160064-031B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet4/18/1 |
| l2leaf | C160064-031B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet4/18/1 |
| l2leaf | C160064-032B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet5/18/1 |
| l2leaf | C160064-032B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet5/18/1 |
| l2leaf | C160064-033B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet6/18/1 |
| l2leaf | C160064-033B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet6/18/1 |
| l2leaf | C160064-034B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet7/18/1 |
| l2leaf | C160064-034B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet7/18/1 |
| l2leaf | C160064-035B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet8/18/1 |
| l2leaf | C160064-035B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet8/18/1 |
| l2leaf | C160064-036B301A | Ethernet53/1 | l3spine | C160064-037B300A | Ethernet9/18/1 |
| l2leaf | C160064-036B301A | Ethernet54/1 | l3spine | C160064-037B301A | Ethernet9/18/1 |
| l3spine | C160064-037B300A | Ethernet3/1/1 | l2leaf | C160064-037B302A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet3/2/1 | l2leaf | C160064-037B310A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet3/3/1 | l2leaf | C160064-037B318A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet3/4/1 | l2leaf | C160064-037B327A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet3/5/1 | l2leaf | C160064-037B335A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet3/6/1 | l2leaf | C160064-037B343A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet3/7/1 | l2leaf | C160064-037B351A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet3/8/1 | l2leaf | C160064-037B358A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet3/19/1 | l2leaf | C160064-040B301A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet3/20/1 | l2leaf | C160064-046B301A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet3/21/1 | l2leaf | C160064-049B301A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet3/22/1 | l2leaf | C160064-050B303A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet3/23/1 | l2leaf | C160064-051B305A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet3/32/1 | mlag_peer | C160064-037B301A | Ethernet3/32/1 |
| l3spine | C160064-037B300A | Ethernet4/1/1 | l2leaf | C160064-037B303A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet4/2/1 | l2leaf | C160064-037B311A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet4/3/1 | l2leaf | C160064-037B319A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet4/4/1 | l2leaf | C160064-037B328A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet4/5/1 | l2leaf | C160064-037B336A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet4/6/1 | l2leaf | C160064-037B344A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet4/7/1 | l2leaf | C160064-037B352A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet4/8/1 | l2leaf | C160064-037B359A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet4/19/1 | l2leaf | C160064-041B301A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet4/20/1 | l2leaf | C160064-046B302A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet4/21/1 | l2leaf | C160064-049B302A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet4/22/1 | l2leaf | C160064-050B304A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet4/23/1 | l2leaf | C160064-051B306A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet4/32/1 | mlag_peer | C160064-037B301A | Ethernet4/32/1 |
| l3spine | C160064-037B300A | Ethernet5/1/1 | l2leaf | C160064-037B309A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet5/2/1 | l2leaf | C160064-037B312A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet5/3/1 | l2leaf | C160064-037B320A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet5/4/1 | l2leaf | C160064-037B329A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet5/5/1 | l2leaf | C160064-037B337A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet5/6/1 | l2leaf | C160064-037B345A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet5/7/1 | l2leaf | C160064-037B353A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet5/8/1 | l2leaf | C160064-037B360A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet5/19/1 | l2leaf | C160064-042B301A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet5/20/1 | l2leaf | C160064-046B303A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet5/21/1 | l2leaf | C160064-049B303A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet5/22/1 | l2leaf | C160064-050B305A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet5/23/1 | l2leaf | C160064-051B307A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet5/32/1 | mlag_peer | C160064-037B301A | Ethernet5/32/1 |
| l3spine | C160064-037B300A | Ethernet6/1/1 | l2leaf | C160064-037B304A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet6/2/1 | l2leaf | C160064-037B313A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet6/3/1 | l2leaf | C160064-037B321A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet6/4/1 | l2leaf | C160064-037B330A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet6/5/1 | l2leaf | C160064-037B338A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet6/6/1 | l2leaf | C160064-037B346A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet6/7/1 | l2leaf | C160064-037B354A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet6/8/1 | l2leaf | C160064-037B361A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet6/19/1 | l2leaf | C160064-043B301A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet6/20/1 | l2leaf | C160064-047B301A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet6/21/1 | l2leaf | C160064-049B304A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet6/22/1 | l2leaf | C160064-050B306A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet6/23/1 | l2leaf | C160064-056B301A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet6/32/1 | mlag_peer | C160064-037B301A | Ethernet6/32/1 |
| l3spine | C160064-037B300A | Ethernet7/1/1 | l2leaf | C160064-037B305A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet7/2/1 | l2leaf | C160064-037B314A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet7/3/1 | l2leaf | C160064-037B323A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet7/4/1 | l2leaf | C160064-037B331A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet7/5/1 | l2leaf | C160064-037B339A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet7/6/1 | l2leaf | C160064-037B347A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet7/7/1 | l2leaf | C160064-037B362A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet7/19/1 | l2leaf | C160064-044B301A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet7/20/1 | l2leaf | C160064-048B301A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet7/21/1 | l2leaf | C160064-049B305A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet7/22/1 | l2leaf | C160064-050B307A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet7/23/1 | l2leaf | C160064-056B302A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet7/32/1 | mlag_peer | C160064-037B301A | Ethernet7/32/1 |
| l3spine | C160064-037B300A | Ethernet8/1/1 | l2leaf | C160064-037B306A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet8/2/1 | l2leaf | C160064-037B315A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet8/3/1 | l2leaf | C160064-037B324A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet8/4/1 | l2leaf | C160064-037B332A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet8/5/1 | l2leaf | C160064-037B340A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet8/6/1 | l2leaf | C160064-037B348A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet8/7/1 | l2leaf | C160064-037B355A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet8/19/1 | l2leaf | C160064-045B301A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet8/20/1 | l2leaf | C160064-048B302A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet8/21/1 | l2leaf | C160064-049B306A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet8/22/1 | l2leaf | C160064-051B301A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet8/32/1 | mlag_peer | C160064-037B301A | Ethernet8/32/1 |
| l3spine | C160064-037B300A | Ethernet9/1/1 | l2leaf | C160064-037B307A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet9/2/1 | l2leaf | C160064-037B316A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet9/3/1 | l2leaf | C160064-037B325A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet9/4/1 | l2leaf | C160064-037B333A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet9/5/1 | l2leaf | C160064-037B341A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet9/6/1 | l2leaf | C160064-037B349A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet9/7/1 | l2leaf | C160064-037B356A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet9/19/1 | l2leaf | C160064-045B302A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet9/20/1 | l2leaf | C160064-048B303A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet9/21/1 | l2leaf | C160064-050B301A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet9/22/1 | l2leaf | C160064-051B302A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet9/32/1 | mlag_peer | C160064-037B301A | Ethernet9/32/1 |
| l3spine | C160064-037B300A | Ethernet10/1/1 | l2leaf | C160064-037B308A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet10/2/1 | l2leaf | C160064-037B317A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet10/3/1 | l2leaf | C160064-037B326A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet10/4/1 | l2leaf | C160064-037B334A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet10/5/1 | l2leaf | C160064-037B342A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet10/6/1 | l2leaf | C160064-037B350A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet10/7/1 | l2leaf | C160064-037B357A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet10/18/1 | l2leaf | C160064-037B369A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet10/19/1 | l2leaf | C160064-045B303A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet10/20/1 | l2leaf | C160064-048B304A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet10/21/1 | l2leaf | C160064-050B302A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet10/22/1 | l2leaf | C160064-051B304A | Ethernet53/1 |
| l3spine | C160064-037B300A | Ethernet10/32/1 | mlag_peer | C160064-037B301A | Ethernet10/32/1 |
| l3spine | C160064-037B301A | Ethernet3/1/1 | l2leaf | C160064-037B302A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet3/2/1 | l2leaf | C160064-037B310A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet3/3/1 | l2leaf | C160064-037B318A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet3/4/1 | l2leaf | C160064-037B327A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet3/5/1 | l2leaf | C160064-037B335A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet3/6/1 | l2leaf | C160064-037B343A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet3/7/1 | l2leaf | C160064-037B351A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet3/8/1 | l2leaf | C160064-037B358A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet3/19/1 | l2leaf | C160064-040B301A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet3/20/1 | l2leaf | C160064-046B301A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet3/21/1 | l2leaf | C160064-049B301A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet3/22/1 | l2leaf | C160064-050B303A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet3/23/1 | l2leaf | C160064-051B305A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet4/1/1 | l2leaf | C160064-037B303A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet4/2/1 | l2leaf | C160064-037B311A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet4/3/1 | l2leaf | C160064-037B319A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet4/4/1 | l2leaf | C160064-037B328A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet4/5/1 | l2leaf | C160064-037B336A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet4/6/1 | l2leaf | C160064-037B344A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet4/7/1 | l2leaf | C160064-037B352A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet4/8/1 | l2leaf | C160064-037B359A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet4/19/1 | l2leaf | C160064-041B301A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet4/20/1 | l2leaf | C160064-046B302A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet4/21/1 | l2leaf | C160064-049B302A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet4/22/1 | l2leaf | C160064-050B304A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet4/23/1 | l2leaf | C160064-051B306A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet5/1/1 | l2leaf | C160064-037B309A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet5/2/1 | l2leaf | C160064-037B312A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet5/3/1 | l2leaf | C160064-037B320A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet5/4/1 | l2leaf | C160064-037B329A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet5/5/1 | l2leaf | C160064-037B337A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet5/6/1 | l2leaf | C160064-037B345A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet5/7/1 | l2leaf | C160064-037B353A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet5/8/1 | l2leaf | C160064-037B360A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet5/19/1 | l2leaf | C160064-042B301A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet5/20/1 | l2leaf | C160064-046B303A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet5/21/1 | l2leaf | C160064-049B303A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet5/22/1 | l2leaf | C160064-050B305A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet5/23/1 | l2leaf | C160064-051B307A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet6/1/1 | l2leaf | C160064-037B304A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet6/2/1 | l2leaf | C160064-037B313A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet6/3/1 | l2leaf | C160064-037B321A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet6/4/1 | l2leaf | C160064-037B330A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet6/5/1 | l2leaf | C160064-037B338A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet6/6/1 | l2leaf | C160064-037B346A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet6/7/1 | l2leaf | C160064-037B354A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet6/8/1 | l2leaf | C160064-037B361A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet6/19/1 | l2leaf | C160064-043B301A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet6/20/1 | l2leaf | C160064-047B301A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet6/21/1 | l2leaf | C160064-049B304A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet6/22/1 | l2leaf | C160064-050B306A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet6/23/1 | l2leaf | C160064-056B301A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet7/1/1 | l2leaf | C160064-037B305A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet7/2/1 | l2leaf | C160064-037B314A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet7/3/1 | l2leaf | C160064-037B323A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet7/4/1 | l2leaf | C160064-037B331A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet7/5/1 | l2leaf | C160064-037B339A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet7/6/1 | l2leaf | C160064-037B347A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet7/7/1 | l2leaf | C160064-037B362A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet7/19/1 | l2leaf | C160064-044B301A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet7/20/1 | l2leaf | C160064-048B301A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet7/21/1 | l2leaf | C160064-049B305A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet7/22/1 | l2leaf | C160064-050B307A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet7/23/1 | l2leaf | C160064-056B302A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet8/1/1 | l2leaf | C160064-037B306A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet8/2/1 | l2leaf | C160064-037B315A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet8/3/1 | l2leaf | C160064-037B324A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet8/4/1 | l2leaf | C160064-037B332A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet8/5/1 | l2leaf | C160064-037B340A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet8/6/1 | l2leaf | C160064-037B348A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet8/7/1 | l2leaf | C160064-037B355A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet8/19/1 | l2leaf | C160064-045B301A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet8/20/1 | l2leaf | C160064-048B302A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet8/21/1 | l2leaf | C160064-049B306A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet8/22/1 | l2leaf | C160064-051B301A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet9/1/1 | l2leaf | C160064-037B307A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet9/2/1 | l2leaf | C160064-037B316A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet9/3/1 | l2leaf | C160064-037B325A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet9/4/1 | l2leaf | C160064-037B333A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet9/5/1 | l2leaf | C160064-037B341A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet9/6/1 | l2leaf | C160064-037B349A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet9/7/1 | l2leaf | C160064-037B356A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet9/19/1 | l2leaf | C160064-045B302A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet9/20/1 | l2leaf | C160064-048B303A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet9/21/1 | l2leaf | C160064-050B301A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet9/22/1 | l2leaf | C160064-051B302A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet10/1/1 | l2leaf | C160064-037B308A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet10/2/1 | l2leaf | C160064-037B317A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet10/3/1 | l2leaf | C160064-037B326A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet10/4/1 | l2leaf | C160064-037B334A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet10/5/1 | l2leaf | C160064-037B342A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet10/6/1 | l2leaf | C160064-037B350A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet10/7/1 | l2leaf | C160064-037B357A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet10/18/1 | l2leaf | C160064-037B369A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet10/19/1 | l2leaf | C160064-045B303A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet10/20/1 | l2leaf | C160064-048B304A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet10/21/1 | l2leaf | C160064-050B302A | Ethernet54/1 |
| l3spine | C160064-037B301A | Ethernet10/22/1 | l2leaf | C160064-051B304A | Ethernet54/1 |

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
| FABRIC | C160064-037B300A | 169.27.195.1/32 |
| FABRIC | C160064-037B301A | 169.27.195.2/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------ | ------------------- | ------------------ | ------------------ |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
