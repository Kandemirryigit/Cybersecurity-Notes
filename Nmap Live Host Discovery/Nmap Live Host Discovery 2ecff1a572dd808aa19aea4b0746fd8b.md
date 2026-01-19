# Nmap Live Host Discovery

# ARP (Adress Resolution Protocol)

## Definition:

- **ARP (Address Resolution Protocol)** is a network protocol used to **map an IP address to a MAC address** inside a **local network (LAN)**.

***In simple terms:***

- **ARP answers the question:**
- “Who has this IP address? What is your MAC address?”

## Why ARP Is Needed:

Computers communicate:

- **Logically** using IP addresses
- **Physically** using MAC addresses

ARP acts as a **bridge between IP and MAC**.

## Where ARP Works:

- Only inside the **local network**
- Does **not** work over the internet
- Used between devices in the same subnet

## How ARP Works (Step by Step)

- 1.)Device wants to send data to `192.168.1.10`
- 2.)It checks its **ARP cache**
- 3.)If MAC is unknown → sends **ARP Request (broadcast)**
- 4.)All devices receive the request
- 5.)Target device replies with **ARP Reply (unicast)**
- 6.)MAC address is saved in the ARP cache

## ARP Cache:

- Each device keeps a table called the **ARP cache**.

***It stores:***

- IP address
- MAC address

This avoids sending ARP requests repeatedly.

# ARP Request

## Definition:

- An **ARP Request** is a **broadcast message** sent on a **local network** to find the **MAC address** of a device when only its **IP address** is known.

***In short:***

- **ARP Request asks:**
- “Who has this IP address?”

## Why ARP Request Is Needed:

Devices need:

- **IP address** → for logical routing
- **MAC address** → for physical delivery
- If the MAC address is unknown, the device sends an **ARP Request**.

# What Is Host Dıscovery

## Definition:

- **Host Discovery** is the process of finding **which systems (hosts) are alive** on a network.

## What Is a Host:

- A **host** is any device with an IP address, for example:
- Computer 💻
- Server 🖥️
- Router 📡
- Printer 🖨️
- Phone 📱
- If it has an IP and is connected → it is a **host**.

## Why Host Dıscovery Is Important:

***Before scanning ports or services, we must know:***

- Which hosts are **alive**
- Which IPs are **unused**

***Without Host Discovery:***

- You scan dead IPs
- Waste time
- Generate unnecessary noise

***With Host Discovery:***

- Faster scans
- Less detection
- More efficient attacks / audits
- **This is why Host Discovery is always the first step in reconnaissance.**

## Common Host Discovery Techniques:

Host discovery can use different protocols:

### ICMP:

- Ping (Echo Request / Reply)
- Most common
- Often blocked

### ARP:

- Used in local networks
- Very reliable

### TCP:

- SYN, ACK probes
- Works even if ICMP is blocked

### UDP:

- Rare, noisy
- Less reliable

## Host Discovery vs Port Scanning

| Feature | Host Discovery | Port Scanning |
| --- | --- | --- |
| Purpose | Find alive hosts | Find open ports |
| Target | IP address | Ports (80, 443, etc.) |
| Output | Host up/down | Open/closed ports |
| First step? | ✅ Yes | ❌ No |

# Nmap Host Discovery Using ARP

## Definition:

- **Nmap Host Discovery using ARP** is a technique where **Nmap uses ARP requests** to discover **live hosts** on a **local network (LAN)**.
- Instead of using ICMP (ping), Nmap sends **ARP requests** and checks who replies.
- Nmap ARP host discovery is an active reconnaissance technique that uses ARP requests to identify live hosts on a local network.
- ARP works only inside the local network (LAN).
- This is the **most important concept** about ARP.

## Why nmap Uses ARP:

***ARP-based discovery is:***

- **Very fast**
- **Very accurate**
- Works **only in the local network**
- Works even when **ICMP is blocked**

## Information You Can Get:

- Live IP addresses
- MAC addresses
- Device vendors (from MAC),

## Key Point:

- If a device replies to ARP, **it is definitely alive**.
- Firewalls usually **cannot block ARP** inside a LAN.

# Nmap Host Discovery Using ICMP

## What It Is:

- Nmap uses **ICMP packets** (ping-like messages) to check **which hosts are alive**.
- Before scanning ports, Nmap first asks:
- Does this IP respond to ICMP

## ICMP Reminder:

***ICMP (Internet Control Message Protocol) is used for:***

- Network testing
- Error messages
- Connectivity checks

***Most important ICMP message:***

- **Echo Request**
- **Echo Reply**
- This is exactly how the `ping` command works.

## Basic ICMP Host Discovery In nmap

- The simplest ICMP discovery method is **ICMP Echo Request**.
- nmap -PE 192.168.1.0/24

### What Happens:

1- Nmap sends ICMP Echo Requests

