# Active Directory Cybersecurity Home Lab

A hands-on cybersecurity and Windows infrastructure lab built with Oracle VM VirtualBox. This repository documents the design, configuration, testing, and lessons learned while building a small Active Directory domain from the ground up.

> **Project status:** In progress  
> **Environment:** Personal, isolated learning lab  
> **Domain:** `corp.in`

## Project goals

- Build and administer a Windows Server 2022 Active Directory domain.
- Configure DNS, domain-joined Windows clients, and a segmented virtual network.
- Practice organizational unit (OU), user, and security-group administration.
- Configure departmental file shares with both SMB share and NTFS permissions.
- Apply and validate Group Policy security controls.
- Enable Windows security auditing and investigate authentication events.
- Develop practical troubleshooting, documentation, and defensive-security skills.

## Lab environment

### Host machine

| Component | Configuration |
|---|---|
| Laptop | Lenovo ThinkPad T470 |
| Host operating system | Windows 10 |
| Processor | Intel Core i5 |
| Memory | 8 GB RAM |
| Storage | SSD |

The host has limited memory, so the virtual machines are run selectively rather than all at once.

### Virtual machines

| Machine | Operating system | Role | Lab network address |
|---|---|---|---|
| DC01 | Windows Server 2022 Standard Evaluation (Desktop Experience) | Domain Controller and DNS | 192.168.56.10 |
| CL01 | Windows 7 Professional 64-bit | Domain client | 192.168.56.101 |
| CL02 | Windows 7 Professional 64-bit | Domain client | 192.168.56.102 |
| KALI01 | Kali Linux | Planned security-testing workstation | 192.168.56.50 (planned) |

### Virtual networking

| Network | Type | Purpose |
|---|---|---|
| AD-LAB | VirtualBox Internal Network | Isolated communication between the domain controller and Windows clients |
| NAT-LAB | VirtualBox NAT Network | Controlled outbound connectivity for the domain controller |

- NAT-LAB subnet: `10.10.10.0/24`
- NAT-LAB gateway: `10.10.10.1`
- Active Directory domain: `corp.in`
- NetBIOS name: `CORP`
- Domain DNS server: `192.168.56.10`

The Windows 7 clients are attached to the isolated AD-LAB network and are not intentionally given direct public-internet access.

## Work completed

The following exercises have been configured and tested in the lab.

### 1. VirtualBox and lab foundation

- Installed VirtualBox on the Windows 10 host.
- Created an organized folder structure for virtual machines, ISO files, snapshots, and tools.
- Created the AD-LAB internal network and NAT-LAB NAT network.
- Defined the virtual machine roles and IP addressing plan.

### 2. Windows Server and Active Directory

- Installed Windows Server 2022 Standard Evaluation with Desktop Experience.
- Renamed the server to `DC01`.
- Configured its lab network interface with a static IP address.
- Installed the Active Directory Domain Services and DNS Server roles.
- Promoted DC01 to a domain controller and created the `corp.in` forest.
- Verified domain DNS resolution and ran a DNS diagnostic check.

### 3. Domain client deployment

- Created two Windows 7 Professional virtual machines, CL01 and CL02.
- Configured static IP addresses and pointed both clients to the domain DNS server.
- Joined both clients to `corp.in`.
- Confirmed that both computer accounts appeared in Active Directory Users and Computers.

### 4. Organizational units, users, and groups

Created a company OU structure with departmental OUs for IT, HR, and Finance, along with separate Users, Computers, and Groups OUs.

Created fictional lab user accounts and matching global security groups:

| Department | Example lab account | Security group |
|---|---|---|
| IT | `James.IT` | `IT_Staff` |
| HR | `Sarah.HR` | `HR_Staff` |
| Finance | `David.FIN` | `Finance_Staff` |

Added each test account to its corresponding departmental security group.

### 5. Departmental file sharing and access control

- Created separate IT, HR, and Finance folders on DC01.
- Shared the folders over SMB.
- Configured share permissions and NTFS permissions for the corresponding departmental groups.
- Tested access from a domain client using each departmental test account.

**Validation results:**

| Test account | IT share | HR share | Finance share |
|---|---|---|---|
| `James.IT` | Allowed | Denied | Denied |
| `Sarah.HR` | Denied | Allowed | Denied |
| `David.FIN` | Denied | Denied | Allowed |

The tests demonstrated that access was restricted by the combined effect of SMB share permissions and NTFS permissions.

### 6. Domain password and account lockout policy

Configured the domain password and account lockout settings through Group Policy:

