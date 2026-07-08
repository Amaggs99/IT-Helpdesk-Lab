\# Commands Used



This document contains PowerShell, Windows, Active Directory, and Git commands used throughout the IT Helpdesk Lab project.



\---



\# HD-001 — Password Reset



\## Reset User Password



```powershell

Set-ADAccountPassword `

\-Identity jsmith `

\-NewPassword (ConvertTo-SecureString "Password123!" -AsPlainText -Force)

```



Resets the Active Directory password for the specified user.



\---



\## Force User to Change Password at Next Logon



```powershell

Set-ADUser jsmith -ChangePasswordAtLogon $true

```



Requires the user to create a new password after signing in.



\---



\## Verify User Account Properties



```powershell

Get-ADUser jsmith -Properties PasswordLastSet,PasswordNeverExpires,Enabled |

Format-List Name,Enabled,PasswordLastSet,PasswordNeverExpires

```



Displays password-related account properties.



\---



\## Graphical Tool



Launch Active Directory Users and Computers.



```cmd

dsa.msc

```



\---



\# HD-002 — Account Lockout Investigation



\## View Locked Accounts



```powershell

Search-ADAccount -LockedOut

```



Displays every locked Active Directory account.



\---



\## Unlock User Account



```powershell

Unlock-ADAccount sbrown

```



Unlocks the specified user account.



\---



\## Verify User Properties



```powershell

Get-ADUser sbrown -Properties LockedOut

```



Displays lockout-related account information.



\---



\## Refresh Group Policy



```cmd

gpupdate /force

```



Immediately refreshes Computer and User Group Policy.



\---



\## Account Lockout Policy Location



```text

Computer Configuration

└── Policies

&#x20;   └── Windows Settings

&#x20;       └── Security Settings

&#x20;           └── Account Policies

&#x20;               └── Account Lockout Policy

```



Settings configured:



\- Account lockout threshold

\- Account lockout duration

\- Reset account lockout counter



\---



\# Active Directory Administration



\## Open Active Directory Users and Computers



```cmd

dsa.msc

```



\---



\## Open Group Policy Management



```cmd

gpmc.msc

```



\---



\## Open Local Security Policy



```cmd

secpol.msc

```



\---



\## Open Computer Management



```cmd

compmgmt.msc

```



\---



\# Networking Commands



\## Display Network Configuration



```cmd

ipconfig /all

```



Displays complete network configuration.



\---



\## Flush DNS Cache



```cmd

ipconfig /flushdns

```



Clears the local DNS cache.



\---



\## Test Connectivity



```cmd

ping dc01

```



Tests communication with the domain controller.



\---



```cmd

ping 192.168.66.10

```



Tests network connectivity using the IP address.



\---



\## Test DNS Resolution



```cmd

nslookup adlab.local

```



Verifies Active Directory DNS functionality.



\---



\# Git Commands



\## Check Repository Status



```bash

git status

```



Displays modified, staged, and untracked files.



\---



\## Stage All Files



```bash

git add .

```



Stages all changes.



\---



\## Commit Changes



```bash

git commit -m "Commit message"

```



Creates a new Git commit.



\---



\## Push to GitHub



```bash

git push origin main

```



Uploads commits to GitHub.



\---



\## Pull Latest Changes



```bash

git pull origin main

```



Downloads updates from GitHub.



\---



\## View Commit History



```bash

git log --oneline

```



Displays concise commit history.



\---



\## Clone Repository



```bash

git clone https://github.com/Amaggs99/IT-Helpdesk-Lab.git

```



Downloads the repository locally.



\---



\## Display Current Directory



```bash

pwd

```



Shows the current working directory.



\---



\## Change Directory



```bash

cd FolderName

```



Moves to another directory.



\---



\## List Files



```bash

ls

```



Lists files and folders.



\---



\## Create Folder



```bash

mkdir FolderName

```



Creates a new folder.



\---



\## Create File



```bash

touch filename.md

```



Creates a new Markdown file.



\---



\## Rename File



```bash

mv oldname.md newname.md

```



Renames a file.



\---



\# Skills Demonstrated



The commands in this document demonstrate experience with:



\- Windows Server Administration

\- Active Directory Users and Computers (ADUC)

\- PowerShell Administration

\- Group Policy Management

\- Active Directory Account Management

\- DNS Troubleshooting

\- Windows Networking

\- Git Version Control

\- GitHub Portfolio Documentation

