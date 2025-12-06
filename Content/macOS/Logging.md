## macOS Logging

### Unified Logging System

macOS uses the Unified Logging System (introduced in macOS 10.12 Sierra) which centralizes system and application logs. The `log` command is the primary tool for querying these logs.

### Log Command Basics

- Show all logs: `log show`
- Show recent logs: `log show --last 1h` (1h, 1d, 1w, etc.)
- Stream live logs: `log stream`
- Collect logs to archive: `log collect --output /tmp/logs.logarchive`
- Show specific process: `log show --predicate 'process == "processname"'`
- Show specific subsystem: `log show --predicate 'subsystem == "com.apple.subsystem"'`
- Show by time range: `log show --start "2024-01-01 12:00:00" --end "2024-01-01 13:00:00"`

### Useful Predicates

Predicates filter log output based on specific criteria:

#### Authentication Events
```bash
# Authentication attempts
log show --predicate 'eventMessage contains "authentication"' --info --last 24h

# Sudo commands
log show --predicate 'eventMessage contains "sudo"' --info --last 7d

# Login attempts
log show --predicate 'process == "loginwindow"' --last 1d

# SSH authentication
log show --predicate 'process == "sshd"' --info --last 1d

# Screen unlock events
log show --predicate 'eventMessage contains "unlock"' --last 1d
```

#### Network Events
```bash
# Network changes
log show --predicate 'subsystem == "com.apple.network"' --last 1h

# WiFi events
log show --predicate 'process == "airportd"' --last 1h

# VPN connections
log show --predicate 'process == "neagent"' --last 24h

# DNS queries (requires additional logging)
log show --predicate 'subsystem == "com.apple.network.dns"' --last 1h
```

#### Security Events
```bash
# Gatekeeper events
log show --predicate 'subsystem == "com.apple.gatekeeper"' --last 7d

# XProtect malware scanning
log show --predicate 'subsystem == "com.apple.XProtect"' --last 7d

# Keychain access
log show --predicate 'process == "securityd"' --info --last 1h

# Code signing verification
log show --predicate 'subsystem == "com.apple.security.assessment"' --last 1d

# TCC (Transparency, Consent, and Control) privacy events
log show --predicate 'subsystem == "com.apple.TCC"' --last 1d
```

#### Application Events
```bash
# Application crashes
log show --predicate 'eventMessage contains "crash"' --last 7d

# Specific application
log show --predicate 'process == "Safari"' --last 1h

# Application installations
log show --predicate 'process == "installer"' --last 7d

# LaunchServices (app launches)
log show --predicate 'subsystem == "com.apple.launchservices"' --last 1h
```

#### System Events
```bash
# Kernel messages
log show --predicate 'processImagePath contains "kernel"' --last 1h

# System boot/shutdown
log show --predicate 'eventMessage contains "shutdown" OR eventMessage contains "boot"' --last 7d

# Sleep/wake events
log show --predicate 'eventMessage contains "sleep" OR eventMessage contains "wake"' --last 1d

# USB device connections
log show --predicate 'subsystem == "com.apple.iokit.IOUSBHostFamily"' --last 1d

# Disk mounting
log show --predicate 'process == "diskmanagementd"' --last 1d
```

#### Error and Debug Messages
```bash
# All errors
log show --predicate 'messageType == error' --last 1h

# Faults (critical errors)
log show --predicate 'messageType == fault' --last 1h

# Specific error message
log show --predicate 'eventMessage contains "failed"' --last 1h

# Debug level messages
log show --predicate 'messageType == debug' --debug --last 10m
```

### Legacy Log Files

Older macOS versions and some applications still use traditional log files located in `/var/log/`:

| Log File               | Location                            | Contents                                      |
| ---------------------- | ----------------------------------- | --------------------------------------------- |
| System Log (Legacy)    | /var/log/system.log                 | General system messages (pre-Sierra)          |
| Installation Log       | /var/log/install.log                | Software installation activity                 |
| WiFi Log               | /var/log/wifi.log                   | WiFi connection history and diagnostics        |
| Firewall Log           | /var/log/appfirewall.log            | Application firewall blocks and allows         |
| Kernel Log             | /var/log/kernel.log                 | Kernel messages and panics                     |
| FSEvent Log            | /var/log/fsevents.log               | File system event information                  |
| Daily/Weekly/Monthly   | /var/log/daily.out, weekly.out, monthly.out | Periodic maintenance task output  |

### Application-Specific Logs

| Application      | Location                                               | Notes                                    |
| ---------------- | ------------------------------------------------------ | ---------------------------------------- |
| Safari           | ~/Library/Logs/Safari/                                 | Browser-specific logs                    |
| Mail             | ~/Library/Logs/Mail/                                   | Email client logs                        |
| Messages         | ~/Library/Logs/Messages/                               | iMessage/SMS logs                        |
| Console          | ~/Library/Logs/Console/                                | Per-user console logs                    |
| DiagnosticReports| ~/Library/Logs/DiagnosticReports/                      | Crash and hang reports                   |
| System Reports   | /Library/Logs/DiagnosticReports/                       | System-wide crash reports                |
| CrashReporter    | ~/Library/Logs/CrashReporter/                          | Legacy crash report location             |
| Adobe            | ~/Library/Logs/Adobe/                                  | Adobe application logs                   |

