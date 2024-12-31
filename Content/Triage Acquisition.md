## Triage Acquisition
### Key Items for Triage
- Registry Hives 
	- SOFTWARE 
	- SAM
	- SYSTEM
	- NTUSER.DAT
	- USRCLASS.DAT
- LNK Files (.lnk)
- Jump Lists
- Prefetch Files
- Event Logs
- Other Log Files
- AppData Folder
- $MFT
- NTFS $Logfile and UsnJrnl $J
- pagefile.sys
- hiberfile.sys

### Tools
- [CyLR](https://github.com/orlikoski/CyLR)
- [KAPE](https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape)
- [Velociraptor](https://github.com/Velocidex/velociraptor)
- Build Your Own

#### CyLR
- `.\CyLR.exe -od c:\temp\forensic` (`-v` for verbose, `-q` for quiet)
#### KAPE
- `.\kape.exe --tsource C: --tdest C:\temp\forensics\%d%m --target !SANS_Triage --zip triage` 
#### Velociraptor
- `velociraptor-v0.73.1-windows-amd64.exe -- --embedded_config Collector_velociraptor-collector`
- Create your `Collector_velociraptor-collector` file in the server GUI by running `velociraptor-v0.73.1-windows-amd64.exe gui`.  [Documentation here.](https://docs.velociraptor.app/docs/offline_triage/#the-generic-offline-collector)
#### Build Your Own

```
$collection_path = 'C:\temp\forensics\'
$collection_file = 'triage.zip'

# Get all History directories
$HistoryDirectories = Get-ChildItem "C:\Users\*\AppData\Local\*\*\User Data\*\History" | Select-Object -ExpandProperty DirectoryName

# Create a temporary working directory
$TempWorkingDir = "c:\temp\forensics\temp"
New-Item -Path $TempWorkingDir -ItemType Directory -Force

# Copy History files to the working directory
foreach ($dir in $HistoryDirectories) {
    $sourceFile = Join-Path -Path $dir -ChildPath "History"
    $destinationFile = Join-Path -Path $TempWorkingDir -ChildPath  ($dir -replace ":","")
    New-Item -Path $destinationFile -ItemType Directory -Force
    Copy-Item -Path $sourceFile -Destination $destinationFile -Force
}

# Zip all files in the working directory
$zipFilePath = Join-Path -Path $collection_path -ChildPath $collection_file
Compress-Archive -Path ($TempWorkingDir + '\C') -DestinationPath $zipFilePath -Force 

# Remove the temporary working directory
Remove-Item -Path $TempWorkingDir -Recurse -Force

# Output success message
Write-Host "Acquisition completed successfully. Zip file saved to: $zipFilePath"
```

*** 
[Return to home page](../README.md)