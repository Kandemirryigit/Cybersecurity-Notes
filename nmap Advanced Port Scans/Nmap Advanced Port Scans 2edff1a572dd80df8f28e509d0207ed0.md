# Nmap Advanced Port Scans

# NULL Scan (-sN)

- if an RST packet is received, it means that the port is closed. Otherwise, it will be reported as open|filtered.

## What Is a NULL Scan:

A **NULL scan** is a TCP scan where:

- Nmap sends a TCP packet with NO flags set

That means:

- SYN
- ACK
- FIN
- PSH
- URG

The TCP flags field is **NULL (empty)**.

- Requires **root / sudo**.

## Why NULL Scan Exists

- **Closed ports** must respond with **RST**
- **Open ports** should **ignore** unexpected packets
- if an RST packet is received, it means that the port is closed. Otherwise, it will be reported as open|filtered.

## NULL Scan vs SYN Scan

| Feature | NULL Scan | SYN Scan |
| --- | --- | --- |
| Flags used | None | SYN |
| Needs sudo | ✅ | ✅ |
| Reliable | ❌ | ✅ |
| Stealth | High | Medium |
| Port state clarity | Low | High |

## Why NULL Scan Is “Stealthy”

- No SYN packets
- Looks abnormal, not like a real connection
- Can bypass **simple firewalls**
- Modern IDS detect it easily.

## Limitations of NULL Scan

- Open ports give **no response**
- Results often **inconclusive**
- Does **not work on Windows** (Windows replies RST to everything)

📌 Best for **learning**, not primary scanning.

# FIN Scan (-sF)

- if an RST packet is received, it means that the port is closed. Otherwise, it will be reported as open|filtered.

## What Is a FIN Scan:

A **FIN scan** is a TCP scan where Nmap:

- Sends a TCP packet with only the FIN flag set

FIN normally means:

- “I’m finished sending data, let’s close the connection”

But here, it’s sent **without an existing connection**, which is unusual.

📌 Requires **root / sudo**.

## Why FIN Scan Exists

FIN scan is based on **RFC 793 TCP behavior**:

- **Closed ports** must respond with **RST**
- **Open ports** should **ignore** unexpected FIN packets

Nmap uses this difference to infer port state.

- Actually to find the closed ports

## FIN Scan vs SYN Scan

| Feature | FIN Scan | SYN Scan |
| --- | --- | --- |
| Flags used | FIN | SYN |
| Needs sudo | ✅ | ✅ |
| Reliability | Low | High |
| Stealth | High | Medium |
| Port clarity | Low | High |

## Why FIN Scan Is Considered Stealthy

- Does not look like a real connection start
- Can bypass **simple packet filters**
- Less noisy than SYN scans

Modern firewalls & IDS detect FIN scans easily.

# xmas Scan (-sX)

- if an RST packet is received, it means that the port is closed. Otherwise, it will be reported as open|filtered.

## What is an Xmas Scan?

An **Xmas scan** is a TCP scan where Nmap:

> Sets multiple TCP flags at the same time
> 

Specifically:

- **FIN**
- **PSH**
- **URG**

The packet is “lit up” like a Christmas tree 🎄

→ That’s why it’s called **Xmas scan**.

- Requires **root / sudo**.

## Why Xmas Scan Exists

Xmas scan relies on **RFC 793 TCP behavior**, just like NULL and FIN scans:

- **Closed ports** → must reply with **RST**
- **Open ports** → should **ignore** the packet

Nmap uses this difference to guess port states.

- Actually uses for finding closed ports

## Why Xmas Scan Is Considered Stealthy

- No SYN packets
- Unusual flag combination
- Can bypass **basic firewalls**

Modern IDS / IPS detect Xmas scans easily.

# maimon Scan (-sM)

## What is a Maimon Scan?

A **Maimon scan** is a TCP scan where Nmap:

- Sends a TCP packet with FIN + ACK flags set

Requires **root / sudo**.

## Why Maimon Scan Exists

Maimon scan targets **how firewalls handle FIN/ACK packets**.

Some firewalls:

- Allow FIN/ACK packets through
- Block SYN packets

This scan can sometimes **bypass simple firewalls**.

