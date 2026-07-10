\# HD-008 — Printer Deployment



\## Objective



Simulate a common Help Desk request by deploying a shared network printer from a Windows Server to a domain-joined Windows client. Demonstrate how to install a printer, configure printer sharing, deploy the printer to a client workstation, and verify the deployment using both graphical tools and PowerShell.



\---



\# Ticket Information



\*\*Ticket ID:\*\* HD-008



\*\*Priority:\*\* Medium



\*\*Category:\*\* Printer Administration



\*\*Status:\*\* Completed



\---



\## Scenario



The Sales department requested access to a shared network printer for printing department documents.



The Help Desk was responsible for:



\- Installing a network printer on the print server.

\- Configuring printer sharing.

\- Deploying the printer to a Windows client.

\- Verifying successful installation.

\- Confirming printer availability using PowerShell.



\---



\## Environment



| Item | Value |

|------|-------|

| Domain | adlab.local |

| Domain Controller | DC01 |

| Client | CLIENT01 |

| User | Mike Wilson (mwilson) |

| Printer Name | SalesPrinter |

| Printer Driver | Generic / Text Only |

| Operating System | Windows Server 2022 |

| Client OS | Windows 11 |



\---



\## Investigation



Verified the Print Spooler service was operational.



Attempted to use \*\*Microsoft Print to PDF\*\*, but Windows Server does not support sharing this virtual printer.



Created a new shared printer using the \*\*Generic / Text Only\*\* driver to simulate an enterprise network printer deployment.



\---



\# Resolution



Opened the classic \*\*Add Printer Wizard\*\*.



Selected:



```text

Add a local printer or network printer with manual settings

```



Created a new \*\*Local Port\*\*.



Configured:



```text

Port Name:

C:\\PrintQueue

```



Selected the printer driver:



```text

Manufacturer:

Generic



Driver:

Generic / Text Only

```



Named the printer:



```text

SalesPrinter

```



Enabled printer sharing.



Configured the share name:



```text

SalesPrinter

```



Verified the printer appeared in \*\*Devices and Printers\*\*.



Logged into CLIENT01.



Opened:



```text

\\\\dc01

```



Connected to the shared printer.



Verified the printer successfully installed on the Windows client.



\---



\## Validation



Completed the following validation tests:



\- ✅ Printer successfully installed on DC01

\- ✅ Printer sharing enabled

\- ✅ Printer visible from CLIENT01

\- ✅ Client successfully connected

\- ✅ Printer installed successfully

\- ✅ Printer verified using PowerShell

\- ✅ Shared printer accessible through \\\\DC01



\---



\## PowerShell / Commands Used



\### Display Installed Printers



```powershell

Get-Printer

```



Displays all printers installed on the system.



\---



\### Verify Shared Printer



```powershell

Get-Printer |

Format-Table Name, DriverName, Shared

```



Displays printer name, driver, and sharing status.



\---



\## Result



✔ Network printer successfully deployed



✔ Printer shared across the domain



✔ CLIENT01 successfully connected



✔ Shared printer verified using PowerShell



✔ Ticket resolved successfully



\---



\## Lessons Learned



\- Installed a network printer using the Windows Add Printer Wizard.

\- Configured printer sharing for client access.

\- Connected a domain-joined Windows client to a shared network printer.

\- Verified printer deployment using PowerShell.

\- Learned that Microsoft Print to PDF cannot be shared and that a Generic / Text Only printer provides a realistic enterprise lab simulation.



\---



\## Screenshots



\- 01-Add-Printer-Wizard.png

\- 02-Create-Local-Port.png

\- 03-Select-Printer-Driver.png

\- 04-Printer-Sharing-Properties.png

\- 05-Printer-Installed.png

\- 06-Printer-Visible-From-Client.png

\- 07-Printer-Installed-On-Client.png

\- 08-PowerShell-Verification.png

