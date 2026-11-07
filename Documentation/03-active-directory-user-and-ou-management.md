# 03 – Active Directory User and OU Management

## 1. Overview

This phase covers the creation and organization of Organizational Units (OUs), user accounts, and security groups in the Active Directory domain.

The objective is to practice centralized identity management and understand how administrators organize users and manage access within a Windows domain.

## 2. Lab Configuration

| Item | Configuration |
|---|---|
| Domain | corp.in |
| Domain Controller | DC01 |
| NetBIOS Name | CORP |
| Active Directory Domain | corp.in |

## 3. Organizational Unit Structure

A top-level Organizational Unit named `Company` was created.

The following OUs were created under it:

- IT
- HR
- Finance
- Users
- Computers
- Groups

This structure separates directory objects into logical departments and administrative categories.

## 4. User Account Creation

The following fictional domain user accounts were created:

| Full Name | Logon Name | Department |
|---|---|---|
| James Wilson | James.IT | IT |
| Sarah Johnson | Sarah.HR | HR |
| David Brown | David.FIN | Finance |

These accounts provide separate identities for testing authentication, permissions, and Group Policy settings.

## 5. Security Group Management

The following security groups were created:

| Security Group | Department |
|---|---|
| IT_Staff | IT |
| HR_Staff | HR |
| Finance_Staff | Finance |

The corresponding user accounts were assigned to their departmental groups:

- James.IT — IT_Staff
- Sarah.HR — HR_Staff
- David.FIN — Finance_Staff

Security groups simplify permission management by allowing administrators to assign access to groups rather than configuring permissions separately for every user.

## 6. Verification

The Active Directory structure and accounts were checked to confirm that:

- The `Company` OU was created.
- The departmental and administrative OUs were created.
- The three fictional user accounts were created.
- The departmental security groups were available.
- Each user was assigned to the appropriate departmental group.

## 7. Practical Importance

This exercise provides practical experience in:

- Creating and managing Active Directory OUs.
- Creating domain user accounts.
- Organizing users by department.
- Creating and managing security groups.
- Understanding group-based access control.
- Preparing Active Directory for Group Policy and resource-permission management.

## 8. Project Maintainer

**Maintainer:** [@Jaywon123art](https://github.com/Jaywon123art)  
**Project:** Active Directory Cybersecurity Home Lab