## Why Maimon Scan Is Rarely Used

- Works only on **very specific firewall setups**
- Often gives **open|filtered**
- Modern firewalls handle it correctly

📌 Mostly **educational**, not practical.

# TCP ACK Scan

## Definition:

- **TCP ACK scan** is used to **map firewall rules**
- It **does NOT detect open ports**
- It only determines whether a port is **filtered or unfiltered**

## Purpose

- Identify **firewall presence**
- Detect **stateful firewalls**
- Discover which ports are **allowed through the firewall**

## How It Works

- Nmap sends a **TCP packet with only the ACK flag set**
- No existing TCP connection
- This is an **abnormal packet**

## Target Responses

### RST → Unfiltered

- Packet reached the target
- Firewall did **not** block it
- Port is **UNFILTERED**
- Port may be **open or closed** (unknown)

### No Response / ICMP Error → Filtered

- Firewall blocked the packet
- Port is **FILTERED**

# TCP Window Scan (-sW)

## Definition:

- **TCP Window Scan** is an advanced scan used to **distinguish open and closed ports**
- It is based on the **TCP Window Size** in RST packets
- Works only on **some operating systems**

## Purpose

- Detect **open vs closed ports**
- Bypass some **firewall rules**
- Gain more info than an ACK scan

## How It Works

1. Nmap sends a **TCP ACK packet**
2. Target replies with **RST**
3. Nmap checks the **TCP Window size** in the response

## Target Responses

### Open Port

- Response: **RST**
- **Window size > 0**
- Indicates port is **OPEN**

### Closed Port

- Response: **RST**
- **Window size = 0**
- Indicates port is **CLOSED**

### Filtered Port

- No response or ICMP error
- Port is **FILTERED**

## Result Interpretation

| Response | Window Size | Port State |
| --- | --- | --- |
| RST | > 0 | Open |
| RST | 0 | Closed |
| No response / ICMP | — | Filtered |

# Custom Scan

## Definition

- A **Custom Scan** is a scan where you **manually control TCP flags**
- Used to create **non-standard packets**
- Helps **bypass firewalls, IDS, and IPS**
- Advanced scanning technique

## Why Use Custom Scans

- Evade **signature-based detection**
- Test **firewall behavior**
- Explore **unexpected target responses**
- When default scans are blocked

## How It Works

- Nmap lets you set **any TCP flag combination**
- Target reacts based on TCP RFC behavior
- Responses are analyzed manually or by Nmap

## Common TCP Flags

- SYN
- ACK
- FIN
- RST
- PSH
- URG

## Target Responses

### Open Port

- Usually **no response**
- (Unless OS behaves incorrectly)

### Closed Port

- **RST packet** sent back

### Filtered Port

- No response or ICMP error

## Advantages

- Harder to detect
- Flexible
- Can mimic other scan types

## Limitations

- OS-dependent behavior
- Less reliable than SYN scan
- Not standardized

# Spoofing

## Definition:

- **Spoofing** means **pretending to be someone or something else**
- In networking, it means **forging identity information** in packets

## Why Spoofing Is Used

- Hide real identity
- Bypass weak security controls
- Confuse logs and monitoring systems
- Test network security

## Limitations of Spoofing

- Easily detected by modern IDS
- Often blocked by ISPs and routers
- Not true anonymity

# IP Spoofing

## Definition

- **IP spoofing** is the act of **forging the source IP address** in IP packets
- The attacker pretends to be **another host**
- Commonly used in **network attacks and testing**

## Why IP Spoofing Is Used

- Hide the real attacker IP
- Bypass IP-based trust rules
- Confuse logs and monitoring systems
- Perform **blind attacks**

# MAC Spoofing

## Definition

- **MAC spoofing** is the act of **changing a device’s MAC address**
- The attacker pretends to be **another device on the local network**
- Works at **Layer 2 (Data Link Layer)**

## Why MAC Spoofing Is Used

- Bypass MAC-based access controls
- Hide real device identity
- Impersonate trusted devices
- Gain network access (Wi-Fi, LAN)

# ARP Spoofing

## Definition

