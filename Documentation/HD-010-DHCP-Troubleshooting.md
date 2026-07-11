\# HD-010 — DHCP Server Installation, Configuration, and Troubleshooting



\---



\## Table of Contents



\- \[Objective](#objective)

\- \[Ticket Information](#ticket-information)

\- \[Scenario](#scenario)

\- \[Environment](#environment)

\- \[Initial Verification](#initial-verification)

\- \[Installing the DHCP Server Role](#installing-the-dhcp-server-role)

\- \[Authorizing the DHCP Server](#authorizing-the-dhcp-server)

\- \[Creating the DHCP Scope](#creating-the-dhcp-scope)

\- \[Verifying DHCP Lease Assignment](#verifying-dhcp-lease-assignment)

\- \[Verifying Active DHCP Lease](#verifying-active-dhcp-lease)

\- \[Simulating the Failure](#simulating-the-failure)

\- \[Restoring the DHCP Service](#restoring-the-dhcp-service)

\- \[Verification](#verification)

\- \[PowerShell / Command Prompt Commands Used](#powershell--command-prompt-commands-used)

\- \[Skills Demonstrated](#skills-demonstrated)

\- \[Lessons Learned](#lessons-learned)



\---



\## Objective



Simulate a common Help Desk incident where a Windows client is unable to obtain a valid IP address because the DHCP Server service is unavailable. Demonstrate the complete lifecycle of installing, configuring, verifying, troubleshooting, and restoring a Windows Server 2022 DHCP environment while documenting each step using enterprise-style technical documentation.



\---



\## Ticket Information



| Item | Value |

|------|-------|

| Ticket ID | HD-010 |

| Priority | High |

| Category | Network Services |

| Status | Completed |



\---



\## Scenario



A user reported that their Windows workstation could no longer connect to the network after restarting their computer.



The workstation was configured to obtain an IP address automatically but failed to receive a valid DHCP lease.



The objective was to investigate the issue, verify DHCP server availability, restore service, and confirm the client successfully obtained a new lease.



\---



\## Environment



| Component | Value |

|-----------|-------|

| Domain | adlab.local |

| Domain Controller | DC01 |

| Client Computer | CLIENT01 |

| Server OS | Windows Server 2022 |

| Client OS | Windows 11 |

| Network | 192.168.66.0/24 |

| DHCP Scope | 192.168.66.100 – 192.168.66.200 |

| DNS Server | 192.168.66.10 |

| Virtualization | VMware Workstation Pro |



\---



\# Initial Verification



Verified the client network configuration before beginning troubleshooting.



Confirmed:



\- DHCP Enabled

\- IPv4 configuration

\- DNS configuration

\- Existing lease information



\### Screenshot



!\[Working DHCP Configuration](../Screenshots/HD-010/HD-010-01-Working-DHCP-Configuration.png)



\---



\# Installing the DHCP Server Role



The DHCP Server role was installed using Server Manager.



After installation, the server was authorized within Active Directory.



\### Screenshot



!\[DHCP Role Installed](../Screenshots/HD-010/HD-010-02-DHCP-Role-Installed.png)



\---



\# Authorizing the DHCP Server



Completed the post-installation configuration wizard to authorize the DHCP server within the Active Directory domain.



Authorization ensures the DHCP server is permitted to issue IP addresses to domain clients.



\### Screenshot



!\[DHCP Authorization](../Screenshots/HD-010/HD-010-03-DHCP-Authorized.png)



\---



\# Creating the DHCP Scope



Configured an IPv4 scope with the following settings.



| Setting | Value |

|---------|-------|

| Scope Name | Office Network |

| Address Range | 192.168.66.100 – 192.168.66.200 |

| Subnet Mask | 255.255.255.0 |

| DNS Server | 192.168.66.10 |

| Domain | adlab.local |



The scope was activated after configuration.



\### Screenshot



!\[DHCP Scope](../Screenshots/HD-010/HD-010-04-DHCP-Scope-Configured.png)



\---



\# Verifying DHCP Lease Assignment



After configuring DHCP, CLIENT01 successfully obtained an IP address from DC01.



Verified:



\- DHCP Enabled

\- DHCP Server

\- DNS Server

\- Assigned IPv4 Address



\### Screenshot



!\[DHCP Lease Assigned](../Screenshots/HD-010/HD-010-05-DHCP-Lease-Assigned.png)



\---



\# Verifying Active DHCP Lease



Confirmed that the client lease appeared within the DHCP management console.



Verified:



\- Client hostname

\- Assigned IP address

\- Lease expiration

\- MAC address



\### Screenshot



!\[Address Lease](../Screenshots/HD-010/HD-010-06-Address-Lease.png)



\---



\# Simulating the Failure



To simulate a realistic enterprise Help Desk incident, the DHCP Server service was intentionally stopped.



The client attempted to renew its IP configuration but could not contact the DHCP server.



Observed:



\- DHCP renewal failure

\- Request timeout

\- Client unable to obtain a lease



\### Screenshot



!\[DHCP Failure](../Screenshots/HD-010/HD-010-07-DHCP-Service-Failure.png)



\---



\# Restoring the DHCP Service



Verified that the DHCP Server service was stopped.



Restarted the service using Windows Services.



Confirmed:



\- DHCP Server service status changed to Running.



\### Screenshot



!\[DHCP Service Restored](../Screenshots/HD-010/HD-010-08-DHCP-Service-Restored.png)



\---



\# Recovery



After restoring the DHCP service, CLIENT01 successfully renewed its lease.



Verified:



\- New DHCP lease

\- Correct DNS server

\- Successful IP configuration



\### Screenshot



!\[DHCP Recovery](../Screenshots/HD-010/HD-010-09-DHCP-Recovery.png)



\---



\# Verification



Performed post-recovery validation.



Executed:



```powershell

ipconfig /all

ping 192.168.66.10

ping dc01.adlab.local

nslookup dc01.adlab.local

```



Confirmed:



\- Successful lease renewal

\- Successful DNS resolution

\- Successful communication with DC01



\### Screenshot



!\[DHCP Verification](../Screenshots/HD-010/HD-010-10-DHCP-Verification.png)



\---



\# PowerShell / Command Prompt Commands Used



```powershell

ipconfig /all



ipconfig /release



ipconfig /renew



ping 192.168.66.10



ping dc01.adlab.local



nslookup dc01.adlab.local



services.msc

```



\---



\# Skills Demonstrated



\- Windows Server Administration

\- DHCP Server Installation

\- DHCP Authorization

\- DHCP Scope Configuration

\- DHCP Lease Management

\- DNS Configuration

\- Windows Networking

\- Client Connectivity Troubleshooting

\- Network Services Administration

\- Help Desk Troubleshooting

\- Technical Documentation



\---



\# Lessons Learned



This lab demonstrated the complete deployment and troubleshooting lifecycle of a Windows Server DHCP service.



Key takeaways include:



\- Installing and authorizing the DHCP Server role.

\- Creating and activating a DHCP scope.

\- Verifying client lease assignment.

\- Troubleshooting DHCP service failures.

\- Restoring DHCP functionality.

\- Validating network connectivity after recovery.



These tasks closely mirror real-world responsibilities performed by Help Desk Technicians, Desktop Support Technicians, and Junior Systems Administrators in enterprise Windows environments.

