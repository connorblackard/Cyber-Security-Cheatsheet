## macOS Triage Acquisition

### Key Items for Triage
- System and User Logs
  - Unified Logs (`/var/db/diagnostics/`)
  - Legacy logs (`/var/log/`)
  - User logs (`~/Library/Logs/`)
- Persistence Mechanisms
  - LaunchAgents (`~/Library/LaunchAgents/`, `/Library/LaunchAgents/`)
  - LaunchDaemons (`/Library/LaunchDaemons/`, `/System/Library/LaunchDaemons/`)
  - Login Items
  - Cron jobs
- User Activity
  - Shell history (`.bash_history`, `.zsh_history`)
  - Browser artifacts (Safari, Chrome, Firefox)
  - QuarantineEventsV2 database
  - KnowledgeC database
- File System Artifacts
  - FSEvents (`/.fseventsd/`)
  - Spotlight metadata (`/.Spotlight-V100/`)
  - Trash (`~/.Trash/`)
  - Recent items
- Application Data
  - Application Support folders
  - Preferences (plist files)
  - Keychains
  - Cookies
- Communication
  - Mail databases
  - Messages/iMessage (chat.db)
  - Notes database
- Network
  - Network configuration
  - WiFi known networks
  - Firewall logs
- Installation History
  - `/Library/Receipts/InstallHistory.plist`
  - Application bundles
  - Package receipts

### Tools

