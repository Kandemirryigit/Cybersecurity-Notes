# Vulnerabilities 101

- Cybersecurity is big business in the modern-day world.
- The hacks that we hear about in newspapers are from exploiting vulnerabilities.
- A vulnerability is a weakness that can be exploited to violate confidentiality, integrity, or availability (CIA).

# Vulnerability

## What is a Vulnerability?

A **vulnerability** is a **weakness** in a system, application, network, or process that can be **exploited by an attacker** to cause harm.

In simple terms:

- **If something can be abused → it’s a vulnerability**

## Vulnerability vs Threat vs Exploit

- **Vulnerability** → The weakness
- **Threat** → The potential danger (attacker, malware, etc.)
- **Exploit** → The method/code used to abuse the vulnerability

**Example:**

- Open port with no authentication → *Vulnerability*
- Hacker scanning the network → *Threat*
- Metasploit module → *Exploit*

## Common Types of Vulnerabilities

### 1.Software Vulnerabilities

- Weaknesses in applications or operating systems.

Examples:

- Buffer Overflow
- SQL Injection
- Cross-Site Scripting (XSS)
- Command Injection
- Insecure Deserialization

Cause:

- Bad coding
- Lack of input validation
- Old/unpatched software

### 2.Network Vulnerabilities

- Weaknesses in network design or configuration.

Examples:

- Open ports/services
- Weak firewall rules
- Unencrypted protocols (FTP, Telnet, HTTP)
- Misconfigured routers/switches

Cause:

- Poor configuration
- Legacy protocols
- No monitoring

### 3-Authentication Vulnerabilities

- Weaknesses related to login and identity.

Examples:

- Weak passwords
- Default credentials
- No rate limiting (brute-force possible)
- No Multi-Factor Authentication (MFA)

Cause:

- Poor security policies
- User behavior

### 4-Authorization Vulnerabilities

- Users can access things they **should not**

Examples:

- Privilege Escalation
- Insecure Direct Object Reference (IDOR)
- Broken Access Control

Cause:

- Logic errors in the application

### 5-Configuration Vulnerabilities

- System is set up insecurely.

Examples:

- Debug mode enabled
- Directory listing enabled
- Sensitive files exposed (.env, backups)
- Services running as root

Cause:

- Default settings
- Admin mistakes

### 6-Cryptographic Vulnerabilities

- Weak or broken encryption.

Examples:

- Weak hashing (MD5, SHA1)
- Hardcoded keys
- No TLS / SSL misconfiguration
- Reused encryption keys

Cause:

- Outdated crypto
- Poor implementation

## Vulnerabilities in Real Life

- FTP allows anonymous login
- SSH allows password authentication with weak passwords
- Web app doesn’t sanitize input → SQL Injection
- SUID binary misconfigured → Privilege Escalation

## How Vulnerabilities Are Found

### Manual Methods:

- Code review
- Configuration review
- Logic testing

### Automated Tools:

- **Nmap** → Find open ports & services
- **NSE scripts** → Detect known vulnerabilities
- **Nikto** → Web server vulnerabilities
- **Burp Suite** → Web vulnerabilities
- **OpenVAS / Nessus** → Vulnerability scanners

## Vulnerability Identification (CVEs)

- CVE (Common Vulnerabilities and Exposures)
- Example: `CVE-2017-0144` (EternalBlue)

**CVSS Score** (Severity)

- 0–3.9 → Low
- 4.0–6.9 → Medium
- 7.0–8.9 → High
- 9.0–10 → Critical

## Why Vulnerabilities Exist

- Developers make mistakes
- Systems get old
- Updates are not applied
- Security is ignored for speed/convenience

## Vulnerability Management Lifecycle

- 1-Discover
- 2-Analyze
- 3-Prioritize
- 4-Fix (patch / mitigate)
- 5-Verify
- 6-Monitor

# Vulnerability Database

## What is a Vulnerability Database?

- A **vulnerability database** is a **public or private repository** that stores information about **known security vulnerabilities** in software, hardware, and systems.

It usually contains:

- Vulnerability ID
- Description
- Affected products/versions
- Severity score
- References and mitigation info

## Why Vulnerability Databases Are Important

- Help **identify known weaknesses**
- Used by **security tools** (Nmap, Nessus, OpenVAS, Metasploit)
- Help defenders **patch systems**
- Help attackers (and CTF players) **find exploits**

## Most Important Vulnerability Databases

### 1. CVE (Common Vulnerabilities and Exposures)

### 2. NVD (National Vulnerability Database

### 3. Exploit Database (Exploit-DB)

# Finding a Vulnerability

## 1.Reconnaissance (Information Gathering)

### Goal:

- Learn **what the target is running**

### Passive Recon:

- WHOIS
- DNS records
- OSINT
- No direct interaction

### Active Recon:

- Ping
- Nmap scans
- Banner grabbing

- You are not finding vulnerabilities yet — you are **collecting clues**

## 2.Enumeration (Most Important Step)

### Goal:

- Discover **services, versions, and configurations**

Examples:

- Open ports
- Running services
- Software versions
- Users, shares, directories

Tools:

- `nmap -sV`
- `nmap -A`
- `enum4linux`
- `gobuster`
- `nikto`

Enumeration answers:

**“What exactly is running here?”**

## 3-Identifying Potential Vulnerabilities

- Now you **match versions to known weaknesses**

### Key Question:

> Is this service/version known to be vulnerable?
> 

### Methods:

- Google: `service version vulnerability`
- CVE / NVD
- Exploit-DB
- searchsploit

## 4-Manual Testing (Very Important)

- Not all vulnerabilities are in databases.

### Manual checks:

- Weak credentials
- Default passwords
- Logic flaws
- Misconfigurations

Examples:

- Anonymous FTP login
- Writable directories
- No authentication on admin panels
- SUID binaries
- Many real-world vulnerabilities are **misconfigurations**, not CVEs.

## 5.Web Vulnerability Discovery (If Web Exists)

### Look for:

- Input fields
- File uploads
- URL parameters
- Cookies & headers

Test for:

- SQL Injection
- XSS
- LFI / RFI
- Command Injection
- IDOR

Tools:

- Burp Suite
- Browser DevTools
- Manual payload testing

## Common Places Vulnerabilities Hide

- Old software versions
- Default credentials
- Misconfigured permissions
- Legacy protocols (FTP, Telnet)
- Backup files
- Admin panels
- SUID binaries
- Cron jobs