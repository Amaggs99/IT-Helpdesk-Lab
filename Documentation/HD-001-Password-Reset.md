# HD-001 — Password Reset

## Objective

Simulate a common Help Desk request by resetting a user's forgotten Active Directory password and requiring a password change at the next logon.

---

# Ticket Information

**Ticket ID:** HD-001

**Priority:** Medium

**Category:** User Account Administration

**Status:** Completed

---

## Scenario

User **John Smith (jsmith)** contacted the Help Desk after forgetting their Active Directory password and was unable to sign in to the domain.

---

## Environment

| Item | Value |
|------|-------|
| Domain | adlab.local |
| Domain Controller | DC01 |
| Client | CLIENT01 |
| User | John Smith (jsmith) |

---

# Investigation

Verified the user account existed in Active Directory.

Confirmed the account was enabled and not locked.

Verified the user's identity before performing the password reset.

---

# Resolution

Opened **Active Directory Users and Computers (ADUC)**.

Navigated to:

```text
Company
└── Users
```

Right-clicked **John Smith** and selected **Reset Password**.

Assigned a temporary password.

Enabled:

- User must change password at next logon

Applied the changes.

Performed the same task using PowerShell:

```powershell
Set-ADAccountPassword `
-Identity jsmith `
-NewPassword (ConvertTo-SecureString "Password123!" -AsPlainText -Force)

Set-ADUser jsmith -ChangePasswordAtLogon $true
```

Verified the account properties:

```powershell
Get-ADUser jsmith -Properties PasswordLastSet,PasswordNeverExpires,Enabled |
Format-List Name,Enabled,PasswordLastSet,PasswordNeverExpires
```

---

# Validation

Completed the following validation tests:

- ✅ Password successfully reset
- ✅ User account remained enabled
- ✅ Temporary password accepted
- ✅ User prompted to change password at next logon
- ✅ User successfully authenticated

---

## PowerShell / Commands Used

```powershell
Set-ADAccountPassword `
-Identity jsmith `
-NewPassword (ConvertTo-SecureString "Password123!" -AsPlainText -Force)

Set-ADUser jsmith -ChangePasswordAtLogon $true

Get-ADUser jsmith -Properties PasswordLastSet,PasswordNeverExpires,Enabled |
Format-List Name,Enabled,PasswordLastSet,PasswordNeverExpires
```

---

# Result

✔ Password successfully reset

✔ User required to change password at next sign-in

✔ User successfully authenticated

✔ Ticket resolved successfully

---

# Lessons Learned

- Reset Active Directory user passwords using both ADUC and PowerShell.
- Enforced password changes at the next logon.
- Verified user account status before and after the password reset.
- Reinforced standard Help Desk identity verification procedures before modifying user credentials.

---

## Screenshots

- 01-Reset-Password.png
- 02-Temporary-Password.png
- 03-Force-Password-Change.png
- 04-PowerShell-Verification.png