- **ARP spoofing** is an attack where an attacker **sends fake ARP messages**
- It links the **attacker’s MAC address** to the **IP address of another device**
- Works in the **local network (LAN)**

## Why ARP Is Vulnerable

- ARP has **no authentication**
- Devices **trust ARP replies**
- Any device can send ARP responses

# Decoys

## Definition

- **Decoys** are **fake source IP addresses** used during scanning
- The real attacker IP is **hidden among fake ones**
- Goal: **confuse logs and defenders**

## Why Decoys Are Used

- Hide the real scanning IP
- Mislead SOC / IDS analysts
- Reduce attribution
- Increase stealth during reconnaissance

## Target’s Perspective

- Defender sees **many scanning IPs**
- Hard to identify the real attacker
- Wastes analysis time

## Decoys vs IP Spoofing

| Feature | Decoys | IP Spoofing |
| --- | --- | --- |
| Real IP included | ✅ Yes | ❌ No |
| Receive responses | ✅ Yes | ❌ No |
| Practical scanning | ✅ Yes | ❌ Limited |
| Stealth level | Medium | Low |

## Limitations

- Not true anonymity
- IDS can detect decoy patterns
- Some networks block fake IPs
- Decoys must be **alive IPs** for realism

# Fragmented Packets

## Definition:

- **Fragmentation** means **splitting a packet into smaller pieces**
- Each piece is sent **separately**
- Receiver **reassembles** fragments into the original packet

## Why Fragmentation Exists

- Networks have **MTU (Maximum Transmission Unit) limits**
- If a packet is larger than MTU → it must be fragmented

## Fragmentation in Security (Why Attackers Use It)

- Evade firewalls
- Bypass IDS / IPS
- Hide payload and headers
- Avoid signature-based detection

## How Fragmentation Works

1. Original packet is split into **multiple fragments**
2. Each fragment has:
    - Same **Identification ID**
    - Fragment offset
3. Target reassembles fragments

## Advantages

- Stealthy
- Bypasses simple firewalls
- Useful in recon

## Limitations

- Easily detected by modern IDS
- Slower scanning
- Some networks drop fragments
- Can break scans

# idle/zombie Scan

## Definition

- **Idle (Zombie) Scan** is a **very stealthy scan**
- The attacker **does not send packets directly** to the target
- A third machine (**Zombie**) is used to scan the target

## Why It’s Called “Idle”

- The zombie host is:
    - Online
    - Trusted
    - **Not actively sending traffic**
- Its **IP ID values increase predictably**

## Purpose

- Hide the real attacker IP completely
- Bypass logging and detection
- Extremely stealthy reconnaissance

## Advantages

- Real attacker IP is **never seen**
- Very stealthy
- Bypasses firewalls and IDS

## Limitations

- Hard to find a good zombie
- Modern OSes randomize IP ID
- Slow scan
- Rarely usable in real life

# Getting More Details

## —reason

- tells you **WHY Nmap decided a host or port is in a certain state**
- It shows the **exact packet or response** that caused the result

## -v

- verbose output
- Nmap shows **more details about what it is doing**

## -vv

- very verbose output
- It shows **more details than `-v`**

# Summary

## TCP NULL Scan

- sudo nmap -sN 10.82.175.74

## TCP FIN Scan

- sudo nmap -sF 10.82.175.74

## TCP Xmas Scan

- sudo nmap -sX 10.82.175.74

## TCP Maimon Scan

- sudo nmap -sM 10.82.175.74

## TCP ACK Scan

- sudo nmap -sA 10.82.175.74

## TCP Window Scan

- sudo nmap -sW 10.82.175.74

## Custom TCP Scan

- sudo nmap --scanflags URGACKPSHRSTSYNFIN 10.82.175.74

## Spoofed Source IP

- sudo nmap -S SPOOFED_IP 10.82.175.74

## Spoofed MAC Address

- --spoof-mac SPOOFED_MAC

## Decoy Scan

- nmap -D DECOY_IP,ME 10.82.175.74

## Idle(Zombie) Scan

- sudo nmap -sI ZOMBIE_IP 10.82.175.74

## Fragmented IP Data into 8 bytes

- -f

## Fragmented IP Data Into 16 Bytes

- -ff