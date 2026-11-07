# 06 – Security Auditing and Event Logs

## 1. Overview

This phase covers the configuration of Windows security auditing and the investigation of security events using Event Viewer.

The objective is to monitor authentication activity, identify failed logon attempts, and investigate account lockout events within the Active Directory lab.

## 2. Lab Configuration

| Item | Configuration |
|---|---|
| Domain Controller | DC01 |
| Client Computer | CL01 |
| Domain | corp.in |
| Domain NetBIOS Name | CORP |
| Server Operating System | Windows Server 2022 |

## 3. Security Auditing Configuration

A Group Policy Object named `GPO-CL01-Security-Auditing` was created and linked to the `Company\Computers` Organizational Unit.

The policy was configured to audit:

- Successful logon attempts.
- Failed logon attempts.

This allows administrators to monitor authentication activity and investigate suspicious login behavior.

## 4. Logon Event Investigation

Windows Security logs were examined using Event Viewer on CL01.

The following event IDs were identified:

| Event ID | Description |
|---|---|
| 4624 | Successful account logon |
| 4625 | Failed account logon |

These events provide useful information for investigating authentication activity, including account names and logon details.

## 5. Account Lockout Investigation

An account lockout test was performed using the `Lab.Test` account.

After repeated unsuccessful logon attempts, the account was locked.

The Security log on DC01 was examined to investigate the lockout event.

The following event was identified:

| Event ID | Description |
|---|---|
| 4740 | A user account was locked out |

The investigation identified:

- Locked account: `Lab.Test`
- Caller computer: `CL01-PC`

The test account was subsequently unlocked.

## 6. Verification

The following checks were completed:

- Successful logon auditing was tested.
- Failed logon auditing was tested.
- Event ID 4624 was identified.
- Event ID 4625 was identified.
- Account lockout was triggered during testing.
- Event ID 4740 was located on DC01.
- The caller computer was identified as CL01-PC.
- The test account was unlocked.

## 7. Practical Importance

This exercise provides practical experience in:

- Configuring Windows security auditing.
- Monitoring successful and failed authentication attempts.
- Investigating account lockouts.
- Using Windows Event Viewer.
- Identifying important Windows Security Event IDs.
- Understanding basic security monitoring and incident investigation.

## 8. Project Maintainer

**Maintainer:** [@Jaywon123art](https://github.com/Jaywon123art)  
**Project:** Active Directory Cybersecurity Home Lab
