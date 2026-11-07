# Network Configuration

This document describes the network configuration of my Active Directory Cybersecurity Home Lab. It covers the virtual networks, IP addressing, DNS configuration and communication between the virtual machines.

## VirtualBox Networks

### AD-LAB
- Network Type: Internal Network
- Purpose: Private communication between lab virtual machines.
- Network Name: AD-LAB
### NAT-LAB
- Network Type: NAT Network
- Purpose: Provides network access through VirtualBox NAT.
- Network Name: NAT-LAB
- Subnet: 10.10.10.0/24
- Gateway: 10.10.10.1
- DHCP: Enabled

## IP Addressing

### DC01
- IP Address: 192.168.56.10
- Role: Domain Controller and DNS Server
### CL01
- IP Address: 192.168.56.101
- Role: Domain Client
### CL02
- IP Address: 192.168.56.102
- Role: Domain Client
### KALI01
- IP Address: 192.168.56.50
- Role: Cybersecurity Testing Machine
- Status: Planned

## Domain and DNS Configuration

### Active Directory Domain
- Domain Name: corp.in
- NetBIOS Name: CORP
- Domain Controller: DC01
### DNS Configuration
- DNS Server: 192.168.56.10
- Primary DNS Host: DC01
- DNS Purpose: Resolves domain names and supports Active Directory services.

## Network Communication
- AD-LAB provides a private network for communication between lab virtual machines.
- NAT-LAB provides network access through VirtualBox NAT.
- DC01 provides Active Directory and DNS services.
- CL01 and CL02 communicate with DC01 for domain authentication and DNS resolution.
- KALI01 is planned for future cybersecurity testing.

## Network Security
- Keep lab systems isolated from untrusted networks.
- Use NAT only when external network access is required.
- Avoid exposing the Domain Controller directly to the internet.
- Perform cybersecurity testing only on authorised lab systems.
- Verify network connectivity and DNS resolution when troubleshooting.
