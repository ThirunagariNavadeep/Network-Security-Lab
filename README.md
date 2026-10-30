# Network Security Lab — Cisco Packet Tracer

## Project Overview

This project demonstrates basic enterprise network segmentation and access control using Cisco Packet Tracer.

The network is divided into three VLANs — Admin, Employee, and Guest — to isolate departments and control communication between devices. Inter-VLAN routing is implemented using router-on-a-stick, and an extended Access Control List (ACL) restricts Guest access to the Admin PC.

## Objectives

- Create separate VLANs for different user groups.
- Configure 802.1Q trunking between the switch and router.
- Enable inter-VLAN communication using router subinterfaces.
- Implement ACL-based traffic filtering.
- Verify network connectivity and access restrictions.

## Network Architecture

| Device | Configuration |
|---|---|
| Router | Cisco 2911 |
| Switch | Cisco 2960 |
| End devices | 3 PCs |
| Routing | Router-on-a-stick |
| VLAN trunking | IEEE 802.1Q |
| Security | Extended IPv4 ACL |

## VLAN and IP Addressing

| Department | VLAN | Network | Device IP | Default Gateway |
|---|---:|---|---|---|
| Admin | 10 | 192.168.10.0/24 | 192.168.10.10 | 192.168.10.1 |
| Employee | 20 | 192.168.20.0/24 | 192.168.20.20 | 192.168.20.1 |
| Guest | 30 | 192.168.30.0/24 | 192.168.30.30 | 192.168.30.1 |

## Network Configuration

### 1. VLAN Configuration

Created three VLANs on the Cisco 2960 switch:

- VLAN 10 — ADMIN
- VLAN 20 — EMPLOYEE
- VLAN 30 — GUEST

Assigned switch access ports:

- Fa0/1 → VLAN 10
- Fa0/2 → VLAN 20
- Fa0/3 → VLAN 30

### 2. Trunk Configuration

Configured the switch port connected to the router as an 802.1Q trunk.

### 3. Inter-VLAN Routing

Configured router subinterfaces:

- GigabitEthernet0/0.10 — 192.168.10.1
- GigabitEthernet0/0.20 — 192.168.20.1
- GigabitEthernet0/0.30 — 192.168.30.1

### 4. Access Control List (ACL)

Implemented Extended ACL 100 and applied it inbound on router subinterface GigabitEthernet0/0.30.

Security policy:

- Block Guest PC access to the Admin PC.
- Allow Guest PC communication with the Employee PC.
- Permit ICMP echo replies required for Admin-initiated ping tests.

The ACL permits the required ICMP echo replies before denying other Guest-to-Admin IP traffic, followed by a permit rule for other traffic.

## Testing and Verification

| Test Case | Expected Result | Observed Result |
|---|---|---|
| Admin → Router Gateway | Successful | Passed |
| Admin → Employee | Allowed | Passed |
| Admin → Guest | Allowed | Passed |
| Guest → Admin | Blocked | Passed |
| Guest → Employee | Allowed | Passed |

Connectivity was verified using the `ping` command from the Packet Tracer PCs.

## Screenshots

### 1. Network Topology

![Network Topology](https://github.com/ThirunagariNavadeep/Network-Security-Lab/blob/8cbedf298e93b18ac68688702a76bc9be973997e/Screenshots/Topology.png)

### 2. VLAN Configuration

![VLAN Configuration](https://github.com/ThirunagariNavadeep/Network-Security-Lab/blob/07f93807e97d6b112790adb89320f44b064dcb57/Screenshots/Vlan_Configuration.png)

### 3. Router Interfaces

![Router Interfaces](https://github.com/ThirunagariNavadeep/Network-Security-Lab/blob/91cb45f7783e2880e5bf2d1b8c38ecee0f53b416/Screenshots/router-interfaces.png)

### 4. Guest-to-Admin Access Blocked

![Guest Blocked](https://github.com/ThirunagariNavadeep/Network-Security-Lab/blob/f95b355c60563720ed7c385dadcf92006347efda/Screenshots/guest-blocked.png)

### 5. Guest-to-Employee Access Allowed

![Guest Employee Allowed](screenshots/guest-employee-allowed.png)

## Technologies Used

- Cisco Packet Tracer
- Cisco IOS CLI
- VLANs
- IEEE 802.1Q
- Inter-VLAN Routing
- Extended Access Control Lists (ACLs)
- IPv4 Addressing and Subnetting

## How to Run

1. Install Cisco Packet Tracer.
2. Clone or download this repository.
3. Open `Network_Security_Lab.pkt` in Cisco Packet Tracer.
4. Inspect the router, switch, VLAN, and ACL configurations.
5. Use the PC command prompts to repeat the connectivity tests.

## Key Learnings

- Configuring VLAN-based network segmentation.
- Understanding access and trunk ports.
- Implementing router-on-a-stick.
- Applying extended ACLs to control network traffic.
- Troubleshooting connectivity using Cisco IOS commands.

## Author

**Navadeep Thirunagari**

GitHub: [ThirunagariNavadeep](https://github.com/ThirunagariNavadeep)
