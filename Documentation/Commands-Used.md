# Commands Used

This document contains PowerShell, Windows, Active Directory, networking, file sharing, and Git commands used throughout the IT Helpdesk Lab project.

---

# HD-001 — Password Reset

## Reset User Password

```powershell
Set-ADAccountPassword `
-Identity jsmith `
-NewPassword (ConvertTo-SecureString "Password123!" -AsPlainText -Force)
```

Resets the Active Directory password for the specified user.

---

## Force User to Change Password at Next Logon

```powershell
Set-ADUser jsmith -ChangePasswordAtLogon $true
```

Requires the user to create a new password after signing in.

---

## Verify User Account Properties

```powershell
Get-ADUser jsmith -Properties PasswordLastSet,PasswordNeverExpires,Enabled |
Format-List Name,Enabled,PasswordLastSet,PasswordNeverExpires
```

Displays password-related account properties.

---

## Graphical Tool

Launch Active Directory Users and Computers.

```cmd
dsa.msc
```

---

# HD-002 — Account Lockout Investigation

## View Locked Accounts

```powershell
Search-ADAccount -LockedOut
```

Displays every locked Active Directory account.

---

## Unlock User Account

```powershell
Unlock-ADAccount sbrown
```

Unlocks the specified user account.

---

## Verify Locked Accounts

```powershell
Search-ADAccount -LockedOut
```

Verifies whether any Active Directory accounts remain locked.

---

# Group Policy Commands

## Refresh Group Policy

```cmd
gpupdate /force
```

Immediately refreshes Computer and User Group Policy.

---

## Account Lockout Policy Location

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Account Policies
                └── Account Lockout Policy
```

Settings configured:

- Account lockout threshold
- Account lockout duration
- Reset account lockout counter

---

# HD-003 — User Onboarding

## Open Active Directory Users and Computers

```cmd
dsa.msc
```

Launches Active Directory Users and Computers.

---

## View User Group Membership

```powershell
Get-ADPrincipalGroupMembership ecarter |
Format-Table Name, GroupScope
```

Displays all Active Directory security groups assigned to the user.

---

## Verify Group Membership Attribute

```powershell
Get-ADUser ecarter -Properties MemberOf |
Select-Object Name,@{Name="Groups";Expression={$_.MemberOf}}
```

Displays the user's Active Directory group membership attribute.

---

## Add User to Security Group

Graphical Tool:

```text
User Properties
└── Member Of
    └── Add...
```

Adds the user to a departmental security group.

---

## Verify User Group Membership (GUI)

Graphical Tool:

```text
User Properties
└── Member Of
```

Verifies the user belongs to the correct Active Directory security groups.

---

# HD-004 — User Offboarding

## Remove User from Security Group

Graphical Tool:

```text
User Properties
└── Member Of
    └── Remove
```

Removes unnecessary security group memberships during the offboarding process.

---

## Disable User Account

Graphical Tool:

```text
Right-click User
└── Disable Account
```

Disables the Active Directory user account.

---

## Move User to Disabled Users OU

Graphical Tool:

```text
Right-click User
└── Move...
```

Moves the account to the Disabled Users Organizational Unit.

---

## Verify Account Status

```powershell
Get-ADUser ecarter -Properties Enabled |
Select-Object Name, Enabled
```

Verifies whether the Active Directory account is enabled or disabled.

---

## Verify Organizational Unit

```powershell
Get-ADUser ecarter |
Select DistinguishedName
```

Displays the distinguished name of the user account, including its Organizational Unit.

---

# HD-005 — Shared Folder Permissions

## Display Network Configuration

```cmd
ipconfig /all
```

Displays complete network adapter configuration.

---

## Flush DNS Cache

```cmd
ipconfig /flushdns
```

Clears the local DNS resolver cache.

---

## Register DNS Records

```cmd
ipconfig /registerdns
```

Forces the client or server to register its DNS records.

---

## Test Domain Controller Connectivity

```cmd
ping dc01
```

Verifies hostname resolution and connectivity to the domain controller.

---

## Test Domain Connectivity

```cmd
ping adlab.local
```

Verifies DNS resolution using the Active Directory domain name.

---

## Test DNS Resolution

```cmd
nslookup dc01
```

Resolves the domain controller hostname through DNS.

---

## Test DNS Resolution (FQDN)

```cmd
nslookup adlab.local
```

Verifies DNS resolution for the Active Directory domain.

---

## Access Shared Folder

```text
\\dc01\Sales
```

Opens the Sales network share from a domain-joined client workstation.

---

# HD-006 — NTFS Permissions

## View NTFS Permissions

```powershell
Get-Acl "C:\CompanyShares\HR" | Format-List
```

Displays the NTFS Access Control List (ACL) for the HR folder.

---

## View SMB Share Permissions

```powershell
Get-SmbShareAccess -Name HR
```

Displays all configured share permissions for the HR network share.

---

## Access Shared Folder

```text
\\dc01\HR
```

Tests network access to the HR shared folder from a domain-joined client.

---

# HD-007 — Network Drive Mapping

## Map Network Drive (GUI)

Graphical Tool:

```text
This PC
└── Map network drive
    ├── Drive: S:
    └── Folder: \\dc01\Sales
