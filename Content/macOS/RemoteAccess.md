## macOS Remote Access

### Native Remote Access Methods

macOS provides several built-in methods for remote access and management:

| Method                    | Port(s)      | Protocol | Encryption | Notes                                                |
| ------------------------- | ------------ | -------- | ---------- | ---------------------------------------------------- |
| SSH                       | 22           | TCP      | Yes        | Preferred method, enabled via System Preferences     |
| Screen Sharing (VNC)      | 5900         | TCP      | Optional   | Can use encryption, Apple Remote Desktop protocol    |
| Apple Remote Desktop      | 3283, 5900   | TCP/UDP  | Yes        | Enterprise remote management (requires license)      |
| Apple File Protocol (AFP) | 548          | TCP      | Yes        | Legacy file sharing (deprecated)                     |
| SMB File Sharing          | 445          | TCP      | Yes        | Modern file sharing protocol                         |
| Remote Apple Events       | 3031         | TCP      | No         | Legacy, disabled by default (security risk)          |
| Back to My Mac           | N/A          | iCloud   | Yes        | Deprecated in macOS Mojave                           |

### SSH Remote Access

SSH is the recommended method for secure remote access to macOS systems.

#### Enable SSH (Remote Login)
```bash
# Enable SSH via command line
sudo systemsetup -setremotelogin on

# Enable for specific users
sudo dseditgroup -o edit -a username -t user com.apple.access_ssh

# Disable SSH
sudo systemsetup -setremotelogin off

# Check SSH status
sudo systemsetup -getremotelogin
```

#### SSH Connection
```bash
# Basic SSH connection
ssh username@hostname

# SSH with specific key
ssh -i ~/.ssh/id_rsa username@hostname

# SSH with port forwarding
ssh -L local_port:remote_host:remote_port username@hostname

# SSH with X11 forwarding (GUI apps)
ssh -X username@hostname

# Execute single command
ssh username@hostname 'command'

# Copy files via SCP
scp file.txt username@hostname:/path/to/destination
scp -r directory/ username@hostname:/path/to/destination

# Copy files via SFTP
sftp username@hostname
```

#### SSH Security Best Practices
```bash
# Disable password authentication (key-only)
# Edit /etc/ssh/sshd_config:
PasswordAuthentication no
ChallengeResponseAuthentication no
UsePAM no

# Disable root login
PermitRootLogin no

# Limit users who can SSH
AllowUsers user1 user2

# Change default SSH port
Port 2222

# Restart SSH after config changes
sudo launchctl unload /System/Library/LaunchDaemons/ssh.plist
sudo launchctl load -w /System/Library/LaunchDaemons/ssh.plist
```

#### SSH Logging
SSH authentication and connection logs are found in:
- Unified Logs: `log show --predicate 'process == "sshd"' --last 24h`
- Legacy: `/var/log/system.log` (older macOS versions)

### Screen Sharing (VNC)

macOS includes built-in VNC server capabilities.

#### Enable Screen Sharing
```bash
# Enable via command line
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -activate -configure -access -on -restart -agent -privs -all

# Enable for all users
sudo defaults write /var/db/launchd.db/com.apple.launchd/overrides.plist com.apple.screensharing -dict Disabled -bool false

# Check Screen Sharing status
sudo launchctl list | grep screensharing
```

#### Connect to Screen Sharing
```bash
# From macOS Finder
# Go > Connect to Server > vnc://hostname

# From command line
open vnc://hostname:5900

# With authentication
open vnc://username:password@hostname:5900
```

#### Screen Sharing Security Considerations
- VNC traffic can be unencrypted by default
- Tunnel VNC through SSH for encryption:
  ```bash
  ssh -L 5900:localhost:5900 username@remote_host
  # Then connect to localhost:5900
  ```
- Screen Sharing logs: `log show --predicate 'subsystem contains "screensharing"' --last 24h`

### Apple Remote Desktop (ARD)

Apple's enterprise remote management solution.

