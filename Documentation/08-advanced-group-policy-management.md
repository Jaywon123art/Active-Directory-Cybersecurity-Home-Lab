# Exercise 08 – Advanced Group Policy Management

## 1. Overview

This exercise demonstrates advanced Group Policy Management techniques in a Windows Server 2022 Active Directory environment.

The practical tasks covered security filtering, GPO inheritance, Block Inheritance, enforcement, WMI filtering, and GPO backup and restoration.

**Domain:** `corp.in`  
**Domain Controller:** DC01  
**Client:** CL01  
**Operating System:** Windows Server 2022 and Windows 7 Professional

## 2. Security Filtering

### Objective
Apply a Group Policy Object only to members of a specific security group.

### Implementation
- Created the security group `GPO_Test_Users`.
- Added the test account `Lab.Test` to the group.
- Created `GPO-08-Security-Filtering-Test`.
- Linked the GPO to the IT Organizational Unit.
- Configured Security Filtering to use `GPO_Test_Users`.
- Granted the group Read and Apply Group Policy permissions.
- Configured the policy **Remove Run menu from Start Menu** as Enabled.

### Verification
- Signed in as `CORP\Lab.Test` on CL01 and confirmed the Run option was hidden.
- Signed in as `CORP\James.IT` and confirmed the Run option remained visible because the account was not a member of the test group.

**Result:** Security filtering worked as expected.

## 3. GPO Inheritance

### Objective
Understand how policies linked to parent Organizational Units are inherited by child OUs.

### Implementation
- Created the OU `GPO-Inheritance-Lab`.
- Created the child OU `Inheritance-Test-Users`.
- Created the test account `Inheritance.Test` in the child OU.
- Created and linked `GPO-08-Inheritance-Parent-Test` to the parent OU.
- Enabled **Remove Run menu from Start Menu**.

### Verification
Signed in as `CORP\Inheritance.Test` on CL01 and confirmed that the inherited policy applied.

**Result:** The child OU inherited the policy from its parent OU.

## 4. Block Inheritance

### Objective
Demonstrate how an OU can prevent ordinary policies linked to parent OUs from applying.

### Implementation
- Enabled **Block Inheritance** on `Inheritance-Test-Users`.
- Updated Group Policy on CL01 using `gpupdate /force`.

### Verification
- Confirmed that the inherited GPO no longer applied.
- Confirmed that the Run option became visible.

**Result:** Block Inheritance successfully prevented the ordinary parent GPO from applying.

## 5. GPO Enforcement

### Objective
Understand how an enforced GPO behaves when a child OU has Block Inheritance enabled.

### Implementation
- Enabled **Enforced** on the parent GPO link.
- Kept Block Inheritance enabled on the child OU.
- Updated Group Policy on CL01.

### Verification
Confirmed that the enforced GPO applied despite Block Inheritance, and the Run option became hidden again.

**Result:** GPO Enforcement successfully demonstrated.

### Cleanup
Disabled Enforced on the parent GPO link and disabled Block Inheritance on the child OU after testing.

## 6. WMI Filtering

### Objective
Apply a Group Policy Object only to computers matching a specified Windows Management Instrumentation (WMI) query.

### Implementation
- Created the WMI filter `WMI-Filter-Windows-7`.
- Configured the following query:

```sql
SELECT * FROM Win32_OperatingSystem WHERE Caption LIKE "%Windows 7%"
```

- Created `GPO-08-WMI-Filtering-Test`.
- Linked the GPO to the OU containing the CL01 computer account.
- Attached the Windows 7 WMI filter to the GPO.
- Added a Registry Preference as a test setting:

| Setting | Value |
|---|---|
| Action | Update |
| Hive | HKEY_LOCAL_MACHINE |
| Key Path | SOFTWARE\HomeLab |
| Value Name | WMI-Filter-Test |
| Value Type | REG_SZ |
| Value Data | Windows7FilterApplied |

### Verification
- Ran `gpupdate /target:computer /force` on CL01.
- Confirmed the GPO appeared under Applied Group Policy Objects.
- Opened Registry Editor and verified the test value under:

`HKEY_LOCAL_MACHINE\SOFTWARE\HomeLab`

**Result:** WMI filtering successfully applied the test policy to the Windows 7 client.

## 7. GPO Backup and Restoration

### Objective
Learn how to back up and restore Group Policy Objects to support recovery from accidental or unwanted policy changes.

### Backup Implementation
- Selected `GPO-08-Security-Filtering-Test` in Group Policy Management.
- Used the Back Up option.
- Saved the backup in:

`C:\GPO-Backups`

- Added the description: `Backup of Exercise 08 Security Filtering Test GPO`.
- Verified that the backup appeared in Manage Backups.

### Restoration Test
- Temporarily changed **Remove Run menu from Start Menu** from Enabled to Disabled.
- Restored `GPO-08-Security-Filtering-Test` from the saved backup.
- Reopened the policy and confirmed that the setting had returned to Enabled.
- Confirmed that `GPO_Test_Users` remained listed under Security Filtering.
- Updated Group Policy on CL01 using `gpupdate /force`.

### Verification
Signed in as `CORP\Lab.Test` and confirmed that the Run option was hidden again.

**Result:** GPO backup and restoration were successful.

## 8. Commands Used

| Command | Purpose |
|---|---|
| `gpupdate /force` | Forces Group Policy to refresh. |
| `gpupdate /target:computer /force` | Refreshes computer policies only. |
| `gpresult /scope user /r` | Displays applied user policies. |
| `gpresult /scope computer /r` | Displays applied computer policies. |
| `whoami /groups` | Displays the groups associated with the current logon token. |

## 9. Skills Demonstrated

- Active Directory Group Policy Management.
- Group Policy Security Filtering.
- GPO inheritance and precedence.
- Block Inheritance and Enforcement.
- Windows Management Instrumentation (WMI) filtering.
- GPO backup and restoration.
- Group Policy troubleshooting and verification.
- Registry Preferences.
- User and computer policy administration.

## 10. Conclusion

Exercise 08 successfully demonstrated advanced Group Policy Management in the `corp.in` Active Directory environment.

The exercise provided practical experience controlling policy application, managing inheritance, targeting computers through WMI filters, and recovering Group Policy configurations through backup and restoration.

These skills are relevant to Windows Server administration, enterprise IT support, and cybersecurity operations.

---

**Project:** Active Directory & Cybersecurity Home Lab  
**Exercise:** 08 – Advanced Group Policy Management  
**Status:** Completed
