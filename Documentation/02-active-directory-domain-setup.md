# 02 – Active Directory Domain Setup

## 1. Overview

This phase covers the installation and configuration of Active Directory Domain Services (AD DS) and DNS on the Windows Server 2022 virtual machine (DC01).

The objective is to establish a Windows domain environment for centralized user, computer, and network management.

## 2. Lab Configuration

| Item | Configuration |
|---|---|
| Server Name | DC01 |
| Operating System | Windows Server 2022 Standard Evaluation |
| Domain Name | corp.in |
| NetBIOS Name | CORP |
| Static IP Address | 192.168.56.10 |
| DNS Server | 192.168.56.10 |
| Internal Network | AD-LAB |

## 3. Active Directory Domain Services

The Active Directory Domain Services (AD DS) role was installed on DC01.

AD DS provides centralized authentication, authorization, and management of users, computers, and other network resources.

## 4. DNS Configuration

DNS was installed and configured as part of the domain controller setup.

DNS translates domain names into IP addresses and helps domain-joined computers locate Active Directory services.

DC01 uses its static IP address, `192.168.56.10`, as its DNS server.

## 5. Domain Controller Promotion

DC01 was promoted to a Domain Controller by creating a new forest.

The following configuration was used:

- Root domain name: `corp.in`
- NetBIOS domain name: `CORP`
- Server: `DC01`

This established the first domain controller for the lab environment.

## 6. Verification

The following configurations were confirmed:

- DC01 was configured as a Domain Controller.
- The `corp.in` domain was created successfully.
- DNS was installed and configured.
- The server used the static IP address `192.168.56.10`.
- Client computers were subsequently able to join the domain.

## 7. Practical Importance

This setup provides the foundation for practicing:

- Centralized identity and access management.
- User and computer account administration.
- Group Policy management.
- DNS administration.
- Active Directory security and troubleshooting.

## 8. Project Maintainer

**Maintainer:** [@Jaywon123art](https://github.com/Jaywon123art)  
**Project:** Active Directory Cybersecurity Home Lab
