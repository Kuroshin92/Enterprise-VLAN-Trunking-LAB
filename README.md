# Enterprise VLAN & 802.1Q Trunking Configuration Lab
## 📌 Overview
### This lab simulates a multi-switch enterprise environment implementing VLAN segmentation, management VLAN configuration, and 802.1Q trunking.

## The objective was to design and configure secure VLAN segmentation across three switches while validating inter-switch communication and Layer 2 isolation.

## 🏢 Network Design
Three Cisco Switches(SW1, SW2, SW3) were configured with:
- VLAN 10 - Faculty/Staff
- VLAN 20 - Students
- VLAN 30 - Guest 
- VLAN 99 - Management
Native VLAN configured as VLAN 99 for trunk links. 

## Management IP addressing:
Switch          VLAN 99 IP
- SW1             172.17.99.11
- SW2             172.17.99.12
- SW3             172.17.99.13

## ⚙️Key Configurations
VLAN Creation 
```
  vlan 10
  name faculty/staff
  vlan 20
  name students
  vlan 30
  name  guest
  vlan 99 
  name management
  ```
## Access Port Assignment
```
SW2 & SW3
interface fa0/11
switchport access vlan 10
interface fa0/18
switchport access vlan 20
interface fa0/6
swithcport access vlan 30
```
## Port security 
```
SW1
interface range fa0/6-24, gi0/1-2
description Not in Use
shutdown

SW2 & SW3
interface range fa0/7-10,fa0/12-17,fa0/19-24,gi0/1-2
description Not in Use
shutdown
```
## Trunk Configuration
```
SW1
interface range fa0/1-5
switchport mode trunk
switchport trunk native vlan 99

SW2 & SW3
interface range fa0/1-5
switchport mode trunk
switchport trunk native vlan 99
```
## Management VLAN Interface
```
SW1
interface vlan 99
ip address 172.17.99.11 255.255.0.0
no shutdown

SW2
interface vlan 99
ip address 172.17.99.12 255.255.0.0
no shutdown

SW3
interface vlan 99
ip address 172.17.99.13 255.255.0.0
no shutdown
```
## 🔎 Verification & Testing
# ✔️ Verified VLAN creation using:
```
show vlan brief
```
# ✔️ Verified Trunk configuration using:
```
show interface trunk
```
✔️ Tested switch-to-switch connectivity via VLAN 99 management network
✔️ Verified that devices in different VLANs could **NOT** communicate without Layer 3 routing
✔️ Reassigned ports to validate VLAN mobility behavior

## Key Concepts Reinforced 
- VLAN segmentation reduces broadcast domains
- Native VLAN best practice (avoid VLAN 1)
- 802.1Q trunking between switches
- Management VLAN security considerations

<img width="796" height="355" alt="image" src="https://github.com/user-attachments/assets/d529d708-0473-4f66-802a-4d7853a11600" />

