## Remote Access

### Safe Methods of Remote Access
Safe methods of remote access are methods that do not leave cached/stored credentials in memory on the device.

| Method Name                     | Logon Type | Notes                           |
| ------------------------------- | ---------- | ------------------------------- |
| Net Use                         | 3          | /u: parameter                   |
| PowerShell Remoting             | 3          | Invoke-Command; Enter-PSSession |
| PsExec w/o Explicit Credentials | 3          |                                 |
| Remote Registry                 | 3          |                                 |

### Unsafe Methods of Remote Access
Unsafe methods of remote access are methods that leave stored/cached credentials on the device.

| Method Name                     | Logon Type | Notes                                    |
| ------------------------------- | ---------- | ---------------------------------------- |
| Console Logon*                  | 2          | *Except when credential Guard is enabled |
| RunAs*                          | 2          | *Except when credential Guard is enabled |
| Remote Desktop*                 | 10         | *Except when credential Guard is enabled |
| PsExec w/ Alternate Credentials | 3 + 2      | -u username -p password                  |
| Remote Scheduled Tasks          | 4          | LSA Secret                               |
| Run as a Service                | 5          | LSA Secret                               |

More details on remote access tools and logon types can be found [here](https://learn.microsoft.com/en-us/windows-server/identity/securing-privileged-access/reference-tools-logon-types).

*** 
[Return to home page](../README.md)