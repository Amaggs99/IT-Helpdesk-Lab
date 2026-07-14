# HD-007 — Network Drive Mapping

## Objective

Simulate a common Help Desk request by mapping a departmental network drive for a domain user. Verify that the mapped drive reconnects automatically at sign-in and allows authorized users to access shared departmental resources.

---

## Ticket Information

**Ticket ID:** HD-007

**Priority:** Medium

**Category:** File Services

**Status:** Completed

---

## Scenario

The Sales department requested that employees have easier access to their shared folder by mapping it as a persistent network drive.

Instead of manually browsing to:

```text
\\DC01\Sales
```

users should be able to access the shared folder through the **S:** drive.

The Help Desk was responsible for:

- Mapping the Sales network share.
- Configuring the drive to reconnect automatically at sign-in.
- Verifying access to the shared folder.
- Confirming persistence after logging off and back on.
- Validating the mapping using PowerShell.

---

## Environment

| Item | Value |
|------|-------|
| Domain | adlab.local |
| Domain Controller | DC01 |
| Client | CLIENT01 |
| User | Mike Wilson (mwilson) |
| Share | \\DC01\Sales |
| Drive Letter | S: |
| Operating System | Windows 11 |

---

## Investigation

Verified the following before creating the mapped drive:

- The Sales shared folder already existed.
- Mike Wilson (mwilson) was a member of the Sales security group.
- CLIENT01 was successfully joined to the Active Directory domain.
- The Sales share was accessible using its UNC path.

---

## Resolution

Opened **File Explorer** on CLIENT01.

Navigated to:

```text
This PC
└── Map network drive
```

Configured the following settings:

| Setting | Value |
|---------|-------|
| Drive Letter | S: |
| Folder | \\DC01\Sales |
| Reconnect at sign-in | Enabled |
| Connect using different credentials | Disabled |

Completed the network drive mapping.

Verified the mapped drive appeared under **This PC**.

Opened the mapped drive and confirmed the **Welcome.txt** file was accessible.

Logged off the workstation and signed back in to verify the drive automatically reconnected.

Validated the mapping using PowerShell.

---

## Validation

Completed the following validation tests:

- ✅ Network drive successfully mapped
- ✅ Drive assigned the letter **S:**
- ✅ Sales shared folder accessible
- ✅ Welcome.txt opened successfully
- ✅ Drive automatically reconnected after sign-in
- ✅ Verified using PowerShell
- ✅ Verified using **net use**

---

## PowerShell / Commands Used

```powershell
Get-PSDrive
```

Displays all available PowerShell drives, including mapped network drives.

```cmd
net use
```

Displays active mapped network drives and network connections.

---

## Result

✔ Sales network drive successfully mapped

✔ Drive automatically reconnected after user sign-in

✔ User successfully accessed shared resources

✔ PowerShell verification completed successfully

✔ Network drive available through drive letter **S:**

✔ Ticket resolved successfully

---

## Lessons Learned

- Network drive mapping provides users with a consistent drive letter for accessing shared resources.
- Persistent mappings automatically reconnect after user sign-in.
- Mapping network drives simplifies access to departmental file shares.
- PowerShell and **net use** provide quick methods for validating mapped network drives.
- Network drive mappings rely on proper Active Directory authentication and SMB share permissions.

---

## Screenshots

- 01-Map-Network-Drive.png
- 02-Network-Drive-Mapped.png
- 03-Drive-Access.png
- 04-Reconnected-After-Logon.png
- 05-PowerShell-Verification.png