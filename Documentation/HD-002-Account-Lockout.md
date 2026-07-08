# HD-002 — Account Lockout Investigation

## Objective

Simulate a common Help Desk support request by investigating and resolving an Active Directory account lockout caused by multiple failed sign-in attempts.

---

# Ticket Information

**Ticket ID:** HD-002

**Priority:** Medium

**Category:** Account Administration

**Status:** Completed

---

## Scenario

User **Sarah Brown (sbrown)** contacted the Help Desk after being unable to sign in to the domain.

Windows displayed the following message:

> **"The referenced account is currently locked out and may not be logged on to."**

The user's account had exceeded the configured failed sign-in threshold and was automatically locked by the Active Directory Account Lockout Policy.

---

## Environment

| Item | Value |
|------|-------|
| Domain | adlab.local |
| Domain Controller | DC01 |
| Client | CLIENT01 |
| User | Sarah Brown (sbrown) |
| Operating System | Windows Server 2022 |
| Management Tools | Active Directory Users and Computers (ADUC), PowerShell |

---

## Investigation

Verified the configured Account Lockout Policy using Group Policy.

Executed the following PowerShell command to identify locked Active Directory accounts:

```powershell
Search-ADAccount -LockedOut
```

Confirmed that **Sarah Brown (sbrown)** was currently locked out.

Opened **Active Directory Users and Computers** and navigated to the user's account properties.

Verified the **Unlock account** option was available, confirming the account was currently locked.

---

# Resolution

Unlocked the account using **Active Directory Users and Computers**.

Steps performed:

1. Open Active Directory Users and Computers.
2. Navigate to the **Users** Organizational Unit.
3. Open the user account properties.
4. Select the **Account** tab.
5. Enable **Unlock account**.
6. Click **Apply** and **OK**.

The same task was also completed using PowerShell:

```powershell
Unlock-ADAccount sbrown
```

---

# Validation

Completed the following validation tests:

- ✅ Account successfully unlocked
- ✅ Lockout status cleared
- ✅ No remaining locked accounts detected
- ✅ User successfully authenticated
- ✅ Ticket successfully resolved

Verified using:

```powershell
Search-ADAccount -LockedOut
```

No locked accounts were returned.

---

## PowerShell / Commands Used

```powershell
Search-ADAccount -LockedOut

Unlock-ADAccount sbrown

Search-ADAccount -LockedOut

gpupdate /force
```

---

# Result

✔ Account successfully unlocked

✔ User successfully authenticated

✔ Account Lockout Policy verified

✔ Active Directory account functioning normally

✔ Ticket resolved successfully

---

# Lessons Learned

- Investigated Active Directory account lockouts using both ADUC and PowerShell.
- Verified Account Lockout Policy configuration through Group Policy.
- Resolved user authentication issues using graphical and command-line tools.
- Confirmed remediation by validating account status and successful user authentication.
- Reinforced the importance of verifying policy configuration before assuming credential-related issues.

---

## Screenshots

- 01-Account-Lockout-Policy.png
- 02-Locked-Account-Error.png
- 03-ADUC-Unlock-Account.png
- 04-PowerShell-Locked-Accounts.png
- 05-PowerShell-Unlock-Verification.png