2- Hosts reply with ICMP Echo Replies

3- Reply received → **Host is UP**

4- No reply → **Host may be blocked or down**

## Important ICMP Options in nmap:

### -PE  (ICMP Options Request)

- Most common and default ICMP method.

***nmap -PE 10.10.10.10***

- Fast
- Simple
- Often blocked by firewalls

### -PP  (ICMP Timestamp Request)

- Asks the target for its system time.

***nmap -PP 10.10.10.10***

- Some systems respond even if ping is blocked
- Rarely enabled

### -PM  (ICMP Address Mask Request)

- Asks for subnet mask information.

***nmap -PM 10.10.10.10***

- Very old systems
- Almost always blocked today

## Why ICMP Host Discovery Fails:

***A host can be alive but:***

- Firewall blocks ICMP
- IDS/IPS drops ping packets
- Server ignores Echo Requests
- No ICMP reply ≠ host is dead

# Using nmap with sudo or not

- With sudo, Nmap can do advanced host discovery AND advanced port scanning.Without sudo, Nmap still does both, but in a limited way.

## When you run nmap with sudo:

***Nmap can:***

- Send **raw packets**
- Use **ICMP Echo** (ping)
- Use **ARP** (local network)
- Use **TCP SYN scans** (half-open)
- **More accurate host discovery**
- **Faster and stealthier port scanning**

## When you run nmap without sudo:

Nmap:

- **Cannot send raw packets**
- **Cannot send ICMP Echo**
- Uses **TCP connect()** instead
- Uses **TCP-based host discovery**
- Host discovery still happens
- Port scanning still happens
- But
- **less powerful methods**  are used

| Feature | With sudo | Without sudo |
| --- | --- | --- |
| Host discovery | ICMP, ARP, TCP | TCP only |
| Port scan type | SYN scan | TCP Connect scan |
| Raw packets | ✅ Yes | ❌ No |
| Accuracy | High | Lower |
| Speed | Faster | Slower |

# Nmap Host Discovery Using TCP and UDP

## Why TCP&UDP Host Discovery:

***Sometimes:***

- **ICMP is blocked**
- Firewalls drop ping requests

***So Nmap asks a different question:***

- “Can I get **any TCP or UDP response** from this host
- If the host responds → **it is alive**

## TCP Host Discovery:

***TCP host discovery works by:***

- Sending **TCP packets** to specific ports
- Analyzing the **response**

***If there is any valid TCP response, the host is considered UP***

## TCP SYN Ping (-PS)

### What It Does:

- Sends a **TCP SYN** packet
- Usually to port **80, 443, or 22**
- nmap -PS 10.10.10.10

### Possible responses:

| Response | Meaning |
| --- | --- |
| SYN/ACK | Port open → host up |
| RST | Port closed → host up |
| No response | Filtered / blocked |

## TCP ACK Ping (-PA)

### What it does:

- Sends a **TCP ACK** packet
- Bypasses some firewalls
- nmap -PA 10.10.10.10

### Response:

- **RST** → host is alive
- No response → filtered

📌 Useful when SYN packets are blocked.

## Choosing Ports for TCP Ping

***You can specify ports manually:***

- nmap -PS22,80,443 10.10.10.10

## UDP Host Discovery:

UDP host discovery:

- Sends **UDP packets** to a port
- Waits for an **ICMP Port Unreachable** response

📌 This ICMP error proves the host is alive.

## UDP Ping (-PU)

- nmap -PU 10.10.10.10

### Possible responses:

| Response | Meaning |
| --- | --- |
| ICMP Port Unreachable | Host is alive |
| UDP reply | Host is alive |
| No response | Filtered / inconclusive |
- UDP is **slow** and **unreliable**

## Comparing ICMP vs TCP vs UDP

| Method | Reliable | Fast | Often Blocked |
| --- | --- | --- | --- |
| ICMP | ⭐⭐⭐ | ⭐⭐⭐ | Yes |
| TCP | ⭐⭐⭐⭐ | ⭐⭐⭐ | Less |
| UDP | ⭐⭐ | ⭐ | Often |

# Summary

## ARP Scan:

- sudo nmap -PR -sn MACHINE_IP/24

## IMCP Echo Scan:

- sudo nmap -PE -sn MACHINE_IP/24

## ICMP Timestamp Scan:

- sudo nmap -PP -sn MACHINE_IP/24

## ICMP Adress Mask Scan:

- sudo nmap -PM -sn MACHINE_IP/24

## TCP SYN Ping Scan:

- sudo nmap -PS22,80,443 -sn MACHINE_IP/30

## TCP ACK Ping Scan:

- sudo nmap -PA22,80,443 -sn MACHINE_IP/30

## UDP Ping Scan:

- sudo nmap -PU53,161,162 -sn MACHINE_IP/30

#