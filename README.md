# Task-1-Scan-Your-Local-Network-for-Open-Ports-
Objective: Learn to discover open ports on devices in your local network to understand network exposure.
## Prerequisites

- Nmap installed on your system
- Basic understanding of TCP protocol and port scanning
- Administrative/root privileges (required for SYN scans)
- Access to a local network for testing

## Installation

### Installing Nmap

**Linux (Ubuntu/Debian):**
```bash
sudo apt update
sudo apt install nmap
```

**Linux (CentOS/RHEL):**
```bash
sudo yum install nmap
# or
sudo dnf install nmap
```

**macOS:**
```bash
brew install nmap
```

**Windows:**
- Download from: https://nmap.org/download.html
- Run the installer as Administrator

### Clone This Repository
```bash
git clone https://github.com/yourusername/network-port-scanner.git
cd network-port-scanner
```

## Usage

### Basic TCP SYN Scan
```bash
sudo nmap -sS -T4 <target_ip> -oN nmap_result.txt
```

### Example Commands

**Scan a single host:**
```bash
sudo nmap -sS -T4 192.168.1.1 -oN nmap_result.txt
```

**Scan a subnet:**
```bash
sudo nmap -sS -T4 192.168.1.0/24 -oN nmap_result.txt
```

**Scan specific ports:**
```bash
sudo nmap -sS -T4 -p 22,80,443 192.168.1.1 -oN nmap_result.txt
```

**Scan port range:**
```bash
sudo nmap -sS -T4 -p 1-1000 192.168.1.1 -oN nmap_result.txt
```

## Command Breakdown

- `nmap`: The network mapping tool
- `-sS`: TCP SYN scan (stealth scan)
- `-T4`: Timing template (aggressive timing)
- `<target_ip>`: IP address or range to scan
- `-oN`: Output results in normal format to file
- `nmap_result.txt`: Output filename

## Understanding the Flags

### `-sS (TCP SYN Scan)`
- Also known as "stealth scan"
- Sends SYN packets without completing the TCP handshake
- Faster and more stealthy than full TCP connect scans
- Requires root/administrator privileges

### `-T4 (Timing)`
- Aggressive timing template
- Faster scan with higher packet rates
- Options range from T0 (paranoid) to T5 (insane)
- T4 is good balance between speed and reliability

### `-oN (Normal Output)`
- Saves results in human-readable format
- Includes timestamps and scan summary
- Easy to review and analyze later

## Example Output

```
Starting Nmap 7.94 ( https://nmap.org )
Nmap scan report for 192.168.1.1
Host is up (0.0012s latency).
Not shown: 997 closed ports
PORT    STATE SERVICE
22/tcp  open  ssh
80/tcp  open  http
443/tcp open  https
MAC Address: AA:BB:CC:DD:EE:FF (Vendor Name)

Nmap done: 1 IP address (1 host up) scanned in 0.85 seconds
```

## Educational Goals

By completing this project, you will learn:
- How TCP SYN scanning works at the packet level
- The difference between stealth and connect scans
- How to interpret Nmap output and port states
- Network reconnaissance fundamentals
- The importance of proper network security configuration

## Port States Explained

- **Open**: Service is actively listening and accepting connections
- **Closed**: Port is accessible but no service is listening
- **Filtered**: Port is blocked by firewall or packet filter
- **Unfiltered**: Port is accessible but state cannot be determined

## File Structure

```
network-port-scanner/
├── README.md
├── nmap_result.txt    # Scan output file
└── examples/          # Example scan results
    └── sample_scan.txt
```

## Important Notes

⚠️ **Legal and Ethical Use Only**
- Only scan networks you own or have explicit permission to test
- This tool is for educational purposes and authorized security testing
- Unauthorized network scanning may violate laws and terms of service
- Always follow responsible disclosure practices

⚠️ **Technical Requirements**
- TCP SYN scans require root/administrator privileges
- Some firewalls may detect and block SYN scans
- Results may vary based on target system configuration

## Common Use Cases

1. **Network Discovery**: Find active hosts on your network
2. **Service Enumeration**: Identify running services and versions
3. **Security Assessment**: Check for unexpected open ports
4. **Compliance Verification**: Ensure only required services are running

## Next Steps

After mastering TCP SYN scanning, consider exploring:
- UDP scanning (`-sU`)
- Service version detection (`-sV`)
- Operating system detection (`-O`)
- Script scanning (`-sC` or `--script`)
- Stealth techniques and evasion

## Troubleshooting

**Permission Denied Error:**
```bash
# Make sure to run with sudo on Linux/macOS
sudo nmap -sS -T4 <target_ip> -oN nmap_result.txt
```

**No Results:**
- Check if target host is up: `ping <target_ip>`
- Try different timing: `-T3` (slower) or `-T2`
- Check firewall settings on both scanner and target

## Contributing

This is an educational project. Feel free to:
- Add example scan results
- Improve documentation
- Share interesting findings
- Suggest additional scanning techniques