| Policy | Lab setting |
|---|---:|
| Minimum password length | 12 characters |
| Password history | 10 passwords |
| Minimum password age | 1 day |
| Maximum password age | 90 days |
| Password complexity | Enabled |
| Account lockout threshold | 5 invalid attempts |
| Account lockout duration | 10 minutes |
| Reset lockout counter after | 10 minutes |

Ran policy updates and verified the applicable domain account settings. Also tested password rejection and acceptance using a lab account.

These values are used for this learning exercise and should not be treated as a universal production password-policy recommendation.

### 7. Group Policy restrictions

**HR Control Panel restriction**
- Created and linked `GPO-HR-ControlPanel-Restriction` to the HR OU.
- Enabled the policy that prohibits access to Control Panel and PC settings.
- Confirmed that the HR test account was restricted while an IT test account was not.

**CL01 removable-storage restriction**
- Created and linked `GPO-CL01-USB-Restriction` to the custom Computers OU.
- Configured removable-disk read, write, and execute restrictions.
- Confirmed that the policy applied to CL01.
- Tested a USB flash drive passed through to CL01 and confirmed that access was denied.
- Confirmed that CL02, which was outside the targeted OU, could still access the USB drive.

### 8. Windows security auditing and account lockout monitoring

- Created and linked `GPO-CL01-Security-Auditing`.
- Enabled auditing of successful and failed logon events.
- Generated test logon activity and examined the Security log on CL01.
- Reviewed relevant Windows Security event IDs, including 4624 (successful logon) and 4625 (failed logon).
- Deliberately entered an incorrect password five times for a dedicated test account.
- Confirmed the domain account lockout event (Event ID 4740) on DC01.
- Identified the originating client computer in the event details.
- Unlocked the test account through Active Directory Users and Computers.

## Skills practiced

- VirtualBox virtual machine and network configuration
- Windows Server 2022 administration
- Active Directory Domain Services
- DNS configuration and troubleshooting
- Domain joining and client administration
- Organizational units, users, and security groups
- SMB file sharing and NTFS access control
- Group Policy creation, linking, and troubleshooting
- Password and account lockout policy configuration
- Windows Event Viewer and Security log analysis
- Authentication troubleshooting and account lockout investigation
- Basic security validation and technical documentation

## Lessons learned

- Active Directory clients depend on correctly configured DNS to locate domain services.
- Share permissions and NTFS permissions work together to determine effective file access.
- Group Policy scope and OU placement matter: a policy only affects the users or computers within its applicable scope.
- Security logs provide useful evidence for investigating successful logons, failed logons, and account lockouts.
- Testing with separate departmental accounts helps verify that access controls work as intended.
- A change should be validated from the affected client, not assumed to have applied simply because it was configured on the server.

## Planned work

The lab is still being developed. Planned exercises include:

- Active Directory account lifecycle management (disable, enable, reset, move, and manage group membership).
- More advanced Group Policy administration.
- Additional Windows Server administration and troubleshooting.
- Network administration and troubleshooting exercises.
- Windows security hardening.
- Kali Linux VM deployment and configuration.
- Controlled Active Directory security testing.
- Defensive security and incident-response exercises.
- Backup, recovery, and lab maintenance.

Only mark an exercise as complete after it has been configured and tested.

## Safety and scope

This repository describes a controlled educational environment. It is not a production deployment guide.

- Windows 7 is end-of-life and unsupported. These clients are used only in an isolated lab for legacy-domain learning.
- Do not expose the lab clients to untrusted networks or use them for everyday computing.
- Use fictional accounts and sanitized screenshots in public documentation.
- Never commit passwords, recovery keys, API keys, tokens, private configuration files, or personal information.
- Obtain authorization before performing security tests, and keep all testing within systems you own or are explicitly permitted to assess.

## Repository structure

Documentation and sanitized evidence will be added progressively as the project develops.

```text
.
├── README.md
├── architecture/
│   ├── lab-overview.md
│   └── network-configuration.md
├── documentation/
│   ├── 01-virtualbox-setup.md
│   ├── 02-windows-server-and-ad.md
│   ├── 03-active-directory-users-and-groups.md
│   ├── 04-departmental-file-sharing.md
│   ├── 05-password-and-lockout-policy.md
│   ├── 06-group-policy-restrictions.md
│   └── 07-security-auditing.md
├── screenshots/
│   ├── active-directory/
│   ├── file-sharing/
│   ├── group-policy/
│   └── security-auditing/
└── future-work/
    └── project-roadmap.md


```
Maintainer: @Jaywon123art
Project: Active Directory Cybersecurity Home Lab
