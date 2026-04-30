# Cybersecurity Testing Methodology

## 1. Reconnaissance

### Passive Information Gathering
- WHOIS lookup
- DNS enumeration
- Website analysis (robots.txt, sitemap.xml)
- Google dorking
- GitHub repository searches

### Active Information Gathering
- Ping sweep
- Port scanning
- Service enumeration
- Version detection
- OS detection

## 2. Scanning

### Network Scanning
```bash
nmap -sV -sC -O -A -p- <target>
```

### Vulnerability Scanning
- Nessus
- OpenVAS
- Qualys

### Web Application Scanning
- Burp Suite
- OWASP ZAP
- Nikto

## 3. Enumeration

### Service-Specific Enumeration

#### HTTP/HTTPS
- Directory enumeration
- Parameter fuzzing
- File discovery
- Subdomain enumeration

#### SMB
- Share enumeration
- User enumeration

#### LDAP
- User enumeration
- Group enumeration

## 4. Vulnerability Assessment

### Common Vulnerabilities
- SQL Injection
- Cross-Site Scripting (XSS)
- Cross-Site Request Forgery (CSRF)
- Authentication bypass
- Path traversal
- Command injection

## 5. Exploitation

### Pre-Exploitation
- Verify permissions
- Understand architecture
- Prepare payloads
- Document proof of concept

### Post-Exploitation
- Verify access level
- Document configuration
- Check for lateral movement
- Identify sensitive data

## 6. Privilege Escalation

### Linux
- Kernel exploits
- Sudo misconfiguration
- SUID binaries
- Weak file permissions
- Cron jobs

### Windows
- Token impersonation
- Kernel exploits
- Service misconfiguration

## 7. Lateral Movement
- Credential harvesting
- Pivot techniques
- Network segmentation bypass

## 8. Post-Exploitation

### Data Exfiltration
- Identify sensitive data
- Plan exfiltration method
- Execute carefully

### Persistence
- Backdoor installation
- Reverse shell setup
- Cron job persistence

## 9. Documentation

### Report Contents
- Executive summary
- Technical findings
- Vulnerability descriptions
- Impact assessment
- Remediation recommendations

## 10. Tools by Phase

### Reconnaissance
- Nmap
- Whois
- Dig/nslookup
- Shodan

### Scanning
- Nmap
- Nessus
- OpenVAS
- Burp Suite

### Enumeration
- Gobuster
- Ffuf
- Enum4linux

### Exploitation
- Metasploit
- SQLmap
- Hydra

## Best Practices

1. **Document everything**: Commands, outputs, times
2. **Be methodical**: Follow structured approach
3. **Stay organized**: Clear naming conventions
4. **Verify findings**: Double-check results
5. **Minimize impact**: Only access what's necessary
6. **Maintain ethics**: Follow rules of engagement
7. **Communicate**: Regular updates to stakeholders
8. **Keep learning**: Stay updated on vulnerabilities