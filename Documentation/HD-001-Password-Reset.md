\# Ticket HD-001 - Password Reset



\## Ticket Information



\*\*Ticket ID:\*\* HD-001



\*\*Priority:\*\* Medium



\*\*Category:\*\* User Account Management



\*\*Status:\*\* Resolved



\---



\## Scenario



User \*\*John Smith (jsmith)\*\* contacted the Help Desk because they forgot their password and could no longer sign in to the domain.



\---



\## Symptoms



\- User unable to authenticate.

\- Password forgotten.

\- Account not locked.



\---



\## Resolution (Active Directory GUI)



1\. Open \*\*Active Directory Users and Computers\*\*.

2\. Navigate to:



```text

Company

└── Users

```



3\. Right-click \*\*John Smith\*\*.

4\. Select \*\*Reset Password\*\*.

5\. Assign a temporary password.

6\. Enable \*\*User must change password at next logon\*\*.

7\. Apply the changes.



\---



\## Resolution (PowerShell)



```powershell

Set-ADAccountPassword `

\-Identity jsmith `

\-NewPassword (ConvertTo-SecureString "Password123!" -AsPlainText -Force)



Set-ADUser jsmith -ChangePasswordAtLogon $true



Get-ADUser jsmith -Properties PasswordLastSet,PasswordNeverExpires,Enabled |

Format-List Name,Enabled,PasswordLastSet,PasswordNeverExpires

```



\---



\## Validation



\- Password reset successfully.

\- User authenticated successfully.

\- Windows prompted the user to change the password at first sign in.

\- Account verified as enabled.



\---



\## Skills Demonstrated



\- Active Directory Administration

\- Password Management

\- User Authentication

\- Windows Server Administration

\- PowerShell Administration

\- Help Desk Troubleshooting



\---



\## Screenshots



\- Password-Reset-01.png

\- Password-Reset-02.png

\- Password-Reset-03.png

\- Password-Reset-04-PowerShell.png



\---



\## Outcome



The user successfully logged into the domain after changing their temporary password. The ticket was resolved without additional escalation.

