## macOS Terminal Commands

### System Information

- Get System Information: `system_profiler SPSoftwareDataType SPHardwareDataType`
- Get macOS Version: `sw_vers`
- Get Kernel Information: `uname -a`
- Get System Uptime: `uptime`
- Get Current Date/Time: `date`
- Get Hostname: `hostname` or `scutil --get ComputerName`
- Get Serial Number: `system_profiler SPHardwareDataType | grep "Serial Number"`
- Get Hardware UUID: `system_profiler SPHardwareDataType | grep "Hardware UUID"`
- Get CPU Information: `sysctl -n machdep.cpu.brand_string`
- Get Memory Information: `system_profiler SPHardwareDataType | grep Memory`
- Get Disk Information: `diskutil list`
- Get Disk Usage: `df -h`
- Get System Integrity Protection Status: `csrutil status`

### Process Information

- List All Processes: `ps aux`
- List Process Tree: `ps auxww` or `pstree` (if installed)
- List Processes with Full Command Line: `ps auxww | grep -v grep`
- Find Process by Name: `ps aux | grep <process_name>`
- Get Process Information: `ps -p <PID> -o pid,ppid,user,%cpu,%mem,start,command`
- List Running Applications: `osascript -e 'tell application "System Events" to get name of every process whose background only is false'`
- Kill Process by PID: `kill <PID>` or `kill -9 <PID>` (force)
- Kill Process by Name: `pkill <process_name>` or `killall <process_name>`
- List Open Files by Process: `lsof -p <PID>`
- List Processes Using File: `lsof <file_path>`
- Monitor Process Activity: `top` or `htop` (if installed)
- Monitor Real-time Process Events: `sudo fs_usage -w` (file system usage)

### User Information

- List All Users: `dscl . list /Users` or `dscl . list /Users | grep -v "^_"`
- Get Current User: `whoami` or `id -un`
- Get User ID: `id -u` or `id`
- Get Group Membership: `id <username>` or `groups <username>`
- List Logged In Users: `who` or `w`
- Get Last Login Information: `last` or `last <username>`
- Get User Account Details: `dscl . read /Users/<username>`
- Check User Password Policy: `pwpolicy -u <username> -getpolicy`
- List Admin Users: `dscl . -read Groups/admin GroupMembership`
- Get Current User's Home Directory: `echo $HOME` or `dscl . read /Users/$(whoami) NFSHomeDirectory`

### Network Information

- List Network Interfaces: `ifconfig` or `networksetup -listallhardwareports`
- Get IP Address: `ifconfig | grep "inet "` or `ipconfig getifaddr en0`
- List Active Network Connections: `netstat -an` or `lsof -i`
- List Listening Ports: `netstat -an | grep LISTEN` or `lsof -iTCP -sTCP:LISTEN -n -P`
- List Established Connections: `netstat -an | grep ESTABLISHED` or `lsof -iTCP -sTCP:ESTABLISHED -n -P`
- Get Routing Table: `netstat -rn` or `route -n get default`
- Get ARP Cache: `arp -a`
- Get DNS Configuration: `scutil --dns` or `cat /etc/resolv.conf`
- List WiFi Networks: `networksetup -listpreferredwirelessnetworks en0`
- Get WiFi Information: `/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -I`
- Test Network Connectivity: `ping -c 4 <host>` or `nc -zv <host> <port>`
- Trace Network Route: `traceroute <host>`
- DNS Lookup: `nslookup <domain>` or `dig <domain>` or `host <domain>`
- Show Firewall Status: `sudo /usr/libexec/ApplicationFirewall/socketfilterfw --getglobalstate`
- List Firewall Rules: `sudo /usr/libexec/ApplicationFirewall/socketfilterfw --listapps`

### File System Operations

