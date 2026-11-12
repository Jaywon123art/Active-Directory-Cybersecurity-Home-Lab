# Active Directory & Cybersecurity Home Lab

A practical Windows Server, Active Directory and cybersecurity home lab built using Oracle VM VirtualBox.

This project documents the design, deployment, configuration, administration, security testing and recovery procedures of a simulated corporate IT environment. It demonstrates hands-on experience with Windows Server administration, Active Directory, Group Policy, access control, security auditing and backup management.

> **Project Status:** In Progress  
> **Completed Exercises:** 09  
> **Environment:** Personal, isolated learning lab  
> **Domain:** `corp.in`  
> **Platform:** Oracle VM VirtualBox

---

## Project Objectives

The main objectives of this project are to:

- Deploy and administer a Windows Server 2022 Active Directory domain.
- Configure DNS and domain-joined Windows clients.
- Build and manage Organizational Units, users and security groups.
- Implement departmental file sharing and access restrictions.
- Configure and troubleshoot Group Policy Objects.
- Apply account security and password policies.
- Monitor Windows security events and investigate account lockouts.
- Practice Active Directory account lifecycle management.
- Implement advanced Group Policy security controls.
- Perform and verify Active Directory System State backups.
- Develop practical Windows infrastructure and cybersecurity troubleshooting skills.

---

## Lab Environment

### Host Machine

| Component | Configuration |
|---|---|
| Laptop | Lenovo ThinkPad T470 |
| Operating System | Windows 10 |
| Processor | Intel Core i5 |
| RAM | 8 GB |
| Storage | SSD |
| Virtualisation Platform | Oracle VM VirtualBox |

Due to the host's limited memory, virtual machines are operated selectively to maintain system performance.

### Virtual Machines

| Machine | Operating System | Role | IP Address |
|---|---|---|---|
| DC01 | Windows Server 2022 Standard Evaluation | Domain Controller and DNS | `192.168.56.10` |
| CL01 | Windows 7 Professional 64-bit | Domain Client | `192.168.56.101` |
| CL02 | Windows 7 Professional 64-bit | Domain Client | `192.168.56.102` |
| KALI01 | Kali Linux | Planned Security Testing Workstation | `192.168.56.50` (planned) |

### Network Configuration

| Network | Type | Purpose |
|---|---|---|
| AD-LAB | VirtualBox Internal Network | Isolated communication between lab machines |
| NAT-LAB | VirtualBox NAT Network | Controlled outbound network connectivity |

**Network configuration:**

- Active Directory domain: `corp.in`
- NetBIOS name: `CORP`
- Domain DNS server: `192.168.56.10`
- NAT-LAB subnet: `10.10.10.0/24`
- NAT-LAB gateway: `10.10.10.1`

The AD-LAB network provides private communication for the domain environment. Windows 7 clients are legacy, unsupported operating systems and are used strictly for isolated learning exercises.

---

## Work Completed

The following nine practical exercises have been completed and documented.

### Exercise 01 – VirtualBox Installation and Lab Foundation

- Installed and configured Oracle VM VirtualBox.
- Created an organised directory structure for virtual machines, ISO files, snapshots and tools.
- Created the AD-LAB internal network.
- Configured the NAT-LAB NAT network.
- Established the virtual machine deployment and IP addressing plan.

**Skills demonstrated:** Virtualisation, virtual machine configuration and network planning.

### Exercise 02 – Windows Server and Active Directory Domain Setup

- Installed Windows Server 2022 Standard Evaluation.
- Renamed the server to `DC01`.
- Configured a static IP address.
- Installed Active Directory Domain Services and DNS Server.
- Promoted DC01 to a domain controller.
- Created the `corp.in` Active Directory domain.
- Verified domain and DNS functionality.

**Skills demonstrated:** Windows Server administration, Active Directory deployment and DNS configuration.

### Exercise 03 – Active Directory User and OU Management

