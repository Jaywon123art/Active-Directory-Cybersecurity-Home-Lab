# 05 – File Sharing and Permissions

## 1. Overview

This phase covers the creation and configuration of departmental shared folders on the Windows Server 2022 Domain Controller (DC01).

The objective is to practice centralized file sharing, network access, and permission management using Active Directory security groups.

## 2. Lab Configuration

| Item | Configuration |
|---|---|
| File Server | DC01 |
| Domain | corp.in |
| Server IP Address | 192.168.56.10 |
| Shared Folder Location | C:\DepartmentShares |
| Domain NetBIOS Name | CORP |

## 3. Departmental Shared Folders

The following departmental folders were created on DC01:

- `C:\DepartmentShares\IT`
- `C:\DepartmentShares\HR`
- `C:\DepartmentShares\Finance`

Each folder provides a separate location for departmental files.

## 4. SMB Network Shares

The folders were shared over the network using Server Message Block (SMB).

The following network paths were configured:

| Department | Network Share Path |
|---|---|
| IT | `\\DC01\IT` |
| HR | `\\DC01\HR` |
| Finance | `\\DC01\Finance` |

These paths allow authorized domain users to access departmental resources across the lab network.

## 5. Permission Management

Access to departmental shared folders was configured using Active Directory security groups.

The following groups were used:

| Department | Security Group |
|---|---|
| IT | IT_Staff |
| HR | HR_Staff |
| Finance | Finance_Staff |

Group-based permissions make it easier to manage access and reduce the need to assign permissions individually to every user.

Both share permissions and NTFS permissions are important when securing Windows shared folders.

## 6. Access Verification

Access permissions were tested using departmental domain accounts.

The following checks were performed:

- Departmental users were tested against their respective shared folders.
- Access restrictions were checked to confirm that permissions were applied.
- The shared folders were accessed using their SMB network paths.

## 7. Practical Importance

This exercise provides practical experience in:

- Creating departmental shared folders.
- Configuring Windows SMB file sharing.
- Understanding network share paths.
- Managing NTFS and share permissions.
- Using Active Directory security groups for access control.
- Testing authorized and unauthorized access.
- Applying the principle of least privilege.

## 8. Project Maintainer

**Maintainer:** [@Jaywon123art](https://github.com/Jaywon123art)  
**Project:** Active Directory Cybersecurity Home Lab