### Important Log Locations

| Purpose              | Location                                    | Description                              |
| -------------------- | ------------------------------------------- | ---------------------------------------- |
| Audit Logs           | /var/audit/                                 | BSM (Basic Security Module) audit trails |
| ASL Database         | /var/log/asl/                               | Apple System Log database (legacy)       |
| Unified Log Store    | /var/db/diagnostics/                        | Unified logging persistence              |
| System Diagnostics   | /var/tmp/                                   | sysdiagnose output archives              |
| User Diagnostics     | ~/Library/Logs/DiagnosticReports/           | User application crashes                 |
| System Diagnostics   | /Library/Logs/DiagnosticReports/            | System crashes and panics                |

### Audit Logs (BSM)

macOS includes Basic Security Module (BSM) audit logs for security-relevant events:

```bash
# Enable audit system (typically enabled by default)
sudo audit -s

# Check audit status
sudo audit -t

# View current audit trail
sudo praudit /var/audit/current

# View specific audit file
sudo praudit /var/audit/20240101000000.20240101120000

# Search for specific user activity
sudo praudit /var/audit/* | grep -i "username"

# Search for specific event types
sudo praudit /var/audit/* | grep -i "AUE_execve"
```

### Key Audit Event Types

Common BSM audit event types to investigate:

- `AUE_execve` - Program execution
- `AUE_DARWIN_login` - User login
- `AUE_DARWIN_logout` - User logout
- `AUE_su` - Switch user
- `AUE_sudo` - Sudo command execution
- `AUE_connect` - Network connection
- `AUE_accept` - Incoming network connection
- `AUE_open_rwtc` - File open with write
- `AUE_unlink` - File deletion
- `AUE_rename` - File rename

### Log Analysis Tools

#### Native Tools
- `log` - Unified logging query tool
- `Console.app` - GUI log viewer
- `syslog` - Legacy logging command (deprecated)
- `praudit` - BSM audit log viewer
- `fs_usage` - Real-time file system activity monitor

#### Third-Party Tools
- [UnifiedLogReader](https://github.com/ydkhatri/UnifiedLogReader) - Parse unified logs offline
- [OSXCollector](https://github.com/Yelp/osxcollector) - Forensic evidence collection
- [Crescendo](https://github.com/SuprHackerSteve/Crescendo) - Real-time event viewer
- [Santa](https://github.com/google/santa) - Binary authorization system with logging
- [ELK Stack](https://www.elastic.co/elastic-stack/) - Log aggregation and analysis

### Forensic Log Analysis Examples

#### Identify Suspicious Process Execution
```bash
# Find all process executions in last 24 hours
log show --predicate 'eventMessage contains "execve"' --last 24h

# Find processes run via sudo
log show --predicate 'eventMessage contains "sudo" AND eventMessage contains "command"' --last 7d
```

#### Track User Login Activity
```bash
# User login events
log show --predicate 'process == "loginwindow"' --last 7d

# SSH login attempts
log show --predicate 'process == "sshd" AND eventMessage contains "Accepted"' --last 7d

# Failed authentication
log show --predicate 'eventMessage contains "authentication failure"' --last 24h
```

#### Network Connection Analysis
```bash
# Outbound connections
log show --predicate 'eventMessage contains "connection to"' --last 1h

# VPN activity
log show --predicate 'subsystem contains "vpn"' --last 24h
```

#### Malware and Security Indicators
```bash
# Gatekeeper blocks
log show --predicate 'subsystem == "com.apple.gatekeeper" AND eventMessage contains "blocked"' --last 30d

# XProtect detections
log show --predicate 'subsystem == "com.apple.XProtect" AND messageType == fault' --last 30d

# Code signature failures
log show --predicate 'eventMessage contains "signature" AND messageType == error' --last 7d
```

#### System Changes
```bash
# Kernel extension loads
log show --predicate 'eventMessage contains "kext" AND eventMessage contains "loaded"' --last 7d

# Launch daemon/agent loads
log show --predicate 'process == "launchd"' --last 1h

# Software installations
log show --predicate 'process == "installer"' --last 30d
```

### Log Persistence and Retention

By default, unified logs are rotated based on storage limits (not time). To configure:

```bash
# Check current log size
sudo log config --status

# Set log retention size (in MB)
sudo log config --mode "persist:size=512"

# Set log retention period (requires macOS 11+)
sudo log config --mode "persist:ttl=30" # 30 days
```

### Export Logs for Analysis

```bash
# Export logs to archive for offline analysis
log collect --last 7d --output /tmp/logs_7days.logarchive

# Export to syslog-style text format
log show --last 7d --style syslog > /tmp/logs_7days.txt

# Export with full metadata
log show --last 1d --style json > /tmp/logs_1day.json

# Create comprehensive diagnostic bundle
sudo sysdiagnose -f /tmp/
```

### Real-Time Monitoring

```bash
# Stream all logs in real-time
log stream

# Stream with filter
log stream --predicate 'eventMessage contains "error"'

# Stream specific process
log stream --process "Safari"

# Stream with formatting
log stream --style syslog

# Stream and save to file
log stream --predicate 'messageType == error' > /tmp/errors.log
```

***
[Return to home page](../../README.md)
