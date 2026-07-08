# HD-003 — User Onboarding

## Objective

Simulate a common Help Desk request where Human Resources has hired a new employee. Create the user account in Active Directory, assign the appropriate security group, and verify the configuration using both Active Directory Users and Computers (ADUC) and PowerShell.

---

## Ticket Information

| Field | Value |
|------|-------|
| Ticket ID | HD-003 |
| Priority | Medium |
| Category | User Administration |
| Status | Completed |

---

## Scenario

Human Resources submitted a request to create a new Active Directory account for a recently hired employee.

Employee Information:

- **Name:** Emily Carter
- **Username:** ecarter
- **Department:** Sales

Requested Tasks:

- Create the Active Directory user account
- Place the user in the Company Users OU
- Add the user to the Sales security group
- Require a password change at first logon
- Verify configuration using PowerShell

---

## Environment

| Item | Value |
|------|-------|
| Domain | adlab.local |
| Domain Controller | DC01 |
| Client | Windows 11 Client |
| Management Tool | Active Directory Users and Computers |
| PowerShell | ActiveDirectory Module |

---

## Procedure

### 1. Create the User Account

Opened **Active Directory Users and Computers** and navigated to:

```
Company
└── Users
```

Created a new user with the following information:

| Property | Value |
|----------|-------|
| First Name | Emily |
| Last Name | Carter |
| Username | ecarter |

Configured the account to require a password change during the first successful sign-in.

Screenshot:

`HD-003-01-New-User-Wizard.png`

---

### 2. Verify User Creation

Confirmed that the new user account appeared in the **Company → Users** Organizational Unit.

Screenshot:

`HD-003-02-User-Created.png`

---

### 3. Assign Security Group

Opened the user's **Member Of** tab and added the account to the **Sales** security group.

Verified membership included:

- Domain Users
- Sales

Screenshot:

`HD-003-03-User-Group-Membership.png`

---

### 4. Verify Group Membership

Opened the **Sales** security group and confirmed Emily Carter appeared as a member.

Screenshot:

`HD-003-04-Sales-Group-Members.png`

---

### 5. PowerShell Verification

Verified the account and group membership using PowerShell.

Commands used:

```powershell
Get-ADUser ecarter -Properties MemberOf |
Select-Object Name,@{Name="Groups";Expression={$_.MemberOf}}

Get-ADPrincipalGroupMembership ecarter |
Format-Table Name,GroupScope
```

PowerShell confirmed:

- User account exists
- Member of Domain Users
- Member of Sales security group

Screenshot:

`HD-003-05-PowerShell-Verification.png`

---

## Resolution

Successfully created the new Active Directory user account for Emily Carter.

The account was:

- Created successfully
- Added to the Sales security group
- Configured to change password at first logon
- Verified through both ADUC and PowerShell

The onboarding request was completed successfully.

---

## Verification Checklist

- ✅ User account created
- ✅ User visible in Company → Users
- ✅ Added to Sales security group
- ✅ Password change required at first logon
- ✅ Verified using PowerShell

---

## Commands Used

```powershell
Get-ADUser ecarter -Properties MemberOf |
Select-Object Name,@{Name="Groups";Expression={$_.MemberOf}}

Get-ADPrincipalGroupMembership ecarter |
Format-Table Name,GroupScope
```

---

## Lessons Learned

- Created new Active Directory user accounts using ADUC.
- Assigned users to security groups for access management.
- Verified group membership through both GUI and PowerShell.
- Reinforced the importance of validating account configuration after onboarding.