- [AutoMacTC](https://github.com/CrowdStrike/automactc) - Automated macOS forensic triage collection
- [ORION](https://github.com/Johnng007/ORION) - Artifact collection for macOS
- [mac_apt](https://github.com/ydkhatri/mac_apt) - macOS Artifact Parsing Tool
- [Velociraptor](https://github.com/Velocidex/velociraptor) - Cross-platform endpoint visibility
- [osquery](https://osquery.io/) - SQL-based system instrumentation
- Build Your Own

#### AutoMacTC
AutoMacTC is a modular forensic triage collection framework.

```bash
# Basic collection
sudo python3 automactc.py -m all -o /path/to/output

# Specific modules
sudo python3 automactc.py -m bash chrome safari -o /path/to/output

# With compression
sudo python3 automactc.py -m all -o /path/to/output -f tar
```

**Popular Modules:**
- `bash` - bash/zsh history
- `safari` - Safari artifacts
- `chrome` - Chrome artifacts
- `firefox` - Firefox artifacts
- `quicklook` - QuickLook thumbnail cache
- `lsquarantine` - Quarantine events
- `dirlist` - Directory listings
- `pslist` - Running processes
- `users` - User accounts

#### ORION
ORION collects key forensic artifacts into a structured output.

```bash
# Run collection
sudo ./orion --output /path/to/output

# With specific artifact sets
sudo ./orion --quick --output /path/to/output
```

#### mac_apt
macOS Artifact Parsing Tool - extracts and parses artifacts.

```bash
# Parse all artifacts from live system
sudo python3 mac_apt.py / -o /path/to/output

# Parse specific artifacts
sudo python3 mac_apt.py / -o /path/to/output -p USERS,SAFARI,BASH

# Parse from disk image
sudo python3 mac_apt.py /Volumes/Evidence -o /path/to/output
```

#### Velociraptor
Cross-platform endpoint monitoring and DFIR tool.

```bash
# Run offline collector (create config in GUI first)
./velociraptor-v0.73.1-darwin-amd64 -- --embedded_config collector.yaml
```

Create collector configuration via Velociraptor server GUI. macOS artifacts available in hunt templates.

#### osquery
Query system information using SQL syntax.

```bash
# Interactive mode
osqueryi

# Example queries
SELECT * FROM processes;
SELECT * FROM users;
SELECT * FROM chrome_extensions;
SELECT * FROM startup_items;
SELECT * FROM launchd;

# Run query from file
osqueryi --read_max 0 < query.sql > output.txt
```

#### Build Your Own

**Quick triage collection script:**

```bash
#!/bin/bash
# macOS Quick Triage Collection
# Usage: sudo ./triage.sh

COLLECTION_DIR="/tmp/macos_triage_$(date +%Y%m%d_%H%M%S)"
HOSTNAME=$(hostname)

mkdir -p "$COLLECTION_DIR"/{logs,persistence,users,network,system,browser}

echo "[*] Starting macOS triage collection..."
echo "[*] Output directory: $COLLECTION_DIR"

# System Information
echo "[+] Collecting system information..."
system_profiler SPSoftwareDataType SPHardwareDataType > "$COLLECTION_DIR/system/system_info.txt"
sw_vers > "$COLLECTION_DIR/system/os_version.txt"
uname -a > "$COLLECTION_DIR/system/uname.txt"
uptime > "$COLLECTION_DIR/system/uptime.txt"
date > "$COLLECTION_DIR/system/collection_date.txt"

# Processes and Network
echo "[+] Collecting process and network information..."
ps aux > "$COLLECTION_DIR/system/processes.txt"
lsof -n -P > "$COLLECTION_DIR/network/lsof.txt"
netstat -an > "$COLLECTION_DIR/network/netstat.txt"
arp -a > "$COLLECTION_DIR/network/arp.txt"

# Users
echo "[+] Collecting user information..."
dscl . list /Users > "$COLLECTION_DIR/users/user_list.txt"
last > "$COLLECTION_DIR/users/last_logins.txt"
who > "$COLLECTION_DIR/users/current_users.txt"

# Persistence
echo "[+] Collecting persistence mechanisms..."
ls -la /Library/LaunchAgents/ > "$COLLECTION_DIR/persistence/launch_agents_system.txt" 2>/dev/null
ls -la /Library/LaunchDaemons/ > "$COLLECTION_DIR/persistence/launch_daemons.txt" 2>/dev/null
cp -R /Library/LaunchAgents/ "$COLLECTION_DIR/persistence/LaunchAgents_System/" 2>/dev/null
cp -R /Library/LaunchDaemons/ "$COLLECTION_DIR/persistence/LaunchDaemons/" 2>/dev/null
crontab -l > "$COLLECTION_DIR/persistence/crontab.txt" 2>/dev/null

# Per-user artifacts
for USER_HOME in /Users/*; do
    if [ -d "$USER_HOME" ]; then
        USERNAME=$(basename "$USER_HOME")
        echo "[+] Collecting artifacts for user: $USERNAME"

        # Shell history
        cp "$USER_HOME/.bash_history" "$COLLECTION_DIR/users/${USERNAME}_bash_history.txt" 2>/dev/null
        cp "$USER_HOME/.zsh_history" "$COLLECTION_DIR/users/${USERNAME}_zsh_history.txt" 2>/dev/null

        # User persistence
        ls -la "$USER_HOME/Library/LaunchAgents/" > "$COLLECTION_DIR/persistence/${USERNAME}_launch_agents.txt" 2>/dev/null
        cp -R "$USER_HOME/Library/LaunchAgents/" "$COLLECTION_DIR/persistence/LaunchAgents_${USERNAME}/" 2>/dev/null

        # Browser artifacts
        cp "$USER_HOME/Library/Safari/History.db" "$COLLECTION_DIR/browser/${USERNAME}_safari_history.db" 2>/dev/null
        cp "$USER_HOME/Library/Application Support/Google/Chrome/Default/History" "$COLLECTION_DIR/browser/${USERNAME}_chrome_history.db" 2>/dev/null

        # Quarantine events
        cp "$USER_HOME/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV2" "$COLLECTION_DIR/browser/${USERNAME}_quarantine.db" 2>/dev/null
    fi
done

# Logs
echo "[+] Collecting logs..."
cp -R /var/log/ "$COLLECTION_DIR/logs/var_log/" 2>/dev/null
log show --predicate 'eventMessage contains "sudo"' --info --last 7d > "$COLLECTION_DIR/logs/sudo_events_7days.txt" 2>/dev/null
log show --predicate 'eventMessage contains "authentication"' --info --last 7d > "$COLLECTION_DIR/logs/auth_events_7days.txt" 2>/dev/null

# Installation history
echo "[+] Collecting installation history..."
cp /Library/Receipts/InstallHistory.plist "$COLLECTION_DIR/system/InstallHistory.plist" 2>/dev/null

# Compress collection
echo "[+] Compressing collection..."
tar -czf "${COLLECTION_DIR}.tar.gz" -C /tmp "$(basename $COLLECTION_DIR)"
echo "[*] Collection complete: ${COLLECTION_DIR}.tar.gz"
echo "[*] Size: $(du -h ${COLLECTION_DIR}.tar.gz | cut -f1)"

# Cleanup
rm -rf "$COLLECTION_DIR"
```

**Advanced collection with timeline:**

```bash
#!/bin/bash
# Timeline generation using FSEvents and Unified Logs

OUTPUT="/tmp/macos_timeline_$(date +%Y%m%d_%H%M%S)"
mkdir -p "$OUTPUT"

# FSEvents timeline (requires external tool like FSEventsParser)
# Download from: https://github.com/dlcowen/FSEventsParser

# Unified log timeline (last 24 hours)
log show --style syslog --last 24h > "$OUTPUT/unified_logs_24h.txt"

# File system timeline (modified in last 7 days)
find / -type f -mtime -7 -ls 2>/dev/null > "$OUTPUT/modified_files_7days.txt"

# Create MFT-style timeline
ls -lR / 2>/dev/null > "$OUTPUT/full_directory_listing.txt"

tar -czf "${OUTPUT}.tar.gz" -C /tmp "$(basename $OUTPUT)"
rm -rf "$OUTPUT"
echo "[*] Timeline saved to: ${OUTPUT}.tar.gz"
```

### Remote Collection

**SSH-based remote collection:**

```bash
# Copy script to remote host and execute
scp triage.sh user@remote-host:/tmp/
ssh user@remote-host 'sudo /tmp/triage.sh'
scp user@remote-host:/tmp/macos_triage_*.tar.gz ./evidence/

# One-liner remote collection
ssh user@remote-host 'bash -s' < triage.sh
```

**Using Velociraptor for enterprise collection:**

1. Deploy Velociraptor server
2. Create offline collector with macOS artifact hunts
3. Distribute collector binary
4. Execute: `./velociraptor -- --embedded_config config.yaml`
5. Retrieve generated ZIP file

***
[Return to home page](../../README.md)
