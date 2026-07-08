# HD-003 — User Onboarding

## Objective

Simulate a common Help Desk request by creating a new Active Directory user account for a recently hired employee. Demonstrate how to provision the account, assign the appropriate security group, configure initial account settings, and verify the configuration using both Active Directory Users and Computers (ADUC) and PowerShell.

---

# Ticket Information

**Ticket ID:** HD-003

**Priority:** Medium

**Category:** User Administration

**Status:** Completed

---

## Scenario

Human Resources submitted a request to create a new Active Directory account for a newly hired employee.

Employee Information:

- **Name:** Emily Carter
- **Username:** ecarter
- **Department:** Sales

The Help Desk was responsible for:

- Creating the Active Directory user account.
- Placing the account in the appropriate Organizational Unit.
- Assigning the correct security group.
- Requiring a password change at first logon.
- Verifying the account configuration.

---

## Environment

| Item | Value |
|------|-------|
| Domain | adlab.local |
| Domain Controller | DC01 |
| Client | CLIENT01 |
| User | Emily Carter (ecarter) |
| Operating System | Windows Server 2022 |
| Management Tools | Active Directory Users and Computers (ADUC), PowerShell |

---

## Investigation

Verified the onboarding request submitted by Human Resources.

Confirmed the **Company → Users** Organizational Unit existed for user accounts.

Verified the **Sales** security group already existed and was available for assignment.

Reviewed the requested account information before creating the new user.

---

# Resolution

Opened **Active Directory Users and Computers (ADUC)**.

Navigated to:

```text
Company
└── Users
```

Created a new Active Directory user account using the following information:

| Property | Value |
|----------|-------|
| First Name | Emily |
| Last Name | Carter |
| Username | ecarter |

Configured the account to require a password change at the next successful sign-in.

Added the user to the **Sales** Active Directory security group.

Verified the group membership using both ADUC and PowerShell.

Executed the following PowerShell commands:

```powershell
Get-ADUser ecarter -Properties MemberOf |
Select-Object Name,@{Name="Groups";Expression={$_.MemberOf}}

Get-ADPrincipalGroupMembership ecarter |
Format-Table Name,GroupScope
```

Confirmed the account was a member of:

- Domain Users
- Sales

---

## Validation

Completed the following validation tests:

- ✅ Active Directory user account successfully created
- ✅ User account located in the Company → Users Organizational Unit
- ✅ Sales security group assigned
- ✅ Password change required at next logon
- ✅ Group membership verified using ADUC
- ✅ Group membership verified using PowerShell

---

## PowerShell / Commands Used

```powershell
Get-ADUser ecarter -Properties MemberOf |
Select-Object Name,@{Name="Groups";Expression={$_.MemberOf}}

Get-ADPrincipalGroupMembership ecarter |
Format-Table Name,GroupScope
```

---

## Result

✔ Active Directory user account successfully created

✔ User added to the Sales security group

✔ Password change enforced at next logon

✔ Group membership successfully verified

✔ User account provisioned according to company standards

✔ Ticket resolved successfully

---

## Lessons Learned

- Created new Active Directory user accounts using Active Directory Users and Computers.
- Assigned users to security groups based on departmental access requirements.
- Verified group membership using both graphical tools and PowerShell.
- Reinforced the importance of validating user account configuration before closing a Help Desk ticket.
- Demonstrated a standard enterprise user onboarding workflow.

---

## Screenshots

- 01-New-User-Wizard.png
- 02-User-Created.png
- 03-User-Group-Membership.png
- 04-Sales-Group-Members.png
- 05-PowerShell-Verification.png