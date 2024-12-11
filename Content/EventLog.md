## Event Log Analysis
 
### Tools
- [EvtxECmd](https://github.com/EricZimmerman/evtx) (Preferred)
- [Event Log Explorer](https://eventlogxp.com/)
- [Get-WinEvent](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/get-winevent?view=powershell-7.4)
- [Chainsaw](https://github.com/WithSecureLabs/chainsaw/tree/master)

### EvtxECmd
 - Process event logs into CSV format: `EvtxECmd.exe -d "M:\triage\eventlogs" --csv .\ --csvf eventlogs.csv`

### Event IDs

| Forensic Value                  | Event Provider                                           | Event IDs | Summary                                                                                     |
| ------------------------------- | -------------------------------------------------------- | --------- | ------------------------------------------------------------------------------------------- |
| Logon (Success)                 | Security                                                 | 4624      | An account logged on                                                                        |
| Logon (Fail)                    | Security                                                 | 4625      | An account failed to log on                                                                 |
| Logoff                          | Security                                                 | 4634      | An account was logged off                                                                   |
| Logoff                          | Security                                                 | 4647      | User initiated logoff                                                                       |
| Admin Logon                     | Security                                                 | 4672      | Special privileges assigned to new logon                                                    |
| Workstation Lock                | Security                                                 | 4800      | The workstation was locked                                                                  |
| Workstation Unlock              | Security                                                 | 4801      | The workstation was unlocked                                                                |
| RDP Activity                    | Security                                                 | 4778      | A session was reconnected to a Window Station                                               |
| RDP Activity                    | Security                                                 | 4779      | A session was disconnected from a Window Station                                            |
| RDP Activity                    | RemoteDesktopServices-RDPCoreTS                          | 131       | The server accepted a new TCP connection from client X.X.X.X                                |
| RDP Activity                    | Microsoft-Windows-TerminalServices-RDPClient/Operational | 1024      | RDP ClientActiveX is trying to connect to the server                                        |
| Log Clear                       | Security                                                 | 1102      | The audit log was cleared                                                                   |
| Time Modification               | Security                                                 | 4616      | The system time was changed                                                                 |
| USB                             | Security                                                 | 20001     | Plug and Play events                                                                        |
| USB                             | System                                                   | 20003     | Plug and Play events                                                                        |
| Object Access                   | Security                                                 | 4656      | A handle to an object was requested                                                         |
| Object Access                   | Security                                                 | 4663      | An attempt was made to access an object                                                     |
| External Device Connected       | Security                                                 | 6416      | A new external device was recognized by the system                                          |
| External Device Connected       | Microsoft-Windows-Partition/Diagnostic                   | 1006      | N/A                                                                                         |
| Wifi Connection (Success)       | Microsoft-Windows-WLAN-AutoConfig                        | 8001      | WLAN AutoConfig service has successfully connected to a wireless network                    |
| Wifi Connection (Failed)        | Microsoft-Windows-WLAN-AutoConfig                        | 8002      | WLAN AutoConfig service failed to connect to a wireless network                             |
| Wifi Connection (Disconnection) | Microsoft-Windows-WLAN-AutoConfig                        | 8003      | WLAN AutoConfig service has successfully disconnected from a wireless network.              |
| Wifi Security                   | Microsoft-Windows-WLAN-AutoConfig                        | 11004     | Wireless security stopped.                                                                  |
| Wifi Security                   | Microsoft-Windows-WLAN-AutoConfig                        | 11005     | Wireless security succeeded.                                                                |
| Logon                           | Security                                                 | 4648      | A logon was attempted using explicit credentials                                            |
| Account Creation                | Security                                                 | 4720      | A user account was created                                                                  |
| Account Deletion                | Security                                                 | 4726      | A user account was deleted                                                                  |
| Kerberos Ticket Request         | Security                                                 | 4768      | A Kerberos authentication ticket (TGT) was requested                                        |
| Kerberos Ticket Request         | Security                                                 | 4769      | A Kerberos service ticket was requested                                                     |
| Kerberos Ticket Request         | Security                                                 | 4771      | Kerberos pre-authentication failed                                                          |
| NTLM Authentication             | Security                                                 | 4776      | The domain controller attempted to validate the credentials for an account                  |
| Remote Desktop Session Created  | RemoteDesktopServices-RDPCoreTS                          | 98        | A TCP connection has been successfully established.                                         |
| Network Share Object            | Security                                                 | 5140-5145 | A network share object was accessed/deleted/modified/created                                |
| Scheduled Tasks                 | Security                                                 | 4698      | A scheduled task was created                                                                |
| Scheduled Tasks                 | Task Scheduler                                           | 106       | User created task                                                                           |
| Scheduled Tasks                 | Task Scheduler                                           | 140       | User updated task                                                                           |
| Scheduled Tasks                 | Task Scheduler                                           | 141       | User deleted task                                                                           |
| Scheduled Tasks                 | Task Scheduler                                           | 200       | Task launched                                                                               |
| Scheduled Tasks                 | Task Scheduler                                           | 201       | Task completed                                                                              |
| Installation                    | Application                                              | 1033      | Software uninstallation                                                                     |
| Installation                    | Application                                              | 1034      | Software uninstallation                                                                     |
| Installation                    | Application                                              | 11707     | Installation Successful                                                                     |
| Installation                    | Application                                              | 11708     | Installation Failed                                                                         |
| Installation                    | Application                                              | 11724     | Software uninstallation                                                                     |
| Services                        | System                                                   | 7034-7036 | Volume Shadow Copy Started/Running                                                          |
| Services                        | System                                                   | 7040      | Service start type changed                                                                  |
| Services                        | System                                                   | 7045      | New Service Installed                                                                       |
| Services                        | Security                                                 | 4697      | A service was installed in the system                                                       |
| Log Clear                       | System                                                   | 104       | Event Log Cleared                                                                           |
| Process Creation                | Security (Microsoft-Windows-Security-Auditing)           | 4688      | A new process has been created                                                              |
| Windows Error Reporting         | System                                                   | 1001      | Application Crash                                                                           |
| Application Error               | Application                                              | 1000-1002 | Application Error                                                                           |
| Malware Detection               | Windows-Defender/Operational                             | 1116-1119 | The antimalware platform detected/prevented malware or other potentially unwanted software/ |
| PowerShell Logging              | PowerShell Operational                                   | 4103-4104 | Module Logging/Script Block Logging                                                         |
| WMI                             | WMI-Activity/Operational                                 | 5857-5861 | WMI Activity                                                                                |

*** 
[Return to home page](../README.md)