- Created the company Organizational Unit structure.
- Established departmental OUs for IT, HR and Finance.
- Created user accounts for departmental testing.
- Created and organised security groups.
- Managed user and computer objects within Active Directory.

**Example lab accounts:**

| Department | Account | Security Group |
|---|---|---|
| IT | `James.IT` | `IT_Staff` |
| HR | `Sarah.HR` | `HR_Staff` |
| Finance | `David.FIN` | `Finance_Staff` |

**Skills demonstrated:** Active Directory object management, OU administration and security-group management.

### Exercise 04 – Group Policy Management

- Created and configured Group Policy Objects.
- Applied policies to targeted users and computers.
- Configured departmental restrictions.
- Tested policy application and behaviour.
- Used Group Policy troubleshooting tools to investigate policy issues.

**Skills demonstrated:** Group Policy administration, policy configuration and troubleshooting.

### Exercise 05 – File Sharing and Permissions

- Created IT, HR and Finance departmental folders.
- Configured SMB network shares.
- Applied NTFS permissions.
- Used security groups to control departmental access.
- Tested access from domain-joined clients.

**Access validation:**

| User | IT Share | HR Share | Finance Share |
|---|---|---|---|
| `James.IT` | Allowed | Denied | Denied |
| `Sarah.HR` | Denied | Allowed | Denied |
| `David.FIN` | Denied | Denied | Allowed |

**Skills demonstrated:** SMB file sharing, NTFS permissions, access control and Role-Based Access Control (RBAC).

### Exercise 06 – Security Auditing and Event Logs

- Configured Windows security auditing through Group Policy.
- Audited successful and failed logon attempts.
- Investigated Windows Security event logs.
- Reviewed Event ID 4624 for successful logons.
- Reviewed Event ID 4625 for failed logons.
- Investigated account lockout Event ID 4740.
- Identified the originating client computer.
- Unlocked a test account through Active Directory Users and Computers.

**Skills demonstrated:** Event Viewer, security auditing, authentication troubleshooting and basic security investigation.

### Exercise 07 – Active Directory Account Lifecycle Management

- Created and managed a dedicated test account.
- Disabled and re-enabled user accounts.
- Reset user passwords.
- Configured forced password changes at next logon.
- Moved user accounts between Organizational Units.
- Managed security-group membership.
- Tested departmental resource access.

**Skills demonstrated:** User account administration, access management, least privilege and account lifecycle management.

### Exercise 08 – Advanced Group Policy Management

Practised advanced Group Policy administration techniques:

- Security filtering using dedicated security groups.
- GPO inheritance between parent and child OUs.
- Block Inheritance.
- GPO Enforcement.
- Windows Management Instrumentation (WMI) filtering.
- GPO backup and restoration.
- Registry Preferences.
- Policy verification using `gpresult`, `gpupdate` and `whoami`.

**Skills demonstrated:** Advanced Group Policy administration, policy targeting, troubleshooting and configuration recovery.

### Exercise 09 – Active Directory Backup and Recovery

- Installed Windows Server Backup.
- Created and attached a separate 20 GB virtual backup disk.
- Initialised and formatted the disk using Disk Management.
- Configured an NTFS backup volume labelled `DC01-Backup`.
- Assigned drive letter `E:`.
- Performed an Active Directory System State backup.
- Inspected the Windows Server recovery wizard.
- Confirmed that System State was available as a recovery option.
- Verified the backup using the Windows Server Backup command-line utility.

**Verification command:**

```cmd
wbadmin get versions -backupTarget:E:
```

The command successfully identified the backup version and listed System State among the recoverable items.

No live System State restoration was performed.

**Skills demonstrated:** Windows Server Backup, System State backup, backup verification, recovery planning and disaster recovery fundamentals.

---

## Technical Skills Practised

### Windows Server and Infrastructure
- Windows Server 2022 administration.
- Active Directory Domain Services.
- DNS configuration and troubleshooting.
- Domain controller administration.
- Domain joining and client management.
- Virtual machine deployment and management.