- List Files: `ls -la` (with hidden files) or `ls -lah` (with human-readable sizes)
- Find Files by Name: `find / -name "<filename>" 2>/dev/null`
- Find Files by Extension: `find / -name "*.txt" 2>/dev/null`
- Find Files Modified in Last N Days: `find / -type f -mtime -7 2>/dev/null`
- Find Large Files: `find / -type f -size +100M 2>/dev/null`
- Get File Metadata: `mdls <file>` (Spotlight metadata)
- Get File Information: `stat <file>` or `ls -l <file>`
- Get File Hash (MD5): `md5 <file>`
- Get File Hash (SHA1): `shasum -a 1 <file>`
- Get File Hash (SHA256): `shasum -a 256 <file>`
- Get File Type: `file <file>`
- Search File Contents: `grep -r "search_term" /path/to/search`
- Count Lines in File: `wc -l <file>`
- View File with Timestamps: `ls -lT <file>`
- Show Extended Attributes: `xattr -l <file>`
- Remove Quarantine Attribute: `xattr -d com.apple.quarantine <file>`
- Get ACL Permissions: `ls -le <file>`
- Check Code Signature: `codesign -dv <file>`
- Verify Code Signature: `codesign -v <file>`
- Display File Access History: `mdls -name kMDItemLastUsedDate <file>`

### Persistence and Startup Items

- List LaunchAgents (User): `ls -la ~/Library/LaunchAgents/`
- List LaunchAgents (System): `ls -la /Library/LaunchAgents/`
- List LaunchDaemons: `ls -la /Library/LaunchDaemons/`
- List Running Launch Services: `launchctl list`
- Show LaunchAgent/Daemon Details: `launchctl list | grep <name>` then `launchctl print <service>`
- Load LaunchAgent/Daemon: `launchctl load <plist_path>`
- Unload LaunchAgent/Daemon: `launchctl unload <plist_path>`
- List Startup Items: `defaults read com.apple.loginitems`
- List Kernel Extensions: `kextstat` or `kextfind -loaded`
- List System Extensions: `systemextensionsctl list`
- View Cron Jobs: `crontab -l` or `sudo crontab -l -u <username>`

### Security and Permissions

- Check Gatekeeper Status: `spctl --status`
- Verify Application Signature: `spctl -a -v <app_path>`
- List Allowed Applications: `spctl --list`
- Check XProtect Version: `system_profiler SPInstallHistoryDataType | grep -i xprotect`
- List Keychain Items: `security dump-keychain`
- Find Keychain Item: `security find-generic-password -a <account_name>`
- List Available Keychains: `security list-keychains`
- Check FileVault Status: `fdesetup status`
- List FileVault Users: `sudo fdesetup list`
- Get System Permissions: `ls -le@ <file_or_directory>`
- Change Permissions: `chmod 755 <file>`
- Change Ownership: `sudo chown user:group <file>`
- View Security Assessments: `spctl --assess --verbose <file>`
- Check TCC Database (Privacy): `sudo sqlite3 /Library/Application\ Support/com.apple.TCC/TCC.db "SELECT * FROM access;"`

### Application Information

- List Installed Applications: `ls -la /Applications/` or `system_profiler SPApplicationsDataType`
- Find Application Path: `mdfind "kMDItemKind == 'Application'" | grep -i <app_name>`
- Get Application Info: `mdls -name kMDItemVersion /Applications/<App>.app`
- List Safari Extensions: `ls -la ~/Library/Safari/Extensions/`
- List Chrome Extensions: `ls -la ~/Library/Application\ Support/Google/Chrome/Default/Extensions/`
- Get Install History: `system_profiler SPInstallHistoryDataType` or `cat /Library/Receipts/InstallHistory.plist`
- List Package Receipts: `pkgutil --pkgs`
- Get Package Info: `pkgutil --pkg-info <package_id>`
- List Files in Package: `pkgutil --files <package_id>`

### Log Analysis

