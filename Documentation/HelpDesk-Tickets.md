# Help Desk Ticket Tracker

This document provides a summary of all completed Help Desk scenarios performed within the IT Helpdesk Lab. Each ticket simulates a realistic Help Desk request commonly encountered in an enterprise Active Directory environment.

---

# Completed Tickets

| Ticket ID | Scenario | Category | Status |
|-----------|----------|----------|--------|
| HD-001 | Password Reset | User Account Administration | ✅ Completed |
| HD-002 | Account Lockout Investigation | Account Administration | ✅ Completed |
| HD-003 | User Onboarding | User Administration | ✅ Completed |
| HD-004 | User Offboarding | User Administration | ✅ Completed |
| HD-005 | Shared Folder Permissions | File Services | ✅ Completed |
| HD-006 | NTFS Permissions | File Services | ✅ Completed |
| HD-007 | Network Drive Mapping | File Services | ✅ Completed |
| HD-008 | Printer Deployment | Printer Administration | ✅ Completed |

---

# HD-001 — Password Reset

## Summary

Simulated a Help Desk request where a user forgot their Active Directory password and required a password reset.

### Technologies Used

- Active Directory Users and Computers (ADUC)
- Windows Server 2022
- PowerShell

---

# HD-002 — Account Lockout Investigation

## Summary

Simulated an Active Directory account lockout caused by multiple failed logon attempts. Investigated the issue, verified the account lockout policy, and restored user access.

### Technologies Used

- Active Directory Users and Computers (ADUC)
- Group Policy Management
- Windows Server 2022
- PowerShell

---

# HD-003 — User Onboarding

## Summary

Simulated onboarding a new employee by creating a domain user account, assigning organizational unit placement, configuring account settings, and adding the user to the appropriate security group.

### Technologies Used

- Active Directory Users and Computers (ADUC)
- Windows Server 2022
- PowerShell

---

# HD-004 — User Offboarding

## Summary

Simulated employee termination by removing unnecessary group memberships, disabling the Active Directory account, and moving the account into a Disabled Users organizational unit.

### Technologies Used

- Active Directory Users and Computers (ADUC)
- Windows Server 2022
- PowerShell

---

# HD-005 — Shared Folder Permissions

## Summary

Simulated a departmental file share request by creating a shared folder, assigning NTFS and Share permissions to an Active Directory security group, and validating user access from a domain-joined Windows client.

### Technologies Used

- Windows Server 2022
- Active Directory Users and Computers (ADUC)
- File and Storage Services
- NTFS Permissions
- SMB Share Permissions
- DNS
- Windows Networking
- PowerShell

---

# HD-006 — NTFS Permissions

## Summary

Simulated a Help Desk request requiring a confidential Human Resources shared folder. Configured NTFS permissions, SMB share permissions, validated access for authorized users, denied unauthorized users, and verified configuration using PowerShell.

### Technologies Used

- Windows Server 2022
- Active Directory
- NTFS Permissions
- SMB File Shares
- PowerShell

---

# HD-007 — Network Drive Mapping

## Summary

Simulated a Help Desk request where a user required a persistent mapped network drive to access a departmental shared folder.

### Technologies Used

- Windows Server 2022
- Windows 11
- SMB File Sharing
- Windows File Explorer
- PowerShell

---

# HD-008 — Printer Deployment

## Summary

Simulated a Help Desk request to deploy a shared network printer from a Windows Server to a domain-joined Windows client. Installed a Generic / Text Only printer, enabled printer sharing, connected the client to the shared printer, and verified the deployment using PowerShell.

### Technologies Used

- Windows Server 2022
- Windows 11
- Print Management
- Printer Sharing
- Devices and Printers
- SMB Networking
- PowerShell

---

# Planned Scenarios

- ⏳ HD-009 — DNS Troubleshooting
- ⏳ HD-010 — DHCP Troubleshooting

---

# Skills Demonstrated

- Windows Server Administration
- Active Directory User Management
- Password Management
- Account Lockout Investigation
- User Onboarding
- User Offboarding
- Security Group Administration
- Shared Folder Administration
- NTFS Permissions
- SMB Share Permissions
- Network Drive Mapping
- Printer Administration
- DNS Administration
- Windows Networking
- Group Policy Management
- PowerShell Administration
- Help Desk Troubleshooting
- Technical Documentation
- Git Version Control
- GitHub Portfolio Development