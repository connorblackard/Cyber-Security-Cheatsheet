## macOS Artifacts

| Artifact Name              | Path                                                                                      | Notes                                                                      |
| -------------------------- | ----------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Bash History               | ~/.bash_history                                                                           | Command history for bash shell users                                       |
| Zsh History                | ~/.zsh_history                                                                            | Command history for zsh shell users (default since macOS Catalina)         |
| SSH Keys                   | ~/.ssh/                                                                                   | SSH private/public keys and known_hosts                                    |
| LaunchAgents (User)        | ~/Library/LaunchAgents/                                                                   | User-level persistence mechanism, runs on user login                       |
| LaunchAgents (System)      | /Library/LaunchAgents/                                                                    | System-level persistence, runs when any user logs in                       |
| LaunchDaemons              | /Library/LaunchDaemons/                                                                   | System-level persistence, runs at boot                                     |
| LaunchDaemons (System)     | /System/Library/LaunchDaemons/                                                            | Apple system daemons, runs at boot                                         |
| Cron Jobs                  | /usr/lib/cron/tabs/                                                                       | Scheduled tasks for persistence                                            |
| Login Items                | ~/Library/Preferences/com.apple.loginitems.plist                                          | Applications that start at user login                                      |
| Safari History             | ~/Library/Safari/History.db                                                               | Safari browsing history (SQLite database)                                  |
| Safari Downloads           | ~/Library/Safari/Downloads.plist                                                          | Safari download history                                                    |
| Chrome History             | ~/Library/Application Support/Google/Chrome/Default/History                               | Chrome browsing history (SQLite database)                                  |
| Firefox History            | ~/Library/Application Support/Firefox/Profiles/\<profile\>/places.sqlite                  | Firefox browsing history                                                   |
| Quarantine Events          | ~/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV2                         | Files downloaded from internet, includes URL source (SQLite database)      |
| KnowledgeC Database        | ~/Library/Application Support/Knowledge/knowledgeC.db                                     | User activity database - app usage, focus, device connections              |
| Unified Logs               | /var/db/diagnostics/                                                                      | Unified logging system persistence store                                   |
| System Logs (Legacy)       | /var/log/                                                                                 | Traditional log files (system.log, install.log, wifi.log)                  |
| Install History            | /Library/Receipts/InstallHistory.plist                                                    | Software installation history                                              |
| Application Usage          | /var/db/uuidtext/                                                                         | Maps UUID to application paths                                             |
| Spotlight Index            | /.Spotlight-V100/                                                                         | Indexed file metadata and search history                                   |
| FileVault Keys             | /var/db/FileVaultMaster.keychain                                                          | FileVault encryption recovery keys                                         |
| Keychain Files             | ~/Library/Keychains/                                                                      | User passwords, certificates, secure notes                                 |
| System Keychain            | /Library/Keychains/System.keychain                                                        | System-level credentials and certificates                                  |
| Recent Items               | ~/Library/Application Support/com.apple.sharedfilelist/                                   | Recently accessed files, apps, and servers                                 |
| Trash                      | ~/.Trash/                                                                                 | User deleted files (soft delete)                                           |
| Mail Database              | ~/Library/Mail/V10/MailData/Envelope Index                                                | Email metadata and content (SQLite database)                               |
| iMessage/SMS Database      | ~/Library/Messages/chat.db                                                                | iMessage and SMS history (SQLite database)                                 |
| Notes Database             | ~/Library/Group Containers/group.com.apple.notes/NoteStore.sqlite                         | Apple Notes content                                                        |
| System Preferences         | ~/Library/Preferences/                                                                    | Application and user preferences (plist files)                             |
| Network Preferences        | /Library/Preferences/SystemConfiguration/                                                 | Network configuration, WiFi passwords (encrypted)                          |
| WiFi Known Networks        | /Library/Preferences/SystemConfiguration/com.apple.airport.preferences.plist              | Previously connected WiFi networks                                         |
| Firewall Log               | /var/log/appfirewall.log                                                                  | Application firewall events                                                |
| FSEvents                   | /.fseventsd/                                                                              | File system event logs - file creation, modification, deletion timestamps  |
| User Accounts              | /var/db/dslocal/nodes/Default/users/                                                      | Local user account information (plist files)                               |
| System Extensions          | /Library/SystemExtensions/                                                                | Installed system extensions (kexts)                                        |
| Application Support        | ~/Library/Application Support/                                                            | Application data, caches, and databases                                    |
| Cookies                    | ~/Library/Cookies/Cookies.binarycookies                                                   | Safari cookies (binary format)                                             |
| Crash Reports              | ~/Library/Logs/DiagnosticReports/                                                         | Application crash logs                                                     |
| System Crash Reports       | /Library/Logs/DiagnosticReports/                                                          | System-level crash reports                                                 |
| Bluetooth Artifacts        | /Library/Preferences/com.apple.Bluetooth.plist                                            | Bluetooth device pairing history                                           |
| TimeMachine Configuration  | /Library/Preferences/com.apple.TimeMachine.plist                                          | Time Machine backup configuration                                          |
| Disk Utility History       | ~/Library/Preferences/com.apple.DiskUtility.plist                                         | Disk utility operations history                                            |
| Printer History            | ~/Library/Preferences/org.cups.PrintingPrefs.plist                                        | Printing history and connected printers                                    |
| Screen Sharing Logs        | /var/log/RemoteDesktop/                                                                   | Screen sharing and remote desktop logs                                     |
| Sysdiagnose Archive        | /var/tmp/                                                                                 | System diagnostic bundles (generated via sysdiagnose command)              |

### Important Plist Files
Property List (plist) files store configuration data. Use `plutil` to convert binary plists to XML:
- `plutil -convert xml1 -o output.xml input.plist`
- `defaults read <path-to-plist>` (without .plist extension)

### SQLite Databases
Many macOS artifacts use SQLite databases. Query using:
- `sqlite3 <database-file>`
- `.tables` - list all tables
- `.schema <table>` - show table structure
- `SELECT * FROM <table>;` - query data

### Useful Analysis Tools
- [mac_apt](https://github.com/ydkhatri/mac_apt) - macOS Artifact Parsing Tool
- [AutoMacTC](https://github.com/CrowdStrike/automactc) - Automated macOS forensic triage collection
- [KnockKnock](https://objective-see.org/products/knockknock.html) - Persistence enumeration
- [APOLLO](https://github.com/mac4n6/APOLLO) - Apple Pattern of Life Lazy Output'er

For comprehensive artifact locations, review [mac_apt modules](https://github.com/ydkhatri/mac_apt) and [macOS Forensic Artifacts](https://github.com/pstirparo/mac4n6).

***
[Return to home page](../../README.md)
