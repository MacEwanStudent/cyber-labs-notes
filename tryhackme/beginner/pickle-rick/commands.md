# Commands Summary — Pickle Rick

## Reconnaissance

### Nmap — Service & Port Scan
```bash
nmap -sC -sV -oN scans/initial.txt <target_ip>
```
Scans for open ports and detects services/versions
- sC → default scripts
- sV → version detection
- oN → save output

# ffuf — Directory Brute Force

```bash
ffuf -u http://<target>/FUZZ -w /usr/share/wordlists/dirb/common.txt -mc 200,301,302,403 -fc 404
```
# fuuf with Extensions

```bash
ffuf -u http://<target>/FUZZ -w /usr/share/wordlists/dirb/common.txt -e .php,.html,.txt -mc 200,301,302,403 -fc 404
```

# Web Inspection
# curl-Fetch Web Content

```bash
curl http://<target>
```
- Retrieves raw HTML from the page

# grep — Filter Output

```bash
curl -s http://<target> | grep -i input
```

- Searches for specific patterns (e.g., input fields)

# System Enumeration (Post-Login)
# pwd — Print Current Directory

```bash
pwd
```
```bash
ls
```
```bash
ls -la
```

- Lists files and directories
- la shows hidden files

# Navigate Directories
```bash
/
```
```bash
/home
```
```bash
/home/rick
```

- Explore system structure

# File Handling
# Handling Spaces in Filenames

```bash
ls /home/rick/second\ ingredients
```

- Use \ to escape spaces

# File Reading
# cat (blocked in challenge)
```bash
cat file.txt
```
- Displays file contents
# Bypass cat filter
```bash
ca\t file.txt
```
- Bypasses simple command filtering

# less / more
```bash
less file.txt
more file.txt
```
- View file contents page by page

# Privilege Escalation
whoami — Check Current User
whoami
Displays current user

# sudo -l — Check Privileges
```bash
sudo -l
```
- Lists allowed sudo commands
# Execute as Root

```bash
sudo ls /root
sudo less /root/3rd.txt
```
- Access restricted files

# File Search
# find — Search Files
```bash
find / -name "*keyword*" 2>/dev/null
```
- Searches entire system
- 2>/dev/null hides permission errors
- 
# Misc
# echo — Display Text / Expand Paths
```bash
echo /root/*
```

Useful for testing access and wildcard expansion
