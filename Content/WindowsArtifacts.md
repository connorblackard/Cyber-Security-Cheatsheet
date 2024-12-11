## Windows Artifacts

| Artifact Name         | Path                                                                                            | Notes                                                                         |
| --------------------- | ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| PSReadlines           | C:\users\%UserProfile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine                  | This artifact PowerShell command history for a user. Limited to 4096 commands |
| AutoStart Keys        | HKCU:\\NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run                                 | "Run" registry keys that run programs automatically                           |
| AutoStart Keys        | HKCU:\\NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Runonce                             | "Run" registry keys that run programs automatically                           |
| AutoStart Keys        | Software\Microsoft\Windows\CurrentVersion\Runonce                                               | "Run" registry keys that run programs automatically                           |
| AutoStart Keys        | Software\Microsoft\Windows\CurrentVersion\policies\Explorer\Run                                 | "Run" registry keys that run programs automatically                           |
| AutoStart Keys        | Software\Microsoft\Windows\CurrentVersion\Run                                                   | "Run" registry keys that run programs automatically                           |
| AutoStart Keys        | SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit                                  | "Run" registry keys that run programs automatically                           |
| Registry Hives        | %WinDir%\System32\Config\SOFTWARE \| SAM \| SYSTEM (HKLM)                                       | Configuration data for installed software and Windows OS                      |
| Registry Hives        | C:\Users\\\<Username\>\NTUSER.DAT (HKCU)                                                        | User Related Data                                                             |
| Registry Hives        | C:\Users\\<username\>\AppData\Local\Microsoft\Windows\UsrClass.dat (HKCU)                       | User Related Data                                                             |
| Services              | HKLM:\\SYSTEM\\\<CurrentControlSet\>\Services                                                   | System Services                                                               |
| Prefetch              | C:\Windows\Prefetch\\*.pf                                                                       | Evidence of execution                                                         |
| Firefox History       | %USERPROFILE%\AppData\Roaming\Mozilla\Firefox\Profiles\\\<random text\>\\.default\places.sqlite | Web History                                                                   |
| Chrome History        | %USERPROFILE%\AppData\Local\Google\Chrome\User Data\\<Profile\>\History                         | Web History                                                                   |
| Edge History          | %USERPROFILE%\AppData\Local\Microsoft\Edge\User Data\\<Profile\>\History                        | Web History                                                                   |
| Recycle Bin           | C:\\$Recycle.Bin                                                                                | Soft deleted files. Grouped by Account SID                                    |
| LNK Files (Windows)   | %USERPROFILE%\AppData\Roaming\Microsoft\Windows\Recent\                                         | Recently opened/interacted files                                              |
| LNK Files (Office)    | %USERPROFILE%\AppData\Roaming\Microsoft\Office\Recent\                                          | Recently opened/interacted Office files                                       |
| Recent Files          | NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs                        | Recently opened/interacted Office Files                                       |
| Amache                | C:\Windows\AppCompat\Programs\Amcache.hve                                                       | Presence of executable files/applications                                     |
| Windows Defender Logs | C:\ProgramData\Microsoft\Windows Defender\Support                                               | Logs relating to performance, actions, and detections of Microsoft Defender   |

For other artifacts locations, review [KAPE target files](https://github.com/EricZimmerman/KapeFiles/tree/master/Targets). 

*** 
[Return to home page](../README.md)