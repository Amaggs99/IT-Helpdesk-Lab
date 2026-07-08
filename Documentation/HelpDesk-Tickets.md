# Help Desk Ticket Tracker

This document provides a summary of all completed Help Desk scenarios performed within the Active Directory home lab. Each ticket simulates a realistic IT support request and demonstrates both GUI- and PowerShell-based administration.

---

# Completed Tickets

| Ticket ID | Scenario | Category | Status |
|-----------|----------|----------|--------|
| HD-001 | Password Reset | User Account Administration | ✅ Completed |
| HD-002 | Account Lockout Investigation | Account Administration | ✅ Completed |
| HD-003 | User Onboarding | User Administration | ✅ Completed |

---

# HD-001 — Password Reset

## Summary

Simulated a Help Desk request where a user forgot their Active Directory password and was unable to sign in.

### Tasks Performed

- Verified the user account in Active Directory.
- Reset the user's password using Active Directory Users and Computers (ADUC).
- Configured the account to require a password change at the next logon.
- Verified the configuration using PowerShell.
- Confirmed the user could successfully sign in.

### Technologies Used

- Active Directory Users and Computers
- Windows Server 2022
- PowerShell

### Key PowerShell Commands

```powershell
Set-ADAccountPassword `
-Identity jsmith `
-NewPassword (ConvertTo-SecureString "Password123!" -AsPlainText -Force)

Set-ADUser jsmith -ChangePasswordAtLogon $true
```

---

# HD-002 — Account Lockout Investigation

## Summary

Simulated a user account lockout caused by multiple failed authentication attempts.

### Tasks Performed

- Configured and verified the Account Lockout Policy.
- Forced Group Policy updates.
- Reproduced an account lockout from a client workstation.
- Located and unlocked the account using ADUC.
- Verified the resolution using PowerShell.

### Technologies Used

- Group Policy Management
- Active Directory Users and Computers
- Windows Server 2022
- PowerShell

### Key PowerShell Commands

```powershell
Search-ADAccount -LockedOut

Unlock-ADAccount sbrown

Search-ADAccount -LockedOut
```

---

# HD-003 — User Onboarding

## Summary

Simulated a new employee onboarding request by creating an Active Directory user account and assigning the appropriate security group.

### Tasks Performed

- Created a new Active Directory user account.
- Configured the account to require a password change at first logon.
- Added the user to the Sales security group.
- Verified group membership using ADUC.
- Verified the configuration using PowerShell.

### Technologies Used

- Active Directory Users and Computers
- Windows Server 2022
- PowerShell

### Key PowerShell Commands

```powershell
Get-ADUser ecarter -Properties MemberOf |
Select-Object Name,@{Name="Groups";Expression={$_.MemberOf}}

Get-ADPrincipalGroupMembership ecarter |
Format-Table Name,GroupScope
```

---

# Planned Scenarios

- ⏳ HD-004 — User Offboarding
- ⏳ HD-005 — Shared Folder Permissions
- ⏳ HD-006 — NTFS Permissions
- ⏳ HD-007 — Network Drive Mapping
- ⏳ HD-008 — Printer Deployment
- ⏳ HD-009 — DNS Troubleshooting
- ⏳ HD-010 — DHCP Troubleshooting

---

## Skills Demonstrated

- Active Directory Administration
- User Account Management
- Password Management
- Account Lockout Investigation
- Security Group Management
- Group Policy
- PowerShell Administration
- Windows Server 2022
- Help Desk Troubleshooting
- Technical Documentation