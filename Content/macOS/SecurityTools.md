## macOS Security Tools

### Forensics and Collection Tools

| Name                                                                                           | Purpose                                                                           |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| [mac_apt](https://github.com/ydkhatri/mac_apt)                                                 | macOS Artifact Parsing Tool - comprehensive artifact parsing                      |
| [AutoMacTC](https://github.com/CrowdStrike/automactc)                                          | Automated macOS forensic triage collection framework                              |
| [APOLLO](https://github.com/mac4n6/APOLLO)                                                     | Apple Pattern of Life Lazy Output'er - artifact parsing                           |
| [ORION](https://github.com/Johnng007/ORION)                                                    | macOS artifact collection tool                                                     |
| [OSXCollector](https://github.com/Yelp/osxcollector)                                           | Forensic evidence collection for macOS                                             |
| [KnockKnock](https://objective-see.org/products/knockknock.html)                               | Persistence mechanism enumeration tool                                             |
| [Crescendo](https://github.com/SuprHackerSteve/Crescendo)                                      | Real-time event viewer and process monitoring                                      |
| [UnifiedLogReader](https://github.com/ydkhatri/UnifiedLogReader)                               | Parse macOS unified logs offline                                                   |
| [FSEventsParser](https://github.com/dlcowen/FSEventsParser)                                    | Parse FSEvents logs for file system timeline                                       |

### Security Monitoring and Detection

| Name                                                                                           | Purpose                                                                           |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| [Santa](https://github.com/google/santa)                                                       | Binary authorization system - whitelist/blacklist execution                       |
| [LuLu](https://objective-see.org/products/lulu.html)                                           | Free macOS firewall - monitor and block outbound connections                      |
| [OverSight](https://objective-see.org/products/oversight.html)                                 | Monitor camera and microphone access                                               |
| [ReiKey](https://objective-see.org/products/reikey.html)                                       | Detect keyloggers and keyboard event taps                                          |
| [BlockBlock](https://objective-see.org/products/blockblock.html)                               | Monitor persistence locations and alert on new items                               |
| [TaskExplorer](https://objective-see.org/products/taskexplorer.html)                           | Process viewer with VirusTotal integration                                         |
| [ProcessMonitor](https://objective-see.org/products/processmonitor.html)                       | Monitor process creation and execution                                             |
| [DNSMonitor](https://objective-see.org/products/dnsmonitor.html)                               | Monitor DNS queries and responses                                                  |
| [NetiquetteMonitor](https://objective-see.org/products/netiquette.html)                        | Network monitoring tool                                                            |
| [osquery](https://osquery.io/)                                                                 | SQL-based system instrumentation and monitoring                                    |
| [Velociraptor](https://github.com/Velocidex/velociraptor)                                      | Endpoint visibility and digital forensics                                          |
| [Wazuh](https://wazuh.com/)                                                                    | Security monitoring and threat detection                                           |

### Malware Analysis

| Name                                                                                           | Purpose                                                                           |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| [KnockKnock](https://objective-see.org/products/knockknock.html)                               | Find persistence mechanisms used by malware                                        |
| [WhatsYourSign](https://objective-see.org/products/whatsyoursign.html)                         | View file code signing information                                                 |
| [Capa](https://github.com/mandiant/capa)                                                       | Automatic malware capability detection                                             |
| [YARA](https://virustotal.github.io/yara/)                                                     | Pattern matching for malware research                                              |
| [Floss](https://github.com/mandiant/flare-floss)                                               | Extract obfuscated strings from malware                                            |
| [strings](https://developer.apple.com/library/archive/documentation/Darwin/Reference/ManPages/man1/strings.1.html) | Built-in string extraction (already on macOS)                    |
| [Ghidra](https://ghidra-sre.org/)                                                              | Free reverse engineering tool by NSA                                               |
| [radare2](https://rada.re/)                                                                    | Free reverse engineering framework                                                 |
| [OTX](https://newosxbook.com/tools/otx.html)                                                   | Object Tool eXtended - Mach-O disassembler                                         |
| [MachOView](https://sourceforge.net/projects/machoview/)                                       | Visual Mach-O file browser                                                         |
| [VirusTotal](https://www.virustotal.com/)                                                      | Multi-engine malware scanner (web-based)                                           |

### Network Analysis

| Name                                                                                           | Purpose                                                                           |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| [Wireshark](https://www.wireshark.org/)                                                        | Network protocol analyzer and packet capture                                       |
| [tcpdump](https://www.tcpdump.org/)                                                            | Command-line packet analyzer (built-in)                                            |
| [NetworkMiner](https://www.netresec.com/?page=NetworkMiner)                                    | Network forensic analysis tool                                                     |
| [LuLu](https://objective-see.org/products/lulu.html)                                           | Open-source firewall with network monitoring                                       |
| [nmap](https://nmap.org/)                                                                      | Network discovery and security scanning                                            |

### Utility and System Tools

| Name                                                                                           | Purpose                                                                           |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| [SQLite Browser](https://sqlitebrowser.org/)                                                  | Browse and query SQLite databases                                                  |
| [ExifTool](https://exiftool.org/)                                                             | Read and write file metadata                                                       |
| [HexFiend](https://hexfiend.com/)                                                             | Fast hex editor for macOS                                                          |
| [iHex](https://github.com/suzuki-0000/HexEditor)                                               | Hex editor                                                                         |
| [The Sleuth Kit](https://www.sleuthkit.org/)                                                  | File system forensic analysis tools                                                |
| [Autopsy](https://www.autopsy.com/)                                                           | GUI for The Sleuth Kit (limited macOS support)                                     |
| [plutil](https://developer.apple.com/library/archive/documentation/Darwin/Reference/ManPages/man1/plutil.1.html) | Built-in plist converter and validator                            |
| [defaults](https://ss64.com/osx/defaults.html)                                                | Built-in plist reader/writer                                                       |

### Memory Analysis

| Name                                                                                           | Purpose                                                                           |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| [Volatility](https://github.com/volatilityfoundation/volatility)                              | Memory forensics framework (limited macOS support)                                 |
| [Rekall](http://www.rekall-forensic.com/)                                                     | Memory forensic framework                                                          |
| [osxpmem](https://github.com/google/rekall/tree/master/tools/osx/MacPmem)                     | macOS physical memory acquisition                                                  |

### Incident Response

| Name                                                                                           | Purpose                                                                           |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| [GRR Rapid Response](https://github.com/google/grr)                                           | Remote live forensics for incident response                                        |
| [Velociraptor](https://github.com/Velocidex/velociraptor)                                     | Endpoint visibility and IR tool                                                    |
| [DFIR ORC](https://dfir-orc.github.io/)                                                       | Forensic artifact collection (Windows primary)                                     |
| [AutoMacTC](https://github.com/CrowdStrike/automactc)                                         | Automated triage collection                                                        |

### Objective-See Security Tools Suite

[Objective-See](https://objective-see.org/products.html) provides excellent free macOS security tools:

- **BlockBlock** - Persistence mechanism monitoring
- **DNSMonitor** - DNS query monitoring
- **KextViewr** - Kernel extension viewer
- **KnockKnock** - Persistence enumeration
- **LuLu** - Firewall
- **OverSight** - Camera/microphone monitoring
- **ProcessMonitor** - Process execution monitoring
- **ReiKey** - Keyboard event monitor
- **TaskExplorer** - Enhanced process viewer
- **WhatsYourSign** - Code signing viewer

### Built-in macOS Tools

macOS includes many powerful forensic tools by default:

| Command          | Purpose                                                      |
| ---------------- | ------------------------------------------------------------ |
| `log`            | Unified logging system query tool                            |
| `fs_usage`       | Real-time file system activity monitoring                    |
| `lsof`           | List open files and network connections                      |
| `netstat`        | Network statistics and connections                           |
| `tcpdump`        | Packet capture and analysis                                  |
| `plutil`         | Property list converter and validator                        |
| `defaults`       | Read/write plist files                                       |
| `codesign`       | Code signature verification                                  |
| `spctl`          | Gatekeeper control and verification                          |
| `kextstat`       | List loaded kernel extensions                                |
| `launchctl`      | Manage launch agents and daemons                             |
| `dscl`           | Directory services command-line utility                      |
| `sqlite3`        | SQLite database CLI                                          |
| `mdls`           | List file metadata from Spotlight                            |
| `mdfind`         | Search Spotlight database                                    |
| `system_profiler`| System information and hardware details                      |
| `sysdiagnose`    | Generate comprehensive diagnostic report                     |
| `sample`         | Profile process execution                                    |
| `spindump`       | Generate process hang report                                 |
| `praudit`        | Parse BSM audit logs                                         |

### Installation via Homebrew

Many macOS security tools can be installed using [Homebrew](https://brew.sh/):

```bash
# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Forensic and security tools
brew install --cask wireshark
brew install --cask hex-fiend
brew install --cask sqlitebrowser
brew install exiftool
brew install yara
brew install nmap
brew install osquery
brew install sleuthkit
brew install radare2
brew install ghidra
brew install binwalk

# Objective-See tools (via custom tap or direct download from website)
# Most Objective-See tools are distributed as DMGs from their website

# Install multiple tools at once
brew install exiftool yara nmap osquery sleuthkit radare2 binwalk
```

### Recommended Tool Stack

**Basic forensic investigation:**
- mac_apt (artifact parsing)
- AutoMacTC (triage collection)
- SQLite Browser (database analysis)
- HexFiend (hex analysis)
- UnifiedLogReader (log analysis)
- Built-in macOS commands

**Security monitoring:**
- LuLu (firewall)
- KnockKnock (persistence check)
- BlockBlock (persistence monitoring)
- OverSight (privacy monitoring)
- osquery (system instrumentation)

**Malware analysis:**
- YARA (pattern matching)
- Capa (capability detection)
- Ghidra (reverse engineering)
- strings/Floss (string extraction)
- WhatsYourSign (code signing)

**Network forensics:**
- Wireshark (packet analysis)
- tcpdump (packet capture)
- lsof (connection monitoring)
- LuLu (firewall/monitoring)

***
[Return to home page](../../README.md)
