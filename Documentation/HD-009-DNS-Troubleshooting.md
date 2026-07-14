# HD-009 — DNS Resolution Troubleshooting

## Objective

Simulate a common Help Desk request where a user is unable to access network resources due to an incorrect DNS server configuration. Demonstrate how to identify the issue, investigate connectivity, restore the correct DNS settings, and verify successful name resolution using both graphical tools and PowerShell.

---

## Ticket Information

**Ticket ID:** HD-009

**Priority:** High

**Category:** Network Connectivity

**Status:** Completed

---

## Scenario

A user contacted the Help Desk reporting they could still access network resources by IP address but were unable to access servers using hostnames.

Symptoms reported:

- Direct DNS queries were timing out.
- Hostname resolution was unreliable.
- Connectivity to the Domain Controller by IP address remained functional.

The Help Desk was responsible for:

- Investigating the network configuration.
- Identifying the incorrect DNS server.
- Restoring the proper DNS configuration.
- Verifying successful name resolution.
- Confirming normal access to network resources.

---

## Environment

| Item | Value |
|------|-------|
| Domain | adlab.local |
| Domain Controller | DC01 |
| Client | CLIENT01 |
| Operating System | Windows 11 |
| DNS Server | 192.168.66.10 |

---

## Investigation

Verified the client's current TCP/IP configuration using:

```powershell
ipconfig /all
```

Discovered the Preferred DNS Server had been changed from:

```text
192.168.66.10
```

to:

```text
192.168.66.99
```

Performed additional testing.

Connectivity tests confirmed:

- Ping by IP address succeeded.
- `nslookup dc01` timed out while querying the incorrect DNS server.
- Some hostname resolution continued through cached or alternate local name-resolution methods.
- The incorrect DNS server was confirmed as the root cause.

Executed:

```powershell
ping 192.168.66.10

nslookup dc01

Resolve-DnsName dc01
```

The investigation confirmed that basic IP connectivity remained operational while the client was configured to use an invalid DNS server. Although cached or alternate local resolution could temporarily resolve the hostname, direct DNS queries using `nslookup` failed.

---

## Resolution

Opened:

```text
Network Connections
    ↓
Ethernet Properties
    ↓
Internet Protocol Version 4 (TCP/IPv4)
```

Corrected the Preferred DNS Server from:

```text
192.168.66.99
```

to:

```text
192.168.66.10
```

Applied the updated configuration.

Cleared the DNS resolver cache:

```powershell
ipconfig /flushdns
```

Re-registered the computer's DNS records:

```powershell
ipconfig /registerdns
```

Verified DNS functionality using:

```powershell
nslookup dc01

Resolve-DnsName dc01

ping dc01
```

Successfully accessed the Sales shared folder using the server hostname.

---

## Validation

Completed the following validation tests:

- ✅ Incorrect DNS server identified
- ✅ Correct DNS server restored
- ✅ DNS cache successfully flushed
- ✅ DNS records successfully registered
- ✅ Hostname resolution restored
- ✅ Shared folder accessible using hostname
- ✅ PowerShell verification completed

---

## PowerShell / Commands Used

```powershell
ipconfig /all
```

Displays the complete TCP/IP configuration, including DNS server assignments.

```powershell
ipconfig /flushdns
```

Clears the local DNS resolver cache.

```powershell
ipconfig /registerdns
```

Registers the computer's DNS records with the configured DNS server.

```powershell
ping 192.168.66.10
```

Verifies network connectivity to the Domain Controller using its IP address.

```powershell
ping dc01
```

Verifies successful DNS hostname resolution.

```powershell
nslookup dc01
```

Queries the configured DNS server for the IP address of the specified hostname.

```powershell
Resolve-DnsName dc01
```

Uses PowerShell to verify DNS name resolution.

---

## Result

✔ Incorrect DNS server identified

✔ Correct DNS configuration restored

✔ DNS name resolution functioning normally

✔ Shared folder access restored

✔ Network connectivity verified

✔ Ticket resolved successfully

---

## Lessons Learned

- Incorrect DNS settings can prevent hostname resolution while basic network connectivity continues to function.
- Testing both IP connectivity and hostname resolution quickly isolates DNS-related issues.
- `ipconfig /flushdns` removes stale cached DNS entries after configuration changes.
- `Resolve-DnsName` provides a reliable PowerShell method for validating DNS functionality.
- Verifying end-user access after remediation confirms the issue has been fully resolved.

---

## Screenshots

- 01-Working-DNS-Configuration.png
- 02-Incorrect-DNS-Configured.png
- 03-DNS-Resolution-Failure.png
- 04-Network-Connectivity-Still-Working.png
- 05-DNS-Investigation.png
- 06-Correct-DNS-Restored.png
- 07-DNS-Verification-Success.png
- 08-Shared-Folder-Access-Restored.png
- 09-PowerShell-DNS-Verification.png