#### Enable ARD
```bash
# Enable and configure ARD (requires admin privileges)
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -activate -configure -allowAccessFor -allUsers -privs -all -clientopts -setmenuextra -menuextra yes

# Enable for specific users
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -activate -configure -access -on -users admin -privs -all -restart -agent

# Disable ARD
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -deactivate -stop
```

#### ARD Capabilities
- Remote desktop control
- Remote command execution (sends UNIX commands)
- File transfer
- Software installation
- Inventory collection
- Screen observation (view without control)

#### ARD Forensic Artifacts
- ARD database: `/var/db/RemoteManagement/`
- ARD logs: `/Library/Logs/RemoteManagement/`
- Task history: `/var/db/RemoteManagement/RMDB/RMDB.sqlite3`
- Connection logs in unified logs: `log show --predicate 'process == "ARDAgent"' --last 7d`

### Third-Party Remote Access Tools

Common third-party remote access solutions:

| Tool              | Type        | Encryption | Notes                                       |
| ----------------- | ----------- | ---------- | ------------------------------------------- |
| TeamViewer        | Commercial  | Yes        | Remote support and access                   |
| AnyDesk           | Commercial  | Yes        | Remote desktop                              |
| LogMeIn           | Commercial  | Yes        | Remote access and management                |
| Zoom              | Commercial  | Yes        | Screen sharing and remote control           |
| Chrome Remote     | Free        | Yes        | Browser-based remote desktop                |
| Splashtop         | Commercial  | Yes        | Remote desktop                              |
| NoMachine         | Freemium    | Yes        | Remote desktop (NX protocol)                |
| RealVNC           | Freemium    | Yes        | VNC-based remote access                     |
| Microsoft RDP     | Free        | Yes        | Remote Desktop Protocol client (macOS app)  |

#### Third-Party Tool Artifacts
```bash
# Check for installed remote access apps
ls -la /Applications/ | grep -iE "teamviewer|anydesk|logmein|zoom|chrome|splashtop|nomachine|vnc"

# Check LaunchAgents/Daemons for persistence
ls -la /Library/LaunchAgents/ | grep -iE "teamviewer|anydesk|logmein"
ls -la /Library/LaunchDaemons/ | grep -iE "teamviewer|anydesk|logmein"

# Check running processes
ps aux | grep -iE "teamviewer|anydesk|logmein|vnc"

# Check network connections
lsof -i | grep -iE "teamviewer|anydesk|logmein"

# Application logs
ls -la ~/Library/Logs/ | grep -iE "teamviewer|anydesk|logmein"
```

### Safe vs Unsafe Remote Access Methods

#### Safe Remote Access Methods
Methods that provide strong security and proper audit trails:

| Method                    | Security Level | Audit Trail | Credential Storage          |
| ------------------------- | -------------- | ----------- | --------------------------- |
| SSH with Key Auth         | High           | Yes         | Private key (encrypted)     |
| ARD with TLS              | High           | Yes         | Managed by system           |
| VNC over SSH Tunnel       | High           | Yes         | SSH handles auth            |
| MDM Solutions (Jamf)      | High           | Yes         | Certificate-based           |

**Best Practices:**
- Use SSH key authentication instead of passwords
- Tunnel VNC through SSH
- Enable logging and monitoring
- Use certificate-based authentication when possible
- Implement IP allowlisting/denylisting
- Require multi-factor authentication

#### Unsafe Remote Access Methods
Methods with security concerns:

| Method                    | Risk Level | Issues                                              |
| ------------------------- | ---------- | --------------------------------------------------- |
| VNC without encryption    | High       | Clear-text traffic, credential exposure             |
| SSH with weak passwords   | Medium     | Brute-force attacks, credential stuffing            |
| Remote Apple Events       | High       | Unencrypted, legacy protocol                        |
| Telnet                    | Critical   | No encryption, avoid entirely                       |
| Unauthorized RATs         | Critical   | Malware, backdoors (TeamViewer misuse, etc.)        |

