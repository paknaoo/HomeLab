# 🧪 Enterprise-Style Home Lab – Network \& Security Build



Author: Adam \
Purpose: Enterprise-style lab for System Administration, Red Team & Blue Team practice \
Platform: VirtualBox \
Firewall: pfSense \
Segmentation: LAN / DMZ / ATTACK \

# 📌 1. Network Design \& IP Addressing Plan



## 🏗 Architecture Overview





## 🌐 Network Segments

Segment		Purpose				Subnet			Gateway		Notes

WAN		Simulated Internet		DHCP (VirtualBox NAT)	Auto		External access
LAN		Internal Corporate Network	192.168.10.0/24		192.168.10.1	AD, Clients
DMZ		Public Services			192.168.20.0/24		192.168.20.1	Web, exposed services
ATTACK		Red Team Network		192.168.30.0/24		192.168.30.1	Kali Linux

## 🔐 Security Design Principles

Network segmentation
Default deny between zones
Controlled access from ATTACK → DMZ
No direct DMZ → LAN communication
Centralized routing via firewall

Firewall: pfSense

## 🔌 Network Adapter Layout (pfSense VM)

Adapter		Type		Name		Purpose

Adapter 1	NAT			—		WAN
Adapter 2	Internal Network	LAB\_LAN		LAN
Adapter 3	Internal Network	LAB\_DMZ		DMZ
Adapter 4	Internal Network	LAB\_ATTACK	ATTACK

## 🖥 Other VMs Network Assignment

Machine				Network
Domain Controller	LAB\_LAN
Windows Client		LAB\_LAN
Web Server			LAB\_DMZ
Kali Linux			LAB\_ATTACK

# 📌 3. pfSense Installation \& Configuration

Software: 
pfSense

## 🔧 Installation Steps

Download pfSense ISO
Create VM (2 vCPU, 4GB RAM recommended)
Attach 4 network adapters
Boot and install
Assign interfaces:
	WAN → Adapter 1
	LAN → Adapter 2
	OPT1 → DMZ
	OPT2 → ATTACK

## 🌍 Interface Configuration

Interface	IP	 				Address	DHCP

WAN			DHCP				No
LAN			192.168.10.1/24		Enabled
DMZ			192.168.20.1/24		Optional
ATTACK		192.168.30.1/24		Enabled

## 🔥 Basic Firewall Rules (Initial)

LAN
Allow → Any (initial setup phase)

DMZ
Allow → WAN (HTTP/HTTPS only)
Block → LAN

ATTACK
Allow → DMZ
Allow → WAN
Block → LAN (optional for realism)

# 📌 4. Domain Controller Deployment

OS:
Windows Server

## 🖥 VM Configuration

Network: LAB\_LAN
Static IP: 192.168.10.10
DNS: 192.168.10.10
Gateway: 192.168.10.1

## 🔐 Roles to Install

Active Directory Domain Services (AD DS)
DNS Server

## 🌳 Domain Design

Setting			Value

Domain Name		corp.local
NetBIOS			CORP
Forest Level	Latest supported

# 📌 5. Client Machines

OS:
Windows 10 or Windows 11

## 🖥 Configuration

Network: LAB\_LAN
DHCP or Static
DNS: 192.168.10.10
Join domain: corp.local

# 🎯 Post-Join Configuration

Create test users
Apply GPO
Enable RDP
Install Sysmon (optional for Blue Team phase)

# 📌 6. Kali Linux Deployment

OS:
Kali Linux

## 🖥 Configuration

Network: LAB\_ATTACK
DHCP enabled
Gateway: 192.168.30.1

## 🔴 Usage Purpose
Network scanning (nmap)
Exploitation testing
Lateral movement simulation
Brute force attacks
Pivoting through DMZ

# 📌 Lab Phase 1 Goals

Validate routing between segments
Test firewall segmentation
Join client to domain
Test ATTACK → DMZ access
Confirm DMZ cannot reach LAN
Capture logs on firewall

# 📌 Future Expansion

IDS/IPS (Suricata)
SIEM (Wazuh / ELK)
VPN access
VLAN tagging
Honeypots
EDR simulation
SOC monitoring stack

# 🎯 End State Objective

Create a realistic enterprise lab environment suitable for:
🛠 System Administration practice
🔴 Red Team exercises
🔵 Blue Team detection \& response
📊 Security monitoring implementation

📁 Portfolio \& GitHub documentation