### Active Directory Administration
- Organizational Unit management.
- User and computer account administration.
- Security-group management.
- Account lifecycle management.
- Role-Based Access Control.
- Least-privilege access management.

### Group Policy and Security
- Group Policy creation and configuration.
- Security filtering.
- GPO inheritance and enforcement.
- WMI filtering.
- Password and account lockout policies.
- Removable-storage restrictions.
- Security auditing and event-log investigation.

### File Sharing and Backup
- SMB network sharing.
- NTFS permissions.
- Departmental access restrictions.
- Windows Server Backup.
- Active Directory System State backup.
- Backup verification using WBAdmin.
- Recovery-point inspection.

### Troubleshooting and Administration
- Windows client troubleshooting.
- DNS and network connectivity checks.
- Group Policy troubleshooting.
- Authentication and account lockout investigation.
- Command-line administration.
- Technical documentation.

---

## Lessons Learned

Throughout the project, I have developed practical understanding of several important IT infrastructure concepts:

- Active Directory clients depend on correctly configured DNS to locate domain services.
- Organisational Unit placement and Group Policy scope determine which policies apply.
- SMB share permissions and NTFS permissions work together to control resource access.
- Security groups simplify permission management and support least-privilege access.
- Windows Security logs provide evidence for investigating authentication activity.
- Group Policy filtering and inheritance provide more precise administrative control.
- Backups must be verified rather than assumed successful.
- Domain controller recovery requires careful planning to protect Active Directory consistency.
- Practical testing is essential for confirming that configurations work as intended.

---

## Planned Exercises

The project remains under development.

Future activities include:

- Additional Windows Server administration.
- Network administration and troubleshooting.
- Windows Server security hardening.
- Active Directory disaster recovery planning.
- Improved backup protection and recovery testing.
- Kali Linux deployment and configuration.
- Controlled Active Directory security testing.
- Defensive security monitoring.
- Incident response exercises.
- Further infrastructure documentation and maintenance.

Only exercises that have been practically configured and tested will be marked as completed.

---

## Repository Structure

```text
Active-Directory-Cybersecurity-Home-Lab/
│
├── README.md
│
├── architecture/
│   ├── lab-overview.md
│   └── network-configuration.md
│
├── Documentation/
│   ├── 01-virtualbox-setup.md
│   ├── 02-active-directory-domain-setup.md
│   ├── 03-active-directory-user-and-ou-management.md
│   ├── 04-group-policy-management.md
│   ├── 05-file-sharing-and-permissions.md
│   ├── 06-security-auditing-and-event-logs.md
│   ├── 07-active-directory-account-lifecycle-management.md
│   ├── 08-advanced-group-policy-management.md
│   └── 09-active-directory-backup-and-recovery.md
│
├── screenshots/
│   ├── active-directory/
│   ├── file-sharing/
│   ├── group-policy/
│   └── security-auditing/
│
└── future-work/
    └── project-roadmap.md
```

---

## Safety and Scope

This project is conducted within a controlled personal learning environment.

- Windows 7 is end-of-life and unsupported. It is used only for isolated lab exercises.
- Lab systems should not be exposed to untrusted networks.
- Fictional accounts are used for demonstrations.
- Screenshots and documentation should be sanitised before public sharing.
- Passwords, recovery keys, API keys and other sensitive information must never be committed to the repository.
- Security testing must only be performed on systems owned by the tester or where explicit permission has been granted.

**Important backup limitation:** The dedicated backup virtual disk is separate from the DC01 operating system disk, but both are stored on the same physical host. Additional protected backup copies are necessary for stronger disaster recovery protection.

---

## Project Information

**Project:** Active Directory & Cybersecurity Home Lab  
**Maintainer:** [@Jaywon123art](https://github.com/Jaywon123art)  
**Platform:** Oracle VM VirtualBox  
**Domain:** `corp.in`  
**Completed Exercises:** 09  
**Project Status:** In Progress

This repository serves as a record of practical learning, technical development, troubleshooting and hands-on experience in Windows infrastructure and cybersecurity.
