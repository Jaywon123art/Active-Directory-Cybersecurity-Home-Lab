# 04 – Group Policy Management

## 1. Overview

This phase covers the configuration and testing of Group Policy Objects (GPOs) in the Active Directory domain.

The objective is to understand how administrators enforce security policies, control user access, and manage computer configurations centrally.

## 2. Lab Configuration

| Item | Configuration |
|---|---|
| Domain | corp.in |
| Domain Controller | DC01 |
| Server Operating System | Windows Server 2022 |
| Domain NetBIOS Name | CORP |

## 3. Default Domain Policy

The Default Domain Policy was configured to enforce password and account lockout requirements across the domain.

### Password Policy

| Policy | Configuration |
|---|---|
| Enforce Password History | 10 passwords remembered |
| Maximum Password Age | 90 days |
| Minimum Password Age | 1 day |
| Minimum Password Length | 12 characters |
| Password Complexity | Enabled |
| Store Passwords Using Reversible Encryption | Disabled |

### Account Lockout Policy

| Policy | Configuration |
|---|---|
| Account Lockout Threshold | 5 invalid attempts |
| Account Lockout Duration | 10 minutes |
| Reset Account Lockout Counter After | 10 minutes |

These settings help protect domain accounts against weak passwords and repeated password-guessing attempts.

## 4. HR Control Panel Restriction

A Group Policy Object named `GPO-HR-ControlPanel-Restriction` was created and linked to the HR Organizational Unit.

The policy restricts access to Control Panel for users in the HR department.

### Verification

- Sarah.HR was used to test the restriction.
- Control Panel access was successfully restricted.
- James.IT was tested as a comparison.
- James.IT was not affected by the HR-specific restriction.

This exercise demonstrates how GPOs can apply different configurations to different departments.

## 5. CL01 USB Restriction

A Group Policy Object named `GPO-CL01-USB-Restriction` was created and linked to the `Company\Computers` Organizational Unit.

The policy was configured to deny access to removable storage devices.

The restrictions covered:

- Read access.
- Write access.
- Execute access.

### Verification

- CL01 was placed within the intended policy scope.
- USB removable storage restrictions were tested on CL01.
- CL01 was successfully restricted.
- CL02 remained unaffected because it was outside the targeted Organizational Unit.

This demonstrates how administrators can apply security restrictions to selected computers rather than the entire domain.

## 6. Practical Importance

These exercises provide practical experience in:

- Creating and managing Group Policy Objects.
- Enforcing domain password requirements.
- Configuring account lockout policies.
- Applying department-specific restrictions.
- Controlling removable storage devices.
- Understanding GPO linking and scope.
- Testing policy application and troubleshooting.

## 7. Project Maintainer

**Maintainer:** [@Jaywon123art](https://github.com/Jaywon123art)  
**Project:** Active Directory Cybersecurity Home Lab
