\# HD-002 — Account Lockout Investigation and Resolution



\## Objective



Simulate a common Help Desk support request where a user's Active Directory account becomes locked after multiple failed sign-in attempts. Demonstrate how to investigate the issue, verify the lockout, unlock the account using both graphical tools and PowerShell, and confirm the account is functional again.



\---



\## Ticket Information



| Item | Value |

|------|-------|

| \*\*Ticket ID\*\* | HD-002 |

| \*\*Priority\*\* | Medium |

| \*\*Category\*\* | Account Administration |

| \*\*Status\*\* | ✅ Completed |



\---



\## Scenario



A user contacted the Help Desk reporting they were unable to sign in to their Windows workstation.



Windows displayed the following message:



> \*\*"The referenced account is currently locked out and may not be logged on to."\*\*



The account had exceeded the configured failed logon threshold and was automatically locked by the Active Directory account lockout policy.



\---



\## Lab Environment



| Item | Value |

|------|-------|

| Domain | adlab.local |

| Domain Controller | DC01 |

| Client Computer | CLIENT01 |

| User Account | Sarah Brown (sbrown) |

| Operating System | Windows Server 2022 |

| Management Tools | Active Directory Users and Computers (ADUC), PowerShell |



\---



\## Account Lockout Policy



Configured through the \*\*Default Domain Policy\*\*.



| Policy Setting | Configuration |

|---------------|---------------|

| Account Lockout Threshold | 3 invalid logon attempts |

| Account Lockout Duration | 15 minutes |

| Reset Account Lockout Counter | 15 minutes |



\---



\# Investigation



\## Verify Locked Accounts (PowerShell)



To identify any locked Active Directory accounts, the following PowerShell command was executed:



```powershell

Search-ADAccount -LockedOut

```



\### Result



The command confirmed that \*\*Sarah Brown (sbrown)\*\* was currently locked out.



\---



\## Verify User Properties (GUI)



Opened \*\*Active Directory Users and Computers\*\* and navigated to:



```text

adlab.local

└── Company

&#x20;   └── Users

&#x20;       └── Sarah Brown

&#x20;           └── Properties

&#x20;               └── Account

```



Confirmed the \*\*Unlock account\*\* option was available, indicating that the account was currently locked.



\---



\# Resolution



\## Method 1 — Active Directory Users and Computers



Performed the following steps:



1\. Open Active Directory Users and Computers.

2\. Navigate to the \*\*Users\*\* Organizational Unit.

3\. Open the user account properties.

4\. Select the \*\*Account\*\* tab.

5\. Check \*\*Unlock account\*\*.

6\. Click \*\*Apply\*\* and \*\*OK\*\*.



\---



\## Method 2 — PowerShell



Unlocked the account using PowerShell.



```powershell

Unlock-ADAccount sbrown

```



\---



\## Verification



Confirmed the account was no longer locked.



```powershell

Search-ADAccount -LockedOut

```



\### Result



No locked accounts were returned.



The user successfully authenticated after the account was unlocked.



\---



\# PowerShell Commands Used



\## View Locked Accounts



```powershell

Search-ADAccount -LockedOut

```



Displays all currently locked Active Directory accounts.



\---



\## Unlock User Account



```powershell

Unlock-ADAccount sbrown

```



Unlocks the specified Active Directory user account.



\---



\# Screenshots Collected



The following screenshots were captured during this lab:



\- Account-Lockout-Policy.png

\- Locked-Account-Error.png

\- ADUC-Unlock-Account.png

\- PowerShell-Locked-Accounts.png

\- PowerShell-Unlock-Verification.png



\---



\# Skills Demonstrated



\- Active Directory User Administration

\- Help Desk Account Troubleshooting

\- Account Lockout Investigation

\- PowerShell Administration

\- Group Policy Verification

\- Windows Authentication Troubleshooting

\- Active Directory Users and Computers (ADUC)



\---



\# Lessons Learned



\- Active Directory account lockout policies protect against repeated failed authentication attempts.

\- PowerShell provides a fast method for identifying and unlocking user accounts.

\- Group Policy settings directly influence authentication behavior across the domain.

\- Both GUI and PowerShell methods should be understood by Help Desk technicians.

\- Verifying the resolution ensures the user can successfully sign in after remediation.



\---



\## Outcome



✅ Successfully investigated the account lockout.



✅ Verified the account was locked through both ADUC and PowerShell.



✅ Unlocked the account using administrative tools.



✅ Confirmed successful authentication after remediation.



\*\*Ticket Status:\*\* Closed