- Show Recent System Logs: `log show --predicate 'processImagePath contains "kernel"' --last 1h`
- Show Authentication Logs: `log show --predicate 'eventMessage contains "authentication"' --info --last 24h`
- Show Sudo Events: `log show --predicate 'eventMessage contains "sudo"' --info --last 7d`
- Show Application-Specific Logs: `log show --predicate 'process == "<app_name>"' --last 1h`
- Stream Live Logs: `log stream`
- Stream Filtered Logs: `log stream --predicate 'eventMessage contains "error"'`
- Export Logs: `log collect --output /tmp/logs.logarchive`
- View Legacy Logs: `cat /var/log/system.log` (older macOS versions)
- View Install Logs: `cat /var/log/install.log`
- View WiFi Logs: `log show --predicate 'process == "airportd"' --last 1h`

### Memory and Crash Analysis

- View Memory Usage: `vm_stat` or `top -l 1 | head -n 10`
- List Swap Files: `ls -lh /private/var/vm/`
- View Crash Reports: `ls -la ~/Library/Logs/DiagnosticReports/`
- View System Crash Reports: `ls -la /Library/Logs/DiagnosticReports/`
- Generate Diagnostic Report: `sudo sysdiagnose` (creates report in /var/tmp/)
- Generate Process Sample: `sample <PID> 10` (samples for 10 seconds)
- Generate Spin Report: `spindump <PID>`

### Forensic and Incident Response

- Collect System Diagnostics: `sudo sysdiagnose -f /tmp/` (comprehensive diagnostic bundle)
- Create Disk Image: `sudo hdiutil create -srcfolder /path/to/folder -format UDZO /path/to/image.dmg`
- Mount Disk Image: `hdiutil attach /path/to/image.dmg`
- Calculate Directory Hash: `find /path -type f -exec shasum -a 256 {} \; > hashes.txt`
- Search Spotlight Database: `mdfind <query>`
- Rebuild Spotlight Index: `sudo mdutil -E /`
- Check Code Signing of Running Process: `codesign -dv /proc/<PID>/exe 2>&1`
- List Network Connections with Processes: `sudo lsof -i -n -P`
- Monitor File System Changes: `sudo fs_usage -w -f filesys` (real-time)
- Examine Binary for Indicators: `strings <binary> | grep -i <indicator>`
- Hexdump Binary: `xxd <binary> | head -n 50`
- Disassemble Binary: `otool -tV <binary>` (x86/ARM disassembly)
- List Loaded Dynamic Libraries: `otool -L <binary>`

### Helpful Aliases

Add these to `~/.zshrc` or `~/.bashrc` for quick access:

```bash
# Process shortcuts
alias psgrep='ps aux | grep -v grep | grep -i -e VSZ -e'
alias listening='lsof -iTCP -sTCP:LISTEN -n -P'
alias established='lsof -iTCP -sTCP:ESTABLISHED -n -P'

# Network shortcuts
alias ports='netstat -tulanp'
alias myip='ipconfig getifaddr en0'
alias publicip='curl -s ifconfig.me'

# System shortcuts
alias sysinfo='system_profiler SPSoftwareDataType SPHardwareDataType'
alias cleanup='sudo periodic daily weekly monthly'

# Forensics shortcuts
alias persistence='ls -la /Library/LaunchDaemons/ /Library/LaunchAgents/ ~/Library/LaunchAgents/'
alias quarantine='sqlite3 ~/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV2 "SELECT datetime(LSQuarantineTimeStamp + 978307200, \"unixepoch\") as timestamp, LSQuarantineAgentName, LSQuarantineOriginURLString, LSQuarantineDataURLString from LSQuarantineEvent order by timestamp desc limit 10;"'
```

### Remote Execution

- Execute Remote Command via SSH: `ssh user@host 'command'`
- Copy File via SCP: `scp /local/file user@host:/remote/path`
- Copy Directory via SCP: `scp -r /local/dir user@host:/remote/path`
- Remote Shell Session: `ssh user@host`
- Execute Script Remotely: `ssh user@host 'bash -s' < local_script.sh`

***
[Return to home page](../../README.md)
