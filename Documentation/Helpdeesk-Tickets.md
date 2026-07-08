\# Help Desk Tickets



This document tracks all completed help desk scenarios performed within the Active Directory lab.



\---



\# HD-001 — Password Reset



\## Ticket Information



\*\*Ticket ID:\*\* HD-001



\*\*Priority:\*\* Medium



\*\*Category:\*\* User Account Administration



\*\*Status:\*\* Completed



\---



\## User Issue



A user contacted the Help Desk after forgetting their Active Directory password and was unable to sign in.



\---



\## Investigation



Verified the user account existed and confirmed the user identity.



Located the account within Active Directory Users and Computers.



\---



\## Resolution



Password was reset using:



\- Active Directory Users and Computers

\- PowerShell



The account was configured to require a password change at the next logon.



\---



\## PowerShell Commands



```powershell

Set-ADAccountPassword `

\-Identity jsmith `

\-NewPassword (ConvertTo-SecureString "Password123!" -AsPlainText -Force)



Set-ADUser jsmith -ChangePasswordAtLogon $true

```



\---



\## Result



\- Password successfully reset

\- User required to create a new password

\- User able to sign in successfully



\---



\# HD-002 — Account Lockout Investigation



\## Ticket Information



\*\*Ticket ID:\*\* HD-002



\*\*Priority:\*\* Medium



\*\*Category:\*\* Account Administration



\*\*Status:\*\* Completed



\---



\## User Issue



User was unable to sign in after entering an incorrect password multiple times.



Windows displayed:



> The referenced account is currently locked out and may not be logged on to.



\---



\## Investigation



Verified the Account Lockout Policy.



Checked for locked accounts using PowerShell.



```powershell

Search-ADAccount -LockedOut

```



Confirmed the user's account was locked.



\---



\## Resolution



Unlocked the account using:



\- Active Directory Users and Computers

\- PowerShell



PowerShell:



```powershell

Unlock-ADAccount sbrown

```



Verified no locked accounts remained.



```powershell

Search-ADAccount -LockedOut

```



\---



\## Result



\- Account successfully unlocked

\- User able to authenticate again

\- Ticket resolved



\---



\# Future Tickets



\- HD-003 User Onboarding

\- HD-004 User Offboarding

\- HD-005 Shared Folder Permissions

\- HD-006 NTFS Permissions

\- HD-007 Network Drive Mapping

\- HD-008 Printer Deployment

\- HD-009 DNS Troubleshooting

\- HD-010 DHCP Troubleshooting

