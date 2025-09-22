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

## Results
**The Ip addresses are diguised as Ip1, Ip2, Ip3......**
```
Nmap scan report for Ip1
Host is up (0.00081s latency).
Not shown: 816 filtered tcp ports (net-unreach), 181 filtered tcp ports (no-response)
PORT    STATE SERVICE
53/tcp  open  domain
80/tcp  open  http
443/tcp open  https



Nmap scan report for TIZEN Ip2
Host is up (0.0013s latency).
Not shown: 812 filtered tcp ports (net-unreach), 186 closed tcp ports (reset), 1 closed tcp ports (net-unreach)
PORT     STATE SERVICE
8080/tcp open  http-proxy


Nmap scan report for Ip3
Host is up (0.00079s latency).
Not shown: 825 filtered tcp ports (net-unreach), 172 filtered tcp ports (no-response)
PORT    STATE SERVICE
135/tcp open  msrpc
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds
```
**Ports Opened**
1. **domain** -  DNS service that resolves domain names to IP addresses and handles DNS queries
2. **http** - Web server providing unencrypted HTTP websites and web applications
3. **https** - Secure web server providing encrypted HTTP websites using SSL/TLS
4. **http-proxy** - Web proxy server that forwards HTTP requests between clients and web servers
5. **msrpc** - Microsoft Remote Procedure Call service for inter-process communication in Windows
6. **netbios-ssn** - NetBIOS Session Service for file/printer sharing and network communication in Windows
7. **microsoft-ds** - Microsoft Directory Services (SMB/CIFS) for file sharing and Active Directory communication

## Potential Risks Involved
**domain (Port 53)**

- DNS cache poisoning attacks and DNS spoofing
- Information disclosure about internal network structure
- DNS tunneling for data exfiltration or command & control


**http (Port 80)**

- Unencrypted data transmission (credentials, sensitive data visible)
- Web application vulnerabilities (XSS, SQL injection, CSRF)
- Man-in-the-middle attacks and traffic interception


**https (Port 443)**

- SSL/TLS vulnerabilities and weak encryption protocols
- Certificate-based attacks and certificate spoofing
- Web application attacks despite encryption


**http-proxy (Port 8080/3128)**

- Unauthorized internet access through open proxy
- Traffic interception and data theft
- Proxy chaining for anonymizing malicious activities


**msrpc (Port 135)**

- Remote code execution through RPC vulnerabilities
- Lateral movement and privilege escalation in Windows networks
- Information gathering about system services and processes


**netbios-ssn (Port 139)**

- Null session attacks for user enumeration
- SMB relay attacks and credential theft
- Ransomware propagation through network shares


**microsoft-ds (Port 445)**

- SMB vulnerabilities (EternalBlue, WannaCry-style attacks)
- Credential harvesting and pass-the-hash attacks
- Unauthorized file access and data exfiltration
## Contributing

This is an educational project. Feel free to:
- Add example scan results
- Improve documentation
- Share interesting findings
- Suggest additional scanning techniques
