## Nmap
### Basic Usage

- **Scan a single host:** `nmap <target IP>`
- **Scan a range of hosts:** `nmap 192.168.1.1-254`
- **Scan a network:** `nmap 192.168.1.0/24`
- **Scan multiple hosts:** `nmap <target1> <target2> ...`

### Scan Types

- **TCP Scan:** `nmap -sT <target>`
- **UDP Scan:** `nmap -sU <target>`
- **Stealth Scan:** `nmap -sS <target>`
### Scripting

- **Run default scripts:** `nmap -sC <target>`
- **Run specific scripts:** `nmap -sC --script <script1>,<script2> <target>`

### Output Options

- **Verbose output:** `nmap -v <target>`
- **Quiet output:** `nmap -q <target>`
- **XML output:** `nmap -oX <output_file> <target>`

### Service and OS Detection

- **Service and OS detection:** `nmap -A <target>`
- **Version detection:** `nmap -sV <target>`

### Other Useful Options

- **Specify port range:** `nmap -p <port_range> <target>`
- **Avoid ping sweep:** `nmap -Pn <target>`
- **All Ports:** `-p-`
*** 
[Return to home page](../README.md)