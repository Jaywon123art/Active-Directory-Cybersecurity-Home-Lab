# Lab Overview

This document provides an overview of my Active Directory Cybersecurity Home Lab. The lab is designed to simulate a small corporate IT environment where I can practise Windows Server administration, Active Directory management, network configuration, Group Policy, file sharing and security auditing.

## Host Machine

- Manufacturer: Lenovo
- Model: ThinkPad T470
- Processor: Intel Core i5
- Operating System: Windows 10
- RAM: 8 GB
- Available Storage: 128 GB
- Virtualization Software: Oracle VirtualBox

## Virtual Machines

DC01
- Operating System: Windows Server 2022 Standard Evaluation
- Role: Domain Controller and DNS Server
- IP Address: 192.168.56.10
CL01
- Operating System: Windows 7 Professional 64-bit
- Role: Domain-joined client
- IP Address: 192.168.56.101
CL02
- Operating System: Windows 7 Professional 64-bit
- Role: Domain-joined client
- IP Address: 192.168.56.102
KALI01
- Operating System: Kali Linux
- Role: Cybersecurity testing machine
- IP Address: 192.168.56.50
- Status: Planned

## Network Configuration

Domain Information
- Domain Name: corp.in
- NetBIOS Name: CORP
- DNS Server: 192.168.56.10
VirtualBox Networks
- Internal Network: AD-LAB
- NAT Network: NAT-LAB
- NAT Subnet: 10.10.10.0/24
- NAT Gateway: 10.10.10.1
- DHCP: Enabled on NAT-LAB

## Completed Configurations

- Installed and configured Oracle VirtualBox.
- Installed Windows Server 2022.
- Installed Active Directory Domain Services (AD DS).
- Configured DNS and created the corp.in domain.
- Joined CL01 and CL02 to the domain.
- Created Active Directory Organizational Units (OUs), users and security groups.
- Configured departmental file shares and access permissions.
- Implemented domain password and account lockout policies.
- Configured Group Policy restrictions for HR users.
- Implemented USB storage restrictions on CL01.
- Configured security auditing and verified Windows Security Events.

## Lab Safety and Isolation

- The lab is intended for educational and authorised cybersecurity practice.
- Windows 7 clients are unsupported and must remain isolated from untrusted networks.
- Security testing will be conducted only within the lab environment.
- Passwords, private keys and API credentials must never be published on GitHub.