```

Maps the Sales shared folder to a persistent drive letter.

---

## Access Network Share

```text
\\dc01\Sales
```

Opens the Sales shared folder before mapping it as a network drive.

---

## View Mapped Drives

```powershell
Get-PSDrive
```

Displays all PowerShell drives, including mapped network drives.

---

## View Network Connections

```cmd
net use
```

Displays all active mapped network drives and network connections.

---

# Active Directory Administration

## Open Active Directory Users and Computers

```cmd
dsa.msc
```

---

## Open Group Policy Management

```cmd
gpmc.msc
```

---

## Open Local Security Policy

```cmd
secpol.msc
```

---

## Open Computer Management

```cmd
compmgmt.msc
```

---

# Networking Commands

## Display Network Configuration

```cmd
ipconfig /all
```

Displays complete network configuration.

---

## Flush DNS Cache

```cmd
ipconfig /flushdns
```

Clears the local DNS cache.

---

## Register DNS Records

```cmd
ipconfig /registerdns
```

Registers the computer's DNS records with the configured DNS server.

---

## Test Connectivity

```cmd
ping dc01
```

Tests communication with the domain controller.

```cmd
ping 192.168.66.10
```

Tests network connectivity using the server's IP address.

```cmd
ping adlab.local
```

Tests connectivity using the Active Directory domain name.

---

## Test DNS Resolution

```cmd
nslookup dc01
```

Verifies DNS name resolution for the domain controller.

```cmd
nslookup adlab.local
```

Verifies Active Directory DNS functionality.

---

# Git Commands

## Check Repository Status

```bash
git status
```

Displays modified, staged, and untracked files.

---

## Stage All Files

```bash
git add .
```

Stages all changes.

---

## Commit Changes

```bash
git commit -m "Commit message"
```

Creates a new Git commit.

---

## Push to GitHub

```bash
git push origin main
```

Uploads commits to GitHub.

---

## Pull Latest Changes

```bash
git pull origin main
```

Downloads updates from GitHub.

---

## View Commit History

```bash
git log --oneline
```

Displays concise commit history.

---

## Clone Repository

```bash
git clone https://github.com/Amaggs99/IT-Helpdesk-Lab.git
```

Downloads the repository locally.

---

## Display Current Directory

```bash
pwd
```

Shows the current working directory.

---

## Change Directory

```bash
cd FolderName
```

Moves to another directory.

---

## List Files

```bash
ls
```

Lists files and folders.

---

## Create Folder

```bash
mkdir FolderName
```

Creates a new folder.

---

## Create File

```bash
touch filename.md
```

Creates a new Markdown file.

---

## Rename File

```bash
mv oldname.md newname.md
```

Renames a file.

---

# Skills Demonstrated

The commands in this document demonstrate experience with:

- Windows Server Administration
- Active Directory Users and Computers (ADUC)
- Active Directory User Lifecycle Management
- Active Directory Account Management
- Security Group Administration
- Organizational Unit (OU) Management
- Shared Folder Administration
- NTFS Permission Administration
- SMB Share Administration
- Network Drive Mapping
- SMB Network Shares
- PowerShell Administration
- Group Policy Management
- DNS Troubleshooting
- Windows Networking
- Windows Authentication
- File Server Administration
- Git Version Control
- GitHub Portfolio Documentation