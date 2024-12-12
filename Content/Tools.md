### Tools

| Name                                                                                                                           | Purpose                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| [CyberChef](https://gchq.github.io/CyberChef/)                                                                                 | Encryption, encoding, compression and data analysis                                                |
| [Dcode](https://www.digital-detective.net/dcode/)                                                                              | Timestamp decoder                                                                                  |
| [Timeline Explorer](https://ericzimmerman.github.io/#!index.md)                                                                | CSV Viewer (better than Excel)                                                                     |
| [BStrings](https://ericzimmerman.github.io/#!index.md)                                                                         | String search tool with built-in regex patterns                                                    |
| [EvtxECmd](https://ericzimmerman.github.io/#!index.md)                                                                         | Windows event log parsing and enrichment                                                           |
| [PECmd](https://ericzimmerman.github.io/#!index.md)                                                                            | Prefetch file parser                                                                               |
| [LECmd](https://ericzimmerman.github.io/#!index.md)                                                                            | Link file parser                                                                                   |
| [RECmd](https://ericzimmerman.github.io/#!index.md)                                                                            | Recycle Bin parser                                                                                 |
| [Registry Explorer](https://ericzimmerman.github.io/#!index.md)                                                                | Registry viewer built for forensics                                                                |
| [SQLECmd](https://ericzimmerman.github.io/#!index.md)                                                                          | SQL Database parser (useful for Chrome history files)                                              |
| [FTK Imager](https://www.exterro.com/digital-forensics-software/ftk-imager)                                                    | Disk image creation and exploration                                                                |
| [KAPE](https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape) | Triage collection and parsing tool                                                                 |
| [Velociraptor](https://github.com/Velocidex/velociraptor)                                                                      | Useful for making triage collection binaries                                                       |
| [Exiftool](https://exiftool.org/)                                                                                              | File metadata viewer                                                                               |
| [DB Browser for SQLite](https://sqlitebrowser.org/)                                                                            | SQLite database broswer                                                                            |
| [Arsenal Image Mounter](https://arsenalrecon.com/downloads)                                                                    | Mount forensic disk images                                                                         |
| [Capa](https://github.com/mandiant/capa)                                                                                       | Automatic malware capability scanner                                                               |
| [Yara]()                                                                                                                       | Malware pattern matching tool                                                                      |
| [Kansa](https://github.com/davehull/Kansa)                                                                                     | PowerShell incident response tool                                                                  |
| [Log2Timeline](https://github.com/log2timeline/plaso)                                                                          | Super timeline creation                                                                            |
| [Sigcheck](https://learn.microsoft.com/en-us/sysinternals/downloads/sigcheck)                                                  | Digital signature checking                                                                         |
| [Process Explorer](https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer)                                  | Detailed process tree viewer                                                                       |
| [Process Monitor](https://learn.microsoft.com/en-us/sysinternals/downloads/procmon)                                            | Process monitoring tool                                                                            |
| [Wireshark](https://www.wireshark.org/)                                                                                        | Capture and view PCAP files                                                                        |
| [Fakenet](https://github.com/mandiant/flare-fakenet-ng)                                                                        | Simulated network for dynamic malware analysis                                                     |
| [Autoruns](https://learn.microsoft.com/en-us/sysinternals/downloads/autoruns)                                                  | View programs and scripts set to autorun                                                           |
| [Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)                                                      | Enhanced windows logging. Configuration file [here](https://github.com/olafhartong/sysmon-modular) |
| [TCPView](https://learn.microsoft.com/en-us/sysinternals/downloads/tcpview)                                                    | View what ports are opened by what processes                                                       |
| [CurrPorts](https://www.nirsoft.net/utils/cports.html)                                                                         | View what ports are opened by what processes                                                       |
| [BrowsingHistoryView](https://www.nirsoft.net/utils/browsing_history_view.html)                                                | Web history file parser                                                                            |
| [Everything](https://www.voidtools.com/)                                                                                       | Enhanced Windows file searching                                                                    |
| [7zip](https://www.7-zip.org/)                                                                                                 | File archive tool                                                                                  |
| [Chainsaw](https://github.com/WithSecureLabs/chainsaw)                                                                         | Automatic event log parser with Sigma                                                              |
| [Floss](https://github.com/mandiant/flare-floss)                                                                               | Strings tool specializing in obfuscated strings                                                    |
| [Network Miner](https://www.netresec.com/?page=NetworkMiner)                                                                   | Extract files and create summary from PCAP                                                         |
| [Notepad++](https://notepad-plus-plus.org/)                                                                                    | Enhanced notepad                                                                                   |
| [HxD](https://mh-nexus.de/en/hxd/)                                                                                             | Hex Editor                                                                                         |

### Automated Installation with Chocolatey
Below is a command that will use the package manager, [Chocolatey](https://chocolatey.org/), to install as many of the above tools as possible. Before using this command, review the licensing for each tool to determine which can be freely used and which need commercial licenses. All of the above are legitimate tools but security tools may alert due to the presence of some of the tools, use caution.

Packages will be installed to C:\ProgramData\chocolatey\lib\ by default.

Note: The full Sysinternals and Eric Zimmerman suites are installed, not just the ones listed above.

`choco install cyberchef dcode ericzimmermantools exiftool sqlitebrowser arsenalimagemounter capa yara plaso sysinternals wireshark fakenet browsinghistoryview cports everything 7zip floss network-miner notepadplusplus hxd`

*** 
[Return to home page](../README.md)
