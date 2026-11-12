# 09 – Active Directory Backup and Recovery

## 1. Overview

This exercise demonstrates how to install Windows Server Backup, create a dedicated backup destination, back up Active Directory System State, and verify that the recovery point is available.

**Domain:** `corp.in`  
**Domain Controller:** DC01  
**Backup destination:** `E:\` (`DC01-Backup`)  
**Backup type:** System State  
**Operating System:** Windows Server 2022

## 2. Install Windows Server Backup

### Objective

Install the Windows Server feature required to create and manage server backups.

### Implementation

- Opened Server Manager on DC01.
- Used **Manage → Add Roles and Features**.
- Located **Windows Server Backup** under Features.
- Selected the feature and completed the installation.

### Verification

Opened **Server Manager → Tools → Windows Server Backup** and confirmed that the backup console was available.

**Result:** Windows Server Backup installed successfully.

## 3. Create a Dedicated Backup Virtual Disk

### Objective

Provide a separate virtual disk for the System State backup instead of storing the backup on the operating system disk.

### Implementation

Created a second virtual hard disk in VirtualBox and attached it to DC01.

| Setting | Configuration |
|---|---|
| Virtual disk name | `DC01-Backup` |
| Virtual disk format | VDI |
| Allocation | Dynamically allocated |
| Maximum size | 20 GB |
| Virtual disk location | `C:\Cybersecurity-Home-Lab\Virtual Machines\Server(DC01)\DC01-Backup.vdi` |

### Initialise and format the disk

Used Disk Management inside DC01 to prepare the new disk.

| Setting | Configuration |
|---|---|
| Partition style | GPT |
| Volume type | New Simple Volume |
| Drive letter | E: |
| Volume label | DC01-Backup |
| File system | NTFS |
| Quick format | Enabled |

### Verification

Confirmed that the new volume appeared in Windows as **DC01-Backup (E:)** with status Online and a formatted NTFS volume.

**Result:** A separate 20 GB backup destination was attached and made available to Windows Server.

## 4. Configure and Run a System State Backup

### Objective

Create a backup of critical Windows Server components, including the components required to recover Active Directory.

### Implementation

In Windows Server Backup:

1. Selected **Local Backup → Backup Once**.
2. Chose **Different options**.
3. Selected **Custom** backup configuration.
4. Used **Add Items** to select **System State**.
5. Selected **Local drives** as the destination type.
6. Selected **DC01-Backup (E:)** as the backup destination.
7. Reviewed the configuration and started the backup.

### Verification

Windows Server Backup displayed **Backup complete successfully**. The backup was also listed in the Local Backup console.

**Result:** The System State backup completed successfully and was stored on the dedicated E: volume.

## 5. Inspect the Recovery Options (No Restore Performed)

### Objective

Understand how an administrator locates a recovery point and identifies the System State recovery option without changing the live domain controller.

### Implementation

- Opened **Recover** in Windows Server Backup.
- Selected **This server (DC01)**.
- Selected the date and time of the available backup.
- Confirmed that **System State** was visible and selectable under recovery types.
- Inspected the **Select Location for System State Recovery** page.
- Left **Original location** selected and left **Perform an authoritative restore of Active Directory files** unchecked.
- Cancelled the wizard without starting recovery.

### Important recovery considerations

A System State restore on a domain controller is a sensitive recovery operation. The recovery method depends on the failure scenario and the state of the domain and its replication partners. An authoritative restore is a specialised operation and must not be selected unless the recovery plan specifically requires it.

**No restore was performed.** DC01 and the `corp.in` domain were left running in their existing state.

**Result:** The recovery wizard exposed the System State recovery option, and the inspection was completed without modifying the server.

## 6. Verify the Backup with WBAdmin

### Objective

Use the Windows Server Backup command-line tool to confirm that the backup stored on E: is discoverable and includes System State.

### Command

Run Command Prompt as Administrator on DC01:

```cmd
wbadmin get versions -backupTarget:E:
```

### Verification

The command returned a backup version and identified the backup target as a fixed disk labelled E:. The output included:

```text
Can recover: Volume(s), File(s), Application(s), System State
```

This confirmed that Windows Server Backup could identify the recovery point and listed System State as recoverable content.

**Result:** The backup was successfully verified using `wbadmin`.

## 7. Backup Summary

| Item | Result |
|---|---|
| Windows Server Backup feature | Installed |
| Dedicated backup disk | Created and attached |
| Backup volume | NTFS, E:, label DC01-Backup |
| Backup configuration | Custom |
| Selected backup item | System State |
| Backup operation | Successful |
| Recovery point visible | Yes |
| System State recovery option visible | Yes |
| WBAdmin verification | Successful |
| Restore operation | Not performed |

## 8. Skills Demonstrated

- Installing Windows Server features.
- Creating and attaching VirtualBox virtual disks.
- Initialising disks and creating NTFS volumes with Disk Management.
- Configuring Windows Server Backup.
- Performing an Active Directory System State backup.
- Inspecting Windows Server recovery options safely.
- Verifying backup versions with `wbadmin`.
- Understanding the importance of recovery planning for domain controllers.

## 9. Important Notes and Limitations

- A System State backup is not a complete virtual machine image or a full-server backup.
- The backup disk is a separate virtual disk, but it is still stored on the same physical host and within the same host storage environment as the VM. It therefore does not protect against loss of the host laptop or its physical storage.
- A production backup strategy should include additional protected copies, preferably on separate storage or an appropriately secured backup system, and regular recovery testing.
- The 20 GB virtual disk is a lab destination. Actual backup requirements depend on the server's data and backup configuration.
- Windows Server Backup's successful completion and the `wbadmin` version listing confirm that the backup is recognised; they do not replace a properly planned test recovery.
- No live System State restore was attempted during this exercise.

## 10. Conclusion

Exercise 09 successfully demonstrated the installation and use of Windows Server Backup to create and verify an Active Directory System State backup for DC01.

The exercise also demonstrated how to inspect the recovery workflow without performing a potentially disruptive restore. This provides practical experience with backup administration, recovery-point verification, and safe handling of domain controller recovery operations.

These skills are relevant to Windows Server administration, IT support, infrastructure operations, and cybersecurity resilience.

---

**Project:** Active Directory & Cybersecurity Home Lab  
**Exercise:** 09 – Active Directory Backup and Recovery  
**Status:** Completed
