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
| FABRIC | l3leaf | DC31_L3_LEAF_1_1 | 172.19.180.11/20 | cEOS-lab | Provisioned | - |
| FABRIC | l3leaf | DC31_L3_LEAF_1_2 | 172.19.180.12/20 | cEOS-lab | Provisioned | - |
| FABRIC | l3leaf | DC31_L3_LEAF_2_1 | 172.19.180.21/20 | cEOS-lab | Provisioned | - |
| FABRIC | l3leaf | DC31_L3_LEAF_2_2 | 172.19.180.22/20 | cEOS-lab | Provisioned | - |
| FABRIC | spine | DC31_SPINE_1 | 172.19.180.1/20 | cEOS-lab | Provisioned | - |
| FABRIC | spine | DC31_SPINE_2 | 172.19.180.2/20 | cEOS-lab | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | DC31_L3_LEAF_1_1 | Ethernet1 | spine | DC31_SPINE_1 | Ethernet1 |
| l3leaf | DC31_L3_LEAF_1_1 | Ethernet2 | spine | DC31_SPINE_2 | Ethernet1 |
| l3leaf | DC31_L3_LEAF_1_1 | Ethernet7 | mlag_peer | DC31_L3_LEAF_1_2 | Ethernet7 |
| l3leaf | DC31_L3_LEAF_1_1 | Ethernet8 | mlag_peer | DC31_L3_LEAF_1_2 | Ethernet8 |
| l3leaf | DC31_L3_LEAF_1_2 | Ethernet1 | spine | DC31_SPINE_1 | Ethernet2 |
| l3leaf | DC31_L3_LEAF_1_2 | Ethernet2 | spine | DC31_SPINE_2 | Ethernet2 |
| l3leaf | DC31_L3_LEAF_2_1 | Ethernet1 | spine | DC31_SPINE_1 | Ethernet3 |
| l3leaf | DC31_L3_LEAF_2_1 | Ethernet2 | spine | DC31_SPINE_2 | Ethernet3 |
| l3leaf | DC31_L3_LEAF_2_1 | Ethernet7 | mlag_peer | DC31_L3_LEAF_2_2 | Ethernet7 |
| l3leaf | DC31_L3_LEAF_2_1 | Ethernet8 | mlag_peer | DC31_L3_LEAF_2_2 | Ethernet8 |
| l3leaf | DC31_L3_LEAF_2_2 | Ethernet1 | spine | DC31_SPINE_1 | Ethernet4 |
| l3leaf | DC31_L3_LEAF_2_2 | Ethernet2 | spine | DC31_SPINE_2 | Ethernet4 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 10.255.255.0/27 | 32 | 16 | 50.0 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| DC31_L3_LEAF_1_1 | Ethernet1 | 10.255.255.1/31 | DC31_SPINE_1 | Ethernet1 | 10.255.255.0/31 |
| DC31_L3_LEAF_1_1 | Ethernet2 | 10.255.255.3/31 | DC31_SPINE_2 | Ethernet1 | 10.255.255.2/31 |
| DC31_L3_LEAF_1_2 | Ethernet1 | 10.255.255.5/31 | DC31_SPINE_1 | Ethernet2 | 10.255.255.4/31 |
| DC31_L3_LEAF_1_2 | Ethernet2 | 10.255.255.7/31 | DC31_SPINE_2 | Ethernet2 | 10.255.255.6/31 |
| DC31_L3_LEAF_2_1 | Ethernet1 | 10.255.255.9/31 | DC31_SPINE_1 | Ethernet3 | 10.255.255.8/31 |
| DC31_L3_LEAF_2_1 | Ethernet2 | 10.255.255.11/31 | DC31_SPINE_2 | Ethernet3 | 10.255.255.10/31 |
| DC31_L3_LEAF_2_2 | Ethernet1 | 10.255.255.13/31 | DC31_SPINE_1 | Ethernet4 | 10.255.255.12/31 |
| DC31_L3_LEAF_2_2 | Ethernet2 | 10.255.255.15/31 | DC31_SPINE_2 | Ethernet4 | 10.255.255.14/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 10.255.0.0/27 | 32 | 6 | 18.75 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| FABRIC | DC31_L3_LEAF_1_1 | 10.255.0.3/32 |
| FABRIC | DC31_L3_LEAF_1_2 | 10.255.0.4/32 |
| FABRIC | DC31_L3_LEAF_2_1 | 10.255.0.5/32 |
| FABRIC | DC31_L3_LEAF_2_2 | 10.255.0.6/32 |
| FABRIC | DC31_SPINE_1 | 10.255.0.1/32 |
| FABRIC | DC31_SPINE_2 | 10.255.0.2/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------ | ------------------- | ------------------ | ------------------ |
| 10.255.1.0/27 | 32 | 4 | 12.5 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| FABRIC | DC31_L3_LEAF_1_1 | 10.255.1.3/32 |
| FABRIC | DC31_L3_LEAF_1_2 | 10.255.1.3/32 |
| FABRIC | DC31_L3_LEAF_2_1 | 10.255.1.5/32 |
| FABRIC | DC31_L3_LEAF_2_2 | 10.255.1.5/32 |
