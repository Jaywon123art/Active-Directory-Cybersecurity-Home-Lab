# VirtualBox Installation and Setup

This document describes the installation and initial configuration of Oracle VirtualBox for my Active Directory Cybersecurity Home Lab. VirtualBox provides the virtualisation platform used to create and manage the lab's virtual machines.

## Host System Specifications
- Manufacturer: Lenovo
- Model: ThinkPad T470
- Processor: Intel Core i5
- Operating System: Windows 10
- RAM: 8 GB
- Storage: 238 GB SSD
- Available Storage (Latest Recorded): 128 GB

## VirtualBox Installation
- Virtualization Software: Oracle VirtualBox
- Installation Status: Successful
- Host Operating System: Windows 10
- VirtualBox Manager: Installed and accessible.
- Purpose: Create, configure and manage virtual machines.

## Lab Directory Structure
- Main Directory: C:\Cybersecurity-Home-Lab
- Virtual Machines: C:\Cybersecurity-Home-Lab\Virtual Machines
- ISO Files: C:\Cybersecurity-Home-Lab\ISO Files
- Snapshots: C:\Cybersecurity-Home-Lab\Snapshots
- Tools: C:\Cybersecurity-Home-Lab\Tools

## Virtual Network Configuration

Add:

AD-LAB
- Network Type: Internal Network
- Purpose: Private communication between lab virtual machines.
NAT-LAB
- Network Type: NAT Network
- Subnet: 10.10.10.0/24
- Gateway: 10.10.10.1
- DHCP: Enabled
- Purpose: Provides external network access through VirtualBox NAT

## Virtual Machines Created
- DC01: Windows Server 2022 Standard Evaluation.
- CL01: Windows 7 Professional 64-bit.
- CL02: Windows 7 Professional 64-bit.
- KALI01: Planned for future cybersecurity testing.

## Installation Verification
- VirtualBox Manager launches successfully.
- Virtual machines can be created and configured.
- Virtual machine network adapters can be configured.
- The lab directory structure is available.
- VirtualBox is ready for Active Directory lab operations.
