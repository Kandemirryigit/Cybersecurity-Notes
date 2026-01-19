# Nmap Post Port Scans

# Service Detection

## Definition

- **Service detection** identifies **what service is running on an open port**
- It also tries to find the **service version**
- Goes beyond “port is open”

## Why Service Detection Is Important

- Identify vulnerable services
- Match services with known exploits
- Understand real attack surface
- Very important in **CTFs & pentesting**

## Basic Syntax

- nmap  -sT -sV <target>

## What Nmap Does Internally

1. Finds **open ports**
2. Sends **service-specific probes**
3. Analyzes responses
4. Matches responses against **service fingerprints database**

## What Information You Get

- Service name (ssh, http, ftp)
- Software name (Apache, OpenSSH)
- Version number
- Sometimes OS / platform info

## Risks & Limitations

- More **noise** (easier to detect)
- Slower scans
- Some services hide version info
- Can trigger IDS/IPS

## Mods

### Light Detection

***nmap -sV --version-light <target>***

- Faster
- Less accurate

### Aggressive Detection

***nmap -sV --version-all <target>***

- Slower
- More accurate

# OS Detection

## Definition

- **OS Detection** attempts to identify the **operating system** of a target
- Based on **TCP/IP stack fingerprinting**
- Nmap analyzes how the system **responds to specially crafted packets**

## Basic Syntax

- nmap -O <target>

## Why OS Detection Is Important

- Choose correct exploits
- Understand target environment
- Improve attack accuracy
- Very useful in **CTFs & pentesting**

## OS Detection vs Service Detection

| Feature | OS Detection | Service Detection |
| --- | --- | --- |
| Flag | `-O` | `-sV` |
| Detects | Operating system | Software & version |
| Needs root | ✅ Yes | ❌ No |

## Syntax for

- sudo nmap -A <target>

Includes:

- OS detection
- Service detection
- Script scanning
- Traceroute

# nmap Scripting Engine (NSE)

### What is NSE?

**Nmap Scripting Engine (NSE)** is a feature of Nmap that allows you to use **Lua scripts** to **automate advanced network tasks** such as:

- Vulnerability detection
- Service enumeration
- Authentication testing
- Exploitation checks
- Information gathering

📌 In short:

**NSE extends Nmap from a port scanner into a security auditing tool.**

## Why NSE is Important

Without NSE → Nmap only tells you:

- Open ports
- Services
- Versions

With NSE → Nmap can tell you:

- Is this service vulnerable?
- Can I log in with default credentials?
- What users, shares, or configs exist?
- Is this CVE present?

## Where Are NSE Scripts Located?

On most systems:

- usr/share/nmap/scripts/

Scripts have the extension:

- .nse

Example:

- http-enum.nse
ssh-brute.nse
smb-vuln-ms17-010.nse

## How NSE Works (Simple)

1. Nmap scans a target
2. Detects open ports/services
3. NSE scripts run **based on rules**
4. Scripts send extra probes
5. Results are printed

## Basic Syntax

- nmap --script <script-name> <target>

Example:

- nmap --script http-enum 10.10.10.10

## Script Categories

- NSE scripts are grouped into **categories**.

### Common Categories

| Category | Meaning |
| --- | --- |
| `default` | Safe scripts run with `-sC` |
| `safe` | Non-intrusive |
| `intrusive` | May affect the target |
| `vuln` | Vulnerability detection |
| `exploit` | Exploitation attempts |
| `auth` | Authentication checks |
| `brute` | Brute-force attacks |
| `discovery` | Information gathering |
| `dos` | Denial of Service |

## NSE vs Normal Scan

| Normal Nmap | NSE |
| --- | --- |
| Finds ports | Finds vulnerabilities |
| Service name | Service weaknesses |
| Version info | Misconfigurations |
| Passive | Active testing |

# Saving Output

## Normal

- As the name implies, the normal format is similar to the output you get on the screen when scanning a target
- You can save your scan in normal format by using `-oN FILENAME`
- N stands for normal.

## Grepable

- The grepable format has its name from the command `grep`
- it makes filtering the scan output for specific keywords or terms efficient
- You can save the scan result in grepable format using `-oG FILENAME`
- in grepable output, the lines are so long and are not convenient to read compared to normal output.
- As you can understand from the name this format is so much useful for grep command

## XML

- You can save the scan results in XML format using `-oX FILENAME`

## Normal,Grepable,XML

- you can save the scan output in all three formats using `-oA FILENAME`

# Summary

## -sV

- determine service/version info on open ports

## -sV —version-light

- try the most likely probes (2)

## -sV —version-all

- try all available probes (9)

## -O

- detect OS

## —traceroute

- run traceroute to target

## —script=SCRIPTS

- Nmap scripts to run

## -sC or —script=default

- run default scripts

## -A

- equivalent to `-sV -O -sC --traceroute`

## -oN

- save output in normal format

## -oG

- save output in grepable format

## -oX

- save output in XML format

## -oA

- save output in normal, XML and Grepable formats