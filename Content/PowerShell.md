## PowerShell
### Basic Commands

- List Process Information: `Get-Process | Select-Object -Property Name, Product, Id, CommandLine, StartTime | Format-Table`
- List Process Command Line: `Get-WmiObject Win32_Process | Select-Object Name,  ProcessId, CommandLine, Path | Format-List`
- List Service Information: `Get-Service | Select-Object -Property ServiceName,DisplayName,BinaryPathName,StartType,Status | Format-Table`
- List Windows Event Log Providers: `Get-WinEvent -ListProvider *`
- List Windows Event ID Descriptions: `(Get-WinEvent -ListProvider Microsoft-Windows-Security-Auditing).Events | ft Id, Description`
- Find details on a specific Windows Event ID: `(Get-WinEvent -ListProvider Microsoft-Windows-Security-Auditing).Events | Where-Object -FilterScript {$_.Id -match 4663}`
- List Windows Events: `Get-WinEvent -FilterHashtable @{ LogName="Security"; ID=4624 } -MaxEvents 20` 
- Get Help (Local): `get-help get-childitem`
- Get Help (Online): `Get-Help Get-ChildItem -Online`
- Get File Hash: `Get-FileHash -Algorithm <SHA1|SHA256|MD5> -Path C:\Windows\cmd.exe`
- Get Defender Exclusions: `Get-MpPreference | Select-Object -Property Exclusion* | Format-List`
- Get File Information: `Get-ChildItem C:\temp -Force -Recurse | Select Fullname,LastWriteTime,Attributes,@{Name="Owner";Expression={ (Get-Acl $_.FullName).Owner }}`
- Get Aliases: `Get-Alias`
- Get Registry Value: `Get-ItemProperty "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run"`
- Start Remote PowerShell Session: `Enter-PSSession -ComputerName DC01`
- Stop Remote PowerShell Session: `Exit-PSSession`
- Run Remote PowerShell Commands: `Invoke-Command -ComputerName DC01 -ScriptBlock { Get-ComputerInfo}`
- Run Remote PowerShell Scripts: `Invoke-Command -ComputerName DC01 -filepath C:\temp\triage.ps1`

More DFIR PowerShell commands can be found [here](https://github.com/Bert-JanP/Incident-Response-Powershell/blob/main/DFIR-Commands.md).

*** 
[Return to home page](../README.md)