### Detection of Unauthorized Remote Access

#### Check Enabled Remote Services
```bash
# Check SSH status
sudo systemsetup -getremotelogin

# Check Screen Sharing
sudo launchctl list | grep screensharing

# Check ARD
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -status

# Check file sharing
sharing -l

# List all sharing services
sudo systemsetup -getremotelogin
sudo systemsetup -getremoteappleevents
```

#### Monitor for Remote Connections
```bash
# Active SSH connections
who
w
last | grep "still logged in"

# Network connections
netstat -an | grep ESTABLISHED
lsof -i -n -P | grep ESTABLISHED

# ARD connections
log show --predicate 'process == "ARDAgent"' --last 1h
```

#### Check for Remote Access Persistence
```bash
# LaunchAgents/Daemons
ls -la ~/Library/LaunchAgents/
ls -la /Library/LaunchAgents/
ls -la /Library/LaunchDaemons/

# Login Items
osascript -e 'tell application "System Events" to get the name of every login item'

# Known RAT locations
find /Library -name "*TeamViewer*" -o -name "*AnyDesk*" 2>/dev/null
find ~/Library -name "*TeamViewer*" -o -name "*AnyDesk*" 2>/dev/null
```

### Remote Access Forensic Analysis

#### SSH Investigation
```bash
# View SSH authentication logs
log show --predicate 'process == "sshd"' --last 7d --style syslog

# Failed SSH attempts
log show --predicate 'process == "sshd" AND eventMessage contains "Failed"' --last 7d

# Successful SSH logins
log show --predicate 'process == "sshd" AND eventMessage contains "Accepted"' --last 7d

# SSH connection sources
last | grep ssh

# Check authorized_keys for unauthorized entries
cat ~/.ssh/authorized_keys
cat /var/root/.ssh/authorized_keys
```

#### VNC/ARD Investigation
```bash
# Screen Sharing logs
log show --predicate 'subsystem contains "screensharing" OR process == "screensharingd"' --last 7d

# ARD connections
log show --predicate 'process == "ARDAgent"' --last 7d

# ARD task database
sudo sqlite3 /var/db/RemoteManagement/RMDB/RMDB.sqlite3 "SELECT * FROM Tasks;"

# Check VNC password file
ls -la /Library/Preferences/com.apple.VNCSettings.txt
```

#### Third-Party RAT Detection
```bash
# Search for known RAT applications
mdfind "kMDItemKind == 'Application'" | grep -iE "teamviewer|anydesk|logmein"

# Check for suspicious outbound connections
lsof -i -n -P | grep -v "LISTEN"

# Review quarantine database for downloads
sqlite3 ~/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV2 \
  "SELECT datetime(LSQuarantineTimeStamp + 978307200, 'unixepoch'), LSQuarantineAgentName, LSQuarantineDataURLString
   FROM LSQuarantineEvent
   WHERE LSQuarantineDataURLString LIKE '%teamviewer%'
      OR LSQuarantineDataURLString LIKE '%anydesk%'
   ORDER BY LSQuarantineTimeStamp DESC;"
```

### Recommendations

**For System Administrators:**
1. Only enable necessary remote access methods
2. Use SSH with key authentication
3. Implement network segmentation and firewall rules
4. Enable comprehensive logging
5. Regularly audit remote access permissions
6. Use MDM solutions for enterprise management
7. Implement jump hosts/bastion servers for privileged access

**For Security Teams:**
8. Monitor for unauthorized remote access tools
9. Baseline normal remote access patterns
10. Alert on anomalous remote connections
11. Review remote access logs regularly
12. Implement EDR solutions to detect RATs
13. Use network monitoring to identify C2 traffic

**For Incident Response:**
14. Check all remote access methods during investigations
15. Review ARD task database for malicious commands
16. Analyze SSH logs for lateral movement
17. Identify unauthorized remote access tools
18. Examine network connections for backdoors

***
[Return to home page](../../README.md)
