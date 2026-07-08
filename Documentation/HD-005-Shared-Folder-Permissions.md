# HD-005 — Shared Folder Permissions

## Objective

Simulate a common Help Desk request by creating a departmental shared folder, assigning Active Directory security group permissions, publishing the share on the network, and verifying user access from a Windows client.

---

# Ticket Information

**Ticket ID:** HD-005

**Priority:** Medium

**Category:** File Services

**Status:** Completed

---

## Scenario

The Sales department requested a shared network folder where all Sales employees could store and access department documents.

Requirements:

- Create a shared folder on the file server.
- Allow only members of the Sales security group to access the folder.
- Verify users can access the share from a domain-joined Windows client.

---

## Environment

| Item | Value |
|------|-------|
| Domain | adlab.local |
| Domain Controller | DC01 |
| Client | CLIENT01 |
| Share Name | Sales |
| Folder Path | C:\CompanyShares\Sales |
| Security Group | Sales |

---

# Investigation

Verified the Sales Active Directory security group already existed.

Confirmed user **Mike Wilson (mwilson)** was a member of the Sales security group.

Verified the Windows 11 client was successfully joined to the Active Directory domain.

---

# Resolution

Created the shared folder:

```
C:\CompanyShares\Sales
```

Created a **Welcome.txt** file inside the shared folder for access testing.

Configured NTFS permissions:

- Sales → Modify
- Administrators → Full Control
- SYSTEM → Full Control

Configured Share permissions:

- Sales → Change
- Sales → Read

Verified DNS resolution between CLIENT01 and DC01.

Verified network connectivity using `ping` and `nslookup`.

Logged into CLIENT01 using the **mwilson** domain account.

Successfully accessed the network share:

```
\\dc01\Sales
```

Opened **Welcome.txt** to verify read access.

---

# Validation

Completed the following validation tests:

- ✅ Shared folder successfully created
- ✅ Share permissions configured
- ✅ NTFS permissions configured
- ✅ DNS name resolution successful
- ✅ Client successfully authenticated to the domain
- ✅ Shared folder accessible from CLIENT01
- ✅ Welcome.txt successfully opened

---

## Troubleshooting

During testing, the Windows 11 client was unable to authenticate to the Active Directory domain because the Domain Controller had both **NAT** and **Host-Only** network adapters registered in DNS. This resulted in inconsistent name resolution and prevented successful domain authentication.

### Resolution

- Disabled the NAT network adapter on DC01.
- Re-registered the Domain Controller DNS records using:

```cmd
ipconfig /registerdns
```

- Removed the stale DNS record associated with the NAT adapter from DNS Manager.
- Flushed the DNS resolver cache on CLIENT01 using:

```cmd
ipconfig /flushdns
```

- Verified successful name resolution using `nslookup`.
- Verified network connectivity using `ping`.

These actions restored proper Active Directory name resolution and allowed the Windows 11 client to successfully authenticate and access the `\\dc01\Sales` shared folder.

---

## PowerShell / Commands Used

```powershell
ipconfig /all

ipconfig /flushdns

ipconfig /registerdns

ping dc01

ping adlab.local

nslookup dc01

nslookup adlab.local
```

---

# Result

✔ Shared folder successfully created

✔ NTFS permissions configured correctly

✔ Share permissions configured correctly

✔ Sales security group granted access

✔ Windows client successfully authenticated to the domain

✔ DNS name resolution functioning correctly

✔ Shared folder successfully accessed from CLIENT01

✔ Ticket resolved successfully

---

# Lessons Learned

- Configured SMB shared folders using Windows Server.
- Applied both NTFS and Share permissions using Active Directory security groups.
- Validated user access from a domain-joined Windows client.
- Diagnosed and resolved a real DNS registration issue caused by multiple network adapters.
- Reinforced the importance of validating DNS configuration when troubleshooting Active Directory authentication and network resource access.