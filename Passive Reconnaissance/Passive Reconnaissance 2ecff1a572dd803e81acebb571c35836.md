# Passive Reconnaissance

- If you are playing the role of an attacker, you need to gather information about your target systems.
- If you are playing the role of a defender, you need to know what your adversary will discover about your systems and networks.

# Passive Reconnaissance (Passive Recon)

## Definition:

- **Passive reconnaissance** is the phase of information gathering where **no direct interaction** is made with the target system.
- All information is collected from **publicly available sources**, so the target **does not notice** anything.

## Goal:

- To gather **general and high-level information** about the target without alerting it.

***This helps:***

- Understand the target
- Reduce risk before active actions
- Prepare for active reconnaissance

## Information Colected:

- Domain names
- Subdomains
- IP ranges (indirectly)
- Technologies used
- Emails & usernames
- Company structure
- Leaked data (if publicly exposed)

# Active Reconnaissance (Active Recon)

## Definition:

- **Active reconnaissance** is the phase where the tester **directly interacts with the target system** to gather technical information.
- Because of this interaction, the target **can detect or log** the activity.

## Goal:

- To obtain **accurate, technical, and actionable data** that cannot be reliably collected using passive methods.

***This information is used to:***

- Identify attack surfaces
- Discover vulnerabilities
- Prepare for exploitation

## Information Collected:

- Open ports
- Running services
- Service versions
- Operating system details
- Web directories & files
- Application behavior

# whoıs command

## Definition:

- **WHOIS** is a command-line tool used to **query domain registration information**.
- It tells you **who owns a domain**, **when it was registered**, and **which servers manage it**.
- WHOIS is mainly used in **passive reconnaissance**.

## Why whois Is Important:

***WHOIS helps you:***

- Identify domain ownership
- Learn registration & expiration dates
- Find name servers
- Sometimes discover contact emails
- Understand infrastructure structure

## Basic Syntax

- whois [example.com](http://example.com/)
- This sends a request to WHOIS databases, **not directly to the target server**.

## Information You Can Get:

Depending on privacy settings, WHOIS may show:

- Domain name
- Registrar (GoDaddy, Namecheap, etc.)
- Creation date
- Expiration date
- Last updated date
- Name servers
- Registrant organization
- Registrant email (sometimes hidden)

# nslookup command

## Definition:

- **nslookup (Name Server Lookup)** is a command-line tool used to **query DNS servers** to obtain **domain name and IP address information**.

***It helps translate:***

- Domain name → IP address
- IP address → Domain name

## Basic Syntax:

- nslookup [example.com](http://example.com/)
- This returns the IP address of the domain.

## Types

### A

- nslookup -type=A [example.com](http://example.com/)
- IPv4

### AAAA

- nslookup -type=AAAA [example.com](http://example.com/)
- IPv6

### MX

- nslookup -type=MX [example.com](http://example.com/)
- Mail Servers

### NS

- nslookup -type=NS [example.com](http://example.com/)
- Name Servers

### TXT

- nslookup -type=TXT [example.com](http://example.com/)

## Why nslookup Is Important in Recon

It helps you:

- Discover IP addresses
- Identify mail servers
- Find name servers
- Understand DNS structure
- Prepare for subdomain enumeration

# dig command

## Definition:

- **`dig` (Domain Information Groper)** is a command-line tool used to **query DNS servers** and retrieve **detailed DNS information**.
- It is more **powerful and detailed** than `nslookup`.

## Why dig Is Important In Recon:

`dig` helps you:

- Analyze DNS behavior
- Discover infrastructure details
- Find mail servers & name servers
- Understand domain architecture
- Perform accurate DNS enumeration

# DNSDumspter Website

## Definition:

- **DNSDumpster** is an **online passive reconnaissance tool** used to **discover subdomains and DNS records** of a target domain.
- It collects data from **public sources** and **does not directly interact** with the target server.

## Purpose:

DNSDumpster helps to:

- Discover **subdomains**
- Identify **DNS records**
- Understand **network & infrastructure layout**
- Map external services related to a domain

## How DNSDumspter Works:

DNSDumpster gathers information from:

- Public DNS databases
- Search engines
- Certificate Transparency logs
- Historical DNS data

⚠️ It does **not** brute-force or scan the target.

# Shodan.io website

## Definition:

- **Shodan** is a **search engine for internet-connected devices**.

***Unlike Google (which searches websites), Shodan searches:***

- Servers
- Routers
- IoT devices
- Cameras
- Databases
- Industrial systems

## Information You Can Get:

- Open ports
- Running services
- Service versions
- Operating system clues
- Location (country, city)
- Organization / ISP
- Vulnerabilities (sometimes CVEs)

## Why shodan Is Important In Recon:

Shodan helps you:

- Find **exposed services**
- Detect **misconfigurations**
- Identify **attack surface**
- Discover forgotten assets
- Support vulnerability research

| Feature | Shodan | Nmap |
| --- | --- | --- |
| Scanning | No (database search) | Yes |
| Recon Type | Passive | Active |
| Detection | No | Possible |
| Effort | Low | Manual |