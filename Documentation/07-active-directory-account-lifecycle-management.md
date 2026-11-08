
# 07 – Active Directory Account Lifecycle Management

## 1. Overview

This practical exercise demonstrates how IT administrators manage Active Directory user accounts throughout their lifecycle.

The exercise was performed in a virtualised Active Directory environment using Windows Server 2022 and Windows 7 domain clients.

The main objective was to practise account administration, password management, Organizational Unit (OU) management, security group membership, and departmental resource access verification.

## 2. Lab Environment

| Component | Configuration |
|---|---|
| Domain Controller | DC01 |
| Domain Name | corp.in |
| Domain Administrator | CORP\Administrator |
| Test User | Lab.Test |
| Security Group | IT_Staff |
| Client Computer | CL01 |
| Server Operating System | Windows Server 2022 |
| Client Operating System | Windows 7 |
| Virtualisation Platform | Oracle VirtualBox |


## 3. Account Management Procedures

### 3.1 Disabling a User Account

1. Open Active Directory Users and Computers on DC01.
2. Locate the Lab.Test user account.
3. Right-click the account and select Disable Account.
4. Confirm the account is disabled.
5. Verify the disabled status in the Account properties.

**Result:** The Lab.Test account was successfully disabled.

### 3.2 Re-enabling a User Account

1. Locate the disabled Lab.Test account.
2. Right-click the account.
3. Select Enable Account.
4. Verify that the disabled-account indicator disappears.

**Result:** The Lab.Test account was successfully re-enabled.

### 3.3 Resetting a User Password

1. Right-click Lab.Test in Active Directory Users and Computers.
2. Select Reset Password.
3. Enter and confirm a new temporary password.
4. Select User must change password at next logon.
5. Complete the password reset.

**Result:** The password was successfully reset, and the user was required to change it at the next logon.

### 3.4 Moving a User Between Organizational Units

1. Locate Lab.Test under Company > Users.
2. Right-click the account and select Move.
3. Select Company > IT as the destination.
4. Confirm the move.
5. Verify that Lab.Test appears under Company > IT.

**Result:** The Lab.Test account was successfully moved from the Users OU 
to the IT OU.


### 3.5 Managing Security Group Membership

1. Open the Lab.Test account properties.
2. Select the Member Of tab.
3. Confirm that the account initially belonged to Domain Users.
4. Add Lab.Test to the IT_Staff security group.
5. Verify that IT_Staff appears in the group membership list.
6. Remove Lab.Test from IT_Staff and verify the removal.
7. Add Lab.Test back to IT_Staff.
8. Confirm that both Domain Users and IT_Staff are listed.

**Result:** Successfully added, removed, and restored the user's IT_Staff group membership.

## 4. Departmental Folder Access Verification

Access testing was performed on CL01 while signed in as CORP\Lab.Test.

The account was a member of IT_Staff.

| Shared Folder | Network Path | Access Result |
|---|---|---|
| IT | \\DC01\IT | Access Granted |
| HR | \\DC01\HR | Access Denied |
| Finance | \\DC01\Finance | Access Denied |

**Observations:**

- Lab.Test successfully accessed the IT departmental folder.
- Access to the HR departmental folder was denied.
- Access to the Finance departmental folder was denied.

**Result:** Departmental folder access was successfully verified using security group membership.

## 5. Security Concepts Practised

- Active Directory user account lifecycle management.
- User account disabling and re-enabling.
- Password resets and password-change requirements.
- Organizational Unit management.
- Security group membership administration.
- Departmental resource access verification.
- Role-Based Access Control (RBAC).
- Principle of Leas
- t Privilege.


## 6. Overall Results

The Active Directory account lifecycle management exercise was completed successfully.

The following tasks were performed:

- Disabled and re-enabled the Lab.Test account.
- Reset the account password and configured the next-logon password-change requirement.
- Moved the user from the Company > Users OU to Company > IT.
- Added and removed the user from the IT_Staff security group.
- Restored the user's IT_Staff membership.
- Verified access to IT, HR, and Finance departmental shared folders.

All practical tests produced the expected results.

## 7. Conclusion

This exercise provided practical experience in managing Active Directory user accounts and controlling access to departmental resources.

It demonstrated how Organizational Units, security groups, and shared-folder permissions support effective user administration and access control in a Windows domain environment.

The exercise strengthened practical knowledge of Windows Server administration and Active Directory security.

---

**Project:** Active Directory Cybersecurity Home Lab  
**Platform:** Oracle VirtualBox  
**Domain:** corp.in  
**Maintainer:** [@Jaywon123art](https://github.com/Jay
won123art)
