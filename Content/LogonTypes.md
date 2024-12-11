## Logon Types

| Logon Type                | #   | Examples                                      |
| ------------------------- | --- | --------------------------------------------- |
| Interactive               | 2   | Console Logon/RunAs                           |
| Network                   | 3   | Net Use/RPC Calls/Remote Registry/SMB         |
| Batch                     | 4   | Scheduled Tasks                               |
| Service                   | 5   | Windows services                              |
| Unlock                    | 7   | Unlock Workstation                            |
| Network Cleartext         | 8   | PowerShell with CredSSP/IIS Basic Auth        |
| NewCredentials            | 9   | RunAs /Network                                |
| Remote Interactive        | 10  | Remote Desktop                                |
| Cached Interactive        | 11  | Logon via locally cached credentials          |
| Cached Remote Interactive | 12  | Remote logon against local cached credentials |
| Cached Unlock             | 13  | Unlock via cached credentials                 |

*** 
[Return to home page](../README.md)