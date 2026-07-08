\# HD-004 — User Offboarding



\## Objective



Simulate a common Help Desk request where an employee leaves the organization. Secure the Active Directory account by removing unnecessary group memberships, disabling the account, moving it to the Disabled Users Organizational Unit (OU), and verifying the changes using both Active Directory Users and Computers (ADUC) and PowerShell.



\---



\## Ticket Information



| Field | Value |

|------|-------|

| Ticket ID | HD-004 |

| Priority | Medium |

| Category | User Administration |

| Status | Completed |



\---



\## Scenario



Human Resources notified the Help Desk that employee \*\*Emily Carter (ecarter)\*\* had left the organization.



Following company offboarding procedures, the account needed to be secured while retaining it for auditing and future reference.



Required tasks:



\- Remove the user from departmental security groups

\- Disable the Active Directory account

\- Move the account to the Disabled Users OU

\- Verify the account status

\- Verify the account location



\---



\## Environment



| Item | Value |

|------|-------|

| Domain | adlab.local |

| Domain Controller | DC01 |

| Client | Windows 11 Client |

| Management Tool | Active Directory Users and Computers |

| PowerShell | ActiveDirectory Module |



\---



\## Procedure



\### 1. Remove Security Group Membership



Opened the user's \*\*Member Of\*\* tab and removed the \*\*Sales\*\* security group while leaving \*\*Domain Users\*\* assigned.



Screenshot:



`HD-004-01-Remove-Group-Membership.png`



\---



\### 2. Disable the User Account



Disabled the Active Directory account using ADUC.



Verified the account displayed the disabled account icon.



Screenshot:



`HD-004-02-Disable-User-Account.png`



\---



\### 3. Move Account to Disabled Users OU



Moved the account from the \*\*Users\*\* OU into the \*\*Disabled Users\*\* OU.



Screenshot:



`HD-004-03-Move-To-Disabled-Users.png`



\---



\### 4. Verify Account Status



Verified the account was disabled using PowerShell.



```powershell

Get-ADUser ecarter -Properties Enabled |

Select-Object Name, Enabled

```



Result:



\- Account exists

\- Enabled = False



Screenshot:



`HD-004-04-Verify-Account-Disabled.png`



\---



\### 5. Verify Organizational Unit



Verified the account was moved into the Disabled Users OU.



```powershell

Get-ADUser ecarter |

Select DistinguishedName

```



Screenshot:



`HD-004-05-Verify-Disabled-Users-OU.png`



\---



\## Resolution



Successfully completed the employee offboarding process.



Actions completed:



\- Removed unnecessary security group membership

\- Disabled the user account

\- Moved the account to the Disabled Users OU

\- Verified all changes using PowerShell



The account is now secured while remaining available for future auditing.



\---



\## Verification Checklist



\- ✅ Sales security group removed

\- ✅ Account disabled

\- ✅ Account moved to Disabled Users OU

\- ✅ Verified using ADUC

\- ✅ Verified using PowerShell



\---



\## Commands Used



```powershell

Get-ADUser ecarter -Properties Enabled |

Select-Object Name, Enabled



Get-ADUser ecarter |

Select DistinguishedName

```



\---



\## Lessons Learned



\- Practiced the standard Active Directory user offboarding process.

\- Removed unnecessary permissions by updating group memberships.

\- Disabled accounts instead of deleting them to preserve audit history.

\- Verified administrative changes using both ADUC and PowerShell.

